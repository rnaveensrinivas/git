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

- **Definition**: Version control is a system that tracks changes to files over time, enabling collaboration and version management.

- **Key Benefits**:
  - Maintains a **history of changes**, allowing you to view or revert to earlier versions.
  - Facilitates **collaboration** by letting multiple people work on the same project simultaneously.
  - Tracks **who made what changes** and when, providing accountability.
  - Reduces risk by serving as a **backup system** for your code or files.

- **Types of Version Control**:
  - **Local Version Control**: Stores changes on a single machine. Simple but limited for collaboration.
  - **Centralized Version Control**: Uses a central server to store files and version history (e.g., SVN, CVS).
  - **Distributed Version Control**: Each user has a complete copy of the repository (e.g., Git, Mercurial).

- **Common Use Cases**:
  - Software development (code management).
  - Document versioning and collaborative editing.
  - Managing configuration files and scripts.

- **Popular Tools**:
  - Git, Mercurial, Subversion (SVN), CVS.
  - Hosting services like GitHub, GitLab, and Bitbucket simplify sharing and collaboration.

- **Why It’s Essential**:
  - Helps avoid overwriting others' work.
  - Enables parallel development.
  - Provides a safety net against accidental data loss or errors.

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
  - The working directory gives you access to Git’s features, enabling you to **record changes**, **alter** files, and **transfer** them using Git commands.
  - Git keeps track of any changes you make in this directory before committing them to the project’s history.

---

### 2. The Staging Area
- **What It Is:**
  - The **staging area** acts as an intermediary between the **working directory** and the **project history**.
  - It allows you to prepare and organize changes before committing them to the history.

- **Functionality:**
  - Instead of committing all changes at once, Git allows you to **group related changes** into a **changeset**.
  - Changes staged in this area are not part of the project’s history until they are committed.
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
  - A branch creates a divergent path for your work, enabling you to develop **independently** without disrupting the main project history.

- **Git Branches vs. Centralized Systems:**
  - Git branches are **lightweight**, **cheap to create**, and **simple to merge**.
  - Unlike centralized version control systems, **Git branches** are **easy to share** and manage.

- **Branching in Git:**
  - Git branches are commonly used for:
    - **Long-running features** with multiple contributors.
    - **Quick fixes** (e.g., 5-minute patches).
  - Many developers prefer to work in **dedicated topic branches**, keeping the main history branch (e.g., `main` or `master`) clean and reserved for **public releases**.

# Getting Started

## **Step 1: Install Git and SSH**

### 1. **Install Git**
```bash
sudo apt update
sudo apt install git
```

### 2. **Install OpenSSH**
- If OpenSSH is not already installed, use the following command:
```bash
sudo apt install openssh-client
```

---

## **Step 2: Set Up SSH for GitHub**

### 1. **Generate an SSH Key Pair**
- Run the following command to create an SSH key:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- The above step will ask for a *location* to store SSH and a *passphrase* for protection. You can leave the *location* as default by not providing one. 
- This will generate a public and private SSH key in the `~/.ssh/` directory.

### 2. **Add the SSH Key to the SSH Agent**
- Start the SSH agent:
```bash
eval "$(ssh-agent -s)"
```
- Add your SSH private key:
```bash
ssh-add ~/.ssh/id_ed25519
```

### 3. **Add the SSH Key to GitHub**
- Copy the public SSH key:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Log in to your GitHub account, navigate to **Settings > SSH and GPG Keys**, and add the copied key.

---

## **Step 3: Test Your SSH Connection**
- Verify the SSH connection to GitHub:
```bash
ssh -T git@github.com
```
- If successful, you should see:
```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## **Step 4: Set SSH as Default for All Repositories**
- To always use SSH when cloning or interacting with repositories:
```bash
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
```
- This modifies the `~/.gitconifg` file: 
```
[url "git@github.com:"]
          insteadOf = https://github.com/
```

## **Step 5: Configure Git**

### 1. **Set User Information**
- Set your name and email, which will be recorded with your commits:
```bash
$ git config --global user.name "John Smith"
$ git config --global user.email "john@example.com"
```
- Use the `--global` flag to apply these settings globally or omit it for repository-specific settings.

### 2. **Set Your Preferred Editor**
- Configure the default text editor for Git (e.g., VS Code):
```bash
$ git config --global core.editor "code --wait"
```
- Replace `code --wait` with your preferred editor, like `nano` or `vim`. The `--wait` flag ensures Git waits for the editor to close before proceeding.

### 3. **Create Command Aliases**
- Simplify commonly used Git commands with aliases:
```bash
# Syntax:
$ git config [--global] alias.<alias_name> "<command>"

