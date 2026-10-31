**Standard Operating Procedure (SOP)**

Installing Git on Windows, Creating a GitHub Project, and Pushing a
Local Directory

*Prepared for internal use*

**1. Purpose**

This SOP describes the step-by-step process to install Git on a Windows
machine, create a new project folder, set up a corresponding repository
on GitHub, and push the local directory to that repository.

**2. Install Git on Windows**

**Step 1: Download the Git installer**

Open a browser and go to https://git-scm.com/download/win. The download
should start automatically for the 64-bit Windows version.

*\[ Insert screenshot here: Git download page \]*

**Step 2: Run the installer**

Locate the downloaded .exe file (usually in the Downloads folder) and
double-click it to launch the Git Setup wizard.

**Step 3: Proceed through setup screens**

Keep the default options selected on each screen (Select Components,
default editor, PATH environment adjustment, line-ending conversions,
etc.) and click \'Next\' through each one unless you have a specific
reason to change a setting.

**Step 4: Finish installation**

Click \'Install\', wait for the process to complete, then click
\'Finish\'.

**Step 5: Verify the installation**

Open Command Prompt or PowerShell and run the command below. A version
number confirms Git is installed correctly.

git \--version

**Step 6: Set your Git identity (one-time setup)**

Configure the username and email that will be attached to your commits.

git config \--global user.name \"Your Name\"\
git config \--global user.email \"you@example.com\"

**3. Create a Project Folder and GitHub Repository**

**Step 1: Create a local project folder**

Open Command Prompt, navigate to the desired location, and create a new
folder for the project.

mkdir ProjectFolder\
cd ProjectFolder

**Step 2: Create a new repository on GitHub**

Go to https://github.com, click the \'+\' icon in the top right corner,
and select \'New repository\'. Enter a repository name, choose Public or
Private, and click \'Create repository\'. Do not initialize with a
README if you plan to push an existing local folder, to avoid merge
conflicts.

*\[ Insert screenshot here: New repository creation screen on GitHub \]*

**Step 3: Copy the repository URL**

On the new repository\'s page, copy the HTTPS URL shown (it looks like
https://github.com/\<username\>/\<repo-name\>.git).

**4. Push the Local Directory to GitHub**

**Step 1: Initialize Git in the project folder**

Run this inside the project folder.

git init

**Step 2: Add files to staging**

Stage all files in the folder for commit.

git add .

**Step 3: Commit the files**

Save a snapshot of the staged files with a message.

git commit -m \"Initial commit\"

**Step 4: Set the branch name to main**

Ensure the default branch is named \'main\'.

git branch -M main

**Step 5: Link the local folder to the GitHub repository**

Add the GitHub repository URL copied earlier as the remote origin.

git remote add origin https://github.com/\<username\>/\<repo-name\>.git

**Step 6: Push the folder to GitHub**

Upload the local commits to the GitHub repository.

git push -u origin main

**Step 7: Enter credentials if prompted**

If asked for a password, use a GitHub Personal Access Token instead of
your account password (Settings \> Developer settings \> Personal access
tokens).

**Step 8: Verify the push**

Refresh the GitHub repository page in the browser. The project files
should now be visible there.

*\[ Insert screenshot here: GitHub repository page showing the pushed
files \]*

**5. Command Reference Table**

All commands used in this SOP, listed in order of execution.

  ------------------------------------------------------------------------------------------
  **\#**   **Purpose**                   **Command**
  -------- ----------------------------- ---------------------------------------------------
  1        Check if Git is installed     git \--version

  2        Configure your username       git config \--global user.name \"Your Name\"
           (one-time)                    

  3        Configure your email          git config \--global user.email \"you@example.com\"
           (one-time)                    

  4        Create a new project folder   mkdir ProjectFolder

  5        Move into the project folder  cd ProjectFolder

  6        Initialize a local Git        git init
           repository                    

  7        Check status of files         git status

  8        Stage all files for commit    git add .

  9        Commit the staged files       git commit -m \"Initial commit\"

  10       Rename default branch to main git branch -M main

  11       Link local repo to GitHub     git remote add origin
           repo                          https://github.com/\<username\>/\<repo-name\>.git

  12       Push local directory to       git push -u origin main
           GitHub                        

  13       Check remote link (verify)    git remote -v

  14       Pull latest changes (later    git pull origin main
           use)                          
  ------------------------------------------------------------------------------------------
