### Table of Content
- [Git Branching](#git-branching)
  - [Git Branches in a Nutshell](#git-branches-in-a-nutshell)
    - [How Git Stores Data](#how-git-stores-data)
    - [Git Objects After First Commit](#git-objects-after-first-commit)
    - [Subsequent Commits](#subsequent-commits)
    - [What is a Branch in Git?](#what-is-a-branch-in-git)
    - [Creating a New Branch](#creating-a-new-branch)
    - [Switching Branches](#switching-branches)
  - [Basic Branching and Merging](#basic-branching-and-merging)
    - [Basic Branching](#basic-branching)
    - [Basic Merging](#basic-merging)
    - [Basic Merge Conflict](#basic-merge-conflict)
  - [Branch Management](#branch-management)
    - [Listing Branches](#listing-branches)
    - [Deleting Branches](#deleting-branches)
    - [Changing Branch Name](#changing-branch-name)
    - [Changing `master` Branch Name](#changing-master-branch-name)
  - [Key Commands Summary\*\*](#key-commands-summary)
  - [Branching Workflows](#branching-workflows)
    - [Long-Running Branches](#long-running-branches)
    - [Topic Branches](#topic-branches)
  - [Summary](#summary)
    - [Summary of Commands](#summary-of-commands)

---

# Git Branching

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

## Basic Branching and Merging

Let's try to understand branching and merging with the below example process: 

- **Initial Work**  
  - Work on a website.  
  - Create a new branch for a user story.  
  - Do some work in that branch.  

- **Handling a Critical Hotfix**  
  - Switch to the production branch.  
  - Create a branch for the hotfix.  
  - Test and merge the hotfix branch.  
  - Push the fix to production.  

- **Resuming Work**  
  - Switch back to the user story branch.  
  - Continue working.  

### Basic Branching

- **Starting Point**  
  - You have an existing project with commits on the `master` branch.  
    ```plaintext
                             HEAD              
                              |              
                              V              
                            Master
                              |              
                              |
                              V
    Commit0 <-- Commit1 <-- Commit2
    ```

- **Creating a New Branch**  
  - You decide to work on issue #53.  
  - Create and switch to a new branch using:  
    ```sh
    git checkout -b iss53
    ```
  - This is shorthand for:  
    ```sh
    git branch iss53  
    git checkout iss53  
    ```  
    ```plaintext
                                     HEAD              
                                      |              
                                      V              
                            Master, iss53
                              |              
                              |
                              V
    Commit0 <-- Commit1 <-- Commit2
    ```
- **Making Changes in the New Branch**  
  - Edit files (e.g., `vim index.html`).  
  - Commit changes:  
    ```sh
    git commit -a -m 'Create new footer [issue 53]'
    ```
  - The `iss53` branch moves forward as commits are added.  
    ```plaintext
                                          HEAD              
                                           |              
                                           V              
                             Master      iss53
                               |           |   
                               |           |
                               V           V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit3
    ```

- **Handling an Urgent Issue**  
  - You receive a call about a critical issue that needs fixing.  
  - You don’t need to deploy unfinished `iss53` changes.  
  - Instead of reverting, you simply switch back to the `master` branch.  

- **Ensuring a Clean Working State**  
  - Git won’t allow switching branches if you have uncommitted conflicting changes.  
  - Best practice: commit (amending) or stash changes before switching branches.  

- **Switching Back to `master`**  
  ```sh
  git checkout master
  ```
  - Your working directory now reflects the last committed state of `master`.  
  - This allows you to focus on the hotfix without affecting `iss53`.  
    ```plaintext
                              HEAD              
                               |              
                               V              
                             Master      iss53
                               |           |   
                               |           |
                               V           V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit3
    ```
- **Key Concept**  
  - When switching branches, Git automatically updates your working directory to match the last commit on that branch.  
  
- **Creating a Hotfix Branch**  
  - Switch to a new branch for the hotfix:  
    ```sh
    git checkout -b hotfix
    ```
    ```plaintext
                                  HEAD              
                                   |              
                                   V              
                         Master,hotfix   iss53
                               |           |   
                               |           |
                               V           V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit3
    ```
  - The `hotfix` branch is based on `master`.  
  - Make necessary changes (e.g., edit `index.html`).  
  - Commit the fix:  
    ```sh
    git commit -a -m 'Fix broken email address'
    ```
    ```plaintext
                                      HEAD              
                                       |              
                                       V              
                                    hotfix   
                                       |
                                       |
                             Master    V
                               |     Commit4        
                               |    /    
                               V   /       
    Commit0 <-- Commit1 <-- Commit2  
                                   \
                                    \
                                     Commit3
                                        ^
                                        |
                                        |
                                      iss53
    ```

- **Testing and Merging the Hotfix**  
  - Run tests to ensure the fix is correct.  
  - Merge the hotfix into `master`:  
    ```sh
    git checkout master
    git merge hotfix
    Updating f42c576..3a0874c
    Fast-forward
     index.html | 2 ++
     1 file changed, 2 insertions(+)
    ```
  - Git performs a **fast-forward merge** since `hotfix` is directly ahead of `master`, there is no divergent branch with commits. 
  - No conflicts occur, and `master` simply moves forward to include the hotfix.  

- **Deployment**  
  - The `master` branch now includes the hotfix.  
  - It is ready to be deployed to production.  

    ```plaintext
                                          HEAD              
                                           |              
                                           V              
                                        Master, hotfix   
                                           |
                                           |
                                           V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit4
                                   \
                                    \
                                     Commit3
                                        ^
                                        |
                                        |
                                      iss53
    ```

- **Deleting the Hotfix Branch**  
  - Since the `hotfix` branch is now merged into `master`, it can be deleted:  
    ```sh
    git branch -d hotfix
    ```
  - This removes the branch reference, but the changes remain in `master`.  

- **Switching Back to the User Story (`iss53`)**  
  - Resume work on issue #53:  
    ```sh
    git checkout iss53
    ```
  - Continue editing files (e.g., `vim index.html`).  
  - Commit changes:  
    ```sh
    git commit -a -m 'Finish the new footer [issue 53]'
    ```
    ```plaintext
                                        Master   
                                           |
                                           |
                                           V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit4
                                   \
                                    \
                                     Commit3 <-- Commit5
                                                    ^
                                                    |
                                                    |
                                                  iss53
                                                    ^
                                                    |
                                                    |
                                                   HEAD
    ```
  
- **Hotfix Changes Are Not in `iss53`**  
  - The `iss53` branch does **not** automatically contain the hotfix changes.  
  - Options to integrate the hotfix:  
    1. Merge `master` into `iss53`:  
       ```sh
       git merge master
       ```
    2. Wait until `iss53` is merged back into `master`.  
---

### Basic Merging

- **Merging `iss53` into `master`**  
  - Once work on issue #53 is complete, merge it into `master`:  
  - All you have to do is check out the branch you wish to merge into and then run the git merge command
    ```plaintext
                                        Master   
                            (Common        |
                            Ancestor)      V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit4 (Snaphot to merge into)
                                   \
                                    \
                                     Commit3 <-- Commit5 (Snapshot to merge in)
                                                    ^
                                                    |
                                                    |
                                                  iss53
                                                    ^
                                                    |
                                                    |
                                                   HEAD
    ```
    ```sh
    git checkout master  
    git merge iss53  
    ```  
  - Git performs a **three-way merge** since `iss53` and `master` have diverged.  
  - A **merge commit** is created, combining changes from both branches.  
    ```plaintext
                                                             HEAD              
                                                               |              
                                                               V  
                                                            Master   
                                                               |
                                                               V
    Commit0 <-- Commit1 <-- Commit2 <-- Commit4 <---------- Commit6 (merge commit)
                                   \                     /
                                    \                   / 
                                     Commit3 <-- Commit5 
                                                    ^
                                                    |
                                                    |
                                                  iss53
    ```

- **Understanding Three-Way Merge**  
  - Git compares:  
    1. **`master` branch tip** (latest commit on `master`).  
    2. **`iss53` branch tip** (latest commit on `iss53`).  
    3. **Common ancestor commit** (last shared commit between both branches).  
  - Using these snapshots, Git creates a **new merge commit** that includes changes from both branches.  

- **Deleting the `iss53` Branch**  
  - After merging, the `iss53` branch is no longer needed:  
    ```sh
    git branch -d iss53
    ```  
  - This removes the reference to `iss53`, but all changes remain in `master`.  

- **Final Steps**  
  - The feature is now fully merged.  
  - The issue can be marked as resolved in the issue-tracking system.  

---

### Basic Merge Conflict

- **1. Understanding Merge Conflicts**  
  - Merge conflicts occur when the same part of a file is modified differently in two branches.  
  - Example: If changes made in `iss53` overlap with changes in `master`, Git cannot automatically merge them.  
  - The error message:  
    ```sh
    $ git merge iss53
    Auto-merging index.html
    CONFLICT (content): Merge conflict in index.html
    Automatic merge failed; fix conflicts and then commit the result.
    ```
  - Git stops the merge process and requires manual resolution.  

- **2. Checking Unmerged Files**  
  - To list files with unresolved conflicts, use:  
    ```sh
    $ git status
    ```
    - Output:
      ```
      On branch master
      You have unmerged paths.
        (fix conflicts and run "git commit")
      
      Unmerged paths:
        (use "git add <file>..." to mark resolution)
      
          both modified:      index.html
      ```
  - Conflicted files are labeled as **"both modified."**  

- **3. Understanding Conflict Markers in Files**  
  - Git adds special markers in conflicted files, open the conflicting files:  
    ```html
    <<<<<<< HEAD:index.html
    <div id="footer">contact : email.support@github.com</div>
    =======
    <div id="footer">
     please contact us at support@github.com
    </div>
    >>>>>>> iss53:index.html
    ```
    - **HEAD section**: Code from the current branch (`master`).  
    - **Bottom section**: Code from the merging branch (`iss53`).  
  - **Options to resolve conflicts:**  
    1. Keep one version and remove the other.  
    2. Manually combine both changes.  
    3. Rewrite the section to maintain clarity.  

  - Example resolution:  
    ```html
    <div id="footer">
    please contact us at email.support@github.com
    </div>
    ```
    - Conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) must be **completely removed**.  

- **4. Marking the Conflict as Resolved**  
  - Once changes are manually fixed, mark the file as resolved:  
    ```sh
    git add index.html
    ```
  - Verify resolution using:  
    ```sh
    git status
    ```
    - Expected output:  
      ```
      On branch master
      All conflicts fixed but you are still merging.
        (use "git commit" to conclude merge)
      
      Changes to be committed:
          modified:   index.html
      ```

- **5. Using a Merge Tool (Optional)**  
  - Instead of manually editing, Git provides visual tools:  
    ```sh
    $ git mergetool
    ```
  - If a tool isn't configured, Git suggests available options like:  
    ```
    opendiff, kdiff3, meld, vimdiff, diffuse, etc.
    ```
  - After resolving conflicts in the tool, Git prompts:  
    ```
    Was the merge successful? (yes/no)
    ```
  - If "yes", Git automatically stages the resolved file.  

- **6. Finalizing the Merge**  
  - Once conflicts are resolved and files are staged, commit the merge:  
    ```sh
    git commit
    ```
  - Default merge commit message:  
    ```
    Merge branch 'iss53'
    
    Conflicts:
        index.html
    ```
  - Modify the commit message if necessary, explaining **how** and **why** conflicts were resolved.  

- **7. Summary of Key Commands for Handling Merge Conflicts**  
  | Task | Command |
  |------|---------|
  | Check unmerged files | `git status` |
  | View conflict markers in a file | Open the file in an editor |
  | Resolve conflicts manually | Edit the file, remove conflict markers |
  | Mark conflicts as resolved | `git add <file>` |
  | Use a merge tool (optional) | `git mergetool` and type `yes` for prompt |
  | Commit the merge | `git commit` |

---

## Branch Management

### Listing Branches

- **Listing All Branches**  
  - To see all branches in the repository:  
    ```sh
    $ git branch
    ```
    - Example output:  
      ```
        iss53
      * master
        testing
      ```
    - The `*` indicates the currently checked-out branch.  
    - Any new commits will be added to this active branch.  

- **Viewing the Last Commit on Each Branch**  
  - Use `-v` to display the latest commit message for each branch:  
    ```sh
    $ git branch -v
    ```
    - Example output:  
      ```
        iss53   93b412c Fix javascript issue
      * master  7a98805 Merge branch 'iss53'
        testing 782fd34 Add scott to the author list in the readme
      ```
    - Each branch is followed by:  
      - The latest commit hash.  
      - The commit message.  

- **Checking Merged and Unmerged Branches**  
  - **Find branches that have already been merged** into the current branch:  
    ```sh
    $ git branch --merged
    ```
    - Example output:  
      ```
        iss53
      * master
      ```
    - These branches are safe to delete because their work has already been incorporated into another branch.  

  - **Find branches that have not yet been merged** into the current branch:  
    ```sh
    $ git branch --no-merged
    ```
    - Example output:  
      ```
        testing
      ```
    - Be cautious before deleting these, as they contain changes that haven't been merged yet.  

### Deleting Branches

- **Deleting a Branch**  
  - **Delete a fully merged branch:**  
    ```sh
    $ git branch -d iss53
    ```
    - This safely deletes the branch if it has been merged.  

  - **Attempting to Delete an Unmerged Branch**  
    - If you try to delete an unmerged branch using `-d`, Git will **prevent** deletion:  
      ```sh
      $ git branch -d testing
      ```
      - Example error message:  
        ```
        error: The branch 'testing' is not fully merged.
        If you are sure you want to delete it, run 'git branch -D testing'.
        ```
      - Git warns you that deleting `testing` would result in **data loss**.  

  - **Force delete a branch (even if unmerged):**  
    ```sh
    $ git branch -D testing
    ```
    - This permanently removes the branch **without checking** if it’s merged.  
    - Use cautiously to avoid losing work.  

- **Checking Unmerged Work Relative to Another Branch**  
  - By default, `--no-merged` checks against the **current branch**.  
  - You can specify another branch without checking it out:  
    ```sh
    $ git checkout testing
    $ git branch --no-merged master
    ```
    - Example output:  
      ```
        topicA
        featureB
      ```
    - This shows `topicA` and `featureB` **have changes not merged into master**.  

### Changing Branch Name

- **⚠️ Caution**  
  - **Do not rename active branches** used by collaborators without prior coordination.  
  - Avoid renaming `master/main/mainline` without understanding potential consequences.  


- **Rename a Local Branch**  
- To rename a local branch **while keeping all history**, use:  
  ```sh
  $ git branch --move bad-branch-name corrected-branch-name
  ```
  - This renames `bad-branch-name` to `corrected-branch-name` **only locally**.  


- **Push the Renamed Branch to Remote**  
  - After renaming locally, push the corrected name to the remote repository:  
  ```sh
  $ git push --set-upstream origin corrected-branch-name
  ```
  - This creates `corrected-branch-name` on the remote and links it to your local branch.  

- **Check the Updated Branches**  
  - Verify that the new branch exists using:  
  ```sh
  $ git branch --all
  ```
  Example output:  
  ```
  * corrected-branch-name  
    main  
    remotes/origin/bad-branch-name  
    remotes/origin/corrected-branch-name  
    remotes/origin/main  
  ```
  - The **new branch is now tracked remotely**.  
  - The **old branch (`bad-branch-name`) still exists on the remote**.  

- **4. Delete the Old Branch from Remote**  
  - Now, remove the incorrectly named branch from the remote repository:  
  ```sh
  $ git push origin --delete bad-branch-name
  ```
  - This **completely removes** `bad-branch-name` from the remote.  


- **Final State**  
  - Running `git branch --all` now shows only:  
  ```
  * corrected-branch-name  
    main  
    remotes/origin/corrected-branch-name  
    remotes/origin/main  
  ```

---

### Changing `master` Branch Name

-  **⚠️ Warning**  
   - Renaming a core branch like `master`, `main`, `mainline`, or `default` **can break**:  
     - **Integrations** (e.g., CI/CD pipelines, GitHub Actions)  
     - **Services and helper utilities** (e.g., webhooks, APIs)  
     - **Build and release scripts**  
     - **References in code and documentation**  

   - **Before renaming:**  
     - **Discuss with collaborators** and ensure all team members are aware.  
     - **Search the repository** for hardcoded references to `master`.  
     - **Update dependent projects, build scripts, and CI/CD configurations.**  

---

- **1. Rename the Local `master` Branch to `main`**  
  - Run the following command to rename `master` to `main` **locally**:  
    ```sh
    $ git branch --move master main
    ```
  - This **removes the local `master` branch** and **replaces it with `main`**.  
  - No changes have been pushed yet; this is only a local update.  

---

- **2. Push the Renamed `main` Branch to Remote**  
  - After renaming locally, push the `main` branch to the remote repository:  
  ```sh
  $ git push --set-upstream origin main
  ```
  - This makes `main` available on the remote.  
  - However, the remote **still contains `master`** at this point.  

---

- **3. Verify the Updated Branch List**  
  - To check the branches on local and remote, run:  
    ```sh
    $ git branch --all
    ```
  Example output:  
    ```
    * main  
      remotes/origin/HEAD -> origin/master  
      remotes/origin/main  
      remotes/origin/master  
  ```
  - ✅ **`main` is now the active branch** (denoted by `*`).  
  - ❗ **`master` still exists remotely**, meaning others might still be using it.  

---

- **4. Update Repository Configuration and Dependencies**  
  - Before deleting `master`, **ensure all dependencies and configurations are updated**:  
    - **✅ Update GitHub/GitLab/Bitbucket Settings**  
      - Change the **default branch** from `master` to `main` in repository settings.  
      - Adjust merge rules, protected branch settings, and CI/CD triggers.  

    - **✅ Modify Local and Remote Code References**  
      - Update all scripts, services, and configurations referring to `master`:  
        ```sh
        git grep -l 'master' | xargs sed -i 's/master/main/g'
        ```
      - If using CI/CD (e.g., GitHub Actions, Jenkins, Travis, GitLab CI):  
        - Update `.github/workflows/*.yml`, `.gitlab-ci.yml`, etc.  
        - Modify `Jenkinsfile`, `travis.yml`, or any build scripts.  
        - Update webhooks and API references.  

    - **✅ Adjust Dependent Projects and Repositories**  
      - Any repositories that reference `master` as a dependency must be updated.  
      - Update `submodules`, `package.json`, `Makefile`, etc.  

    - **✅ Fix Branch References in Documentation**  
      - Update `README.md`, `CONTRIBUTING.md`, and Wiki pages.  
      - Change links and examples pointing to `master`.  

    - **✅ Close/Merge Pull Requests Targeting `master`**  
      - Check for any open PRs still pointing to `master`.  
      - Either **retarget them to `main`** or **merge them** before deletion.  

---

- **5. Delete the Old `master` Branch from Remote**  
  - Once all updates are complete, remove `master` from the remote:  
    ```sh
    $ git push origin --delete master
    ```
  - This **completely removes `master` from the remote repository**.  
  - Any collaborators who haven't switched to `main` will need to do so manually:  
    ```sh
    git checkout master
    git branch --move master main
    git fetch origin
    git branch --set-upstream-to=origin/main main
    ```

---

- **Final State**  
  - Running `git branch --all` now shows only:  
    ```
    * main  
      remotes/origin/HEAD -> origin/main  
      remotes/origin/main  
    ```
  - ✅ **Migration to `main` is now complete!** 🚀  

---

- **Key Commands Summary**  

| **Command** | **Description** |
|------------|---------------|
| `git branch --move master main` | Rename `master` to `main` locally |
| `git push --set-upstream origin main` | Push the new `main` branch to remote |
| `git branch --all` | List all local and remote branches |
| `git grep -l 'master' \| xargs sed -i 's/master/main/g'` | Find and replace `master` with `main` in files |
| `git push origin --delete master` | Delete the `master` branch from remote |
| `git checkout master && git branch --move master main` | Rename `master` for other collaborators |
| `git branch --set-upstream-to=origin/main main` | Set tracking for the `main` branch |

---

## Branching Workflows

- You now understand the basics of branching and merging.  
- Next, explore what you can do with them.  
- This section covers common workflows enabled by lightweight branching.  
- You can decide whether to incorporate these workflows into your development cycle.

### Long-Running Branches

- **Merging Over Time is Easy in Git**  
  - Git uses a **simple three-way merge**.  
  - Merging from one branch into another **multiple times** over a long period is straightforward.  
  - Enables maintaining several **always-open branches** for different development stages.  
  - Regular merges can be performed between these branches.  

- **Common Git Workflow for Stability**  
  - Many developers follow a structured approach using **multiple long-running branches**.  
  - **Master branch** contains only **entirely stable code** (typically released or ready for release).  
  - A **develop or next branch** exists for testing new features before merging into master.  
    - Not always stable.  
    - Pulls in **topic branches** (short-lived branches, e.g., bug fixes or features).  
    - Ensures tests pass and no bugs are introduced before merging into master.  

- **Progressive-Stability Branching Model**  
  - Conceptually, branches move **up the commit history** based on stability.  
  - **Stable branches** are further down the commit history.  
  - **Bleeding-edge branches** are further up in the history.  
  - Two common visual representations:  
    - **Linear view:** Commits progress from unstable to stable branches.  
      ```plaintext

      Master (most stable)             Develop               Topic (least stable)                 
        V                                V                     V
      Commit1 <- Commit2 <- Commit3 <- Commit4 <- Commit5 <- Commit6
      ```
    - **Silo view:** Commits **graduate** to more stable silos when fully tested.  
      ```plaintext

      Master ==>  Commit1 
                         \
                          \ 
      Develop ==>          Commit2 <- Commit3 <- Commit4 
                                                        \
                                                         \
      Topic ==>                                           Commit5 <- Commit6
      ```

- **Additional Levels of Stability**  
  - Some larger projects introduce a **proposed (pu) branch**:  
    - Contains experimental or integrated branches **not yet ready** for master or next.  
    - Acts as an intermediate level before merging into more stable branches.  
  - This structure is **optional** but helps in **large or complex projects**.  

### Topic Branches

- **Definition & Purpose**  
  - **Short-lived branches** created for a **single feature or related work**.  
  - Useful in **projects of any size**.  
  - Unlike traditional VCS, Git makes branching **lightweight and efficient**.  
  - Creating, working on, merging, and deleting branches multiple times a day is **common**.  

- **Example of Topic Branch Usage**  
  - Seen previously with **iss53** and **hotfix** branches.  
  - Worked on them briefly, merged, and then deleted them.  
  - Helps in **context-switching quickly** and **isolating work** into silos.  
  - Changes can be kept for **minutes, days, or months** and merged when ready.  

- **Multiple Topic Branch Workflow**  
  - Example workflow:  
    1. Start working on **master**.  
    2. Branch off for an issue (**iss91**).  
    3. Create another branch (**iss91v2**) to try a different approach.  
    4. Return to **master** and continue working.  
    5. Branch off again for an experimental idea (**dumbidea**).  
  - This results in multiple topic branches in the commit history.  
    ```plaintext
    dumbidea                                  
      |                                      
      C13            iss91v2                        
      |                |                     
      V               C11                     
      C12        iss91  |                        
        \         |    V                      
          \       C6   C8                        
          \       |    |                      
            \      V    V                       
            C10  C5   C7                      
              |    |  /                     
              V    V /                       
              C9  C4                        
              |    |
              V    V
              C3  C2
              |  /
              V / 
              C1
              |
              V
              C0
    ```

- **Selecting & Merging the Best Branches**  
  - Suppose the **iss91v2** branch turns out better than **iss91**.  
  - The **dumbidea** branch, initially uncertain, turns out to be a great solution.  
  - The original **iss91** branch can be **discarded** (losing commits C5 and C6).  
  - The **dumbidea** and **iss91v2** branches are merged into the main history.  
    ```plaintext
            master (merge commit)                             
            C14                
              |  \                      
    dumbidea C13  C11 iss91v2                       
              |    |                      
              V    V                        
             C12  C8                      
              |    |      
              V    V    C5 <- C6 - iss91 (discarded)                    
             C10  C7   /                    
              |    |  /                    
              V    V /                        
              C9  C4                        
              |    |
              V    V
              C3  C2
              |  /
              V / 
              C1
              |
              V
              C0
    ```

- **Local Nature of Git Branches**  
  - All branching and merging happens **locally** within your Git repository.  
  - There is **no communication with a remote server** during these operations.  

- **Further Reading**  
  - More details on branching schemes will be covered in **Distributed Git**.  
  - Read that chapter before finalizing a branching strategy for your project.  

---

## Summary

### Summary of Commands

---