# Examples:
$ git config --global alias.st status
$ git config --global alias.pu "push -u origin main"
```
- For instance, use `git st` instead of `git status`.
- Here is how `~/.gitconfig` file would like after executing above commands:
```
[user]
	name = John Smith
	email = john@example.com
[core]
	editor = code --wait
[alias]
	st = status
	pu = push -u origin main
```

### 4. **Explore More Options**
- Run `git help config` in the terminal to see all available configuration options.


# **Initializing Repositories**

## **Creating a New Repository:**
  
- To initialize a repository, run the following:
```bash
# Syntax
$ git init <path>

# Examples
$ git init 
$ git init ~/Documents/SampleProject
```
- The `<path>` argument can be left blank to initialize the repository in the current directory.
 -  Git is minimally invasive; it only adds a `.git` directory in the root of your project folder.

## **Cloning an Existing Repository:**
- Instead of initializing a new repository, you can **clone** an existing Git repository:
```bash
# Syntax
$ git clone ssh://<user>@<host>/path/to/repo[.git]
$ git clone https://github.com/user/repo[.git]

# Examples
$ git clone ssh://git@github.com/rnaveensrinivas/GitRepo
$ git clone https://github.com/rnaveensrinivas/GitRepo
```
- This command will create a full copy of the repository, including its history, working directory, staging area, and branch structure. Changes won’t be visible to others until you push them to a public repository.

## Optional: Swtiching to use SSH Instead of HTTPS for Cloned Repositories

### 1. **Check Your Current Remote URL**
- You must in a repository that is associated with Github execute the following command. If you don't have one simply create a GitHub repository and clone it in local. 
- Run the following command:
```bash
$ git remote -v
```
- If the URL starts with `https://`, you need to change it to SSH.

### 2. **Update the Remote URL**
- Replace `username/repository` with your GitHub username and repository name:
```bash
$ git remote set-url origin git@github.com:username/repository.git
```

### 3. **Verify the Change**
- Check the updated remote URL:
```bash
$ git remote -v
```
- The output should now display `git@github.com` instead of `https://`.

### 4. **Push Changes Using SSH**
- Push your changes without being prompted for a username and password:
```bash
$ git push
```

### 5. **Optional: Set SSH as Default for All Repositories**
- To always use SSH when cloning or interacting with repositories:
```bash
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
```

## Summary of Commands
| Command  | Description |
|----------|-------------|
| `git config --global user.name "name"`| Sets the global Git username for all repositories.|
| `git config --global user.email "email"`| Sets the global Git email for all repositories.|
| `git config --global core.editor "editor --wait"`| Sets the default text editor for Git commands requiring user input, like commit messages.|
| `git config --global alias.alias_name "command"`| Creates a shortcut (alias) for a Git command.|
| `git help config`| Displays help information about Git configuration options.|
| `git init`| Initializes a new Git repository in the current directory.|
| `git init path`| Initializes a new Git repository at the specified path.|
| `git clone ssh://<user>@<host>/path/to/repo[.git]`| Clones a repository from a remote server using an SSH URL with user and host details.|
| `git clone https://github.com/user/repo[.git]`| Clones a repository from GitHub or another remote server using an HTTPS URL.|
| `git remote -v`| Displays the list of remote repositories and their URLs.|
| `git remote url remote_name new_url`| Updates the URL for a specified remote repository.|

# Recording Changes

## **Git Snapshots vs. CVCS Diffs**
### **Git’s Snapshot Model**:
  - Git records **snapshots** of the entire project instead of just diffs between files (as in SVN or CVS).
  - Each **commit** in Git represents a complete snapshot of all project files at a given point in time, making Git faster and more reliable.
  - Unlike systems that record incremental changes, Git stores the full version of each file in a commit.
  
#### **Advantages:**
  - Faster access to file versions.
  - Avoids the need to regenerate file states when requested.

## **The Staging Area**

