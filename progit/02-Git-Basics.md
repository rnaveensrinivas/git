# Git Basics

## Table of Contents
- [Git Basics](#git-basics)
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
    - [`git log`:](#git-log)
    - [`git log -p` or `git log --patch`:](#git-log--p-or-git-log---patch)
    - [`git log --stat`](#git-log---stat)
    - [`git log --pretty`](#git-log---pretty)
    - [`--graph` option](#--graph-option)
    - [Difference between 'Author' and 'Committer'](#difference-between-author-and-committer)
    - [More options for `git log`](#more-options-for-git-log)
    - [Limiting Commits with `git log`](#limiting-commits-with-git-log)
  - [Undoing Things](#undoing-things)
    - [Undoing Commits](#undoing-commits)
    - [Undoing Staged Files](#undoing-staged-files)

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
- If you want to track existing files, use `git add` to stage files and commit:
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
  - GitHub changed the default branch name to `main` in mid-2020, with other hosts following suit.  
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
- Use `git diff --staged` (or `git diff --staged`, as they are synonyms) to see changes that are staged for the next commit, comparing them to the **last commit**.
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

### `git log`: 
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

### `git log -p` or `git log --patch`:
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

- Here is a list of common placeholders for `--pretty`: 
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
