# Chapter 2: Git Basics

If you read one Git chapter, make it this one. It covers essential commands for configuring, initializing, tracking, staging, committing, ignoring files, undoing mistakes, browsing history, and syncing with remote repositories.

## Table of Contents
- [Chapter 2: Git Basics](#chapter-2-git-basics)
  - [Table of Contents](#table-of-contents)
  - [Getting a Git Repository](#getting-a-git-repository)
    - [1. Initializing a Repository in an Existing Directory:](#1-initializing-a-repository-in-an-existing-directory)
    - [2. Cloning an Existing Repository:](#2-cloning-an-existing-repository)
  - [Recording Changes to Repository](#recording-changes-to-repository)
    - [Checking the Status of Your Files](#checking-the-status-of-your-files)
    - [Tracking New Files](#tracking-new-files)
    - [Staging Modified Files](#staging-modified-files)
    - [Short Status](#short-status)
    - [Ignoring Files](#ignoring-files)
    - [Viewing Your Staged and Unstaged Changes](#viewing-your-staged-and-unstaged-changes)
    - [Commiting Your Changes](#commiting-your-changes)
    - [Skippping the Staging Area](#skippping-the-staging-area)
    - [Removing Files](#removing-files)
    - [Moving Files](#moving-files)
  - [Viewing the Commit History](#viewing-the-commit-history)
    - [`git log`](#git-log)
    - [`git log -p` or `git log --patch`](#git-log--p-or-git-log---patch)
    - [`git log --stat`](#git-log---stat)
    - [`git log --pretty`](#git-log---pretty)
    - [A list of common placeholders for `--pretty`:](#a-list-of-common-placeholders-for---pretty)
    - [`--graph` option](#--graph-option)
    - [Difference between 'Author' and 'Committer'](#difference-between-author-and-committer)
    - [More options for `git log`](#more-options-for-git-log)
    - [Limiting Commits with `git log`](#limiting-commits-with-git-log)
  - [Undoing Things](#undoing-things)
    - [Undoing Commits](#undoing-commits)
    - [Undoing Staged Files](#undoing-staged-files)
    - [Unmodifying a Modified File](#unmodifying-a-modified-file)
    - [Undoing Things with `git restore`](#undoing-things-with-git-restore)
  - [Working with Remote](#working-with-remote)
    - [Showing Your Remotes](#showing-your-remotes)
    - [Adding Remote Repositories](#adding-remote-repositories)
    - [Fetching and Pulling from Your Remotes](#fetching-and-pulling-from-your-remotes)
    - [Pushing to Your Remotes](#pushing-to-your-remotes)
    - [Inspecting a Remote](#inspecting-a-remote)
    - [Renaming and Removing Remotes](#renaming-and-removing-remotes)
  - [Tagging](#tagging)
    - [Annotated Tags](#annotated-tags)
    - [Lightweight Tags](#lightweight-tags)
    - [Tagging Later](#tagging-later)
    - [Sharing Tags](#sharing-tags)
    - [Deleting Tags](#deleting-tags)
    - [Checking out Tags](#checking-out-tags)
  - [Git Aliasing](#git-aliasing)
  - [Summary](#summary)
    - [Summary of Commands](#summary-of-commands)

---

## Getting a Git Repository

**Two ways to obtain a Git repository**:
- Turn a local directory into a Git repository using `git init`.
- Clone an existing Git repository using `git clone`.

### 1. Initializing a Repository in an Existing Directory:
- Navigate to the project directory:
  ```
  $ cd /home/user/my_project
  ```
- Initialize a new Git repository:
  ```
  $ git init
  ```
  - This creates a `.git` subdirectory containing the repository's necessary files.
- If you want to **track** existing files, use `git add` to stage files and commit:
  ```
  $ git add *.c
  $ git add LICENSE
  $ git commit -m 'Initial project version'
  ```
  - This stages the files and commits them to the repository.

### 2. Cloning an Existing Repository:
- Use `git clone <url> [<directory_name>]` to clone a repository and get a full copy, including all file versions:
  ```
  $ git clone https://github.com/libgit2/libgit2
  ```
  - This creates a directory named `libgit2`, initializes a `.git` directory, and checks out the latest version.
- To clone into a custom directory name:
  ```
  $ git clone https://github.com/libgit2/libgit2 mylibgit
  ```
  - This will create a directory named `mylibgit` instead of `libgit2`.
- Git supports various transfer protocols, such as:
  - `https://`, `git://`, or `user@server:path/to/repo.git` (SSH).

---

## Recording Changes to Repository

Once you have a Git repository and a working copy of its files, you can start making changes and recording snapshots of your progress.  

Files in your working directory can either be:  
- **Tracked**: Files already in the last commit or newly staged. These can be unmodified, modified, or staged.  
- **Untracked**: Files not included in the last commit or staging area.  

When a repository is cloned, all files start as tracked and unmodified. As you make edits, Git marks them as modified. You can then **stage** the changes selectively and **commit** them, repeating this process as needed.

```plaintext
+------------+   +------------+   +------------+   +------------+
| Untracked  |   | Unmodified |   |  Modified  |   |   Staged   |
+------------+   +------------+   +------------+   +------------+
      |                 |                |                |
      | Add the file    |                |                |
      +-----------------+----------------+--------------->+
      |                 | Edit the file  |                |
      |                 +--------------->+                |
      |                 |                | Stage the file |
      |                 |                +--------------->+
      | Remove the file |                |                |
      +<----------------+                |                |
      |                 |                | Commit the file|
      |                 +<---------------+----------------+
      |                 |                |                |

```
---

### Checking the Status of Your Files

- The `git status` command is used to check the state of files in your working directory and staging area.  

- **After cloning a repository**, running `git status` might show:  
  ```
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  nothing to commit, working tree clean
  ```
  This indicates:
  - No modified tracked files.  
  - No untracked files.  
  - The current branch (e.g., `master`) is in sync with the remote branch.  

- **Default Branch Name**:  
  - Historically, the default branch name was `master`.  
  - GitHub changed the default branch name to `main` in **mid-2020**, with other hosts following suit.  
  - The default branch name can be customized, so it may vary in newly created repositories.  

- **Book's Convention**: Despite changes, the book uses `master` as the default branch name for consistency.

- If you add a new file (e.g., `README`) to your project, it will initially be **untracked** by Git.  

- Running `git status` after adding the file will display:  
  ```
  Untracked files:
    (use "git add <file>..." to include in what will be committed)

      README
  nothing added to commit but untracked files present (use "git add" to track)
  ```
  - This indicates that the file is not yet part of Git's tracking or staging process.  

- **Untracked Files**:  
  - Files that were not part of the last commit and are not yet staged.  
  - Git ignores these files until explicitly instructed to track them (e.g., using `git add`).  

- **Reason for Untracked State**:  
  - Git avoids automatically including new files to prevent accidental inclusion of generated or unintended files (e.g., binaries).  

---

### Tracking New Files

- To start tracking a new file, use the `git add` command:  
  ```
  $ git add README
  ```  

- After running `git add`, the file becomes **tracked** and is **staged** for the next commit.  

- Running `git status` after staging shows:  
  ```
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)

      new file:   README
  ```
  - The file appears under the “Changes to be committed” section, indicating it is staged.  

- When you commit, the version of the file at the time of running `git add` will be included in the next snapshot.  

- The `git add` command:  
  - Can be used to add individual files or entire directories.  
  - If given a directory path, it recursively stages all files within that directory.  

---

### Staging Modified Files

- When you modify a previously tracked file (e.g., `CONTRIBUTING.md`), it will appear under the **"Changes not staged for commit"** section in the `git status` output:  
  ```
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

      modified:   CONTRIBUTING.md
  ```  

- This indicates:  
  - The file is tracked.  
  - Changes have been made but are not yet staged for the next commit.  

- Use `git add` to stage the changes:  
  ```
  $ git add CONTRIBUTING.md
  ```  

- After staging, the file will appear under the **"Changes to be committed"** section in `git status`:  
  ```
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

      new file:   README
      modified:   CONTRIBUTING.md
  ```  

- **Key Points About `git add`:**  
  - It is used to stage files for a commit, whether they are newly added, modified, or involved in a merge conflict.  
  - Think of it as adding the **exact current content of the file** to the next commit, not just adding the file itself.  

- Once staged, both `README` and `CONTRIBUTING.md` will be included in the next commit.

- Say, you open `CONTRIBUTING.md` to make a small change and modify it.
- Now let's run `git status` to check the state of your working directory:
  ```bash
  $ git status
  ```
  Output:
  ```
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

      new file:   README
      modified:   CONTRIBUTING.md

  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

      modified:   CONTRIBUTING.md
  ```
  - `CONTRIBUTING.md` is listed **both** as staged and unstaged.
  
- Explanation: Git stages a file **exactly as it was** when you last ran `git add`. If you modify the file after that, the new changes won't be staged.
  
- To include the latest changes, you must run `git add` again:
  ```bash
  $ git add CONTRIBUTING.md
  ```

- Now, run `git status` again:
  ```bash
  $ git status
  ```
  Output:
  ```
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

      new file:   README
      modified:   CONTRIBUTING.md
  ```
  - `CONTRIBUTING.md` is now properly staged with the latest modifications.

---

### Short Status

- The `git status` command can be run with the `-s` or `--short` flag for a more compact output:
  ```bash
  $ git status -s
  ```

- Example output:
  ```
   M README
  MM Rakefile
  A  lib/git.rb
  M  lib/simplegit.rb
  ?? LICENSE.txt
  ```
- The output consists of two columns:
  - **Left column (staging area)**: Shows the status of the file in the staging area.
  - **Right column (working directory)**: Shows the status of the file in the working directory.
  
- Key symbols in the output:
  - `??` indicates a new, untracked file (e.g., `LICENSE.txt`).
  - `A` indicates a new file that has been added to the staging area (e.g., `lib/git.rb`).
  - `M` indicates a modified file.
    - `README` is modified in the working directory but not yet staged.
    - `lib/simplegit.rb` is modified and staged.
  - `MM` indicates a file that has been modified, staged, and modified again (e.g., `Rakefile`).

---

### Ignoring Files

- Use `.gitignore` to specify files or patterns to ignore, such as automatically generated files (e.g., log files, build outputs).
- Example `.gitignore` file:
  ```bash
  *.[oa]
  *~
  ```
  - First line ignores files ending in `.o` or `.a` (object and archive files).
  - Second line ignores files ending with a tilde (`~`), often used by editors like Emacs for temporary files.

**Pattern rules for `.gitignore`:**
- Blank lines and lines starting with `#` are ignored.
- Standard glob patterns work and are applied recursively in the working directory.
- Patterns starting with `/` avoid recursion (match only in the current directory).
- Patterns ending with `/` specify directories to ignore.
- Use `!` to negate a pattern (to track files even if they're matched by another rule).
  
**Examples of glob patterns:**
- `*` matches zero or more characters.
- `[abc]` matches any character inside the brackets (a, b, or c).
- `?` matches a single character.
- `[0-9]` matches any character between 0 and 9.
- `**` matches nested directories (e.g., `a/**/z` matches `a/z`, `a/b/z`, `a/b/c/z`, etc.).

**Another example `.gitignore` file:**
```bash
# ignore all .a files
*.a

# but do track lib.a
!lib.a

# only ignore the TODO file in the current directory
/TODO

# ignore all files in any build directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in doc/ and subdirectories
doc/**/*.pdf
```

**Additional `.gitignore` tips:**
- GitHub maintains a list of `.gitignore` examples for various languages and projects at [GitHub's gitignore repository](https://github.com/github/gitignore), which can be a good starting point. 
- A `.gitignore` file is typically placed in the root directory and applies recursively to the entire repository.
- A subdirectory can also have a `.gitignore` file, which applies only to that subdirectory. 
- Multiple `.gitignore` files can exist in subdirectories, with rules applying only to files in those directories (e.g., the Linux kernel repository has 206 `.gitignore` files).

---

### Viewing Your Staged and Unstaged Changes

- If `git status` is too vague and you want to see the exact lines of code added or removed (the patch), use `git diff`.
- It helps answer the following questions:
  - What changes have you made but not yet staged?
  - What changes have you staged and are about to commit?

**Example Scenario:**
- You edit and stage the `README` file, then edit the `CONTRIBUTING.md` file without staging it.
- Running `git status` will show:
  ```bash
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
      modified:   README
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
      modified:   CONTRIBUTING.md
  ```

**Viewing unstaged changes with `git diff`:**
- To see the exact changes made but not yet staged, run `git diff`:
  ```bash
  $ git diff
  ```
- Example output (shows added/removed lines in `CONTRIBUTING.md`):
  ```diff
  diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
  index 8ebb991..643e24f 100644
  --- a/CONTRIBUTING.md
  +++ b/CONTRIBUTING.md
  @@ -65,7 +65,8 @@ branch directly, things can get messy.
  Please include a nice description of your changes when you submit your PR;
  if we have to read the whole diff to figure out why you're contributing
  in the first place, you're less likely to get feedback and have your change
  -merged in.
  +merged in. Also, split your changes into comprehensive chunks if your patch is
  +longer than a dozen lines.
  
  If you are starting to work on a particular area, feel free to submit a PR
  that highlights your work in progress (and note in the PR title that it's
  ```

**What `git diff` does:**
- `git diff` compares the changes in your working directory with what is **staged**.
- It shows the differences between the current state of files and the version that has been staged for commit.
- If the current file has never been staged before then it will show all the changes made so far from the previous snapshot.
- If all changes are staged, `git diff` will show no output, since the file is no longer in unstaged mode.


**View staged changes with `git diff --staged`:**
- Use `git diff --staged` (or `git diff --cached`, as they are synonyms) to see changes that are staged for the next commit, comparing them to the **last commit**.
  ```bash
  $ git diff --staged
  diff --git a/README b/README
  new file mode 100644
  index 0000000..03902a1
  --- /dev/null
  +++ b/README
  @@ -0,0 +1 @@
  +My Project
  ```

**Git Diff in External Tools**:  
- You can also use graphical or external diff tools to view your changes.
- Run `git difftool` instead of `git diff` to view diffs in programs like `emerge`, `vimdiff`, etc.  
- Use `git difftool --tool-help` to see what tools are available on your system.

---

### Commiting Your Changes

- Before committing, ensure that all the changes you want to keep in the commit are staged using `git add`.
- Unstaged files (those not added with `git add`) will not be included in the commit.

**Committing**:
- To commit the changes in the staging area, run:
  ```bash
  $ git commit
  ```
- This will open your editor (usually `vim` or `emacs`), where you can write a commit message. The default editor screen will show something like this:
  ```
  # Please enter the commit message for your changes. Lines starting
  # with '#' will be ignored, and an empty message aborts the commit.
  # On branch master
  # Your branch is up-to-date with 'origin/master'.
  #
  # Changes to be committed:
  #   new file:   README
  #   modified:   CONTRIBUTING.md
  #
  ```
- Notice how the above commented message look very similar to `git status` result.
- You can remove the comment lines and add a meaningful commit message. For example:
  ```
  Add README and update contributing guidelines
  ```
- Once you save and exit the editor, Git will commit your changes.

**Commit Options**:
- To add "diff of the changes" while editing the commit message, use the `-v` option:
  ```bash
  $ git commit -v
  ```
- Alternatively, you can specify the commit message inline using the `-m` flag:
  ```bash
  $ git commit -m "Story 182: fix benchmarks for speed"
  ```

**Commit Output**:
- After committing, Git will show output like:
  ```
  [master 463dc4f] Story 182: fix benchmarks for speed
  2 files changed, 2 insertions(+)
  create mode 100644 README
  ```
- The output includes:
  - The branch you're committing to (`master`).
  - The commit SHA-1 hash (`463dc4f`).
  - The files affected by the commit and the changes made (insertions, deletions).

---

### Skippping the Staging Area

To skipping the staging area, use `-a` option, when you want to commit all changes to files that are already **tracked**.

**Using `git commit -a`**:
- If you run `git status` and see that files are modified but not staged, you can use the `-a` option with `git commit` to automatically stage all tracked files and commit them in one step.
- Example:
  ```bash
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

     modified:   CONTRIBUTING.md
  no changes added to commit (use "git add" and/or "git commit -a")
  $ git commit -a -m 'Add new benchmarks'
  [master 83e38c7] Add new benchmarks
  1 file changed, 5 insertions(+), 0 deletions(-)
  ```
- The `-a` flag stages all tracked files and commits them directly, bypassing the need for a `git add` step.
- If you have files in staged, git will add them also to the commit. 

**When to Use `git commit -a`**:
 - This is especially useful when you’ve made changes to files that are already tracked by Git, and you **don’t want to manually stage** them before committing.
 - However, it only works for modified files that Git is already tracking. New files (untracked files) **will not be included** in the commit with `git commit -a`. You would still need to use `git add` for those.

---

### Removing Files

The `git rm` command is used to remove files from Git, and it offers various options to suit different scenarios.

**Removing a File from the Working Directory and Git Tracking:**
- If you remove a **tracked file** from your working directory manually (e.g., using `rm`), it will show up in the "Changes not staged for commit" section:
  ```bash
  $ rm PROJECTS.md
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes not staged for commit:
   deleted:    PROJECTS.md
  ```

- To remove the file from both the working directory and Git's tracking, use `git rm`:
  ```bash
  $ git rm PROJECTS.md
  rm 'PROJECTS.md'
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes to be committed:
   deleted:    PROJECTS.md
  ```
- `rm`, remove file; `git rm`, remove file and stage it. 
- After committing, the file will be permanently removed from both the working directory and Git's tracking.

**Force Removal with `-f`:**
- If a file has been **modified** or is **staged** for commit, and you want to remove it from Git (even though there are changes), you need to **force** the removal using the `-f` option, since Git wants you to be **cautious** before removing any file:
  ```bash
  $ git rm -f PROJECTS.md
  ```

**Removing a File from Git Tracking but Keeping It Locally (`--cached`):**
- If you want to stop Git from tracking a file but keep it on your local machine (for example, if you've mistakenly staged a large log file or other files that should be ignored), you can use the `--cached` option:
  ```bash
  $ git rm --cached README
  ```

- This removes the file from Git’s tracking but keeps it in your working directory.
- Makes the file **untracked**. 

**Removing Multiple Files Using Globs:**
- You can use patterns to remove multiple files at once. For example, to remove all `.log` files in a directory, use:
  ```bash
  $ git rm log/*.log
  ```
*Note: Escape the `*` with a backslash (`\`) to prevent shell expansion.*

- To remove all files ending with a `~` (backup files), use:
  ```bash
  $ git rm *~
  ```

---

### Moving Files

- **No explicit tracking of file movement**: Git doesn’t store metadata to track file renaming. But Git is smart enough to figure it out.
- **Git mv command**: 
  - `git mv file_from file_to` renames a file and **stages** it for commit.
  - It’s a convenience function, which combines the steps of moving and staging.
  ```bash
  $ git mv README.md README
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

      renamed:    README.md -> README
  ```
- **Equivalent to manual renaming**:
  ```bash
  $ mv README.md README
  $ git rm README.md
  $ git add README
  ```
- **Git detects renames automatically**: Even without `git mv`, Git figures out file renaming implicitly when you move or rename files.

---

## Viewing the Commit History

### `git log`
- Used to view commit history in a repository.
- Displays commits in reverse chronological order (most recent first).
- Output includes:
  - SHA-1 checksum of the commit
  - Author’s name and email
  - Date of the commit
  - Commit message

- **Example output**:
  ```
  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700
  Change version number
  ```

---

### `git log -p` or `git log --patch`
- `-p` or `--patch`: Shows the differences (patch output) introduced in each commit.
- Example: 
  ```
  $ git log -p -2
  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700

      Change version number

  diff --git a/Rakefile b/Rakefile
  index a874b73..8f94139 100644
  --- a/Rakefile
  +++ b/Rakefile
  @@ -5,7 +5,7 @@ require 'rake/gempackagetask'
  spec = Gem::Specification.new do |s|
      s.platform  =   Gem::Platform::RUBY
      s.name      =   "simplegit"
  -    s.version   =   "0.1.0"
  +    s.version   =   "0.1.1"
      s.author    =   "Scott Chacon"
      s.email     =   "schacon@gee-mail.com"
      s.summary   =   "A simple gem for using Git in Ruby code."

  commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Sat Mar 15 16:40:33 2008 -0700

      Remove unnecessary test

  diff --git a/lib/simplegit.rb b/lib/simplegit.rb
  index a0a60ae..47c6340 100644
  --- a/lib/simplegit.rb
  +++ b/lib/simplegit.rb
  @@ -18,8 +18,3 @@ class SimpleGit
      end

  end
  -
  -if $0 == __FILE__
  -  git = SimpleGit.new
  -  puts git.show
  -end
  ```
  - Limits the log to show only the last two commits with their diffs.

- **Useful output for code review**:
  - Displays commit info followed by a `diff` for each commit.
  - Helps in quickly reviewing changes made during a series of commits.

---

### `git log --stat`


- Summarizes changes made in each commit.
- Displays:
  - List of modified files
  - Number of lines added and deleted in each file
  - Summary of changes at the end (e.g., number of files changed, insertions, and deletions)

- **Example output**:
  ```
  $ git log --stat -2
  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700
  Change version number

  Rakefile | 2 +-
  1 file changed, 1 insertion(+), 1 deletion(-)

  commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Sat Mar 15 16:40:33 2008 -0700

      Remove unnecessary test

  lib/simplegit.rb | 5 -----
  1 file changed, 5 deletions(-)
  ```

- **`git log --stat`** is helpful for:
  - Quickly understanding the scope of changes made in a commit
  - Seeing which files were affected and how much was modified.

---

### `git log --pretty`

- Customizes the format of the log output.
- Several prebuilt format values:
  - `oneline`: Prints each commit on a single line (useful for viewing many commits).
  - `short`, `full`, `fuller`: Provide different levels of information.
  
- **Example of `--pretty=oneline`**:
  ```
  $ git log --pretty=oneline
  ca82a6dff817ec66f44342007202690a93763949 Change version number
  085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 Remove unnecessary test
  a11bef06a3f659402fe7563abf99ad00de2209e6 Initial commit
  ```

- **`format` value for `--pretty`**:
  - Allows custom formatting of the log output.
  - Useful for generating machine-readable output.
  
- **Example of `--pretty=format`**:
  ```
  $ git log --pretty=format:"%h - %an, %ar : %s"
  ca82a6d - Scott Chacon, 6 years ago : Change version number
  085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
  a11bef0 - Scott Chacon, 6 years ago : Initial commit
  ```
  - Format placeholders:
    - `%h`: Abbreviated commit hash
    - `%an`: Author name
    - `%ar`: Relative date (e.g., "6 years ago")
    - `%s`: Commit message

### A list of common placeholders for `--pretty`: 

| Specifier | Description of Output                     |
|-----------|-------------------------------------------|
| `%H`      | Commit hash                               |
| `%h`      | Abbreviated commit hash                   |
| `%T`      | Tree hash                                 |
| `%t`      | Abbreviated tree hash                     |
| `%P`      | Parent hashes                             |
| `%p`      | Abbreviated parent hashes                 |
| `%an`     | Author name                               |
| `%ae`     | Author email                              |
| `%ad`     | Author date (format respects the `--date=` option) |
| `%ar`     | Author date, relative                     |
| `%cn`     | Committer name                            |
| `%ce`     | Committer email                           |
| `%cd`     | Committer date                            |
| `%cr`     | Committer date, relative                  |
| `%s`      | Subject                                   |

---

### `--graph` option

- Adds an ASCII graph to visualize the branch and merge history.
- Useful when combined with the `--pretty` option values like `oneline` or `format`.
- Shows how commits are related in the context of branches and merges.

- **Example output of `git log --pretty=format:"%h %s" --graph`**:
  ```
  * 2d3acf9 Ignore errors from SIGCHLD on trap
  *  5e3ee11 Merge branch 'master' of https://github.com/dustin/grit.git
  |\
  | * 420eac9 Add method for getting the current branch
  * | 30e367c Timeout code and tests
  * | 5a09431 Add timeout protection to grit
  * | e1193f8 Support for heads with slashes in them
  |/
  * d6016bc Require time for xmlschema
  *  11d191e Merge branch 'defunkt' into local
  ```

- **Benefit**: 
  - Provides a visual representation of the branching and merging history.
  - Becomes particularly useful when managing complex branching and merge scenarios.

---

### Difference between 'Author' and 'Committer'

- **Author**: The person who originally wrote the work (e.g., created the code or patch).
- **Committer**: The person who last applies the work (e.g., merges or commits the patch to the repository).
  
- **Purpose**: This distinction allows both contributors to be acknowledged:
  - The **author** for their original work.
  - The **committer** for modifying and integrating that work into the repository.

---

### More options for `git log`

Here is the information as a Markdown table:

| Option             | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `-p`               | Show the patch introduced with each commit.                                 |
| `--stat`           | Show statistics for files modified in each commit.                          |
| `--shortstat`      | Display only the changed/insertions/deletions line from the `--stat` command.|
| `--name-only`      | Show the list of files modified after the commit information.               |
| `--name-status`    | Show the list of files affected with added/modified/deleted information.    |
| `--abbrev-commit`  | Show only the first few characters of the SHA-1 checksum instead of all 40.  |
| `--relative-date`  | Display the date in a relative format (e.g., "2 weeks ago") instead of using the full date format. |
| `--graph`          | Display an ASCII graph of the branch and merge history beside the log output.|
| `--pretty`         | Show commits in an alternate format. Option values include `oneline`, `short`, `full`, `fuller`, and `format` (where you specify your own format). |
| `--oneline`        | Shorthand for `--pretty=oneline --abbrev-commit` used together.              |

---

### Limiting Commits with `git log`

- **`-<n>`**: Show the last `n` commits (e.g., `-2` to show the last two commits).
- Git uses a pager by default, so only one page of log output is displayed at a time, hence rendering the `-<n>` option "useless".
  
- **Time-limiting options**:
  - **`--since`**: Show commits since a specific time (e.g., `--since=2.weeks` for commits in the last two weeks).
  - **`--until`**: Show commits until a specific time (e.g., `--until=2008-01-15`).
  - Dates can be:
    - Specific (e.g., "2008-01-15")
    - Relative (e.g., "2 years 1 day 3 minutes ago")

- **Search filters**:
  - **`--author`**: Filter commits by a specific author.
  - **`--grep`**: Search for keywords in commit messages.
  
- **Multiple search criteria**:
  - You can specify multiple `--author` and `--grep` options to filter by any of the provided patterns.
  - **`--all-match`**: Limits the output to commits that match all of the provided `--grep` patterns (useful for more precise filtering).

- **`-S` option (Git's "pickaxe" option)**:
  - Filters commits based on the number of occurrences of a string.
  - Useful to find commits that added or removed references to a specific function, variable, or string.
  - Example: `git log -S function_name` to see commits involving `function_name`.

- **Limiting by path**:
  - You can limit the `git log` output to specific files or directories.
  - Specify the file or directory path after the options.
  - Typically, the path is preceded by double dashes (`--`) to separate it from other options.
  - Example: `git log -- path/to/file` to show commits that changed that specific file.

- **Other common options**:
  - The section suggests that additional options to limit `git log` output will be listed, but this serves as a reference for commonly used filters.

- **Filtering commits based on multiple criteria**:
  - Example: Find commits modifying test files in the Git source code by **Junio Hamano** in **October 2008**, excluding merge commits.
  - Command: 
    ```bash
    git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
       --before="2008-11-01" --no-merges -- t/
    ```
  - This command filters for:
    - **Author**: Junio C Hamano.
    - **Date range**: Commits between October 1, 2008, and October 31, 2008.
    - **No merge commits**: Excludes merge commits.
    - **Path**: Filters by the `t/` directory (test files).
  - Result: Shows 6 commits that match these criteria.

- **Preventing the display of merge commits**:
  - If merge commits are cluttering the log, use the **`--no-merges`** option to exclude them from the output.
  - This can help focus on non-merge commits that are typically more informative.

---

## Undoing Things

Be cautious when undoing changes in Git as it can lead to data loss if done incorrectly.
  
### Undoing Commits

- **Amending the last commit**:
  - Use the `--amend` option if you want to redo a commit (e.g., to add missing files or fix a commit message).
  - Command: 
    ```bash
    git commit --amend
    ```
  - This command:
    - Takes the current staging area and uses it for the commit.
    - If no changes are staged, only the commit message can be edited.
    - If files are added after the last commit, those files will be included in the new commit.
  
- **Example of amending a commit**:
  - Scenario:
       ```bash
       git commit -m 'Initial commit'
       git add forgotten_file
       git commit --amend
       ```
  - Result: The first commit is replaced with the new one, and only one commit appears in the history.

- **Key points about amending commits**:
  - **Replaces the last commit**: Amending is like replacing the previous commit entirely with a new one. The old commit is removed from the history.
  - **Clean up commit history**: Amend to make small improvements without cluttering the history with unnecessary "Oops" commits.
  
- **Important considerations**:
  - **Local commits only**: Amend only commits that haven’t been pushed to a remote repository. Amending pushed commits and force-pushing can cause issues for collaborators.

### Undoing Staged Files

- `git status` helps track the state of your staging area and working directory. It also provides **hints** on how to undo changes.
  
- If you accidentally stage files you didn’t intend to commit, you can unstage them using:
  ```bash
  git reset HEAD <file>
  ```
- Example:
  1. You stage files:
     ```bash
     git add *
     ```
  2. Check the status:
     ```bash
     git status
     ```
     Output shows the files staged for commit.
  3. To unstage a specific file, such as `CONTRIBUTING.md`:
     ```bash
     git reset HEAD CONTRIBUTING.md
     ```
  4. The file will be unstaged, and the status will reflect the file as modified but not staged.

- **Important Notes**:
  - `git reset` can be a **dangerous command**, particularly with the `--hard` flag, but in this case, using `git reset HEAD` only **affects the staging area**, leaving the working directory untouched.
  - For now, focus on using `git reset HEAD <file>` for unstaging files, as this is a safe and useful practice.

---

### Unmodifying a Modified File  

- **Reverting a modified file**  
  - If you want to discard changes to a file, use:  
    ```
    git checkout -- <file>
    ```  
  - This restores the file to the last committed version.

- **Git status provides guidance**  
  - Running `git status` shows:  
    ```
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    ```

- **Warning: This command is destructive**  
  - `git checkout -- <file>` permanently removes local changes.  
  - Only use it if you are sure you don’t need those modifications.  

- **Alternative approaches**  
  - If you want to keep changes but temporarily set them aside, consider:  
    - **Stashing** (`git stash`)  
    - **Branching** (creating a new branch for changes)

- **Recovering lost commits**  
  - Any committed changes in Git can typically be recovered.  
  - Even deleted branches or amended commits can often be retrieved.  
  - However, **uncommitted changes that are lost cannot be recovered**.

---

### Undoing Things with `git restore`  

- **Introduction to `git restore`**  
  - Introduced in Git **2.23.0** as an alternative to `git reset`.  
  - Used for many undo operations instead of `git reset`.  

- **Unstaging a Staged File**  
  - If you accidentally stage a file, use:  
    ```
    git restore --staged <file>
    ```  
  - Example scenario:  
    - You run `git add *` and stage all changes.  
    - `git status` suggests:  
      ```
      (use "git restore --staged <file>..." to unstage)
      ```  
    - Running `git restore --staged CONTRIBUTING.md` unstages the file.

- **Unmodifying a Modified File**  
  - If you want to discard local changes, use:  
    ```
    git restore <file>
    ```  
  - `git status` will remind you with:  
    ```
    (use "git restore <file>..." to discard changes in working directory)
    ```
  - Example:  
    - Running `git restore CONTRIBUTING.md` reverts it to the last committed state.

- **Warning: `git restore` is destructive**  
  - `git restore <file>` **permanently removes local changes**.  
  - Use this command only if you are **sure** you don’t need those modifications.

---

## Working with Remote

- **Definition of Remote Repositories**  
  - Remote repositories are **versions of your project** hosted on the **Internet or a network**.  
  - They allow **collaboration** by enabling **pushing and pulling of data**.  

- **Managing Remote Repositories**  
  - **Adding** new remotes.  
  - **Removing** outdated or unused remotes.  
  - Managing **remote branches**.  
  - Setting up **tracking branches** for easier updates.  

- **Operations with Remotes**  
  - **Push** changes to share work.  
  - **Pull** updates from others.  
  - **Fetch** remote changes without merging them immediately.  

- **Remote Repositories on the Same Machine**  
  - A "remote" repository **does not have to be on a different machine**.  
  - You can work with a remote repository **on the same host**, using standard Git commands like `push`, `pull`, and `fetch`.

---

### Showing Your Remotes  

- **Checking Remote Repositories**  
  - Use `git remote` to list remote repositories configured for your project.  
  - If you cloned a repository, you will see at least one remote called **`origin`** (default name for the source repository).  

  ```bash
  $ git remote
  origin
  ```

- **Displaying Remote URLs**  
  - Use `git remote -v` to view the URLs associated with each remote.  
  - This shows both **fetch** (read) and **push** (write) URLs.  

  ```bash
  $ git remote -v
  origin  https://github.com/schacon/ticgit (fetch)
  origin  https://github.com/schacon/ticgit (push)
  ```

- **Working with Multiple Remotes**  
  - If collaborating with multiple people, you may have several remotes.  
  - Example:  

  ```bash
  $ git remote -v
  bakkdoor  https://github.com/bakkdoor/grit (fetch)
  bakkdoor  https://github.com/bakkdoor/grit (push)
  cho45     https://github.com/cho45/grit (fetch)
  cho45     https://github.com/cho45/grit (push)
  defunkt   https://github.com/defunkt/grit (fetch)
  defunkt   https://github.com/defunkt/grit (push)
  ```

  - This setup allows pulling contributions from multiple sources.  
  - Push access depends on permissions, which **isn’t shown** in this command output.  

- **Different Remote Protocols**  
  - Remotes can use different protocols, such as:  
    - **HTTPS** (`https://github.com/user/repo.git`)  
    - **SSH** (`git@github.com:user/repo.git`)  
    - **Git protocol** (`git://github.com/user/repo.git`)  

---

### Adding Remote Repositories  

- **Adding a New Remote**  
  - Use `git remote add <shortname> <url>` to add a remote repository with a short alias.  
  - Example:  

    ```bash
    $ git remote add pb https://github.com/paulboone/ticgit
    ```

- **Verifying Added Remotes**  
  - Run `git remote -v` to list all remotes and their URLs.  
  - Example output:  

    ```bash
    $ git remote -v
    origin  https://github.com/schacon/ticgit (fetch)
    origin  https://github.com/schacon/ticgit (push)
    pb      https://github.com/paulboone/ticgit (fetch)
    pb      https://github.com/paulboone/ticgit (push)
    ```

- **Fetching Data from a Remote**  
  - Use `git fetch <shortname>` to retrieve new branches and updates from a remote repository.  
  - Example:  

    ```bash
    $ git fetch pb
    ```

  - This fetches new branches and updates from `pb`.  

- **Accessing the Fetched Branches**  
  - After fetching, remote branches can be accessed locally, e.g., `pb/master`.  
  - You can:  
    - **Merge** it into your branch.  
    - **Check it out** to inspect its contents.

---

### Fetching and Pulling from Your Remotes  

- **Fetching Remote Data**  
  - Use `git fetch <remote>` to download new data from the remote repository.  
  - It **does not** merge changes into your working branch automatically.  
  - Example:  

    ```bash
    $ git fetch origin
    ```

- **Fetching vs. Pulling**  
  - `git fetch` → Downloads changes but **does not merge** them.  
  - `git pull` → Fetches **and merges** the remote branch into the current branch.  
  - Example of `git pull`:  

    ```bash
    $ git pull origin master
    ```

- **Tracking Remote Branches**  
  - When you clone a repository, your local `master` branch is automatically set to track `origin/master`.  
  - Running `git pull` fetches and merges updates from the tracked branch.  

- **Handling Git Pull Warnings (Git 2.27+)**  
  - Git warns if `pull.rebase` is not set. Options:  
    - Default behavior (fast-forward if possible, else merge commit):  

      ```bash
      $ git config --global pull.rebase "false"
      ```

    - Always rebase when pulling:  

      ```bash
      $ git config --global pull.rebase "true"
      ```
---

### Pushing to Your Remotes  

- **Pushing Local Changes to a Remote Repository**  
  - Use `git push <remote> <branch>` to push your commits to the remote repository.  
  - Example:  

    ```bash
    $ git push origin master
    ```

- **Push Conditions**  
  - You **must** have write access to the remote repository.  
  - Your push will be **rejected** if someone else has pushed changes before you.  

- **Handling Rejected Pushes**  
  - First, fetch the latest changes:  

    ```bash
    $ git fetch origin
    ```

  - Merge the remote changes into your branch:  

    ```bash
    $ git merge origin/master
    ```

  - Push your changes after resolving conflicts (if any):  

    ```bash
    $ git push origin master
    ```

---

### Inspecting a Remote

To view detailed information about a remote repository, use:  

```bash
$ git remote show <remote>
```

For example, checking details of the `origin` remote:  

```bash
$ git remote show origin
```

**Example Output**  

```bash
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```

**Understanding the Output**  

- **Fetch & Push URL**: The repository’s location for pulling and pushing updates.  
- **HEAD branch**: The main branch the remote repository points to.  
- **Remote branches**: Lists branches that exist on the remote.  
- **Local branch configured for `git pull`**: Specifies which local branch will merge with its remote counterpart when pulling.  
- **Local ref configured for `git push`**: Defines which branch gets updated when pushing.  

---

For more complex repositories, the output may include additional details:  

```bash
$ git remote show origin
* remote origin
  URL: https://github.com/my-org/complex-project
  Fetch URL: https://github.com/my-org/complex-project
  Push  URL: https://github.com/my-org/complex-project
  HEAD branch: master
  Remote branches:
    master                           tracked
    dev-branch                       tracked
    markdown-strip                   tracked
    issue-43                         new (next fetch will store in remotes/origin)
    issue-45                         new (next fetch will store in remotes/origin)
    refs/remotes/origin/issue-11     stale (use 'git remote prune' to remove)
  Local branches configured for 'git pull':
    dev-branch merges with remote dev-branch
    master     merges with remote master
  Local refs configured for 'git push':
    dev-branch                     pushes to dev-branch                     (up to date)
    markdown-strip                 pushes to markdown-strip                 (up to date)
    master                         pushes to master                         (up to date)
```

**Additional Details in This Output**  

- **New branches**:  
  ```bash
  issue-43                         new (next fetch will store in remotes/origin)
  ```
  These are branches that exist on the remote but are not yet fetched locally. Running `git fetch origin` will update your local copy.  

- **Stale branches**:  
  ```bash
  refs/remotes/origin/issue-11     stale (use 'git remote prune' to remove)
  ```
  These branches no longer exist on the remote but still appear locally. Clean them up with:  

  ```bash
  $ git remote prune origin
  ```

This command removes outdated references, keeping your repository up to date.

---

### Renaming and Removing Remotes

**Renaming a Remote**  
To rename a remote repository, use:  

```bash
$ git remote rename <old-name> <new-name>
```

For example, renaming `pb` to `paul`:  

```bash
$ git remote rename pb paul
$ git remote
origin
paul
```
**Note:** This also updates all remote-tracking branches, for e.g., `pb/master` → `paul/master`.


**Removing a Remote**  
If a remote is no longer needed, remove it using:  

```bash
$ git remote remove <remote-name>
```
or  
```bash
$ git remote rm <remote-name>
```

Example: Removing `paul`:  

```bash
$ git remote remove paul
$ git remote
origin
```

**Important:** Removing a remote deletes:  
- **Remote-tracking branches** (e.g., `paul/master`)  
- **Associated configurations**  

---

## Tagging

Git has the ability to tag specific points in a repository’s history as being important. Typically, people use this functionality to mark release points (v1.0, v2.0 and so on).

- **Listing existing tags**: Use the command `git tag` to list all tags in the repository.
  - Example:  
    ```
    $ git tag  
    v1.0  
    v2.0  
    ```

- **Order of tags**: Tags are listed alphabetically by default; the order does not indicate their significance.

- **Listing tags with a pattern**: You can list tags that match a specific pattern using `git tag -l <pattern>`.
  - Example to search for version `1.8.5` tags:  
    ```
    $ git tag -l "v1.8.5*"  
    v1.8.5  
    v1.8.5-rc0  
    v1.8.5-rc1  
    v1.8.5-rc2  
    v1.8.5-rc3  
    v1.8.5.1  
    v1.8.5.2  
    v1.8.5.3  
    v1.8.5.4  
    v1.8.5.5  
    ```

- **Required flag for wildcards**: To use a wildcard pattern, the `-l` or `--list` flag is necessary. Without it, the wildcard search won't work.

- **Optional flag**: The `-l` or `--list` flag is optional when you are listing all tags without any pattern.

- **Types of Tags in Git**:
  - **Lightweight Tags**: A simple pointer to a specific commit, similar to a branch, but it doesn’t change.
  - **Annotated Tags**: Stored as full objects in the Git database, containing:
    - Tagger's name, email, and date.
    - A tagging message.
    - Can be signed and verified with GPG.

- **Recommended Tag Type**: Annotated tags are generally recommended as they store more information and are verifiable.

---

### Annotated Tags
- **Create an annotated tag**: Use `-a` and `-m` flags:
  ```
  $ git tag -a v1.4 -m "my version 1.4"
  ```
- **View all tags**:
  ```
  $ git tag
  v0.1
  v1.3
  v1.4
  ```
- **View tag data**: Use `git show` to see tag information along with the commit:
  ```
  $ git show v1.4
  tag v1.4
  Tagger: Ben Straub <ben@straub.cc>
  Date:   Sat May 3 20:19:12 2014 -0700

  my version 1.4

  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700

      Change version number
  ```

---

### Lightweight Tags
- **Create a lightweight tag**: No `-a`, `-s`, or `-m` options needed:
  ```
  $ git tag v1.4-lw
  ```
- **View all tags**:
  ```
  $ git tag
  v0.1
  v1.3
  v1.4
  v1.4-lw
  v1.5
  ```
- **View lightweight tag**: `git show` only displays commit info (no extra tag details):
  ```
  $ git show v1.4-lw
  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700

      Change version number
  ```

---

### Tagging Later

- **Tagging after the fact**: You can tag any commit, even if you've moved past it in your history.

- **Example scenario**: Suppose you forgot to tag a commit (e.g., `v1.2`), but you want to do so later. Here's how you can add the tag after the commit:

  - **View commit history** using `git log --pretty=oneline`:
    ```
    $ git log --pretty=oneline
    15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
    a6b4c97498bd301d84096da251c98a07c7723e65 Create write support
    0d52aaab4479697da7686c15f77a3d64d9165190 One more thing
    ...
    9fceb02d0ae598e95dc970b74767f19372d61af8 Update rakefile
    964f16d36dfccde844893cac5b347e7b3d44abbc Commit the todo
    8a5cbc430f1a9c3d00faaeffd07798508422908a Update readme
    ```

  - **Tag the commit**: Use the commit checksum (or part of it) at the end of the tag command:
    ```
    $ git tag -a v1.2 9fceb02
    ```
  
  - **View all tags**:
    ```
    $ git tag
    v0.1
    v1.2
    v1.3
    v1.4
    v1.4-lw
    v1.5
    ```

  - **View tag details** using `git show`:
    ```
    $ git show v1.2
    tag v1.2
    Tagger: Scott Chacon <schacon@gee-mail.com>
    Date:   Mon Feb 9 15:32:16 2009 -0800

    version 1.2
    commit 9fceb02d0ae598e95dc970b74767f19372d61af8
    Author: Magnus Chacon <mchacon@gee-mail.com>
    Date:   Sun Apr 27 20:43:35 2008 -0700

        Update rakefile
    ```

---

### Sharing Tags

**Pushing tags to a remote**:
- By default, `git push` does **not** push tags to remote servers. You need to explicitly push tags after creating them.

**Push a single tag**:
- To push a specific tag to a remote:
  ```
  $ git push origin v1.5
  ```

**Push all tags**:
- To push all tags that haven't been pushed yet, use the `--tags` option:
  ```
  $ git push origin --tags
  ```

**Effect of pushing tags**: When you push tags, they become available on the remote, and others who clone or pull from your repository will get the tags too.

**Tag types**: Both **lightweight** and **annotated** tags are pushed by `git push --tags`. However:
- Use `git push <remote> --follow-tags` to only push **annotated** tags, excluding lightweight tags.

**Example output**:
- Pushing a single tag:
  ```
  $ git push origin v1.5
  * [new tag] v1.5 -> v1.5
  ```
- Pushing all tags:
  ```
  $ git push origin --tags
  * [new tag] v1.4 -> v1.4
  * [new tag] v1.4-lw -> v1.4-lw
  ```

---

### Deleting Tags

**Deleting a local tag**:
- To delete a tag from your local repository, use:
  ```
  $ git tag -d <tagname>
  ```
- Example:
  ```
  $ git tag -d v1.4-lw
  Deleted tag 'v1.4-lw' (was e7d5add)
  ```

**Deleting a remote tag**:
- Deleting a tag locally does not remove it from the remote server. There are two common methods to delete a remote tag:

1. **First method**: Using the `:refs/tags/` syntax:
   ```
   $ git push origin :refs/tags/<tagname>
   ```
   - Example:
     ```
     $ git push origin :refs/tags/v1.4-lw
     To /git@github.com:schacon/simplegit.git
      - [deleted]         v1.4-lw
     ```

2. **Second method**: Using `--delete` flag (more intuitive):
   ```
   $ git push origin --delete <tagname>
   ```
   - Example:
     ```
     $ git push origin --delete v1.4-lw
     ```

---

### Checking out Tags

- You can view the version of files a tag is pointing to by using `git checkout <tagname>`:
```
$ git checkout v2.0.0
Note: switching to 'v2.0.0'.
```

**Detached HEAD state**:
- After checking out a tag, your repository enters the "detached HEAD" state.
- In this state, you can:
 - Look around, make experimental changes, and commit them.
 - Any commits made won't be part of any branch and will be lost unless explicitly saved by creating a branch.

**Creating a new branch**:
- If you want to retain commits, create a new branch:
 ```
 $ git checkout -b <new-branch-name> <tagname>
 ```
 Example:
 ```
 $ git checkout -b version2 v2.0.0
 Switched to a new branch 'version2'
 ```

**Handling new commits in detached HEAD**:
- If you make changes and commit in the detached HEAD state without creating a branch, the commit won’t be part of any branch and will be unreachable except by the commit hash.
- To avoid this, always create a branch before making changes if you want to keep your commits.

**Undoing detached HEAD state**:
- To undo the checkout and return to the previous branch:
 ```
 $ git switch -
 ```

**Configuring detached HEAD advice**:
- You can turn off the detached HEAD advice by setting the configuration variable:
 ```
 git config advice.detachedHead false
 ```

---

## Git Aliasing

**Git Aliases**: Aliases allow you to shorten commonly used Git commands, making your workflow faster and easier.

**Setting up aliases**: Use `git config --global alias.<alias-name> <command>` to create an alias. Some common examples:
- `git commit` as `git ci`:
  ```
  $ git config --global alias.ci commit
  ```
- `git checkout` as `git co`:
  ```
  $ git config --global alias.co checkout
  ```
- `git branch` as `git br`:
  ```
  $ git config --global alias.br branch
  ```
- `git status` as `git st`:
  ```
  $ git config --global alias.st status
  ```

**Creating custom aliases**:
- You can create aliases for commands that don’t exist by default, like unstaging a file:
  ```
  $ git config --global alias.unstage 'reset HEAD --'
  ```
  Now, `git unstage <file>` is equivalent to `git reset HEAD -- <file>`.

**Alias for the last commit**:
- To quickly view the last commit, you can create an alias like:
  ```
  $ git config --global alias.last 'log -1 HEAD'
  ```
- Then, use `git last` to see the most recent commit.

**Running external commands with aliases**:
- You can run external commands by starting the alias with a `!`. For example, to use `gitk` with `git visual`:
  ```
  $ git config --global alias.visual '!gitk'
  ```
- Now, `git visual` runs `gitk`, which is an external tool for visualizing the Git history.

---

## Summary

At this point, you can do all the basic local Git operations — creating or cloning a repository, making changes, staging and committing those changes, and viewing the history of all the changes the repository has been through. Next, we’ll cover Git’s killer feature: its branching model.

### Summary of Commands

| Command | Description |
|---------|------------|
| `git init` | Initialize a new Git repository. |
| `git add <file/directory>` | Add a file or directory to the staging area. |
| `git clone <url> directory_name` | Clone a repository into a specific directory. |
| `git status` | Show the working tree status. |
| `git status -s` | Show a short status output. |
| `git diff` | Show unstaged changes. |
| `git diff --cached / --staged` | Show staged changes. |
| `git commit` | Commit staged changes. |
| `git commit -v` | Show commit diff while committing. |
| `git commit -m "<message>"` | Commit with a message. |
| `git commit -a` | Stage and commit all tracked files. |
| `git commit -a -m "<message>"` | Stage and commit with a message. |
| `rm <file> && git add .` | Remove a file and stage the change. |
| `git rm <file>` | Remove a file from the working directory and Git. |
| `git rm -f <file>` | Force remove a file. |
| `git rm --cached <file>` | Remove a file from Git but keep it locally. |
| `git rm <regular pattern>` | Remove files matching a pattern. |
| `git mv <from> <to>` | Rename/move a file. |
| `mv README.md README; git rm README.md; git add README` | Rename a file using standard shell commands and Git. |
| `git log` | Show commit history. |
| `git log -p` or `git log --patch` | Show commit differences. |
| `git log --stat` | Show commit stats. |
| `git log --pretty=<something>` | Customize log output. |
| `git log --pretty=oneline` | Show logs in a single line. |
| `git log --pretty=format"%h ..."` | Show custom log format. |
| `git log --graph` | Show commits as a graph. |
| `git log --pretty=oneline --graph` | Show a one-line graph view. |
| `git log -<n>` | Show last `n` commits. |
| `git log --since=<commit/date> --until=<commit/date>` | Filter logs by date/commit. |
| `git log --author=<name>` | Show commits by an author. |
| `git log --grep=<pattern>` | Show commits matching a pattern. |
| `git log -S <keyword>` | Show commits adding/removing a keyword. |
| `git log -- <path/to/file>` | Show file-specific history. |
| `git commit --amend` | Edit the last commit. |
| `git reset HEAD <file>` or `git restore --cached / --staged <file>` | Unstage a file. |
| `git checkout -- <file>` or `git restore <file>` | Discard local changes. |
| `git remote` | Show remote repositories. |
| `git remote -v` | Show remote URLs. |
| `git remote add <short_name> url` | Add a remote repository. |
| `git fetch <short_name>` | Fetch changes from a remote. |
| `git push <short_name> <branch>` | Push changes to a remote branch. |
| `git fetch <remote>` | Fetch all changes from a remote. |
| `git merge <remote>/<branch>` | Merge remote branch into local. |
| `git push <remote> <branch>` | Push a branch to a remote. |
| `git remote show <remote>` | Show remote details. |
| `git remote rename <old_remote_name> <new_remote_name>` | Rename a remote. |
| `git remote remove <remote_name>` or `git remote rm <remote_name>` | Remove a remote. |
| `git tag` | List all tags. |
| `git tag <lightWeightTagName> [commit-hash]` | Create a lightweight tag. |
| `git tag -l/--list "<pattern>"` | List tags matching a pattern. |
| `git tag -a <annotatedTagName> -m "<Message>" [commit-hash]` | Create an annotated tag. |
| `git show <annotatedTagName>` | Show tag details. |
| `git push <remote> <tagName>` | Push a tag to a remote. |
| `git push <remote> --tags` | Push all tags to a remote. |
| `git push <remote> --follow-tags` | Push only annotated tags. |
| `git tag -d <tagName>` | Delete a tag locally. |
| `git push <remote> --delete <tagName>` | Delete a tag remotely. |
| `git checkout <tagName>` | Checkout a tag. |
| `git checkout -b <new-branch-name> <tagname>` | Create a new branch from a tag. |
| `git switch -` | Switch to the previous branch. |
| `git config --global alias.<alias-name> <command>` | Create a Git alias. |
| `git config --global alias.<alias-name> "!<terminal commands>"` | Create an alias for shell commands. |
| `git config --global advice.detachedHead "false"/"true"` | Enable/disable detached head warnings. |
| `git config --global pull.rebase "false"/"true"` | Configure pull behavior. |

Also take a look at  
- `git log -pretty` [placeholders](#a-list-of-common-placeholders-for---pretty).  
- `git log` [options](#more-options-for-git-log).

---