### **What is the Staging Area?**
- The **staging area** (also known as the **index**) is an intermediary between the **working directory** and the **committed history**.
- It allows you - The **staging area** (also known as the **index**) is an intermediary between the **working directory** and the **committed history**.
- It allows you to **stage** (select) changes for the next commit, ensuring you can commit only the desired changes and not the entire working directory at once.to **stage** (select) changes for the next commit, ensuring you can commit only the desired changes and not the entire working directory at once.

### **Staging Changes:**
- **Add stuff to the staging area** using:
```bash
# Syntax
$ git add <path>

# Examples
$ git add .
$ git add afolder/
$ git add f1
```

### **Stage file deletion** (without removing the file from the working directory):
```bash
# Syntax
$ git rm --cached <file>

# Examples
$ git rm --cached f1
$ git rm -r --cached afolder/
```
#### **What happens if you simply do `git rm` or `rm`?**
```bash
# trying to use "git rm" on staged f1
$ git rm f1
error: the following file has changes staged in the index:
    f1
(use --cached to keep the file, or -f to force removal)

# trying to use "git rm" on a tracked file afolder/f4
$ git rm afolder/f4
rm 'afolder/f4'
# removes the file from working directory and stages the removal


# trying to use "rm" on staged f1
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

### Inspecting the Stage

#### Check the Status of the Repository:
- To view the state of your repository and see which files are staged, modified, or untracked, use:
```bash
$ git status
```

##### Example Output:
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


#### **Diffs:**
- To see **unstaged changes** (changes in the working directory):
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

- To see **staged changes** (changes in the staging area):
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

## **Commits**

### **What is a Commit?**
- A **commit** is a snapshot of your project at a specific point in time, and it serves as an atomic unit in Git's version control.
- Each commit contains:
  - The **snapshot** of the entire project.
  - **Author information** (name and email).
  - The **commit message**.
  - A **unique SHA-1 checksum** that ensures the commit cannot be unintentionally altered.

### **Commit Process:**
- **Commit the staged snapshot** to the repository history:
```bash
git commit
```
- You'll be prompted to provide a **commit message** in a text editor.

### **Commit Message Format:**
- **First line (summary)**: A brief description (50 characters or less).
- **Second line**: Blank line.
- **Following lines**: A detailed description of changes, reasons, or relevant ticket numbers.

Example:
```plaintext
Fixed bug in user authentication

Detailed fix for user authentication issues, including validation errors
and user session management.
```
### **Commiting using options**
- Commiting without opening default text editor.
```bash
# Sytnax
$ git commit -m "commit message"

# Example
git commit -m "This is a commit message"
[master (root-commit) cbd9be4] This is a commit message
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 afile.txt
```

### **Inspecting Commits**

#### **View Commit History:**
- To see the list of commits in the current branch:
```bash
# Syntax
git log

# Example
git log
commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message
```

#### **Useful Options:**
- **Single-line log** (brief):
```bash
# Syntax
git log --oneline

# Example
git log --oneline
cbd9be4 (HEAD -> master) commit message
```

- **Log for a specific file**:
```bash
# Syntax
git log [--oneline] <file>

