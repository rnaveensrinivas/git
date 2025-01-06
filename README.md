# Table of contents

* [Introduction](#Introduction)
  * [What is Git?](#what-is-git)
  * [Introduction to Version Control](#introduction-to-version-control)
  * [Centralized vs. Distributed Version Control](#centralized-vs-distributed-version-control)
  * [Design Philosophy of Git](#design-philosophy-of-git)
* [Git Components](#git-components)
* [Getting Started](#getting-started)
  * [install Git](#install-git)
  * [Set Up SSH for GitHub](#set-up-ssh-for-github)
  * [Test Your SSH Connection](#test-your-ssh-connection)
  * [Set SSH as Default for All Repositories](#set-ssh-as-default-for-all-repositories)
  * [Configure Git](#configure-git)
  * [**Summary**](#summary-of-git-configuration-commands)
* [initializing Repositories](#initializing-repositories)
  * [Cloning an Existing Repository](#cloning-an-existing-repository)
  * [Optional: Swithcing to use SSH Instead of HTTPS](#optional-swtiching-to-use-ssh-instead-of-https-for-cloned-repositories)
  * [**Summary**](#summary-of-git-initialization-commands)
* [Recording Changes](#recording-changes)
  * [Git Snapshots](#git-snapshots)
  * [Staging Area](#the-staging-area-also-called-index)
  * [Commits](#commits)
  * [Tagging Commits](#tagging-commits)
  * [**Summary**](#summary-of-recording-changes-commands)
* [Undoing Changes](#undoing-changes)
  * [Undoing Changes in Working Directory](#undoing-changes-in-the-working-directory)
  * [Undoing changes in Staging Area](#undoing-in-the-staging-area)
  * [Undoing Commits](#undoing-commits)
  * [Amending Commits](#amending-commits)
  * [**Summary**](#summary-of-undoing-changes)
* [Branches](#branches)
  * [Manipulating Branches](#manipulating-branches)
  * [Merging Branches](#merging-branches)
  * [Rebasing](#rebasing)
  * [**Summary**](#summary-of-branches)
* [Branching Workflows](#branching-workflows)
  * [Types of Branches](#types-of-branches)
    * [Permanent Branches](#permanent-branches)
    * [Topic Branches](#topic-branches)
  * [Sample Workflow](#sample-workflow)
  * [Branching Workflow Flexibility](#branching-workflow-flexibility)
  * [**Summary**](#summary-of-key-points) 
* [Remote Repositories](#remote-repositories)
  * [What is a Remote Repository?](#what-is-a-remote-repository)
  * [Managing Remote Repository](#managing-remote-repositories)
  * [Working with Remote Branches](#working-with-remote-branches)
  * [Integrating changes from Remote Repositories](#integrating-changes-from-remote-branches)
  * [Pushing Changes to Remote Repositories](#pushing-changes-to-remote-repositories)
  * [**Summary**](#summary-of-remote-repositories)
* [Remote Workflows](#remote-workflows)
  * [Public (Bare) Repositories](#public-bare-repositories)
  * [The Centralized Workflows](#the-centralized-workflow)
  * [The Integrator Workflow](#the-integrator-workflow)
* [**Cheat Sheet**](#cheat-sheet)


---

# Introduction
## What is Git?
- Git is an **open-source version control system** known for its:
  - **Speed**
  - **Stability**
  - **Distributed collaboration model**
- Originally created in **2006** by *Linus Torvalds* to manage the Linux kernel.
- Today, Git has:
  - A **comprehensive feature set**
  - **Active development team**
  - Several **free hosting communities** like GitHub, GitLab, Bitbucket, etc.

## Introduction to Version Control

### Definition:
Version control is a system that **tracks changes to files over time**, enabling collaboration and version management.

### Key Benefits:
- Maintains a **history of changes**, allowing you to view or revert to earlier versions.
- Facilitates **collaboration** by letting multiple people work on the same project simultaneously.
- Tracks **who made what changes and when**, providing accountability.
- Reduces risk by serving as a **backup system** for your code or files.

### Types of Version Control:
- **Local Version Control**: Stores changes on a single machine. Simple but limited for collaboration.
- **Centralized Version Control**: Uses a central server to store files and version history (e.g., SVN, CVS).
- **Distributed Version Control**: Each user has a complete copy of the repository (e.g., Git, Mercurial).

### Common Use Cases:
- Software development (code management).
- Document versioning and collaborative editing.
- Managing configuration files and scripts.

### Popular Tools:
- Git, Mercurial, Subversion (SVN), CVS.
- Hosting services like GitHub, GitLab, and Bitbucket simplify sharing and collaboration.

### Why It's Essential:
- Helps avoid overwriting others' work.
- Enables **parallel development**.
- Provides a **safety net** against accidental data loss or errors.

## Centralized vs. Distributed Version Control

### Centralized Version Control Systems (CVCS)
- **How It Works**:
  - A single **central repository** stores all project files and version history.
  - Developers pull files from the central server, make changes, and push them back.
- **Examples**: Subversion (SVN), CVS.  
- **Key Features**:
  - **Single Point of Truth**: The central server holds all the data.
  - **Network Dependency**: You need to be connected to the server for most operations.
  - **Simple to Understand**: The workflow is straightforward for small teams.
- **Challenges**:
  - If the central server goes down, work halts for everyone.
  - Limited offline capabilities.

### Distributed Version Control Systems (DVCS)
- **How It Works**:
  - Each developer has a **complete copy** of the repository, including full version history.
  - Changes can be made offline and shared with others by syncing repositories.
- **Examples**: Git, Mercurial.
- **Key Features**:
  - **Decentralized Model**: No single point of failure since every developer has a full backup.
  - **Offline Work**: You can commit changes, view history, and work locally without a network.
  - **Collaboration**: Developers can push/pull changes to/from each other's repositories.
- **Advantages**:
  - Fast and reliable, as most operations are local.
  - Great for large teams and open-source projects.

## Design Philosophy of Git
- Git was designed with a focus on **distributed software development**, avoiding the limitations of centralized systems like SVN (Subversion) or CVS (Concurrent Versions Systems).

## Key Benefits of Git's Distributed Model

1. **Faster Commands**:
   - Since Git stores the repository locally, almost all actions are performed on the **local machine**, eliminating the need to communicate with a central server.
   - This leads to **faster commands** and the ability to **work offline** without workflow disruption.

2. **Stability**:
   - Git's distributed nature means each collaborator has a **backup** of the entire project.
   - This lowers the risk of **data loss** from server crashes or repository corruption, a common issue in centralized systems reliant on a single point of access.

3. **Isolated Environments**:
   - Every Git repository, whether **local or remote**, retains the **full history** of a project.
   - Having a complete and isolated environment allows users to experiment with **new features** before integrating them into the main project.

4. **Efficient Merging**:
   - Since each developer has their own local history, their development branches may diverge.
   - Git excels in handling **divergent histories**, making it **highly efficient** at **merging branches** and resolving conflicts between different lines of development.

---

# Git Components

## Four Key Components of a Git Repository
1. **The Working Directory**
2. **The Staging Area**
3. **Committed History**
4. **Development Branches**

---

### 1. The Working Directory
- **What It Is:**
  - The **working directory** is where you interact with your files during development.
  - It is where you **edit files**, **compile code**, and perform other tasks related to your project.
  - You can treat the working directory as a **normal folder** where you directly modify the contents of the project.

- **Git's Role:**
  - The working directory gives you access to Git's features, enabling you to **record changes**, **alter** files, and **transfer** them using Git commands.
  - Git keeps track of any changes you make in this directory before committing them to the project's history.

---

### 2. The Staging Area
- **What It Is:**
  - The **staging area** acts as an intermediary between the **working directory** and the **project history**.
  - It allows you to **prepare and organize changes before committing** them to the history.

- **Functionality:**
  - Instead of committing all changes at once, Git allows you to **group related changes** into a **changeset**.
  - Changes staged in this area are not part of the project's history until they are committed.
  - This gives you control over which changes to include in your commit.

---

### 3. Committed History
- **What It Is:**
  - Once changes are staged, you can **commit** them to the project history.
  - A **commit** records the state of the repository at a particular point in time.

- **Safety of Commits:**
  - Commits are considered "safe" in the sense that **Git does not alter them automatically**.
  - However, it is possible to **manually rewrite the project history** (e.g., with rebase or amend operations).

---

### 4. Development Branches
- **What They Are:**
  - Branches allow you to **fork the project history** and develop multiple features in **parallel**. 
  - Facilitates non linear project history.
  - A branch creates a divergent path for your work, enabling you to develop **independently** without disrupting the main project history.

- **Git Branches vs. Centralized Systems:**
  - Git branches are **lightweight**, **cheap to create**, and **simple to merge**.
  - Unlike centralized version control systems, **Git branches** are **easy to share** and manage.

- **Branching in Git:**
  - Git branches are used for everything from **long-running** features involving multiple contributors and to quick fixes, such as **5-minute patches**.
  - Many developers prefer to work in **dedicated topic branches**, keeping the main history branch (e.g., `main` or `master`) clean and reserved for **public releases**.

---

# Getting Started

## Install Git and SSH

### Install Git
```bash
$ sudo apt update
$ sudo apt install git
```

### Install OpenSSH
If OpenSSH is not already installed, use the following command:
```bash
$ sudo apt update
$ sudo apt install openssh-client
```

---

## Set Up SSH for GitHub

### Generate an SSH Key Pair
1. Run the command in your terminal.
    ```bash
    $ ssh-keygen -t ed25519 -C "your_email@example.com"
    ```
   - **`ssh-keygen`**: This is the command used to generate a new SSH key pair (a private and public key).
   - **`-t ed25519`**: Specifies the type of the key to be generated. In this case, **ED25519** is used, which is a modern, secure, and fast elliptic-curve algorithm.
   - **`-C "your_email@example.com"`**: This is a comment or label that will be associated with the key. It's often an email address that helps identify the key, especially when managing multiple keys.
2. It will prompt you to **enter a file in which to save the key**. If you just press **Enter**, it will save the key to the default location (`~/.ssh/id_ed25519`).
3. You will be asked to **enter a passphrase** for added security (optional). If you don't want a passphrase, just press **Enter**.
4. After that, the key pair will be generated:
   - The **private key** is stored in the file you specified (e.g., `~/.ssh/id_ed25519`).
   - The **public key** is stored in a corresponding file (e.g., `~/.ssh/id_ed25519.pub`).

### Add the SSH Key to the SSH Agent
Start the SSH agent:
```bash
$ eval $(ssh-agent -s)
```
* What does ```ssh-agent -s``` contain?
  ```bash
  $ ssh-agent -s  
  SSH_AUTH_SOCK=/tmp/ssh-abc12345/agent.1234; export SSH_AUTH_SOCK;
  SSH_AGENT_PID=1234; export SSH_AGENT_PID;
  echo Agent pid 1234;
  ```

Add your SSH **private key**:
```bash
$ ssh-add ~/.ssh/id_ed25519
```

### Add the SSH Key to GitHub
Copy the **public SSH key**:
```bash
$ cat ~/.ssh/id_ed25519.pub
```
Log in to your GitHub account, navigate to **Settings > SSH and GPG Keys**, and add the copied key.

---

## Test Your SSH Connection
Verify the SSH connection to GitHub:
```bash
$ ssh -T git@github.com
```
If successful, you should see:
```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Set SSH as Default for All Repositories
To always use SSH when cloning or interacting with repositories:
```bash
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
```
This modifies the `~/.gitconifg` file, which will look like the follow: 
```
[url "git@github.com:"]
          insteadOf = https://github.com/
```

## Configure Git

### Set User Information
Set your name and email, which will be recorded with your commits and also third-party services require them:
```bash
$ git config --global user.name "Naveen Srinivas"
$ git config --global user.email "tonaveensrinivas@gmail.com"
```
Use the `--global` flag to apply these settings globally (modifies the `~/.gitconfig file`) or omit it for repository-specific settings.

### Set Your Preferred Editor
Configure the default text editor for Git (e.g., VS Code):
```bash
$ git config --global core.editor "code --wait"
```
Replace `code --wait` with your preferred editor, like `nano` or `vim`. The `--wait` flag ensures Git waits for the editor to close before proceeding.

### Create Command Aliases
Simplify commonly used Git commands with aliases:
```bash
# Syntax:
$ git config [--global] alias.<alias_name> "<command>"

# Examples:
$ git config --global alias.st status
$ git config --global alias.pu "push -u origin main"
```

Here is how `~/.gitconfig` file would like after executing above commands:
```plaintext
[user]
	name = Naveen Srinivas
	email = tonaveensrinivas@gmail.com
[core]
	editor = code --wait
[alias]
	st = status
	pu = push -u origin main
```

### Explore More Options
Run `git help config` in the terminal to see all available configuration options.

---

## Summary of Git Configuration Commands
| Command  | Description |
|----------|-------------|
| `git config --global user.name "name"`| Sets the global Git username for all repositories.|
| `git config --global user.email "email"`| Sets the global Git email for all repositories.|
| `git config --global core.editor "editor --wait"`| Sets the default text editor for Git commands requiring user input, like commit messages.|
| `git config --global alias.alias_name "command"`| Creates a shortcut (alias) for a Git command.|
| `git help config`| Displays help information about Git configuration options.|

# Initializing Repositories

## Creating a New Repository:
  
To initialize a repository, run the following:
```bash
# Syntax
$ git init <path>

# Examples
$ git init 
$ git init ~/Documents/SampleProject
```
The `<path>` argument can be left blank to initialize the repository in the current directory. Git is **minimally invasive**; it only adds a `.git` directory in the root of your project folder.

## Cloning an Existing Repository:
Instead of initializing a new repository, you can **clone** an existing Git repository using ssh (preferred) or https:
```bash
# Syntax
$ git clone ssh://<user>@<host>/path/to/repo[.git]
$ git clone https://github.com/user/repo[.git]

# Examples
$ git clone ssh://git@github.com/rnaveensrinivas/GitRepo
$ git clone https://github.com/rnaveensrinivas/GitRepo
```
This command will create a full copy of the repository, including its history, working directory, staging area, and branch structure. Changes won't be visible to others until you push them to a public repository.

## Optional: Swtiching to use SSH Instead of HTTPS for Cloned Repositories

### Check Your Current Remote URL
You must be in a repository that is associated with Github to execute the following command. If you don't have one simply create a GitHub repository and clone it in local. 
- Run the following command:
```bash
$ git remote -v
```
If the URL starts with `https://`, then it uses HTTPS Protocol, it can be changed to use `ssh` with the following steps. 

### Update the Remote URL
Replace `username/repository` with your GitHub username and repository name:
```bash
$ git remote set-url origin git@github.com:username/repository.git
```

### Verify the Change
Check the updated remote URL:
```bash
$ git remote -v
```
The output should now display `git@github.com` instead of `https://`.

### Push Changes Using SSH
Push your changes without being prompted for a username and password:
```bash
$ git push
```
**Note**: You may have to provide ssh passphrase. 

### Optional: Set SSH as Default for All Repositories
- To always use SSH when cloning or interacting with repositories:
```bash
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
```

## Summary of Git Initialization Commands
| Command  | Description |
|----------|-------------|
| `git init`| Initializes a new Git repository in the current directory.|
| `git init path`| Initializes a new Git repository at the specified path.|
| `git clone ssh://<user>@<host>/path/to/repo[.git]`| Clones a repository from a remote server using an SSH URL with user and host details.|
| `git clone https://github.com/user/repo[.git]`| Clones a repository from GitHub or another remote server using an HTTPS URL.|
| `git remote -v`| Displays the list of remote repositories and their URLs.|
| `git remote url remote_name new_url`| Updates the URL for a specified remote repository.|

---

# Recording Changes
Version Control System's core job is to maintain a series of *safe* revisions of project. Git does this with the help of **snapshots**. 

## Git Snapshots
- Git records **snapshots** of the entire project instead of just diffs between files (as in SVN or CVS).
- Each **commit** in Git represents a complete snapshot of all project files at a given point in time, making Git faster and more reliable.
- Unlike systems that record incremental changes, Git stores the full version of each file in a commit.
  
### Advantages:
- Faster access to file versions.
- Avoids the need to regenerate file states when requested.

## The Staging Area (also called Index)

### What is the Staging Area?
- The **staging area** (also known as the **index**) is an intermediary between the **working directory** and the **committed history**.
- It allows you to **stage** (select) changes for the next commit, ensuring you can commit only the desired changes and not the entire working directory at once. 

---

### Staging Changes

#### Stage File Addition
To stage a file or directory, use `git add`. This prepares changes to be committed.

```bash
# Syntax
$ git add path_to_file_or_directory

# Examples
$ git add .           # Stages all changes in the current directory
$ git add adir/       # Stages changes in the "adir" directory
$ git add f1          # Stages the "f1" file
```

#### Stage File Deletion (Without Removing the File from the Working Directory)
To stage the removal of a file or directory, but keep it in the working directory, use `git rm --cached`. This removes the file from the staging area but leaves it in your local file system. 

**Note**: The file now becomes **untracked**. 

```bash
# Syntax
$ git rm [-r] --cached file_or_directory

# Examples
$ git rm --cached f1               # Stages the removal of the file "f1"
$ git rm -r --cached afolder/      # Stages the removal of the "afolder" directory
```

#### Using `git rm` on a Staged File:

```bash
# Trying to use "git rm" on a staged file (f1)
$ git rm f1
error: the following file has changes staged in the index:
    f1
(use --cached to keep the file, or -f to force removal)
```
This shows that you can't use `git rm` directly on a staged file unless you either:
1. Use the `--cached` option to only remove the file from the staging area, or
2. Use `-f` to force removal.

#### Using `git rm` on a Tracked File:

```bash
# Trying to use "git rm" on a tracked file (afolder/f4)
$ git rm afolder/f4
rm 'afolder/f4'    
```
This removes the file from the working directory and **stages the removal**

#### Using `rm` on a Staged File:

```bash
# Trying to use "rm" on a staged file (f1)
$ rm f1

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
  new file:   f1

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  deleted:    f1
```
Here, `rm` removes the file from the working directory but doesn't unstage it. You'll see the file listed under "Changes not staged for commit" in the `git status` output.

---

### Inspecting the Stage

#### Check the Status of the Repository:
To view the state of your repository and see which files are staged, modified, or untracked, use:
```bash
$ git status
```

**Output**:
- **Changes to be committed**: Files staged for commit.
- **Changes not staged for commit**: Modified files that are not yet staged.
- **Untracked files**: Files in the working directory that are not part of the repository.

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   f1

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   afolder/f3

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	f2
```

---

### Viewing Diffs

#### See Unstaged Changes
To view changes made in your working directory (but not yet staged for commit), use the following command:

```bash
# Syntax
$ git diff

# Example
$ git diff
diff --git a/afolder/f3 b/afolder/f3
index e69de29..3b18e51 100644
--- a/afolder/f3
+++ b/afolder/f3
@@ -0,0 +1 @@
+hello world
```
This shows the difference between your working directory and the last commit for unstaged files.

#### See Staged Changes
To view changes that have been staged for commit (but not yet committed), use the following command:

```bash
# Syntax
$ git diff --cached

# Example
$ git diff --cached
diff --git a/f1 b/f1
index e69de29..3b18e51 100644
--- a/f1
+++ b/f1
@@ -0,0 +1 @@
+hello world
```
This shows the difference between the staged changes and the last commit.

---

## Commits

### What is a Commit?
A **commit** represents a snapshot of your project at a specific point in time and acts as an **atomic unit** in Git's version control. Each commit contains:

- A **snapshot** of the entire project at the moment of committing.
- **Author information** (name and email).
- A **commit message** describing the changes.
- A **unique SHA-1 checksum** to ensure the commit's integrity and prevent unintended changes.

### Commit Process
To create a commit, stage the changes first and then commit the snapshot to your repository's history:

```bash
$ git commit
```

After running this command, you will be prompted to enter a **commit message** in your default text editor.

### Commit Message Format
Follow this format when writing commit messages:

1. **First Line (Summary)**: A brief description of the changes (50 characters or fewer).
2. **Second Line**: Leave this line blank.
3. **Following Lines**: A detailed explanation of the changes, reasons, or relevant ticket numbers.

**Example**:

```plaintext
Fixed bug in user authentication

Detailed fix for user authentication issues, including validation errors
and user session management.
```

**Note**: If you have a hard time give a short description for a commit, then you should split the commit into many commits. You take help of staging area for this. You can have **logical snapshots** instead of just chronological snapshots. 

---

#### Commit Message Rules

Short commit messages are typically used to provide a concise summary of changes. While they are brief, they should still follow best practices to ensure clarity and usefulness. Here are some rules for writing effective short commit messages:


1. **Keep It Under 50 Characters**
   - The message should fit within 50 characters for readability.
   - If more detail is needed, use the body section in a longer commit message.

2. **Use the Imperative Mood**
   - Write as if giving a command.
   - **Examples**:
     - ✅ "Fix broken navbar links"
     - ❌ "Fixed broken navbar links"

3. **Focus on the "What"**
   - Summarize what the change does, not how or why.
   - **Examples**:
     - ✅ "Add search bar to header"
     - ❌ "Add code for implementing the search bar"

4. **Avoid Noise**
   - Do not use vague terms like "Updated files" or "Changes made."
   - Be specific: "Remove unused imports" or "Optimize image loading."

5. **Use Consistent Style**
   - Maintain a uniform structure across all commits for consistency.
   - Decide as a team or individually on a style guide (e.g., capitalization, tense).

6. **Avoid Redundancy**
   - Skip prefixes like "Commit:" or "Change:."
   - The fact that it's a commit is implied.

7. **No Periods at the End**
   - Short commit messages do not require punctuation unless it's a complete sentence.

8. **Use Tags (Optional)**
   - For clarity in large projects, use a prefix or tag if helpful:
     - `[Bugfix] Fix crash on login`
     - `[UI] Update button styles`

**Examples of Good Short Commit Messages**:
- "Fix typo in README"
- "Update dependencies"
- "Add error handling for API calls"
- "Remove deprecated methods"
- "Refactor login logic"


---


### Committing Using Options

You can skip the default text editor and directly provide a commit message using the `-m` option:

```bash
# Syntax
$ git commit -m "commit message"

# Example
$ git commit -m "This is a commit message"
[master (root-commit) cbd9be4] This is a commit message
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 afile.txt
```

---

### Inspecting Commits

#### View Commit History:

To view commit history for a specified branch, use the following command: 
```bash
# Syntax
$ git log branch_name

# Example
$ git log main
commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message
```

To see the list of commits in the current branch, use the following command:

```bash
# Syntax
$ git log

# Example
$ git log
commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message
```

#### Useful Log Options:

##### Single-Line Log (Brief View):
To display the log in a brief, single-line format:

```bash
# Syntax
$ git log --oneline

# Example
$ git log --oneline
cbd9be4 (HEAD -> master) commit message
```

##### Log for a Specific File:
To view the log for a specific file, use:

```bash
# Syntax
$ git log [--oneline] file_or_directory

# Example
$ git log afile.txt
commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message

# Example with oneline option
$ git log --oneline afile.txt
cbd9be4 (HEAD -> master) commit message
```

##### Log for a Specific Range of Commits:
To view commits between two points, use the following syntax. Note that the commit marked as **`<since>` is excluded**, while **`<until>` is included**.

```bash
# Syntax
$ git log <since>..<until>

# Examples
$ git log
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

commit e09fdab287149a6c6a4c176b8c4a40df15284abd
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:03:24 2024 +0530

    changed file names

commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message

# Exclude cbd9be4 and include 169223b
$ git log cbd9be4..169223b
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

commit e09fdab287149a6c6a4c176b8c4a40df15284abd
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:03:24 2024 +0530

    changed file names

# Exclude e09fdab and include 169223b
$ git log e09fdab..169223b
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder
```

##### Display a Diffstat (Summary of Changes in Each Commit):
To show a diffstat summarizing the changes made in each commit, use:

```bash
# Syntax
$ git log --stat

# Example
$ git log --stat
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

afolder/f3 | 0
afolder/f4 | 0
2 files changed, 0 insertions(+), 0 deletions(-)

commit e09fdab287149a6c6a4c176b8c4a40df15284abd
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:03:24 2024 +0530

    changed file names

a => afile.txt | 0
afolder/f1     | 0
afolder/f2     | 0
3 files changed, 0 insertions(+), 0 deletions(-)

commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message

a | 0
1 file changed, 0 insertions(+), 0 deletions(-)
```

#### Visualizing History:
For a graphical view of the commit history, use the `gitk` tool, which is available as a separate program:

It is not installed by default. To install: 
```bash
$ sudo apt update
$ sudo apt install gitk -y
```

To launch gitk, just type `gitk`, which will open a GUI: 
```bash
$ gitk
```

--- 

## Tagging Commits

### What are Tags
Tags in Git are **pointers** to specific commits. They are **lightweight markers** that help you highlight important points in your project's history, such as release versions.

### Creating a Tag
To create a tag on the current commit, use the following syntax:

```bash
# Syntax
$ git tag <tag_name>

# Example
$ git tag v1.0
```

After creating the tag, you can see it in the commit log:

```bash
$ git log
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master, tag: v1.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

commit e09fdab287149a6c6a4c176b8c4a40df15284abd
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:03:24 2024 +0530

    changed file names
...
```

If you add a new commit, the tag will **remain with the previous commit**:

```bash
$ git log
commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder
...
```

### Creating an Annotated Tag
To create an **annotated tag** (a tag with a message), use the following syntax:

```bash
# Syntax
$ git tag -a <tag_name> -m "Tag Message"

# Example
$ git tag -a v2.0 -m "Initial release"
```

You can verify the tag in the commit log:

```bash
$ git log
commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master, tag: v2.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

...
```
---

### Listing Tags
To list all tags in the repository, use:

```bash
# Syntax
$ git tag

# Example
$ git tag
v1.0
v2.0
```

### Pushing Tags to Remote
By default, **tags are not automatically pushed** to the remote repository. To push a specific tag, use:

```bash
# Syntax 
$ git push origin <tag_name>
```

To **push all tags** at once:

```bash
# Syntax
$ git push --tags
```

### Viewing a Tag
To view the details of a tag, use the following command:

```bash
# Syntax
$ git show <tag_name>
```

#### Normal Tag
For a normal tag, this command will show details like the commit associated with the tag:

```bash
$ git show v1.0
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

diff --git a/afolder/f3 b/afolder/f3
new file mode 100644
index 0000000..e69de29
diff --git a/afolder/f4 b/afolder/f4
new file mode 100644
index 0000000..e69de29
```

#### Annotated Tag
For an annotated tag, additional information like the tagger's name and the tag message is included:

```bash
$ git show v2.0
tag v2.0
Tagger: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:24:26 2024 +0530

Initial release

commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master, tag: v2.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

diff --git a/afile.txt b/f1
similarity index 100%
rename from afile.txt
rename to f1
```

### Using Tags for Checkout
To check out a specific tag (in a detached HEAD state), use the following:

```bash
# Syntax
$ git checkout <tag_name>

# Example
$ git checkout v1.0
```

The output will look like this, **it's worth to take and read and follow it**. :

```bash
Note: switching to 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 169223b added some files in afolder
```

---

## Summary of Recording Changes Commands:
| Command                               | Description                                                                                       |
|---------------------------------------|---------------------------------------------------------------------------------------------------|
| `git add`                             | Stages all changes in the working directory for the next commit.                                  |
| `git add file/folder`                 | Stages specific files or folders for the next commit.                                             |
| `git rm`                              | Removes files from the working directory and stages the deletion for the next commit.             |
| `git rm --cached file`                | Removes a file from the staging area without deleting it from the working directory.              |
| `git rm -r --cached folder`           | Removes a folder from the staging area without deleting it from the working directory.            |
| `git status`                          | Shows the status of the working directory and staging area, listing changes to be committed.      |
| `git diff`                            | Displays unstaged changes in the working directory.                                               |
| `git diff --cached`                   | Displays changes staged for the next commit.                                                      |
| `git commit`                          | Commits staged changes to the repository.                                                         |
| `git commit -m "commit message"`      | Commits staged changes with a descriptive message in a single step.                               |
| `git log branch_name`                 | Displays the commit history of the repository for the specified branch.                           |
| `git log`                             | Displays the commit history of the repository.                                                    |
| `git log --oneline`                   | Shows a concise commit history with one commit per line.                                          |
| `git log --oneline file/folder`       | Shows a concise commit history for a specific file or folder.                                     |
| `git log <since>..<until>`            | Displays commits between two references (e.g., tags, branches), with `<since>` being exclusive.   |
| `git log --stat`                      | Shows commit history along with a summary of changes made in each commit.                         |
| `git tag tag_name`                    | Creates a lightweight tag for the current commit.                                                 |
| `git tag -a tag_name -m "tag message"`| Creates an annotated tag with a message for the current commit.                                   |
| `git tag`                             | Lists all tags in the repository.                                                                 |
| `git push origin tag_name`            | Pushes a specific tag to the remote repository.                                                   |
| `git push --tags`                     | Pushes all tags to the remote repository.                                                         |
| `git show tag_name`                   | Displays details of a specific tag, including the commit it references.                           |
| `git checkout tag_name`               | Checks out a specific tag, detaching the HEAD to a read-only state.                               |
| `gitk`                                | Opens a graphical tool to visualize the commit history.                                           |

---

# Undoing Changes
What's the point of having commits when you don't have the ability to undo changes? Git provides tools to undo changes at various stages, allowing you to correct mistakes or discard experiments without fear of breaking your code. These tools can help you reset the **working directory**, **staging area**, or even undo an **entire commit**.

---

## What Does Undoing Changes Mean?

- **Working Directory**: Reverting changes made to files before staging.
- **Staging Area**: Removing changes staged for a commit.
- **Commits**: Reverting or amending an entire commit.

---

## Undoing Changes in the Working Directory

### Reset to the Last Commit
To discard all uncommitted changes (in both the working directory and staging area), use:
```bash
# Syntax
$ git reset --hard HEAD

# Example
$ git status
On branch master
Changes to be committed:
  deleted:    afolder/f4
  modified:   f1

Changes not staged for commit:
  modified:   afolder/f3

Untracked files:
  commands
  f2

# Resetting the working directory and staging area to the last commit
$ git reset --hard HEAD
HEAD is now at 8325a85 changed file name

$ git status
On branch master
Untracked files:
  commands
  f2
nothing added to commit but untracked files present (use "git add" to track)
```

#### Key Points:
- `git reset --hard HEAD`: Resets the working directory and staging area to match the last commit.
- **Untracked Files**: Not affected by this command.

#### Remove Untracked Files
To delete untracked files:
```bash
# Syntax
$ git clean -f

# Example
$ git status
Untracked files:
  commands
  f2

# Removing untracked files
$ git clean -f
Removing commands
Removing f2

$ git status
nothing to commit, working tree clean
```

##### Key Points:
- `git clean -f`: Deletes untracked files from the working directory.
- **Force Option (`-f`)**: Required to confirm deletion of untracked files.

---

### Undo Changes to a Specific File
To restore a specific file to its state in the last commit:
```bash
# Syntax
$ git checkout HEAD <file>

# Example
$ git status
Changes not staged for commit:
  modified:   afolder/f2
  modified:   f1

Untracked files:
  f

# Reverting `f1` to the state of the last commit
$ git checkout HEAD f1
Updated 1 path from dd3c5af

$ git status
Changes not staged for commit:
  modified:   afolder/f2

Untracked files:
  f
```

#### Key Points
- Replaces the file in the working directory with the version from **HEAD** (last commit).
- Does not affect untracked files or project history.

---

## Undoing in the Staging Area

When a file is mistakenly added to the staging area, you can unstage it without affecting the changes in your working directory.

To remove a file from the staging area: 
```bash
$ git reset HEAD <file>
```

### Key points
* **Effect**: Moves the file from the staging area back to the working directory as an **unstaged change**.
* **Working Directory**: The file remains unchanged, preserving your modifications.
* This action is non-destructive, making it safe for recovering from accidental staging.


### What is the difference between `reset HEAD file` and `rm --cached file`?

| Command                   | Purpose                                    | Effect on Working Directory | Effect on Repository |
|---------------------------|--------------------------------------------|-----------------------------|-----------------------|
| `git reset HEAD <file>` | Unstages a file without deleting it.      | **Keeps the file unchanged**. | File remains tracked in the repository. |
| `git rm --cached <file>` | Removes a file from the repository's index (staging area) but leaves it in the working directory. | **Keeps the file intact** but marks it as untracked. | File is no longer tracked in the repository. |

### Key Differences:

1. **Use Case**:
   - `git reset HEAD <file>`: Used to **unstage changes** that were added with `git add` but not yet committed.
   - `git rm --cached <file>`: Used to **stop tracking a file** entirely, often for files that were mistakenly added to the repository (like large binaries or sensitive data).

2. **Impact on Tracking**:
   - `git reset HEAD <file>`: The file remains **tracked**; only its staging status changes.
   - `git rm --cached <file>`: The file is **untracked** by Git but stays in your working directory.

3. **Practical Example**:
   - `git reset HEAD example.txt`: Reverts `example.txt` from the staging area to the working directory, keeping it tracked for future commits.
   - `git rm --cached example.txt`: Stops tracking `example.txt` entirely but leaves it in the working directory as an untracked file.


## Undoing Commits

**Two Ways to Undo Commits**:
1. **Reset**: Removes a commit entirely from the history.
2. **Revert**: Creates a new commit that undoes the changes of a previous commit.

### Resetting Commits

The `git reset` command is used to move the `HEAD` pointer to a specific commit, effectively removing commits from the history. Depending on the mode, it can also preserve or discard changes.

The syntax for resetting the commits is as follows: 
```bash
$ git reset HEAD~<number>
```

#### Resetting the Most Recent Commit

The syntax for resetting the most recent commit is as follows: 
```bash
$ git reset HEAD~1
```

##### Example: Undo the Most Recent Commit
1. **Check Commit History**:
   ```bash
   $ git log
   commit bdab6c6e81cb82dd603db485c5e41c564a210dde (HEAD -> master)
   Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
   Date:   Sun Dec 29 05:37:31 2024 +0530

       bad commit

   commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (tag: v2.0)
   Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
   Date:   Sat Dec 28 18:19:52 2024 +0530

       changed file name
   ```

2. **Undo the Most Recent Commit**:
   ```bash
   $ git reset HEAD~1
   Unstaged changes after reset:
   M    afolder/f2
   ```

3. **Verify the New History**:
   ```bash
   $ git log
   commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master, tag: v2.0)
   Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
   Date:   Sat Dec 28 18:19:52 2024 +0530

       changed file name
   ```

---

#### Resetting to a Specific Commit

You can reset your repository to any commit in the history. Consider the following commit log:

```bash
$ git log
commit 173d36dddfc4c474ac38135f95dd00bb377ed9e8 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:58:47 2024 +0530

    updated f1
    fixed a typo in f1

... # bunch of commits

commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (tag: v2.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name
```

To reset your repository to `tag: v2.0`, there are **two options**:

---

##### Option 1: `git reset --soft`

1. **Command**:
   ```bash
   $ git reset --soft 8325a854   # Or git reset --soft v2.0
   ```

2. **Effect**:
   - Moves `HEAD` to `tag: v2.0`.
   - Removes all commits after `tag: v2.0`.
   - Preserves the changes from deleted commits and stages them.

3. **Example**:
   ```bash
   $ git reset --soft 8325a854

   $ git log
   commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master, tag: v2.0)
   Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
   Date:   Sat Dec 28 18:19:52 2024 +0530

       changed file name

   $ git status # notice how the deleted commit's changes are in staged.
   Changes to be committed:
     (use "git restore --staged <file>..." to unstage)
     modified:   f1
   ```

---

##### Option 2: `git reset --hard`

1. **Command**:
   ```bash
   $ git reset --hard 8325a854   # Or git reset --hard v2.0
   ```

2. **Effect**:
   - Moves `HEAD` to `tag: v2.0`.
   - Removes all commits after `tag: v2.0`.
   - Discards all changes from deleted commits, without saving them.

3. **Example**:
   ```bash
   $ git reset --hard 8325a854
   HEAD is now at 8325a85 changed file name
   ```

---

#### Key Points

1. **`HEAD~<number>`**: Refers to a specific number of commits back from the current `HEAD`.  
   - Example: `HEAD~3` moves 3 commits back.

2. **Modes of Reset**:
   - **Soft**: Keeps changes from deleted commits and stages them.
   - **Mixed (default)**: Keeps changes from deleted commits but unstages them.
   - **Hard**: Discards all changes from deleted commits.

3. **Rewriting History**:
   - Resetting rewrites commit history, which can lead to issues in collaborative projects if the commits have been shared. Use with caution!

4. **Safe Usage**:
   - Reset private commits that haven't been pushed.
   - Avoid resetting shared commits to prevent conflicts.
- 
### Reverting Commits

The `git revert` command is a safer alternative to `git reset`, particularly in public repositories. Instead of rewriting commit history, it **creates a new commit that reverses the changes introduced by a commit**.

```bash
$ git revert <commit-id>
```

---

#### Example: Reverting the Most Recent Commit

##### Step 1: Check the Commit History
```bash
$ git log
commit e4a9e9928f1648638e3292f5d0a36934ff18ecd6 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:42:51 2024 +0530

    bad commit

commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (tag: v2.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name
```

##### Step 2: Revert the Commit
```bash
$ git revert HEAD
hint: Waiting for your editor to close the file...
```

This opens the editor for a commit message. The default message typically includes the reverted commit details:

```plaintext
Revert "bad commit"

This reverts commit e4a9e9928f1648638e3292f5d0a36934ff18ecd6.
```

- Edit the message as needed and close the editor.  
- Once the editor is closed, the revert operation completes.

---

#### Step 3: Verify the Revert
```bash
$ git log
commit 442f724d702b6ac5199bfe80de8e08009b737019 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:47:13 2024 +0530

    Revert "bad commit"
    
    This reverts commit e4a9e9928f1648638e3292f5d0a36934ff18ecd6.
    
    Changed the file by mistake

commit e4a9e9928f1648638e3292f5d0a36934ff18ecd6
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:42:51 2024 +0530

    bad commit
```


#### Key Features of `git revert`

1. **Does Not Rewrite History**:
   - Unlike `git reset`, which modifies the commit history, `git revert` creates a new commit that cancels out the changes of the specified commit.

2. **Safe for Public Repositories**:
   - Since it avoids altering history, `git revert` is ideal for projects where multiple people are working collaboratively.

3. **Works on Specific Commits**:
   - You can revert any commit in the history, not just the latest one. Simply replace `HEAD` with the appropriate `<commit-id>`.

4. **Interactive Editor**:
   - The revert process opens a text editor for the new commit message. You can customize it or leave the default message.

---


## Amending Commits

Amending a commit allows you to **modify the most recent commit**, whether to include forgotten changes or fix the commit message. The syntax for ammending a commit: 
```bash
$ git commit --amend
```

### Example Workflow:

#### 1. Initial Commit:
Let's intentionally make a mistake and commit it. 
```bash
# Making a mistake. 
$ echo "hello wordl" > f1

# Commiting it. 
$ git add .
$ git commit -m "update f1"
[master 53932d1] update f1
1 file changed, 1 insertion(+)
```

#### 2. Check Commit History:
```bash
$ git log
commit 53932d1315f14a3a0bff75f24918848fc71b598c (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:58:47 2024 +0530

   update f1
...
```

#### 3. Make Corrections:

Fix the typo in `f1`:

```bash
$ echo "hello world" > f1
$ git add .
```

Amend the commit:

```bash
$ git commit --amend
hint: Waiting for your editor to close the file...
```

This opens the COMMIT_EDITOR, showing the current commit message:
```plaintext
update f1

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sun Dec 29 05:58:47 2024 +0530
#
# On branch master
# Changes to be committed:
#    modified:   f1
#
fix typo in f1
```
Edit the message if needed and save the file.

#### 4. Result:
```bash
# After closing the COMMIT_EDITOR windows:
[master 173d36d] update f1
Date: Sun Dec 29 05:58:47 2024 +0530
1 file changed, 1 insertion(+)

$ git log
commit 173d36dddfc4c474ac38135f95dd00bb377ed9e8 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sun Dec 29 05:58:47 2024 +0530

   update f1
    
   fix typo in f1
...
```

### Key Points:
- **Purpose**: Replaces the previous commit with a new one, incorporating changes to the message or content without creating a new commit.
- **Rewriting History**: Amending a commit changes its hash. **Avoid amending commits that have already been pushed or shared**, as this can cause issues for collaborators.

## Summary of Undoing Changes

| **Command**| **Description**|
|------------|----------------|
| `git reset --hard HEAD`| Resets the working directory to the state of the last commit.|
| `git clean -f`| **Deletes untracked files** from the working directory.|
| `git checkout HEAD <file>`| Reverts a specific file to its state in the last commit.|
| `git reset HEAD <file>`| Removes a file from the staging area, **leaving its changes in the working directory**. |
| `git rm --cached <file>`| Removes a file from the staging area, removing it from the repository and make it **untracked**. |
| `git reset HEAD~<number>`| Removes commits until the number from history and keeps its changes in the working directory. |
| `git reset HEAD~1`| Removes the last commit from history and keeps its changes in the working directory. |
| `git reset --hard <commit-id>`| Resets to a specific commit, **discarding all changes** after it.|
| `git reset --soft <commit-id>`| Resets to a specific commit, **keeping changes staged** but removing subsequent commits. |
| `git revert <commit-id>`| Creates a new commit that reverses the changes made by a specific commit.|
| `git revert HEAD`| Creates a new commit that reverses the changes made by a most recent commit.|
| `git commit --amend`| Edits the most recent commit message or adds changes to it.|

---

# Branches

Branches in Git allow you to create multiple development paths, enabling parallel work on different versions of a project. **When you create a new branch, you essentially get a new environment for working**, including an isolated working directory, staging area, and project history. 

Branches are **nothing but a pointer** to a commit. The default branch in any Git repo is **master**, which is created with first commit. Branches are nothing but files containing commit hash, you can view these files in `.git/refs/heads/branch_name`.

## Manipulating Branches

### Listing Branches  
You can view all your branches with the `git branch` command, which shows the current branch with an asterisk next to it:
```bash
# Syntax
$ git branch

# Example
$ git branch
* main
```

### Creating Branches
Create a new branch using the command:
```bash
# Syntax
$ git branch <name> [<base_branch>]

# Example
$ git branch sample_branch main
$ git branch
* main
  sample_branch
  develop
$ git branch feature/BBMC-5555 develop
```
This creates a new branch that points to the current commit, but it **does not automatically switch to it**.

### Deleting Branches
To delete a branch, use:
```bash
# Syntax
$ git branch -d <name>

# Example
$ git branch -d sample_branch 
Deleted branch sample_branch (was 8325a85).
```

If the branch has unmerged commits, Git will prevent the deletion to avoid data loss. You can force deletion with:

```bash
$ git branch -D <name>
```

### Checking Out Branches
To switch between branches, use the `git checkout` or `git switch` command:
```bash
# Syntax
$ git checkout <branch>
$ git switch <branch>

# Example
$ git checkout sample_branch 
Switched to branch 'sample_branch'

$ git switch sample_branch 
Switched to branch 'sample_branch'
```
**Note**: Before checking out, ensure that working directory is clean. Logically this makes sense, when you checkout, the **entire working directory is reconstructed from the .git repository**, if you leave something uncommited then those tracked files will be overriden or cleaned. 

### Creating and Checking out Simulataneously

#### 1. `git checkout -b <new-branch-name>`

- **Function:** 
  - Creates a new branch with the specified name.
  - Automatically switches the working directory to this new branch.

- **Usage Example:**
  ```bash
  $ git checkout -b feature/login
  ```
  This command:
  - Creates a new branch called `feature/login`.
  - Switches to the `feature/login` branch.

- **Behind the scenes:**
  - Equivalent to running:
    ```bash
    $ git branch <new-branch-name>
    $ git checkout <new-branch-name>
    ```
  - This two-step process (create and switch) is combined into one with the `-b` option.

#### 2. `git switch -c <new-branch-name>`

- **Function:** 
  - A newer and more intuitive command introduced in Git 2.23 (released in August 2019).
  - Similar to `git checkout -b`, it creates and switches to a new branch in a single step.

- **Usage Example:**
  ```bash
  $ git switch -c feature/login
  ```
  This command does the same as `git checkout -b feature/login`.

- **Why `git switch`?**
  - `git switch` was introduced to separate branch-related operations from file-related ones.
  - Makes it clear that you're working with branches and not modifying files in the working directory.

#### When to Use Which?

- **If you prefer older commands or are using an older version of Git (< 2.23):**
  Use `git checkout -b`.

- **If you're using Git 2.23 or later and prefer clarity:**
  Use `git switch -c`.

#### Key Notes:

1. **Naming the branch:**
   Ensure your branch name is descriptive and relevant to the work you'll be doing on it, e.g., `bugfix/payment`, `feature/signup`, etc.

2. **Branch creation context:**
   - The new branch is created from the **current branch's HEAD**. If you want to create it from a different branch, you must first switch to that branch or use `git switch`/`checkout` with additional options.

3. **Default branch movement:**
   By default, branches are based on the `HEAD` of your current branch unless you specify a different base.


### Detached HEADs
A detached HEAD occurs when you **checkout to a specific commit or tag** rather than a branch. In this state, any new commits won't belong to a branch and may be lost when switching branches. 
```bash
# Background
$ git log
commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> sample_branch, tag: v2.0, master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

...

# Checking out tag v1.0, we are warned!
$ git checkout v1.0
Note: switching to 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 169223b added some files in afolder
```

You can create a new branch from this state with:
```bash
$ git checkout -b <new-branch-name>
# or
$ git switch -c <new-branch-name>
```
---

## Merging Branches

Merging is used to combine changes from one branch into another. The general process involves two steps:

```bash
$ git checkout <branch_you_want_other_branch_to_merge_into>
$ git merge <other_branch_name>
```

This tells Git to merge the changes from `<other_branch_name>` into the branch you currently have checked out.

Internally git manages merging in two ways: 
1. **Fast-forward Merge**
2. **3-way Merge**
---

### 1. Fast-forward Merge

A fast-forward merge happens when there have been no new commits on the target branch since the branch was created. Git **simply moves the branch pointer forward** to include the commits from the other branch. **No new commits are created for merges.**

#### Example:

1. Assume the following branch structure:
   ```
   * Commit C (feature)
   |
   * Commit B
   |
   * Commit A (main)
   ```
   - `main` is the target branch.
   - `feature` is the branch to merge.

2. Commands:
   ```bash
   $ git checkout main
   $ git merge feature
   ```

3. Resulting branch structure:
   ```
   * Commit C (main, feature)
   |
   * Commit B
   |
   * Commit A
   ```
   The `main` branch now includes all commits from `feature`, and the `feature` branch pointer fast-forwards to the same commit as `main`.

---

### 2. Three-way Merge

A 3-way merge is required when the **two branches have diverged**, meaning both branches have new commits. Git uses the **common ancestor** of both branches and the changes on each branch to create a new **merge commit**. Two branch commits, and one common ancestor make up three commits, hence called three-way merge. 

#### Example:

1. Assume the following branch structure:
   ```
   (feature) D *          * Commit C (main)
                \        /
                 * Commit B
                 |
                 * Commit A
   ```
   - Both `main` and `feature` have unique commits (`C` and `D`, respectively).

2. Commands:
   ```bash
   $ git checkout main
   $ git merge feature
   ```

3. Resulting branch structure:
   ```
                  * Merge Commit (main)
                /        \
   (feature) D *          * Commit C
                \        /
                 * Commit B
                 |
                 * Commit A
   ```
   A **merge commit** is created to combine the changes from both branches.

---

### Merge Conflicts

If there are conflicting changes in the files between the two branches, Git will pause the merge and mark the conflicting files. You'll need to manually resolve it by editing the file.

1. Identify conflicts:
   ```bash
   $ git status
   ```
   Conflicting files will be listed with the status **both modified**.

2. Open the conflicting files and resolve conflicts:
   - Git marks conflicts in the file like this:
     ```diff
     <<<<<<< HEAD
     Changes from the current branch
     =======
     Changes from the branch being merged
     >>>>>>> <other_branch_name>
     ```
   - Edit the file to combine or choose the appropriate changes.

3. After fixing the conflict, stage the file with
   ```bash
   $ git add <conflicted_file>
   ```

4. Complete the merge:
   ```bash
   $ git commit
   ```
---

### Summary of Merge Strategies

| **Merge Type**| **When It Happens**| **Result**|
|---------------|--------------------|-----------|
| **Fast-forward Merge**  | When the target branch has no new commits since branching.| Moves the branch pointer forward, no new commit is created.|
| **3-way Merge**| When both branches have diverged with new commits.| Creates a new merge commit to combine changes.|
| **Merge Conflicts**| When changes in the branches conflict and cannot be automatically merged. | Requires manual resolution before completing the merge.|

## Rebasing
Rebasing is the process of moving a branch to a new base. Rebasing is better than merging when you want a **clean, linear commit history**. It eliminates unnecessary merge commits, making the project history easier to read and navigate. Merge Commit hold no significance apart from merging, hence having lot of merges may clutter the tree. Rebasing is particularly useful for feature branches being integrated into main branches, as it simplifies tracking changes and avoids the clutter of multiple merge points. However, it should be used cautiously in collaborative workflows to avoid issues from rewritten history.


### Basic Rebasing Workflow Syntax
1. Check out the branch you want to rebase:
```bash
$ git checkout some-feature
```
2. Rebase onto another branch:
```bash
$ git rebase master
```
- This moves the `some-feature` branch onto the tip of `master`, creating a linear history.

### Comparison: Rebase vs. Merge
#### Rebase
Creates a linear history by moving the branch onto the new base. No additional merge commits are created. Consider the following example: 
```
* Commit C (main)
|
|  * Commit D (some-feature)
|/
* Commit B
|
* Commit A
```

After rebasing, 
```
   * Commit D (some-feature)
 / 
* Commit C (main)
|
|  
|
* Commit B
|
* Commit A
```
#### Merge
- Combines branches using a merge commit.
- May result in a cluttered history if done repeatedly.
- Example:
```
                *   Merge Commit (main)
                |\  
                | * Commit D (some-feature)
                | |  
Commit C (main) * | 
                |/  
                * Commit B
                |
                * Commit A

```
### Advantages of Rebasing
- Creates a clean and linear history.
- Eliminates superfluous merge commits.
- Enhances readability and navigability of the project history.

### Disadvantages of Rebasing
- **History Rewriting**:
  - Rebasing creates new commits with different IDs, effectively destroying the original commits.
  - This can lead to issues in collaborative workflows if others are working on the same branch.

---

### Interactive Rebasing

#### Initial Commit History  
Imagine you have the following Git history for a feature branch (`some-feature`):  

```
* 7d2e4c8 Fix typos in the feature implementation
* 5b1a7c3 Add unit tests for the feature
* 3f8c6b2 Implement the feature logic
* e1f1d7a Initial commit for the feature
* a1f76d0 Latest commit on master
* b3c19e1 Older commit on master
```

The feature branch includes **four commits**:  
1. `e1f1d7a`: Initial commit for the feature  
2. `3f8c6b2`: Implement the feature logic  
3. `5b1a7c3`: Add unit tests for the feature  
4. `7d2e4c8`: Fix typos in the feature implementation  

You want to clean up this history by:  
- Combining the four feature branch commits into one.  
- Writing a single, meaningful commit message summarizing the changes.  

---

#### Step-by-Step Workflow

##### 1. Start Interactive Rebase
Run the following command:  
```bash
# Syntax
$ git rebase -i master
```  
This tells Git:  
- Rebase all commits in `some-feature` (`7d2e4c8`, `5b1a7c3`, `3f8c6b2`, `e1f1d7a`) onto `master` (`a1f76d0`).  

---

##### 2. Interactive Rebase Prompt
Git opens an editor showing the commits in the feature branch:  

```plaintext
pick e1f1d7a Initial commit for the feature
pick 3f8c6b2 Implement the feature logic
pick 5b1a7c3 Add unit tests for the feature
pick 7d2e4c8 Fix typos in the feature implementation
```

Each line represents a commit. The `pick` command means "keep this commit as is."  

---

##### 3. Modify the Rebase Instructions
To combine all four commits into one, change `pick` to `squash` for the last three commits:  

```plaintext
pick e1f1d7a Initial commit for the feature
squash 3f8c6b2 Implement the feature logic
squash 5b1a7c3 Add unit tests for the feature
squash 7d2e4c8 Fix typos in the feature implementation
```

**Explanation**:  
- The first commit (`pick e1f1d7a`) will remain as the base.  
- The changes from the next three commits will be **combined (squashed)** into the first commit.  

---

##### 4. Edit the Commit Message
Git prompts you to write a new commit message summarizing the combined changes:  

```plaintext
# This is a combination of 4 commits.
# The first commit's message is:
Initial commit for the feature

# The following commit messages will be discarded:
Implement the feature logic
Add unit tests for the feature
Fix typos in the feature implementation

# Write a new commit message:
Added a new feature with logic, tests, and typo fixes
```

**Tip**: Write a clear and descriptive message summarizing the changes.  

---

##### 5. View the Cleaned-Up Commit History
After completing the rebase, the branch history now looks like this:  

```
* 9d3f2a5 Added a new feature with logic, tests, and typo fixes
* a1f76d0 Latest commit on master
* b3c19e1 Older commit on master
```

**Key Changes**:  
- The four commits in the feature branch are now combined into one (`9d3f2a5`).  
- The history is clean, linear, and easier to understand.  

---

### Commands Used in Interactive Rebase

| **Command** | **Effect** | **Example Use Case** |
|-------------|------------|----------------------|
| **pick**    | Keep the commit as is. | Retain an important commit without changes. |
| **squash**  | Combine the commit with the previous one and merge their messages. | Reduce multiple related commits into one. |
| **fixup**   | Combine the commit with the previous one but discard its message. | Clean up small fixes without keeping commit messages. |
| **reword**  | Keep the commit but edit its message. | Clarify an unclear commit message. |
| **drop**    | Remove the commit from history. | Delete unnecessary or experimental commits. |
| **edit**    | Pause the rebase to make changes to the commit or files. | Modify a specific commit in the middle of history. |

---

### Best Practices for Interactive Rebase
1. **Use for Local Cleanup**:  
   - Squash commits and refine messages before sharing the branch with others.  

2. **Avoid Rebasing Public Branches**:  
   - Rewriting history on branches shared with others can cause conflicts.  

3. **Combine Related Commits**:  
   - Merge small, incremental commits into a single meaningful change.  

4. **Keep Commit Messages Clear**:  
   - Write descriptive and concise commit messages for easier collaboration.  

--- 

## Summary of Branches

| **Command**                            | **Description**                                                                 |
|----------------------------------------|---------------------------------------------------------------------------------|
| `git branch`                           | Lists all local branches in the repository.                                    |
| `git branch branch_name [base_branch_name]`| Creates a new branch with the specified name, based out of base branch     |
| `git branch -d branch_name`            | Deletes the specified branch (only if it has been fully merged).               |
| `git branch -D branch_name`            | Force deletes the specified branch, even if it has not been merged.            |
| `git checkout branch_name`             | Switches to the specified branch.                                              |
| `git switch branch_name`               | Another command to switch to the specified branch (preferred over `checkout`). |
| `git checkout -b branch_name`          | Creates a new branch and switches to it.                                       |
| `git switch -c branch_name`            | Creates a new branch and switches to it (preferred over `checkout`).           |
| `git checkout <commit-id>/<tags>`      | Checks out a specific commit or tag in a detached HEAD state.                  |
| **Merging**                            |                                                                                 |
| `git checkout branch_you_want_other_branch_to_merge_into`| Switches to the `branch_you_want_other_branch_to_merge_into` branch.|
| `git merge other_branch_name`| Merges the `other_branch_name` branch into the current branch (`branch_you_want_other_branch_to_merge_into`).               |
| **Rebasing (Opposite of Merging)**     |                                                                                 |
| `git checkout other_branch_name`| Switches to the `other_branch_name` branch.                                              |
| `git rebase branch_you_want_other_branch_to_rebase_into`| Reapplies the commits from `other_branch_name` onto `branch_you_want_other_branch_to_rebase_into` for a linear history.      |
| **Interactive Rebasing**               |                                                                                 |
| `git checkout other_branch_name`| Switches to the `other_branch_name` branch.                                              |
| `git rebase -i branch_you_want_other_branch_to_rebase_into`| Opens an interactive rebase session for `other_branch_name` on top of `branch_you_want_other_branch_to_rebase_into`.         |

---

# Branching Workflows

Git's lightweight and easy-to-merge branches make it a powerful tool for software development. 

## Key Commands for Branching Workflows
- `git branch`: Create, list, or delete branches.
- `git checkout`: Switch to another branch or restore files.
- `git merge`: Merge changes from one branch into another.
- `git rebase`: Reapply commits from one branch onto another to create a linear history.

---

## Types of Branches

Branches can be categorized into two main types:
1. **Permanent Branches**
2. **Topic Branches**
  
---


### Permanent Branches
- **Purpose**: These branches contain the main history of a project and serve as **integration points** for stable, finalized changes.
- **Characteristics**:
  - Typically long-lived and persist throughout the project lifecycle.
  - Often include branches like `master` (or `main`) and `develop`.
- **Common Workflows**:
  - Use `master` exclusively for stable, production-ready code.
  - Use an intermediate integration branch like `develop` for combining and testing features before merging them into `master`.
- **Example Workflow**:
  - Developers work on feature branches.
  - Feature branches are merged into `develop` for integration and testing.
  - Once stable, `develop` is merged into `master` for public release.
- **Benefits**:
  - Clear distinction between stable code and code under development.
  - Allows for orderly releases and minimizes risks to the production branch.

#### Example:
```plaintext
master ← develop ← [feature-1, feature-2, ...]
```
### Topic Branches

Topic branches are temporary and created for specific tasks or changes. They help keep the project organized and protect permanent branches from untested code.

#### Feature Branches
- **Purpose**: Encapsulate a new feature or refactor.
- **Characteristics**:
  - Typically stem from `develop` or another integration branch.
  - Not merged directly into `master`.
  - Short-lived and deleted after the feature is completed and integrated.
- **Benefits**:
  - Isolates new features from the main codebase until they are complete and tested.
  - Encourages parallel development by multiple contributors.

#### Example Workflow:
```plaintext
master ← develop ← feature/new-feature
```
1. Create a feature branch:
   ```bash
   # create a new branch based on develop
   git checkout -b feature/new-feature develop
   ```
2. Work on the feature and commit changes.
3. Merge the feature branch into `develop` when ready:
   ```bash
   git checkout develop
   git merge feature/new-feature
   ```
4. Delete the feature branch:
   ```bash
   git branch -d feature/new-feature
   ```

#### Hotfix Branches
- **Purpose**: Quickly patch bugs or issues in the production code.
- **Characteristics**:
  - Stem directly from `master` (or the public release branch).
  - Focus on critical bug fixes or updates that cannot wait for the next release cycle.
  - Merged back into both `master` and `develop` to keep branches synchronized.
- **Example Workflow**:
  - Developers work on feature branches.
  - Feature branches are merged into `develop` for integration and testing.
  - Once stable, `develop` is merged into `master` for public release.
- **Benefits**:
  - Ensures production issues are resolved quickly.
  - Maintains consistency across all branches.

#### Example Workflow:
```plaintext
master ← hotfix/fix-critical-bug
```
1. Create a hotfix branch:
   ```bash
   # create a hotfix branch based on master
   git checkout -b hotfix/fix-critical-bug master
   ```
2. Apply the patch and commit changes.
3. Merge the hotfix into `master`:
   ```bash
   git checkout master
   git merge hotfix/fix-critical-bug
   ```
4. Merge the hotfix into `develop` to synchronize:
   ```bash
   git checkout develop
   git merge hotfix/fix-critical-bug
   ```
5. Delete the hotfix branch:
   ```bash
   git branch -d hotfix/fix-critical-bug
   ```

## Sample Workflow
```
            hotfix/fix-critical-bug             hotfix/fix-critical-bug
          --*--                               --*--
v0.3     /   /      v0.4            v1.0     /   /
*---*---*---*---*---*---*---*---*---*---*---*---*---*---*  main
         \                     /
          *---*---*---*---*---*---*---*  develop
               \         /         \
                *---*---*           *---*---*---*---* feature/big-feature
                        feature/new-feature  \
                                              *---*---* UserStory
```

**Legend**:
- **`main`**: The stable, production-ready branch.
- **`develop`**: The integration branch where features are merged before being released.
- **`feature/*`**: Temporary branches for developing new features.
- **`hotfix/*`**: Urgent branches for fixing critical bugs directly on `main`.
- **`*`**: Commit points on the branches.
- **`v0.3`, `v0.4`, `v1.0`**: Version tags marking stable releases in the `main` branch.

### Branch Structure and Workflow

1. **Main Branch (`main`)**:
   - Holds stable, production-ready code.
   - Releases such as **v0.3**, **v0.4**, and **v1.0** are tagged from this branch.

2. **Develop Branch (`develop`)**:
   - Integrates feature developments.
   - Changes are merged here before going to `main`.

3. **Hotfix Branch (`hotfix/fix-critical-bug`)**:
   - Created from `main` for urgent bug fixes.
   - Once fixed, it's merged into both `main` and `develop` to ensure consistency.

4. **Feature Branches**:
   - **`feature/new-feature`** and **`feature/big-feature`** are created from `develop` to work on new functionality.
   - These are merged back into `develop` once the feature is ready.

### Branch Flow

- **Hotfixes** fix urgent issues in `main` and are merged back into `develop`.
- **Feature branches** are created from `develop`, worked on, and then merged back into `develop`.
- Once all features are integrated and tested, `develop` is merged into `main` for the next release.

## Branching Workflow Flexibility

- Git treats all branches equally — the roles and purposes of branches are purely **conventional**.
- Adapt these workflows to suit your project's needs.
- Understanding the mechanics of branches enables you to design custom workflows that align with your team's requirements and preferences.

## Summary of Key Points

- **Permanent Branches**:
  - `master` (stable, production-ready code).
  - `develop` (integration branch for combining features).
- **Topic Branches**:
  - Feature branches (encapsulate new features).
  - Hotfix branches (critical fixes for production).
- **Best Practices**:
  - Always branch off from the appropriate branch (`develop` for features, `master` for hotfixes).
  - Test and review changes before merging.
  - Delete topic branches after merging to keep the repository clean.

---

# Remote Repositories

## What is a Remote Repository?

A **remote repository** is a version of your project stored outside your local machine. It can be hosted on:  
- **Platforms**: GitHub, GitLab, or Bitbucket.  
- **Personal Systems**: Another developer's computer.  
- **Other Locations**: A network server or a shared file system.  

Remote is nothing but a bookmark(an identifier to path) to other repositories that are not in local.

### Why Use Remote Repositories?  
- Facilitate collaboration by allowing developers to share code and changes.  
- Enable distributed development workflows for teams.  

### Best Practices
1. Use **separate repositories** for individual developers' contributions.  
2. Create **branches** for feature development within a repository.  

---

## Managing Remote Repositories  

The `git remote` command helps manage remote repository connections.  

### Listing Remotes  
To see all configured remotes:  
```bash
# Command
$ git remote

# Example
$ git remote
origin
```  
Here, `origin` is the default remote added when a repository is cloned.  

To view remotes with their URLs:  
```bash
# Command
$ git remote -v

# Example
$ git remote -v
origin	git@github.com:user/repo (fetch)
origin	git@github.com:user/repo (push)
```  

---

### Adding a Remote  
To add a new remote repository:  
```bash
# Syntax
$ git remote add <remote_name> <url_ssh_http>

# Example
$ git remote add origin ssh://git@github.com/username/repo.git
```  
- `origin`: A common name for the primary remote repository.  
- `<url>`: The URL of the remote repository, accepts many network protocols including `file://`, `ssh://`, `http://`, and `git://`.  

---

### Deleting a Remote  
To remove a remote:  
```bash
# Command
$ git remote rm <branch_name>

# Example
git remote rm origin
```  
- This only deletes the reference to the remote from your local repository.  
- The actual remote repository remains unaffected.  

---

## Working with Remote Branches  

### What are Remote Branches?  
Remote repositories communicate via **remote branches**. Remote branches are just like local branches, but they represent a "local" branch in someone else's repository. Remote branches represent the state of branches in a remote repository. Example: `origin/master` refers to the `master` branch in the `origin` remote repository.  

---

### Fetching Remote Branches  
The act of downloading branches from another repository is called **fetching**. Fetching downloads **changes** from the remote repository without merging them into your local branches. 

Git will never automatically fetch branches, this needs to be done manually. This is done by design, since one doens't have to worry about others' changes when working in an isolated environment. 

#### Fetch a specific branch:
```bash
# Syntax
$ git fetch <remote_name> <branch_name>

# Example
$ git fetch origin master
```  
Downloads the latest `master` branch from the `origin` remote.  

#### Fetch all branches:
```bash
# Syntax
$ git fetch <remote_name>

# Example
git fetch origin
```  

#### List all remote branches:
Remote branches are prefixed with remote name and are red in color. 
```bash
# Syntax
$ git branch -r

# Example
$ git branch -r
origin/master  
origin/feature/some-feature  
```  

### List all branches (remote and local): 
```bash
# Syntax 
$ git branch -a

# Example 
$ git branch
* main
$ git branch -r
  origin/HEAD -> origin/main
  origin/main
$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```

#### Color coding 
* **Remote branches** are printed in **red colour**. 
* **Local branches** are printed in **green colour**.

---

### Inspecting Remote Branches  

**Remote branches behave like read-only.** To interact with them, you cannot continue developing them before integrating them into you rlocal repository. This is also done by desing because remote branches are *copies* of other users' commits.   

#### Check out a remote branch:
```bash
$ git checkout origin/feature/some-feature
```  
**Note:** This puts you in a **detached HEAD** state, where you're not on any local branch.  

#### Compare commits between a local branch and a remote branch:
The `..` syntax is very useful for filterning log history. It's a good idea to **run this before merging chagnges** so you know exactly what you're integrating. 
```bash
$ git log master..origin/master
```  
**Result:** Displays commits in `origin/master` that are not in your local `master`.  

--- 

## Integrating Changes from Remote Branches
We have got the new changes and we inspected them. The next thing is to combine them into working directory. And, the whole point of fetching is to integrate the resulting remote branches into local. 

### Merging Changes
Use `git merge` to integrate changes from a remote branch into your feature branch:
```bash
# Syntax
$ git checkout some-feature
$ git fetch origin
$ git merge origin/master
```

Let's consider an ASCII art expalanation: 

**Legend**:
| Symbol            | Description                                   |
|-------------------|-----------------------------------------------|
| `*`               | Individual commits in the repository          |
| `master`          | The local master branch                       |
| `origin/master`   | The master branch on the remote repository    |
| `some-feature`    | A feature branch created off the master branch|
| `\` or `/`        | Indicates branch divergence or merging point  |

#### Before the Merge
```plaintext
               master      origin/master
--- ---*---*---*---*---*---*
                \
                 *---*---* some-feature**Summary**
```

1. **Branches**:
   - The `master` branch (local) and `origin/master` (remote copy) are updated independently with different commits.
   - `some-feature` is a separate branch created for a new feature. It was originally branched from `master` but now has additional commits.

2. **Need for Merge**:
   - To ensure `some-feature` has the latest changes from `origin/master`, a merge is required. This avoids potential conflicts during future integrations.

---

#### After the Merge
```plaintext
               master      origin/master
--- ---*---*---*---*---*---*
                \           \
                 *---*---*---* some-feature (merged with origin/master)
```

1. **Integration**:
   - The changes from `origin/master` are fetched and integrated into `some-feature` using `git merge`.
   - `some-feature` now includes all updates from the remote master branch (`origin/master`) while retaining its unique commits.

2. **Merged Timeline**:
   - A new commit is created in `some-feature` to record the merge, showing the integration of the `origin/master` updates.


### Rebasing Changes
Use `git rebase` to update your feature branch with changes from the remote branch by rewriting the commit history.  

```bash
# Syntax
$ git checkout some-feature
$ git fetch origin
$ git rebase origin/master
```

Let's consider an ASCII art expalanation: 

#### Before the Rebase
```plaintext
               master      origin/master
--- ---*---*---*---*---*---*
                \
                 *---*---* some-feature
```

#### After the Rebase
```plaintext
               master      origin/master
--- ---*---*---*---*---*---*
                             \
                              *---*---* some-feature (rebased onto origin/master)
```

#### Explanation of the Rebase Workflow  

**Before the Rebase**  
- **Branches**:
  - `some-feature` branch diverged from `master` and has its own unique commits.  
  - The `origin/master` branch contains new updates that are missing from `some-feature`.  

- **Need for Rebase**:
  - To apply the updates from `origin/master` onto `some-feature`, ensuring it is up-to-date without creating a merge commit.  

**After the Rebase**  
- **Rewritten Timeline**:
  - The commits in `some-feature` are reapplied on top of the latest `origin/master`.  
  - No merge commit is created, resulting in a cleaner, linear commit history.  


### Pulling Changes
`git pull` combines fetch and merge [rebase] in one step:
```bash
$ git pull [--rebase] origin master
```

#### Setting Rebase as Default for `git pull`

To always use `rebase` instead of `merge` for `git pull`:
1. **Globally for all repositories:**
   ```bash
   git config --global pull.rebase true
   ```
2. **For a specific repository:**
   ```bash
   git config pull.rebase true
   ```

   - To check the current setting:
    ```bash
    git config pull.rebase
    ```

## Pushing Changes to Remote Repositories
When pushing to remote, we create **local** branches in remote. But if the remote where to **fetch** from us, it would create **remote branch**. 

### Pushing a Branch
To push your local branch to a remote:
```bash
# Syntax
git push <remote> <branch>

# Example
git push origin my-feature
```
This uploads `my-feature` to the `origin` remote. 

**Note**: 
- If the remote workflow is ahead in commit, then we will have to fetch-rebase and send off. 
- `push` adds the changes to remote without notice, imagine seeing lot of changes that you didn't even inted to get. 
  - For example: 
    ```plaintext
    Mary's Repository before pushing
    
    ---*---*---* master

    Mary's Repository after pushing

    ---*---*---* master
                \
                 *---*---* my-feature (local branch, since we pushed it)
    ```
  - In the above ASCII art, `my-feature` is **local branch** for Mary, if she had fetched, it would be **remote-branch**. 

### `git push -u origin main`

The command `git push -u origin main` serves two purposes:

#### 1. Push the Local `main` Branch to the Remote `origin` Repository

- `git push`: Pushes the changes from your local repository to the remote repository.  
- `origin`: Refers to the name of the remote repository (default name when you clone a repository).  
- `main`: The branch you want to push.  

When executed, this command uploads your local `main` branch to the remote repository named `origin`.

---

#### 2. Set the `main` Branch as the Upstream for Future Push/Pull

- `-u` (or `--set-upstream`):  
  - Links your local `main` branch to the remote `origin/main` branch.  
  - After this, you can simply use `git push` or `git pull` without specifying the remote and branch name again.  

This simplifies workflows by establishing a tracking relationship between your local branch and the remote branch.

---

#### Detailed Workflow

##### Scenario  
You have a local repository with a `main` branch. The remote repository exists but doesn't yet have a `main` branch.

1. **Before the command:**
```plaintext
Local: main branch exists.
Remote: No main branch yet.
```

1. **Run the command:**
```bash
git push -u origin main
```

1. **Result after the command:**
- The `main` branch is created in the remote repository and populated with the contents of your local branch.
- Your local branch now tracks `origin/main`.

```plaintext
Local: main (tracking origin/main)
Remote: main branch now exists.
```

---

#### Why Use `-u`?

- To save time. Once the tracking relationship is established, you can:
  - Push updates using `git push` instead of `git push origin main`.
  - Pull changes using `git pull` instead of `git pull origin main`.

---

#### Example Usage

##### Initial Push
```bash
$ git push -u origin main
```

##### Subsequent Pushes
```bash
$ git push
```

##### Pull Changes
```bash
$ git pull
```

Using `git push -u origin main` is a common practice when you push a branch to a remote repository for the first time. It simplifies future commands by linking the local branch to its remote counterpart.

---

### Push to Colleague
- Pushing to a colleague's repository:
```bash
git push mary my-feature
```
- Sends your `my-feature` branch to Mary's remote repository.

### Caution with Pushing
- Avoid creating unnecessary branches on the remote repository:
  - Pushing creates remote branches visible to all collaborators.
  - Coordinate with your team to avoid cluttering the repository.

---

## Summary of Remote Repositories

| **Command**| **Description**|
|------------|----------------|
| `git remote`| Lists all remote repositories configured in the local repository.|
| `git remote -v`| Displays the full URLs of the configured remote repositories.|
| `git remote add remote_name url`| Adds a new remote repository with a friendly name (`remote_name`) and its URL. |
| `git remote rm remote_name`| Removes the specified remote repository connection.|
| `git fetch remote_name branch_name`| Fetches updates from the specified branch of the remote repository.|
| `git fetch remote_name`| Fetches updates from all branches of the specified remote repository.|
| `git branch -r`| Lists all remote branches available.|
| **Fetching and Merging**||
| `git fetch remote_name`| Fetches changes from the remote repository without merging them.|
| `git merge remote_name/master`| Merges changes from the remote `master` branch into the current branch.|
| **Shortcut for Fetch + Merge**||
| `git pull remote_name master`| Fetches and merges changes from the remote `master` branch into the current branch. |
| **Fetching and Rebasing**||
| `git fetch remote_name`| Fetches changes from the remote repository without merging them.|
| `git rebase remote_name/master`| Rebases the current branch on top of the remote `master` branch.|
| **Shortcut for Fetch + Rebase**||
| `git pull --rebase remote_name master`| Fetches and rebases changes from the remote `master` branch into the current branch. |
| **Pushing Changes**||
| `git push remote_name branch_name`| Pushes the specified local branch to the remote repository.|
| `git push -u remote_name branch_name` | Pushes the branch and sets the upstream branch for future pushes/pulls.|

---

# Remote Workflows

Remote workflows describe how multiple developers collaborate on a project by sharing code through remote repositories. There are two common models for collaboration:

1. **Centralized Workflow**
2. **Integrator Workflow**

Git treats all repositories as equal, unlike SVN or CVS, which have a single "master" repository. In Git, the **central repository is just a project convention**.


## Public (Bare) Repositories

- **Public repositories** are central locations where developers pull and push their changes and collaborate on a project but do not work with it directly. These repositories are designed to be accessible to multiple developers, making it easier to contribute to a shared codebase.
  
- **Bare repositories** are a special type of repository that are intended for collaboration. Unlike standard repositories, a bare repository does not contain a working directory (the actual files of the project). This design ensures that the repository is not used for development directly, but rather serves as a central hub where changes are pushed and pulled from.

  - The absence of a working directory in bare repositories prevents accidental overwriting of files and ensures that developers only push their changes, rather than modifying or deleting files directly.
  
  - To create a bare repository, you can use the following command:
    ```bash
    git init --bare <path>
    ```

  - Example: If you want to create a bare repository named `some-repo.git`, you would use:
    ```bash
    git init --bare some-repo.git
    ```

This setup is ideal for collaboration, as developers will clone this repository and push their changes to it. However, they will not modify files directly in the bare repository itself.

---

## The Centralized Workflow

The **centralized workflow** is best suited for small teams where **all developers have write access** to the central repository.

### Workflow:

1. **Work locally**: Developers work on their local repositories.
2. **Merge feature branches**: Once a developer completes a feature, they merge their feature branch into their local `master` branch.
3. **Push changes**: The developer pushes the merged `master` branch to the central repository.
4. **Fetch and integrate**: Other developers fetch the latest changes from the central repository and integrate them into their local repositories.

---

### Issues in the Centralized Workflow:

Conflicts may arise if multiple developers try to push changes to the central repository simultaneously. For example, if Developer John pushes changes before Developer Mary, she might encounter a **non-fast-forward error**:

```
! [rejected] master -> master (non-fast-forward)
error: failed to push some refs to 'some-repo.git'
```

#### To resolve the conflict:

1. **Fetch the latest changes** from the central repository:
   ```bash
   git fetch origin master
   ```

2. **Rebase her changes** on top of the latest version from the central repository:
   ```bash
   git rebase origin/master
   ```

3. **Push her changes** to the central repository:
   ```bash
   git push origin master
   ```

---

### Advantages of the Centralized Workflow

- **Simple setup**: Only one central server is required.
- **Ideal for small teams**: This workflow is well-suited for teams where developers have trusted access to the central repository.

---

## The Integrator Workflow

The **integrator workflow** addresses **scalability and security concerns** that arise in the centralized model. In this workflow, developers maintain both a **private** and a **public repository**. The **public repository** is used for pushing changes, while an **integrator** (project maintainer) fetches, reviews, and merges those changes into the central project repository.

---

### Workflow in the Integrator Model:

1. **Contributors work on their own repositories**: A contributor makes a fix or adds a feature in **their private repository**.
2. **Integrator fetches changes**: The integrator **uses a read-only HTTP protocol** to fetch the changes from the contributor's public repository.
3. **Review and merge**: After reviewing the changes, the integrator merges them into their local branch and pushes the updates to the official repository.
4. **Limited push access for contributors**: Contributors only need push access to their own repositories, not the central repository.

---

### Security and Scalability in the Integrator Workflow:

- **Security**: Contributors can only push changes to their own repositories, ensuring that no unauthorized changes can reach the central repository.
- **Scalability**: By allowing independent contributions from many developers, this model avoids bottlenecks in the central repository.

---

### Key Characteristics of the Integrator Workflow:

- **Official repository**: A single official repository is designated for the project, ensuring order and synchronization.
- **Multiple remotes**: Integrators manage multiple remotes to maintain flexibility and security while handling contributions.
- **Ideal for open-source projects**: This workflow is particularly effective for **open-source projects** where many developers contribute.

## Comparison of Centralized and Integrator Workflows
- **Centralized Workflow**: Best for small teams with direct access to the central repository.
  - Simple and easy to set up but may lead to conflicts when multiple developers push at the same time.
- **Integrator Workflow**: Ideal for larger teams or open-source projects, offering better security and scalability.
  - Contributors push to their own repositories, while integrators review and merge changes into the central repository.

### Conclusion
- Git's distributed nature makes the **integrator workflow** perfect for large-scale open-source projects.
- The **centralized workflow** is better for small teams but can face issues when multiple developers try to update the central repository at once.'

# Cheat Sheet

| Command  | Description |
|----------|-------------|
| **Basic Commands**    |
| `git config --global user.name "name"`| Sets the global Git username for all repositories.|
| `git config --global user.email "email"`| Sets the global Git email for all repositories.|
| `git config --global core.editor "editor --wait"`| Sets the default text editor for Git commands requiring user input, like commit messages.|
| `git config --global alias.alias_name "command"`| Creates a shortcut (alias) for a Git command.|
| `git help config`| Displays help information about Git configuration options.|
| _______________________________ |
| **Git Initialization Commands** | 
| `git init`| Initializes a new Git repository in the current directory.|
| `git init path`| Initializes a new Git repository at the specified path.|
| `git clone ssh://<user>@<host>/path/to/repo[.git]`| Clones a repository from a remote server using an SSH URL with user and host details.|
| `git clone https://github.com/user/repo[.git]`| Clones a repository from GitHub or another remote server using an HTTPS URL.|
| `git remote -v`| Displays the list of remote repositories and their URLs.|
| `git remote url remote_name new_url`| Updates the URL for a specified remote repository.|
| ______________________________ |
| **Recording Changes Commands** | 
| `git add`                             | Stages all changes in the working directory for the next commit.                                  |
| `git add file/folder`                 | Stages specific files or folders for the next commit.                                             |
| `git rm`                              | Removes files from the working directory and stages the deletion for the next commit.  Makes the file or folder untracked          |
| `git rm --cached file`                | Removes a file from the staging area without deleting it from the working directory. Makes the file untracked.             |
| `git rm -r --cached folder`           | Removes a folder from the staging area without deleting it from the working directory. Makes the folder untracked.           |
| `git status`                          | Shows the status of the working directory and staging area, listing changes to be committed.      |
| `git diff`                            | Displays unstaged changes in the working directory.                                               |
| `git diff --cached`                   | Displays changes staged for the next commit.                                                      |
| `git commit`                          | Commits staged changes to the repository.                                                         |
| `git commit -m "commit message"`      | Commits staged changes with a descriptive message in a single step.                               |
| `git log branch_name`                 | Displays the commit history of the repository for the specified branch.                           |
| `git log`                             | Displays the commit history of the repository.                                                    |
| `git log --oneline`                   | Shows a concise commit history with one commit per line.                                          |
| `git log --oneline file/folder`       | Shows a concise commit history for a specific file or folder.                                     |
| `git log <since>..<until>`            | Displays commits between two references (e.g., tags, branches), with `<since>` being exclusive.   |
| `git log --stat`                      | Shows commit history along with a summary of changes made in each commit.                         |
| `git tag tag_name`                    | Creates a lightweight tag for the current commit.                                                 |
| `git tag -a tag_name -m "tag message"`| Creates an annotated tag with a message for the current commit.                                   |
| `git tag`                             | Lists all tags in the repository.                                                                 |
| `git push origin tag_name`            | Pushes a specific tag to the remote repository.                                                   |
| `git push --tags`                     | Pushes all tags to the remote repository.                                                         |
| `git show tag_name`                   | Displays details of a specific tag, including the commit it references.                           |
| `git checkout tag_name`               | Checks out a specific tag, detaching the HEAD to a read-only state.                               |
| `gitk`                                | Opens a graphical tool to visualize the commit history.                                           |
| ____________________ |
| **Undoing Commands** | 
| `git reset --hard HEAD`| Resets the working directory to the state of the last commit.|
| `git clean -f`| **Deletes untracked files** from the working directory.|
| `git checkout HEAD <file>`| Reverts a specific file to its state in the last commit.|
| `git reset HEAD <file>`| Removes a file from the staging area, **leaving its changes in the working directory** and keeping it **tracked**. |
| `git rm --cached <file>`| Removes a file from the staging area, removing it from the repository and make it **untracked**. |
| `git reset HEAD~<number>`| Removes commits until the number from history and keeps its changes in the working directory. |
| `git reset HEAD~1`| Removes the last commit from history and keeps its changes in the working directory. |
| `git reset --hard <commit-id>`| Resets to a specific commit, **discarding all changes** after it.|
| `git reset --soft <commit-id>`| Resets to a specific commit, **keeping changes staged** but removing subsequent commits. |
| `git reset <commit-id>`| Resets to a specific commit, **keeping changes unstaged (in working directory)** but removing subsequent commits. |
| `git revert <commit-id>`| Creates a new commit that reverses the changes made by a specific commit.|
| `git revert HEAD`| Creates a new commit that reverses the changes made by a most recent commit.|
| `git commit --amend`| Edits the most recent commit message or adds changes to it.|
| ______________________ |
| **Branching Commands** | 
| `git branch`                           | Lists all local branches in the repository.                                    |
| `git branch branch_name [base_branch_name]`| Creates a new branch with the specified name, based out of base branch     |
| `git branch -d branch_name`            | Deletes the specified branch (only if it has been fully merged).               |
| `git branch -D branch_name`            | Force deletes the specified branch, even if it has not been merged.            |
| `git checkout branch_name`             | Switches to the specified branch.                                              |
| `git switch branch_name`               | Another command to switch to the specified branch (preferred over `checkout`). |
| `git checkout -b branch_name`          | Creates a new branch and switches to it.                                       |
| `git switch -c branch_name`            | Creates a new branch and switches to it (preferred over `checkout`).           |
| `git checkout <commit-id>/<tags>`      | Checks out a specific commit or tag in a detached HEAD state.                  |
| **Merging**                            |                                                                                 |
| `git checkout branch_you_want_other_branch_to_merge_into`| Switches to the `branch_you_want_other_branch_to_merge_into` branch.|
| `git merge other_branch_name`| Merges the `other_branch_name` branch into the current branch (`branch_you_want_other_branch_to_merge_into`).               |
| **Rebasing (Opposite of Merging)**     |                                                                                 |
| `git checkout other_branch_name`| Switches to the `other_branch_name` branch.                                              |
| `git rebase branch_you_want_other_branch_to_rebase_into`| Reapplies the commits from `other_branch_name` onto `branch_you_want_other_branch_to_rebase_into` for a linear history.      |
| **Interactive Rebasing**               |                                                                                 |
| `git checkout other_branch_name`| Switches to the `other_branch_name` branch.                                              |
| `git rebase -i branch_you_want_other_branch_to_rebase_into`| Opens an interactive rebase session for `other_branch_name` on top of `branch_you_want_other_branch_to_rebase_into`.         |
| ______________________________ |
| **Remote Repository Commands** | 
| `git remote`| Lists all remote repositories configured in the local repository.|
| `git remote -v`| Displays the full URLs of the configured remote repositories.|
| `git remote add remote_name url`| Adds a new remote repository with a friendly name (`remote_name`) and its URL. |
| `git remote rm remote_name`| Removes the specified remote repository connection.|
| `git fetch remote_name branch_name`| Fetches updates from the specified branch of the remote repository.|
| `git fetch remote_name`| Fetches updates from all branches of the specified remote repository.|
| `git branch -r`| Lists all remote branches available.|
| `git branch -a`| Lists all branches (remote and local) available.|
| **Fetching and Merging**||
| `git checkout branch_you_want_remote_to_merge_into` | |
| `git fetch remote_name`| Fetches changes from the remote repository without merging them.|
| `git merge remote_name/master`| Merges changes from the remote `master` branch into the current branch.|
| **Shortcut for Fetch + Merge**||
| `git pull remote_name master`| Fetches and merges changes from the remote `master` branch into the current branch. |
| **Fetching and Rebasing**||
| `git checkout branch_you_want_remote_to_rebase_into` | |
| `git fetch remote_name`| Fetches changes from the remote repository without merging them.|
| `git rebase remote_name/master`| Rebases the current branch on top of the remote `master` branch.|
| **Shortcut for Fetch + Rebase**||
| `git pull --rebase remote_name master`| Fetches and rebases changes from the remote `master` branch into the current branch. |
| **Pushing Changes**||
| `git push remote_name branch_name`| Pushes the specified local branch to the remote repository.|
| `git push -u remote_name branch_name` | Pushes the branch and sets the upstream branch for future pushes/pulls.|

---