# eMudhra compromised CA — cross-OS trust test

## What this tests

Following the October 2026 eMudhra intermediate CA key compromise
(8 intermediate CA private keys found to be too weak, allowing anyone
to compute them from the public certificate), browsers and OS vendors
revoked trust in the affected intermediates. This test checks whether
two machines in the same home lab actually enforce that revocation.

Test target: `https://dv-g3b-emudhra.we-have-a-problem.com/`, a site
deliberately served with a certificate signed by the compromised
`EM DV TLS CA - G3B` intermediate, built for exactly this kind of
verification.

## Method

```bash
curl.exe -v https://dv-g3b-aaa-emudhra.we-have-a-problem.com/   # Windows
curl https://dv-g3b-emudhra.we-have-a-problem.com/              # Kali
```

## Result

| Machine | Result | Evidence |
|---|---|---|
| Windows 10 (host) | **Blocked.** `CRYPT_E_REVOKED (0x80092010) - The certificate is revoked.` | `windows_revoked.png` |
| Kali Linux (VM) | **Connected.** Site itself returned: "Your client successfully connected to the site. That's bad!" | `kali_still_trusts.png` |

Windows correctly checked certificate revocation (schannel log shows
`checking server certificate revocation`) and rejected the connection.
Kali's default `ca-certificates` bundle had not picked up the
revocation at the time of testing, and the TLS handshake completed
normally — exactly the outcome the test site is designed to flag as
unsafe.

## Why this matters for the capstone

This is a concrete, reproducible example of the problem the AlertMind
project is meant to address: **endpoints in the same environment patch
at different speeds**, and an attacker only needs one lagging machine
to find a foothold. It's a good supporting example for:

- The Week 1 architecture discussion (why multiple log sources /
  endpoints matter, not just one).
- An account-compromise or supply-chain IR playbook in Week 2.
- The oral defense question "did you verify a real-world security
  issue yourself?"

## Remediation attempted — and why it didn't fix it

On the lagging machine (Kali):

```bash
sudo apt update && sudo apt install -y ca-certificates
sudo update-ca-certificates
```

This upgraded the `ca-certificates` package from `20260601` to
`20260816` (log showed "4 added, 4 removed" root certificates). Re-running
the same `curl` test afterward still returned:

```
Your client successfully connected to the site. That's bad!
```

**Finding:** `apt install ca-certificates` only manages which *root* CA
certificates are trusted — it adds or removes whole root CAs when
Mozilla's/Debian's bundle changes. It does **not** track mid-chain
*intermediate* CA revocation like this eMudhra case. That kind of
revocation is normally enforced by the browser itself (Chrome's CRLSets,
Firefox's OneCRL), not by the OS certificate bundle or `curl`/OpenSSL,
which is why Kali's command-line `curl` kept trusting the compromised
intermediate even after a full `ca-certificates` update.

This is itself a useful finding for the report: a patched OS package
does not guarantee protection against every kind of CA-level compromise,
and tools that rely on the OS trust store (like `curl`, many backend
services, and most CLI tools) can remain exposed even when a browser
on the same machine would block the same certificate.

## Caveat

A separate URL variant tested during this session
(`dv-g3b-aaa-emudhra.we-have-a-problem.com`) returned a different curl
error (`unable to get local issuer certificate`) on Kali. That error
means curl couldn't build the certificate chain at all, not that
revocation was enforced — the two errors aren't equivalent, and only
the plain `dv-g3b-emudhra...` result above was treated as the reliable
signal for this writeup.