# Examples
git log afile.txt
commit cbd9be4bb54c7573ff55d8826d8b1ea7582a2d0a (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 17:56:52 2024 +0530

    commit message

# Example
git log --oneline afile.txt
cbd9be4 (HEAD -> master) commit message

```

- **Log for a specific range of commits**:
- `<since>` commit is excluded and `<until>` commit is included. 
```bash
# Syntax
git log <since>..<until>

# Examples
git log
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

# cbd9be4 is excluded but 169223b is included.
git log cbd9be4..169223b
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

commit e09fdab287149a6c6a4c176b8c4a40df15284abd
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:03:24 2024 +0530

    changed file names

# e09fdab is excluded but 169223b is included.
git log e09fdab..169223b
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:04:00 2024 +0530

    added some files in afolder

```


- **Display a diffstat** (changes made in each commit):
```bash
# Syntax
git log --stat

# Example
git log --stat
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

#### **Visualizing History:**
- Use `gitk` to visualize the commit history graphically (available as a separate program).
```bash
gitk
```

## **Tagging Commits**

### **What are Tags?**
- Tags are **pointers** to specific commits, useful for marking important points in the project’s history, such as release versions.


### **Creating a Tag**  
* To create a lightweight tag on the commit you are sitting on:  
```bash
# Syntax
git tag <tag_name>

# Example
git tag v1.0

# notice the end of commit 169223b
git log
commit 169223b27b5039d1d69b83889dd14e776891e9a1 (HEAD -> master, tag: v1.0)
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
```
* Adding a commit and printing the log, we can see tag stays behind.

```bash
git log
commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
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
```

* To create an annotated tag with a message:  
```bash
# Syntax
git tag -a <tag_name> -m "Tag Message"

# Example
git tag -a v2.0 -m "Initial release"
git log
commit 8325a85452c5f8c2d2c6559e2cc055a1cce116ac (HEAD -> master, tag: v2.0)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 28 18:19:52 2024 +0530

    changed file name

commit 169223b27b5039d1d69b83889dd14e776891e9a1 (tag: v1.0)
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
```

### **Listing Tags**  
* To see all tags in the repository:  
```bash
# Syntax
git tag

# Example
git tag
v1.0
v2.0
```

### **Pushing Tags to Remote**  
* By default, tags are not pushed to remote. Push a specific tag:  
```bash
# Syntax 
git push origin <tag_name>
```

To push all tags:  
```bash
# Syntax
git push --tags
```

### **Viewing a Tag**  
* To see details of a tag:  
```bash
# Syntax
git show <tag_name>
```
#### Examples

* Normal tag
```bash
git show v1.0
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

* Annotated tag
```bash
git show v2.0
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

### **Using Tags for Checkout**  
* To checkout a specific tag (in a detached HEAD state):  
```bash
# Syntax
git checkout <tag_name>

# Example
git checkout v1.0 
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


## Summary of Commands:
| Command                               | Description                                                                                         |
|---------------------------------------|-----------------------------------------------------------------------------------------------------|
| `git add`                             | Stages all changes in the working directory for the next commit.                                   |
| `git add file/folder`                 | Stages specific files or folders for the next commit.                                              |
| `git rm`                              | Removes files from the working directory and stages the deletion for the next commit.             |
| `git rm --cached file`                | Removes a file from the staging area without deleting it from the working directory.              |
| `git rm -r --cached folder`           | Removes a folder from the staging area without deleting it from the working directory.            |
| `git status`                          | Shows the status of the working directory and staging area, listing changes to be committed.      |
| `git diff`                            | Displays unstaged changes in the working directory.                                               |
| `git diff --cached`                   | Displays changes staged for the next commit.                                                      |
| `git commit`                          | Commits staged changes to the repository.                                                         |
| `git commit -m "commit message"`      | Commits staged changes with a descriptive message in a single step.                               |
| `git log`                             | Displays the commit history of the repository.                                                    |
| `git log --oneline`                   | Shows a concise commit history with one commit per line.                                          |
| `git log --oneline file/folder`       | Shows a concise commit history for a specific file or folder.                                     |
| `git log <since>..<until>`            | Displays commits between two references (e.g., tags, branches), with `<since>` being exclusive.    |
| `git log --stat`                      | Shows commit history along with a summary of changes made in each commit.                         |
| `git tag tag_name`                    | Creates a lightweight tag for the current commit.                                                 |
| `git tag -a tag_name -m "tag message"` | Creates an annotated tag with a message for the current commit.                                   |
| `git tag`                             | Lists all tags in the repository.                                                                 |
| `git push origin tag_name`            | Pushes a specific tag to the remote repository.                                                   |
| `git push --tags`                     | Pushes all tags to the remote repository.                                                         |
| `git show tag_name`                   | Displays details of a specific tag, including the commit it references.                           |
| `git checkout tag_name`               | Checks out a specific tag, detaching the HEAD to a read-only state.                               |


# Undoing Changes

## **Undoing Changes in Git**

- **Importance of Undoing:**
  - Undoing changes allows you to correct mistakes or experiments without fear of breaking the code.
  - Git provides tools to undo changes at different stages: working directory, staging area, and commits.

- **Undoing can mean:**
  - Undo changes in the **working directory**.
  - Undo changes in the **staging area**.
  - Undo an **entire commit**.

## **Undoing in the Working Directory**

- **Reset to the Last Commit:**
  - To discard all uncommitted changes (both in working directory and staging area), use:
    ```bash
    git reset --hard HEAD
    git clean -f
    ```

  - `git reset --hard HEAD` resets the working directory and staging area to the state of the **most recent commit** (HEAD).
  - `git clean -f` removes **untracked files** (files that Git is not tracking).
  - The **-f** flag is required to force deletion of untracked files.

- **Undo Changes to a Specific File:**
  - To revert a single file to the version from the last commit:
    ```bash
    git checkout HEAD <file>
    ```

  - This will replace the file in your working directory with the version from **HEAD**, without altering the project history.

## **Undoing in the Staging Area**

- **Unstage Changes:**
  - If you accidentally stage a file, you can unstage it with:
    ```bash
    git reset HEAD <file>
    ```

  - This command removes the file from the staging area but leaves your working directory unchanged, resulting in an unstaged modification.

## **Undoing Commits**

- **Two Ways to Undo Commits:**
  1. **Reset**: Removes a commit entirely from the history.
  2. **Revert**: Creates a new commit that undoes the changes of a previous commit.

### **Resetting Commits:**
  - **git reset** is used to move the `HEAD` reference and remove a commit from the history:
    ```bash
    git reset HEAD~1
    ```

  - `HEAD~1` refers to the commit before the most recent commit (`HEAD`). This command moves `HEAD` backward, removing the most recent commit.
  
  - **Caution**: Resetting commits **rewrites history** and can cause issues in **collaborative projects**. It’s safe to reset **private commits**, but avoid resetting commits that have been shared with others.

  - **Example**:
    - To reset the last commit, use `git reset HEAD~1`.

### **Reverting Commits:**
  - **git revert** is a safer alternative to `git reset`, especially in public repositories:
    ```bash
    git revert <commit-id>
    ```

  - This creates a new commit that undoes the changes introduced by the specified commit.

  - **Ideal for public repositories**, as it doesn't rewrite history but introduces a new commit that "cancels out" previous changes.


## **Amending Commits**

- **Amend the Most Recent Commit:**
  - If you want to modify the most recent commit (e.g., to add forgotten changes or fix the commit message), use:
    ```bash
    git commit --amend
    ```

  - This replaces the previous commit with a new one, which is useful if you need to tweak the latest commit without creating a new one.

  - **Caution**: This also rewrites history, so avoid amending commits that have already been shared with others.


## Summary of Commands:

- **Undoing in Working Directory:**
  - `git reset --hard HEAD` (reset working directory to last commit)
  - `git clean -f` (remove untracked files)
  - `git checkout HEAD <file>` (revert a specific file to the last commit)
  
- **Undoing in Staging Area:**
  - `git reset HEAD <file>` (unstage a file)

- **Undoing Commits:**
  - `git reset HEAD~1` (remove the most recent commit from history)
  - `git revert <commit-id>` (create a new commit that undoes a previous commit)

- **Amending Commits:**
  - `git commit --amend` (modify the most recent commit)

# **Branches**

Branches in Git allow you to create multiple development paths, enabling parallel work on different versions of a project. When you create a new branch, you essentially get a new environment for working, including an isolated working directory, staging area, and project history.

## Manipulating Branches

1. **Listing Branches**  
   You can view all your branches with the `git branch` command, which shows the current branch with an asterisk next to it:
   ```bash
   git branch
   ```

2. **Creating Branches**  
   Create a new branch using the command:
   ```bash
   git branch <name>
   ```
   This creates a new branch that points to the current commit, but it does not automatically switch to it.

3. **Deleting Branches**  
   To delete a branch, use:
   ```bash
   git branch -d <name>
   ```
   If the branch has unmerged commits, Git will prevent the deletion to avoid data loss. You can force deletion with:
   ```bash
   git branch -D <name>
   ```

4. **Checking Out Branches**  
   To switch between branches, use the `git checkout` command:
   ```bash
   git checkout <branch>
   ```

5. **Detached HEADs**  
   A detached HEAD occurs when you check out a specific commit or tag rather than a branch. In this state, any new commits won’t belong to a branch and may be lost when switching branches. You can create a new branch from this state with:
   ```bash
   git checkout -b <new-branch-name>
   ```

## Merging Branches

Merging is used to combine changes from one branch into another. The two common merge strategies are:

1. **Fast-forward Merge**  
   In a fast-forward merge, Git simply moves the branch pointer to the tip of the merged branch. This happens when no commits have been made on the target branch since the branching.

2. **3-way Merge**  
   A 3-way merge occurs when both branches have diverged (i.e., both have new commits). Git combines the changes and creates a new merge commit. This merge is necessary when a fast-forward merge isn’t possible.

## Merge Conflicts

If two branches have conflicting changes to the same file, Git will raise a merge conflict, and you’ll need to manually resolve it by editing the file. After fixing the conflict, stage the file with:
```bash
$ git add <file>
```
Then commit the merge:
```bash
$ git commit
```

## Branching Workflows

There are two main types of branches:

1. **Permanent Branches**  
   Permanent branches, such as `master`, contain the main project history. Some workflows use a second integration branch, often called `develop`, to prepare for a public release, keeping `master` for stable, released code.

2. **Topic Branches**  
   These are temporary branches for specific tasks like feature development or bug fixes. Once the work is completed, these branches are merged into a permanent branch.

## Rebasing

Rebasing allows you to move a branch to a new base, cleaning up the commit history. This is done using:
```bash
$ git checkout <feature-branch>
$ git rebase <base-branch>
```
Rebasing results in a linear commit history, as opposed to merging, which may introduce unnecessary merge commits.

## Interactive Rebasing

Interactive rebasing allows you to modify commits during the rebase process. You can reorder, squash, or amend commits. To start an interactive rebase, use:
```bash
$ git rebase -i <base-branch>
```

## Rewriting History

Rebasing creates new commits, which means the commit IDs change. This is dangerous for shared/public branches because it rewrites history, which can cause problems in collaborative workflows. Avoid rebasing commits that have already been pushed to a public repository.

# Chapter 6: Remote Repositories

## Overview of Remote Repositories
- A **remote repository** is one that is not hosted on your local machine.
- It can be on a central server, another developer’s personal computer, or even a different part of your file system.
- Remote repositories enable sharing contributions among different repositories.
- **Branches** should only deal with project development and not individual developers. Assign complete repositories to developers and reserve branches for feature development.

## Manipulating Remotes
- The `git remote` command is used to manage connections to other repositories.
  - Remotes are **bookmarks** to other repositories, which let you reference them easily by name instead of full path.
  
### Listing Remotes
- Use `git remote` to list remotes.
  - If no remotes exist, no information will be displayed.
  - When cloning a repository, an `origin` remote is automatically added.
- Use `git remote -v` to view the full URL of your remotes.

### Creating Remotes
- Use `git remote add <name> <path-to-repo>` to create a connection to a remote repository.
  - `<name>` is a friendly name for the remote (like `origin`).
  - `<path-to-repo>` can be an SSH, HTTP, or file-based URL.
  - Example: `git remote add some-user ssh://git@github.com/some-user/some-repo.git`
  
### Deleting Remotes
- Use `git remote rm <remote-name>` to remove a remote connection.

## Remote Branches
- **Remote branches** represent branches from someone else’s repository.
- Once fetched, you can inspect, merge, and extend remote branches like local branches.

### Fetching Remote Branches
- Fetching downloads branches from another repository.
  - Example: `git fetch <remote> <branch>`
  - To fetch all branches, omit the branch name: `git fetch <remote>`
- Use `git branch -r` to list remote branches.
  - Remote branches are prefixed with the remote name (e.g., `origin/master`).

### Inspecting Remote Branches
- Remote branches are read-only.
- To view a remote branch's history or commits, use `git checkout` but be in a **detached HEAD state**.
- Use `git log master..origin/master` to see new commits on the remote master that aren't in your local master.

## Merging/Rebasing Remote Branches
- To integrate changes from a remote branch into your local branch, use `git merge` or `git rebase`.

### Merging Remote Branches
- Fetch the latest changes from the remote and then merge them into your branch:
  ```bash
  git fetch origin
  git merge origin/master
  ```

### Rebasing Remote Branches
- Rebasing avoids cluttering the history with unnecessary merge commits:
  ```bash
  git fetch origin
  git rebase origin/master
  ```

### Pulling Changes
- `git pull` is a shorthand for fetching and merging in one step:
  ```bash
  git pull origin/master
  ```

## Pushing Changes
- **Pushing** exports branches to another repository.
  - Use `git push <remote> <branch>` to send the local branch to the remote repository.
- Pushing is the opposite of fetching, as it uploads your changes to a remote repository.

### Push Example
- If you push a branch, like `my-feature`, from your local repo to a remote:
  ```bash
  git push mary my-feature
  ```

- This creates a branch in the remote repository, which may be tracked by other developers. 

### Caution with Pushing
- Pushing creates new branches on the remote, which can cause unexpected branches to appear in others' repositories.

# Remote Workflows

## Overview of Remote Workflows
- **Remote workflows** refer to the processes in which multiple developers collaborate on a project by sharing code through remote repositories.
- There are two common collaboration models:
  1. **Centralized Workflow**
  2. **Integrator Workflow**
- Git treats all repositories as equals, unlike SVN or CVS which have a "master" repository. The central repository is merely a project convention.

## Public (Bare) Repositories
- **Public repositories** serve as points of entry for multiple developers.
- **Bare repositories** are used for collaboration, and they lack a working directory to prevent overwriting work from multiple developers.
  - Create a bare repository with the command:
    ```bash
    git init --bare <path>
    ```
  - Example of a bare repository:
    ```bash
    git init --bare some-repo.git
    ```

## The Centralized Workflow
- The **centralized workflow** is ideal for small teams where each developer has write access to the central repository.
- Developers work in their own local repositories and push their changes to the central repository.
- Common workflow:
  1. Developers complete their work locally.
  2. They merge the feature into their local master branch.
  3. Changes are pushed to the central repository.
  4. Other developers fetch the changes and integrate them into their local projects.

### Issues in the Centralized Workflow
- Conflicts can arise when multiple developers attempt to push changes simultaneously.
  - Example: If John pushes changes before Mary, Mary will encounter a **non-fast-forward error**:
    ```
    ! [rejected] master -> master (non-fast-forward)
    error: failed to push some refs to 'some-repo.git'
    ```
  - To resolve this, Mary must:
    1. Fetch the latest changes from the central repository:
       ```bash
       git fetch origin master
       ```
    2. Rebase her changes onto the latest version:
       ```bash
       git rebase origin/master
       ```
    3. Push her changes:
       ```bash
       git push origin master
       ```

### Advantages of the Centralized Workflow
- Simple setup with only one server needed.
- Ideal for small teams or projects with a trusted group of developers.

## The Integrator Workflow
- The **integrator workflow** addresses scalability and security issues inherent in the centralized model.
- Developers maintain a **private repository** and a **public repository**. The public repository is used for pushing contributions, while the integrator (maintainer) fetches, reviews, and merges them into the central project repository.
  
### Workflow in the Integrator Model
1. A contributor makes a fix or feature in their own public repository.
2. The integrator (project maintainer) fetches the changes using HTTP (read-only protocol) to ensure no unintended changes are introduced.
3. After review, the integrator merges the changes into their local branch and pushes them to the official repository.
4. Contributors only need push access to their own repositories, not the central repository.

### Security and Scalability in the Integrator Workflow
- **Security**: Contributors can only push to their own repositories, not to the central repository, avoiding potential malicious or unapproved changes.
- **Scalability**: This model allows for greater scalability by avoiding a central choke point and allowing many developers to contribute independently.

### Key Characteristics of the Integrator Workflow
- Developers must agree on a single **official repository** for the project to avoid disorder and keep everyone in sync.
- Integrators need to manage multiple remotes, but this provides the flexibility and security of managing contributions from multiple developers.
- The integrator workflow is ideal for **open-source projects** where large numbers of contributors are involved.

## Comparison of Centralized and Integrator Workflows
- **Centralized Workflow**: Suitable for small teams with direct access to the central repository.
  - Simple, easy to set up, but can lead to conflicts when multiple developers push at the same time.
- **Integrator Workflow**: Suitable for larger teams or open-source projects, providing security and scalability.
  - Contributors push to their own repositories, and integrators review and merge changes into the central repository.

### Conclusion
- Git’s distributed nature makes the **integrator workflow** highly scalable, making it ideal for large open-source projects.
- The **centralized workflow** is easier for small teams but can run into issues when multiple developers try to update the central repository simultaneously.