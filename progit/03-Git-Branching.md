### Table of Content
- [Git Brnaching](#git-brnaching)
  - [Git Branches in a Nutshell](#git-branches-in-a-nutshell)
    - [How Git Stores Data](#how-git-stores-data)
    - [Git Objects After First Commit](#git-objects-after-first-commit)
    - [Subsequent Commits](#subsequent-commits)
    - [What is a Branch in Git?](#what-is-a-branch-in-git)
    - [Creating a New Branch](#creating-a-new-branch)
    - [Switching Branches](#switching-branches)
  - [Summary](#summary)
    - [Summary of Commands](#summary-of-commands)

---

# Git Brnaching

- **Branching in VCS:**  
  - Most Version Control Systems (VCS) support branching.  
  - Branching allows developers to work separately without affecting the main development line.  
  - In many VCS tools, branching is expensive, requiring a full copy of the source code, making it slow for large projects.  

- **Git’s Unique Branching Model:**  
  - Git’s branching is **lightweight** and **fast**.  
  - Creating branches in Git is nearly **instantaneous**.  
  - Switching between branches is also very **quick**.  
  - Encourages frequent branching and merging, even multiple times a day.  

- **Advantages of Git Branching:**  
  - Enables **better workflows** with easy experimentation.  
  - Reduces the overhead of managing separate development lines.  
  - Provides a **powerful** and **flexible** way to develop software.  
  - Can **entirely change** how development is approached.  

## Git Branches in a Nutshell

### How Git Stores Data
- Git **does not** store data as changesets (differences) like other VCS.  
- Instead, it stores **snapshots** of the entire project at each commit.  
- Each commit includes:  
  - A pointer to the staged snapshot.  
  - Metadata (author, email, commit message).  
  - Parent commit(s):  
    - **0 parents** → Initial commit.  
    - **1 parent** → Normal commit.  
    - **Multiple parents** → Merge commit.  

**Example: Creating a Commit**  
- Suppose you have three files (`README`, `test.rb`, `LICENSE`).  
- When you **stage** them (`git add`), Git:  
  - Computes a **SHA-1 checksum** for each file.  
  - Stores them as **blobs** in the repository.  
  - Adds the checksums to the **staging area**.  
- Running `git commit -m 'Initial commit'`:  
  - Creates a **tree object** (snapshot of the directory).  
  - Creates a **commit object** pointing to this tree.  
  - Stores commit metadata.  

### Git Objects After First Commit  
- The repository contains **5 objects**:  
  - **3 blobs** → Contents of the three files.  
  - **1 tree** → Directory structure linking filenames to blobs.  
  - **1 commit** → Points to the root tree and contains metadata.  
  - Each of these 5 objects will have a **SHA-1 hash**.

    ```
    98ca9          92ec2
    [ commit ] ---> [ tree ]
                    |
                ----------------
                |      |       |
                blob   blob    blob
            5b1d3   911e7   cba0a
            README  test.rb  LICENSE
    ```

### Subsequent Commits  
- When you make changes and commit again:  
  - A **new commit** is created.  
  - It **points to the previous commit**.  
  - Forms a **linked chain of commits**.  

    ```
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 - most recent ]
    98ca9            34ac2            f30ab
    Snapshot A       Snapshot B       Snapshot C

    ```

### What is a Branch in Git?
- A **branch** is a **lightweight movable pointer** to a commit.  
- The **default branch** is called `master`.  
- As you commit, `master` **moves forward** to the latest commit automatically, if `HEAD` point at master, will discuss `HEAD` soon.  
- `master` is **not special**, just any other branch, it's just the default branch created by `git init` and people don't bother to change it.
  - Now it goes by the name `main`.

    ```
                                        master
                                        |
                                        | 
                                        V                         
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 - most recent ]
    98ca9            34ac2            f30ab
    Snapshot A       Snapshot B       Snapshot C
    ```

---

### Creating a New Branch

- **New Branch Creation**  
  - Syntax for creating new branch is `git branch <branch-name>`.
  - `git branch testing` creates a new branch named `testing`.  
  - The new branch **points to the same commit** as the current branch.  

- **Branches as Pointers**  
  - A branch in Git is just a **movable pointer** to a commit.  
  - Initially, both `master` and `testing` point to the same commit. Since testing was created when we were in master branch, which was a pointing to a commit.  
  - This is how the current workflow looks like: 
    ```
                                         master, testing
                                           |
                                           | 
                                           V                         
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 - most recent ]
       98ca9            34ac2            f30ab
     Snapshot A       Snapshot B       Snapshot C
    ```
- **Understanding HEAD in Git**  
  - **HEAD** is a **special pointer** that points to the current active branch.  
  - Unlike other VCS (e.g., Subversion, CVS), Git’s HEAD tracks a **branch**, not a specific commit.  
  - `git branch` **creates** a branch but **does not switch** to it.  
    ```
                                         HEAD, still pointing at master
                                           |
                                           | 
                                           V     
                                         master, testing
                                           |
                                           | 
                                           V                         
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 - most recent ]
       98ca9            34ac2            f30ab
     Snapshot A       Snapshot B       Snapshot C
    ```

- **Checking Branch Pointers**  
  - Run `git log --oneline --decorate` to see where branches are pointing.  
  - Example output:  
    ```
    f30ab (HEAD -> master, testing) Add feature #32 - ability to add new formats
    34ac2 Fix bug #1328 - stack overflow under certain conditions
    98ca9 Initial commit
    ```
  - This shows that both `master` and `testing` are at commit `f30ab`.
  - If the `HEAD` were to point at testing, it would look something like this:
    ```
    f30ab (master, HEAD -> testing) Add feature #32 - ability to add new formats
    34ac2 Fix bug #1328 - stack overflow under certain conditions
    98ca9 Initial commit
    ```
### Switching Branches

- **Switching to an Existing Branch**  
  - Syntax to switch branches, `git checkout <branch-name>`
  - Use `git checkout testing` to switch to the `testing` branch.  
  - This moves **HEAD** to point to `testing`.  

- **Significance of HEAD Movement**  
  - HEAD always points to the **current active branch**.  
  - Any new commits will now belong to the **testing** branch.  

- **Making a New Commit**  
  - Modify `test.rb` and commit the changes:  
    ```
    $ vim test.rb
    $ git commit -a -m 'Make a change'
    ```
  - This advances the **testing branch** forward.  
  - However, the **master branch remains at the previous commit**.  

- **Branch Divergence**  
  - `testing` now has an extra commit compared to `master`.  
  - `master` still points to the original commit before switching branches.  

    ```
                                                           HEAD 
                                                            |
                                                            | 
                                                            V     
                                         master           testing
                                           |                |
                                           |                | 
                                           V                V                         
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 ] <--- [ commit4- most recent ]
       98ca9            34ac2            f30ab            87ab2
     Snapshot A       Snapshot B       Snapshot C       Snapshot D
    ```
  - `testing` has moved forward with the new commit.  
  - `master` remains unchanged.

- **Switching back to the Master Branch**:
  - Use the command: `git checkout master`.
  - This moves the `HEAD` pointer back to the `master` branch.
  - **Reverts the working directory** files to the snapshot that `master` points to.
    ```
                                          HEAD 
                                           |
                                           | 
                                           V     
                                         master           testing
                                           |                |
                                           |                | 
                                           V                V                         
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 ] <--- [ commit4- most recent ]
       98ca9            34ac2            f30ab            87ab2
     Snapshot A       Snapshot B       Snapshot C       Snapshot D
    ```
- **Git Log Behavior**:
  - `git log` by default only shows commit history for the currently checked-out branch.
  - To view commit history for a specific branch (e.g., `testing`), use: `git log testing`.
  - To show commit history for all branches, use: `git log --all`.

- **Branch Switching and Working Directory**:
  - Switching branches changes the files in your working directory to match the snapshot of the branch you’re switching to.
  - If you switch to an older branch, your working directory will reflect the state of that branch at its last commit.
  - Git will prevent switching branches if it cannot do so cleanly (e.g., due to uncommitted changes).

- **HEAD Pointer Movement**:
  - The `HEAD` pointer moves to the branch you check out.
  - Checking out a branch essentially "rewinds" your work to the state of that branch, allowing you to diverge in a new direction.

- **Key Notes**:
  - The `testing` branch isn’t lost; it’s just not shown by default in `git log`.
  - Branch switching affects your working directory, so ensure you commit or stash changes before switching branches.

- **Making Changes to `master` and Committing**:
  - Edit a file (e.g., `vim test.rb`).
  - Commit changes with: `git commit -a -m 'Make other changes'`.
  - This creates a divergent history where `master` and `testing` branches have separate changes.

    ```
                                                       HEAD 
                                                        |
                                                        | 
                                                        V     
                                                      master
                                                        |
                                                        |
                                                        V
                                                    [ commit5- most recent ]      
                                                    /
                                                   /
                                                  /       
    [ commit1 ] <--- [ commit2 ] <--- [ commit3 ] \
       98ca9            34ac2            f30ab     \
     Snapshot A       Snapshot B       Snapshot C   \
                                                    [ commit4- most recent ]
                                                       87ab2                
                                                     Snapshot D             
                                                        ^
                                                        |                            
                                                        |      
                                                      testing  
    ```

- **Divergent History**:
  - Branches allow isolated work; you can switch between branches and merge them later.
  - Use `git log --oneline --decorate --graph --all` to visualize the commit history and branch divergence.
  - Example output:
    ```
    * c2b9e (HEAD, master) Make other changes
    | * 87ab2 (testing) Make a change
    |/
    * f30ab Add feature #32 - ability to add new formats to the central interface
    * 34ac2 Fix bug #1328 - stack overflow under certain conditions
    * 98ca9 Initial commit of my project
    ```

- **Branch Creation in Git**:
  - A branch in Git is a lightweight file containing a 40-character SHA-1 checksum of the commit it points to.
  - Creating or destroying branches is fast and efficient (only 41 bytes written to a file).
  - Unlike older VCS tools, Git doesn’t copy project files, making branching instantaneous.

- **Merging and Parent Commits**:
  - Git records parent commits, making it easy to find merge bases for merging branches.
  - Encourages frequent branching and merging due to its simplicity and efficiency.

- **Creating and Switching Branches**:
  - Use `git checkout -b <newbranchname>` to create and switch to a new branch in one command.
  - From Git 2.23 onwards, use `git switch`:
    - Switch to an existing branch: `git switch testing-branch`.
    - Create and switch to a new branch: `git switch -c new-branch` (or `--create`).
    - Return to the previous branch: `git switch -`.

---

## Summary

### Summary of Commands

---