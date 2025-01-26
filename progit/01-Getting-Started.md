# Chapter 1: Getting Started

This chapter covers the basics of **Git** and version control, explaining different types of systems, Git's unique features, and how to install, configure, and use it effectively. It includes setup instructions, key concepts like file states, and ways to get help with Git commands.

## TOC

- [Chapter 1: Getting Started](#chapter-1-getting-started)
  - [TOC](#toc)
  - [Version Control](#version-control)
    - [What is Version Control?](#what-is-version-control)
    - [Why Care About Version Control?](#why-care-about-version-control)
    - [Applications Beyond Code](#applications-beyond-code)
  - [Types of Version Control Systems](#types-of-version-control-systems)
    - [1. Local Version Control Systems](#1-local-version-control-systems)
    - [2. Centralized Version Control Systems (CVCS)](#2-centralized-version-control-systems-cvcs)
      - [Advantages](#advantages)
      - [Disadvantages](#disadvantages)
    - [3. Distributed Version Control Systems (DVCS)](#3-distributed-version-control-systems-dvcs)
      - [Advantages:](#advantages-1)
  - [Git](#git)
    - [A Short History of Git](#a-short-history-of-git)
    - [What is Git?](#what-is-git)
    - [Git Feature 1: Snapshots, Not Differences](#git-feature-1-snapshots-not-differences)
    - [Git Feature 2: Nearly Every Operation Is Local](#git-feature-2-nearly-every-operation-is-local)
    - [Git Feature 3: Git Has Integrity](#git-feature-3-git-has-integrity)
    - [Git Feature 4: Git Generally Only Adds Data](#git-feature-4-git-generally-only-adds-data)
    - [Git Feature 5: The Three States in Git](#git-feature-5-the-three-states-in-git)
  - [The Command Line](#the-command-line)
  - [Installing Git](#installing-git)
    - [Option 1: Install Basic Git](#option-1-install-basic-git)
    - [Option 2: Install Git-All](#option-2-install-git-all)
  - [First-Time Git Setup](#first-time-git-setup)
    - [Configuring Git Environment](#configuring-git-environment)
    - [Setting Up Identity](#setting-up-identity)
    - [Configuring Default Editor](#configuring-default-editor)
    - [Default Branch Name](#default-branch-name)
    - [Checking Settings](#checking-settings)
  - [Getting Help in Git](#getting-help-in-git)
  - [Summary](#summary)

---

## Version Control 

### What is Version Control?
- **Definition:** A system to track and manage changes to files over time.
- **Use Case:** Allows you to return to a specific version of a file or project.

### Why Care About Version Control?
1. **Recovery:** Easily revert files or projects to an earlier state if mistakes occur.
2. **Change Tracking:** Compare changes over time and understand how files evolve.
3. **Collaboration:** Identify who made specific changes, when, and why.
4. **Fault Isolation:** Pinpoint when and who introduced issues to the project.
5. **File Safety:** Protect against accidental data loss or corruption.

And the best thing is you get all the above for very **little overhead**.

### Applications Beyond Code
While Git is often associated with managing software source code, version control systems (VCS) are also useful for:
- Graphic design: Keeping versions of images or layouts.
- Web design: Managing iterations of a site’s design or content.
- Writing and documentation: Tracking drafts and revisions.

It can basically track any type of file on a computer. 

---

## Types of Version Control Systems

### 1. Local Version Control Systems 
- **Traditional Method:** Copying files into separate, often time-stamped directories (e.g. `Project_2025-01-27`).  
  - **Problem:** Error-prone; easy to overwrite or misplace files.  

- **Solution:** Local VCS with a simple database to track file changes.  
  - Stores **patch sets** (differences between file versions).  
  - Can recreate any file version by applying patches sequentially.

- **Example Tool:**  
  - **RCS (Revision Control System):**  
    - Popular early local VCS.  
    - Still available on many systems today.  
  
  ```plaintext
            Local Computer
            --------------

                    _____________________
  Checkout          |  Version Database |
                    |-------------------|           
                    |                   |
  File -------------|--->  Version 3    |
                    |         |         |
                    |      Version 2    |
                    |         |         |
                    |      Version 1    |
                    |___________________|
  ```

---

### 2. Centralized Version Control Systems (CVCS) 

- **Purpose:** Enables collaboration across multiple developers by storing versioned files on a **single central server**.  
- **Examples:** CVS, Subversion, Perforce.  

#### Advantages
- Team visibility: Everyone can see what others are working on.  
- Centralized control: Administrators can manage permissions and access.  
- Simplicity: Easier to manage compared to individual local databases.  

#### Disadvantages
- **Single Point of Failure:**  
  - If the server goes down, collaboration halts, and changes cannot be saved.  
  - Corrupted server data without proper backups leads to complete loss of project history.  
- Risk of losing everything, when entire project history stored in one place. Even LocalVCSs are prone to this. 

  ```plaintext
              Shared Repository
              -----------------
              |  Version 3    |
              |  Version 2    |
              |  Version 1    |
              -----------------
                      ^
                      |
      ---------------------------------
      |               |               |
  Developer 1    Developer 2    Developer 3
  (Working Dir)  (Working Dir)  (Working Dir)

  ```
---

### 3. Distributed Version Control Systems (DVCS) 

- **Definition:** Every client fully mirrors the repository, including its **entire history**.  

#### Advantages:  
- **Full Backups:**  
  - Each clone is a complete backup of the repository.  
  - If the central server fails, any client can restore it.  
- **Multiple Remote Repositories:**  
  - Collaborate with different groups simultaneously.  
  - Supports diverse workflows (e.g., hierarchical models, like GitFlow Model).  
- **Examples** :
  - Git, Mercurial, Darcs.  

  ```plaintext
                    Server Computer
                  --------------------
                  | Version Database |  
                  |    Version 3     |
                  |    Version 2     | 
                  |    Version 1     |
                  --------------------
                          /   \ 
                        /     \
    --------------------         --------------------
    |    Computer A    |         |    Computer B    |
    |                  |         |                  |
    |      File        |         |      File
    |        ^         |         |        ^         |
    |        |         |         |        |         |
    | Version Database |         | Version Database |    
    |    Version 3     | ------  |    Version 3     |
    |    Version 2     |         |    Version 2     |  
    |    Version 1     |         |    Version 1     |
    --------------------         --------------------
  ```

---

## Git

### A Short History of Git  

- **Early Years (1991–2002):**  
  - Linux kernel changes were shared as **patches** (a file that contains the differences (or changes) between two versions of a file or set of files) and **archived files** (`.zip`, `.tar`, or `.tar.gz`).  

- **2002:**  
  - Linux kernel project adopted **BitKeeper**, a proprietary DVCS.  

- **2005:**  
  - Relationship between the Linux community and BitKeeper’s developers broke down.  
  - BitKeeper’s free status was revoked (tool was no longer free), prompting **Linus Torvalds** and the Linux community to create Git.

- **Git’s Goals (inspired by BitKeeper):**  
  - Speed.  
  - Simple design.  
  - Strong support for non-linear development (e.g., many parallel branches).  
  - Fully distributed.  
  - Efficient handling of large projects like the Linux kernel.  

- **Since 2005:**  
  - Git has matured while **retaining** its core qualities.  
  - Known for speed, efficiency with large projects, and an excellent branching system.  

---

### What is Git?  

- **Nutshell Definition:** Git is a Distributed Version Control System (DVCS) with unique concepts and workflows.  
- **Key Advice:**  
  - Clear your mind of assumptions from other VCSs (e.g., CVS, Subversion, Perforce).  
  - Understanding Git’s distinct way of storing and managing information is crucial for effective use.  
- **Why Important:**  
  - While the interface may appear similar to other VCSs, Git operates fundamentally differently.  

---

### Git Feature 1: Snapshots, Not Differences  

- **How Other VCSs Work (e.g., CVS, Subversion):**  
  - Use **delta-based version control**, storing data as a list of changes to files over time.  
  - Conceptualize information as files with changes applied incrementally.  

- **How Git Works:**  
  - Stores **snapshots** of the entire project at each commit.  
  - If files remain unchanged, Git stores a **link** to the previously saved version instead of duplicating the file.  
  - Git thinks about its data more like a **stream of snapshots**.

- **Why This Matters:**  
  - **Efficiency:** Reduced storage requirements for unchanged files.  
  - **Flexibility:** Treats the project as a series of self-contained snapshots rather than incremental differences.  

- **Core Difference:**  
  - Git rethinks version control, treating data like a **mini filesystem** with advanced tools on top, rather than as a simple change-tracking system.  

---

### Git Feature 2: Nearly Every Operation Is Local  

- **Local Operations:**  
  - Git performs most operations using local files and resources.  
  - No need for network access, eliminating network latency overhead.  

- **Speed:**  
  - Operations like browsing history or comparing versions are **almost instantaneous** because data is read directly from the local database.  

- **Offline Work:**  
  - Git allows full functionality offline, including committing changes.  
  - Ideal for situations without network access (e.g., on a plane, train, or without VPN).  

- **Comparison with CVCSs:**  
  - **Perforce:** Requires server connection for most tasks.  
  - **Subversion/CVS:** Allows file editing offline but not committing.  

- **Impact:**  
  - Offers seamless productivity and flexibility, even without a network connection.  
  - Highlights Git’s independence from centralized server dependency.  

---

### Git Feature 3: Git Has Integrity  

- **Checksumming:**  
  - Every file and directory in Git is **checksummed** before storage.  
  - Ensures that any changes to content are detected by Git.  

- **Data Integrity:**  
  - Prevents undetected file corruption or data loss in transit.  
  - Built into Git's core functionality and philosophy.  

- **SHA-1 Hash:**  
  - Git uses a **40-character SHA-1 hash** to identify content.  
  - Hash is calculated based on file or directory contents.  
  - Example of SHA-1 hash: `24b9da6552252987aa493b52f8696cd6d3b00373`.  

- **Hash-Based Storage:**  
  - Git stores everything in its database by **hash value**, not by file name.  
  - These hashes are a fundamental part of Git's operations.  

---

### Git Feature 4: Git Generally Only Adds Data  

- **Data Addition:**  
  - Most actions in Git **add data** to the database without removing or altering existing data.  

- **Safety:**  
  - Once you commit a snapshot, it's **difficult to lose** it, especially if you regularly push to another repository.  
  - Even if changes are lost or messed up before committing, recovery is possible after a commit.  

- **Experimentation:**  
  - Git encourages experimentation since changes can be safely committed and recovered.  

---

### Git Feature 5: The Three States in Git  

- **Three Main States for Files:**  
  - **Modified:** File has changed but not yet staged or committed.  
  - **Staged:** Modified file is marked to be included in the next commit.  
  - **Committed:** Data is safely stored in the local Git database.  

- **Three Main Sections of a Git Project:**  
  - **Working Tree:** A checkout of one version of the project, pulled out of the compressed `.git` database, where you modify files.  
  - **Staging Area:** Stores information about what will go into the next commit. Known as the "**index**."  
  - **Git Directory:** Stores metadata and the object database; crucial for the project and copied when **cloning** a repository.  

- **Basic Git Workflow:**  
  1. Modify files in the working tree.  
  2. Stage **desired** (not necessary to include all) changes to the staging area.  
  3. Commit staged changes, saving them permanently in the `.git` database.  

---

## The Command Line  

- Git can be used through the command line or graphical interfaces.  
- We will focuse on using Git via the command line, as it provides all the functionalities.  
- GUI's don't provide the complete functionalities that CLI offers.
- Knowing the command line version makes it easier to understand GUI tools, but not vice versa.  

---

## Installing Git

To install Git, follow these steps:

```bash
$ sudo apt update
$ sudo apt upgrade -y
$ sudo apt install git[-all] -y
$ git --version
git version 2.43.0
```

### Option 1: Install Basic Git

```bash
$ sudo apt install git -y
```
- **Installs** the core Git package, which includes essential Git tools and command-line utilities.
- Includes the basic commands needed for version control, such as `git`, `git config`, and `git clone`.

### Option 2: Install Git-All

```bash
$ sudo apt install git-all -y
```
- **Installs Git along with all related tools and utilities** for a more comprehensive setup.
- Includes everything from the basic package **plus**:
  - Additional tools like `gitk` (a graphical Git viewer) and `git-gui`.
  - Git's documentation and man pages.
  - Extra utilities for advanced workflows and various environments.

--- 

## First-Time Git Setup

### Configuring Git Environment
- Git uses `git config` to manage configuration variables affecting its appearance and operation.
- Configuration levels:
  1. **System-wide**: `/etc/gitconfig` (requires `--system` option; needs admin privileges).
  2. **User-specific**: `~/.gitconfig` or `~/.config/git/config` (uses `--global` option; applies to all repositories for that user).
  3. **Repository-specific**: `.git/config` (default for repository-specific configurations; uses `--local` option).
- **Precedence**: Repository-level (`.git/config`) overrides user-level (`~/.gitconfig`), which overrides system-level (`/etc/gitconfig`).

### Setting Up Identity
- **User Name and Email**:
  - `$ git config --global user.name "John Doe"`
  - `$ git config --global user.email johndoe@example.com`
  - Needed for commit identification; baked into commits.
  - Use without `--global` to set for a specific repository.
  - Many of the GUI tools will help you do this when you first run them.

### Configuring Default Editor
- Specify a custom text editor for Git (e.g., Visual Studio Code):
  - `$ git config --global core.editor "code --wait"`
- This will be used by when Git needs you to type a message.
- If not configured uses default text editor. 

### Default Branch Name
- By default Git will create a branch called `master` when you create a new repository with `git init`. 
- From Git version 2.28, you can change the default branch name:
  - `$ git config --global init.defaultBranch main`

### Checking Settings
- Use `$ git config --list` to view all settings.
- Use `$ git config --list --show-origin` to view all settings and their sources.
- View a specific key's value: `$ git config <key>` (e.g., `$ git config user.name`)
- Find the origin of a specific setting: `$ git config --show-origin <key>` (e.g., `$ git config --show-origin rerere.autoUpdate`). This will tell you which configuration file had the final say in setting that value.
- Duplicate keys may appear when values are read from multiple files; Git uses the **last value encountered**.
- GUI tools often assist in initial setup.

---

## Getting Help in Git

- **Accessing Git Manpages** (comprehensive help for commands):
  - `$ git help <verb>`
  - `$ git <verb> --help`
  - `$ man git-<verb>`
  - `$ git <verb> -h`, gives concise help on a command.

- **Offline Access**: Manpages are available anytime, even without internet.

---

## Summary:

Version control systems (VCS) track changes to files, allowing easy reversion and collaboration. There are three types:

1. **Local VCS** (e.g., RCS) tracks changes on a single computer, but lacks collaboration features and is prone to errors.
2. **Centralized VCS** (e.g., CVS, Subversion) stores files on a central server, enabling collaboration but risking data loss if the server fails.
3. **Distributed VCS** (e.g., Git, Mercurial) allows each client to store a full repository, offering better backup, collaboration, and flexibility.

Git is a fast, distributed version control system (DVCS) created by Linus Torvalds in 2005 after the relationship with BitKeeper, a proprietary version control system that stored Linux Kernel code, ended. Unlike other systems that store incremental file changes, Git stores full snapshots of the project at each commit, which makes retrieving previous versions efficient. Git operates mostly locally, allowing for offline work and faster execution. Every file in Git is checksummed using SHA-1 hashes, ensuring data integrity. Git is designed to add data rather than removing it, making recovery of lost data easy. Files in Git exist in three states: **Modified** (changes not staged or committed), **Staged** (changes ready for commit), and **Committed** (changes stored in the local repository). Git’s full functionality is available via the command line, offering a more flexible and complete experience than graphical interfaces.

Here is a summary of all the commands: 
| Command                                              | Description                                                                                      |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| `$ sudo apt update`                                  | Updates the package index.                                                                       |
| `$ sudo apt upgrade -y`                              | Upgrades all installed packages to the latest versions.                                          |
| `$ sudo apt install git -y`                          | Installs the core Git package with basic tools and utilities.                                    |
| `$ sudo apt install git-all -y`                      | Installs Git along with all related tools and utilities.                                         |
| `$ git --version`                                    | Displays the installed Git version.                                                              |
| `$ git config --local <key> <value>`                  | Configures a Git setting for the current repository (affects `./git/config`).                    |
| `$ git config --system <key> <value>`                | Configures a Git setting system-wide (affects `/etc/gitconfig`).                                 |
| `$ git config --global <key> <value>`                | Configures a Git setting globally for the user (affects `~/.gitconfig`).                         |
| `$ git config --global user.name "John Doe"`         | Sets the global user name for Git commits.                                                       |
| `$ git config --global user.email johndoe@example.com`| Sets the global user email for Git commits.                                                      |
| `$ git config --global core.editor "code --wait"`     | Specifies the default text editor for Git (e.g., `code --wait` for VS Code).                    |
| `$ git config --global init.defaultBranch main`      | Sets the default branch name for new repositories (e.g., `main`).                                |
| `$ git config --list`                                | Lists all Git configuration settings.                                                            |
| `$ git config --list --show-origin`                  | Lists all Git configuration settings with their source files.                                    |
| `$ git config <key>`                                 | Shows the value of a specific configuration key.                                                 |
| `$ git config <key> --show-origin`                   | Shows the origin of a specific configuration key.                                                |
| `$ git help <verb>`                                  | Displays the manual page for a Git command.                                                      |
| `$ git <verb> --help`                                | Displays the help message for a Git command.                                                     |
| `$ man git-<verb>`                                   | Displays the manual page for a specific Git command.                                             |
| `$ git <verb> -h`                                    | Provides concise help on a Git command.                                                          |
