**[Symmetric key limitations (recap)]{.mark}**

1.  [Symmetric key cryptography ki 3 limitations kya hain? (key
    distribution, non-repudiation, number of keys) - Done]{.mark}

2.  [n users ke liye kitni keys chahiye symmetric cryptography mein?
    Formula likho. - Done]{.mark}

**Public key basics**

3.  [Public key cryptography kab aur kisne introduce ki? (1976,
    Diffie-Hellman-Merkle)]{.mark}

4.  [Public key cryptography ke 2 core assumptions kya hain?
    (encryption/decryption functions exist; public key authenticated hai
    --- certificates se)]{.mark}

5.  [Public key cryptography symmetric key ki teeno limitations kaise
    solve karti hai?]{.mark}

**[One-way functions]{.mark}**

6.  [One-way function ki definition do --- kya properties honi
    chahiye?]{.mark}

7.  [Integer factorization one-way function kyun hai? (n=pq easy
    compute, p,q se n nikalna hard)]{.mark}

8.  [Discrete logarithm problem define karo.]{.mark}

**[RSA]{.mark}**

9.  [RSA kisne invent kiya aur kab? 1978]{.mark}

10. [RSA key generation ke 6 steps bolo (p,q choose → n=pq → φ(n) → e
    choose with gcd(e,φ(n))=1 → d=e⁻¹ mod φ(n) → pk=(n,e), sk=d)]{.mark}

11. [RSA encryption aur decryption formula kya hai?]{.mark}

12. Modulus n ki minimum bit size kya honi chahiye real world mein?
    (1024 bits+)

13. [**Toy example solve karo:** p=3, q=11, e=3 --- n, φ(n), d nikaalo,
    aur ek message encrypt-decrypt karo]{.mark}

14. [RSA integer factorization pe based hai --- iska security se kya
    relation hai?]{.mark}

**Diffie-Hellman Key Exchange**

15. DHKE kisne invent ki aur kab?

16. [DHKE parameters setup phase mein kya hota hai? (p prime, α
    generator, publish karna)]{.mark}

17. [DHKE key exchange phase step by step batao]{.mark}

18. [**Numerical solve karo** (jaise p=29, α=2, a=5, b=12 --- A, B, aur
    shared key K_AB nikaalo)]{.mark}

19. DHKE \"key agreement\" category mein kyun aata hai, \"key
    transport\" mein kyun nahi?

**Digital Signatures**

20. [Digital signature ka basic idea kya hai? (sign with private key,
    verify with public key)]{.mark}

21. RSA digital signature scheme likho --- sign aur verify formula (s =
    m\^d mod n; verify: s\^e mod n ≡ m)

22. Digital signature aur encryption mein kya farak hai? (keys ka
    opposite use hota hai)

**Key Management**

23. \"Key establishment\" ka matlab kya hai?

24. Key Transport aur Key Agreement mein farak batao, example sahit

25. Naive n² key distribution approach ki do challenges kya hain?

**Key Distribution Centre (KDC)**

26. KDC approach ka basic idea kya hai?

27. KDC ke 2 advantages kya hain?

28. **KDC ki 4 weaknesses batao:**

    - Single point of failure

    - Perfect Forward Secrecy na hona (agar K_A leak ho, purani sessions
      bhi decrypt ho sakti hain)

    - Replay attacks

    - Key confirmation attack

29. \"No Perfect Forward Secrecy\" ka matlab kya hai?

30. Kerberos protocol KDC ki kaunsi do weaknesses solve karta hai?
    (replay + key confirmation attacks)

**Kerberos**

31. Kerberos protocol step by step explain karo (jo humne abhi detail
    mein kiya)

32. Kerberos mein nonce (r_A) ka kya role hai?

**MITM aur Certificates**

33. MITM attack DHKE pe kaise kaam karta hai?

34. MITM attack kyun possible hota hai? (public keys authenticated nahi
    hoti)

35. Certificate ki definition kya hai? (\"authenticated public keys\")

36. Certificate generate karne ke 2 approaches kya hain? (user-provided
    keys vs CA-provided keys)

37. X.509 certificate mein kaunse do algorithms involve hote hain?
    (signing algorithm jaise RSA+SHA1, public key algorithm jaise DHKE)

38. DHKE with certificates --- kaise MITM attack ko rokta hai?

**Chain of Certificates**

39. \"Chain of certificates\" kya hota hai, aur Alice Bob ki public key
    kaise verify karti hai is chain se?

40. India mein Certifying Authorities (CA) ka example do.

------------------------------------------------------------------------

**Sabse zyada likely poochhe jaane wale (high-priority,
numerical/conceptual mix):**

- [Symmetric key limitations aur unke solutions]{.mark}

- [RSA toy example (numerical, almost certainly aayega)]{.mark}

- [DHKE numerical example]{.mark}

- KDC ki weaknesses (especially Perfect Forward Secrecy)

- MITM attack explanation + Certificates solution

- Kerberos step-by-step
