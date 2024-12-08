Complete Git and GitHub Tutorial
https://www.youtube.com/watch?v=apGV9Kg7ics

echo "# Python-DSA" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/rnaveensrinivas/Python-DSA.git
git push -u origin main

Git repository is .git folder. 

sri@envy MINGW64 ~/Desktop
$ mkdir project

sri@envy MINGW64 ~/Desktop
$ cd project

sri@envy MINGW64 ~/Desktop/project
$ git init
Initialized empty Git repository in C:/Users/sri/Desktop/project/.git/

sri@envy MINGW64 ~/Desktop/project (master)
$ ls -al
total 8
drwxr-xr-x 1 sri 197121 0 Dec  7 12:09 ./
drwxr-xr-x 1 sri 197121 0 Dec  7 12:09 ../
drwxr-xr-x 1 sri 197121 0 Dec  7 12:09 .git/

sri@envy MINGW64 ~/Desktop/project (master)
$ ls -al .git
total 11
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 ./
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 ../
-rw-r--r-- 1 sri 197121  23 Dec  7 12:09 HEAD
-rw-r--r-- 1 sri 197121 130 Dec  7 12:09 config
-rw-r--r-- 1 sri 197121  73 Dec  7 12:09 description
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 hooks/
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 info/
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 objects/
drwxr-xr-x 1 sri 197121   0 Dec  7 12:09 refs/

sri@envy MINGW64 ~/Desktop/project (master)
$ touch names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        names.txt

nothing added to commit but untracked files present (use "git add" to track)

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "names.txt file added"
[master (root-commit) 14f64a3] names.txt file added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
nothing to commit, working tree clean

sri@envy MINGW64 ~/Desktop/project (master)
$ vi names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ cat names.txt
Kunal Kushwaha
Rahul Rana
Community Classroom

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   names.txt

no changes added to commit (use "git add" and/or "git commit -a")

sri@envy MINGW64 ~/Desktop/project (master)
$ git add names.txt
warning: in the working copy of 'names.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git restore --staged names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   names.txt

no changes added to commit (use "git add" and/or "git commit -a")

sri@envy MINGW64 ~/Desktop/project (master)
$ git add names.txt
warning: in the working copy of 'names.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "names.txt file modified"
[master a82acb4] names.txt file modified
 1 file changed, 3 insertions(+)

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit a82acb48627cc6c79c58c8fe2fced453f4d4a8c0 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:22:21 2024 +0530

    names.txt file modified

commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added


sri@envy MINGW64 ~/Desktop/project (master)
$ rm names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    names.txt

no changes added to commit (use "git add" and/or "git commit -a")

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    names.txt


sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "names.txt file deleted"
[master e78cee0] names.txt file deleted
 1 file changed, 3 deletions(-)
 delete mode 100644 names.txt


sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit e78cee0fc9dab75ff01d1cf657e57abf38832e22 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:26:23 2024 +0530

    names.txt file deleted

commit a82acb48627cc6c79c58c8fe2fced453f4d4a8c0
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:22:21 2024 +0530

    names.txt file modified

commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added


sri@envy MINGW64 ~/Desktop/project (master)
$ git reset 14f64a318ac434629e22d8a0a093d38d9c1c8f77
Unstaged changes after reset:
D       names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added

# what happened to files that were in the commits that we deleted?
# they are moved to unstaged area. 

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    names.txt

no changes added to commit (use "git add" and/or "git commit -a")


# Now let's talk about stashing

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ touch surnames.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    names.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        surnames.txt


sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    names.txt -> surnames.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ vi surnames.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ cat surnames.txt
Kushwaha

sri@envy MINGW64 ~/Desktop/project (master)
$ touch houses.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .
warning: in the working copy of 'surnames.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    names.txt -> houses.txt
        new file:   surnames.txt

# now we don't want to commit these changes, neither do we want to loose them. 
# hence we can stash them

sri@envy MINGW64 ~/Desktop/project (master)
$ git stash
Saved working directory and index state WIP on master: 14f64a3 names.txt file added

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
nothing to commit, working tree clean

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added

# we have our project base back to how it was
# let's see the content of names.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ cat names.txt

# brining back the changes made. 

sri@envy MINGW64 ~/Desktop/project (master)
$ git stash pop
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   houses.txt
        new file:   surnames.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    names.txt

Dropped refs/stash@{0} (f50fb6bc7f6cb0175e7805743ba841cf3dc5c396)

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   houses.txt
        new file:   surnames.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    names.txt

# for now let's keep the stuff stashed

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git stash
Saved working directory and index state WIP on master: 14f64a3 names.txt file added

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
nothing to commit, working tree clean

# how to clear the stash

sri@envy MINGW64 ~/Desktop/project (master)
$ git stash clear

# now we are going to create a GitHub repo and attach it with this repo.
# first, create a repo in GitHub. 

sri@envy MINGW64 ~/Desktop/project (master)
$ git remote add origin https://github.com/rnaveensrinivas/GitTutorial

# remote - working with remote repos
# add - adding a url
# origin - identifier - name of the url that we going to add. 

sri@envy MINGW64 ~/Desktop/project (master)
$ git remote -v
origin  https://github.com/rnaveensrinivas/GitTutorial (fetch)
origin  https://github.com/rnaveensrinivas/GitTutorial (push)

# remote -v -> shows all the remote url attached to the current project. 
# now url is connected with particular folder now.

sri@envy MINGW64 ~/Desktop/project (master)
$ git push origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 216 bytes | 216.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/rnaveensrinivas/GitTutorial
 * [new branch]      master -> master

# origin - to which url you want to pish
# master - which branch do you want to push to origin

# refresh the GitHub repository - you will see the changes there. 

# NOw let's talk about branches

sri@envy MINGW64 ~/Desktop/project (master)
$ touch hotel.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   hotel.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "hotel.txt file added"
[master c592cff] hotel.txt file added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 hotel.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ touch rollno.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .

sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "rollno.txt file added"
[master 55dec57] rollno.txt file added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 rollno.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ vi rollno.txt

sri@envy MINGW64 ~/Desktop/project (master)
$ cat rollno.txt
342342342

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   rollno.txt

no changes added to commit (use "git add" and/or "git commit -a")

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .
warning: in the working copy of 'rollno.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/project (master)
$ git commit -m "rollno.txt file modified"
[master 667a857] rollno.txt file modified
 1 file changed, 1 insertion(+)

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit 667a8572205a533da3d16e2a35daccf258209feb (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:58:40 2024 +0530

    rollno.txt file modified

commit 55dec57de847e0073ee9d864f2da69691ad6a349
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:54:20 2024 +0530

    rollno.txt file added

commit c592cffe12e1935bd1b584e5e74bcd227e224a03
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:53:41 2024 +0530

    hotel.txt file added

commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77 (origin/master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added

# in the first commit we have HEAD -> master - shows head in currently at master branch
# and coincidently that is also the first commit. 
# in the last commit we have (origin/master) shows which commit is the master branch is on.

sri@envy MINGW64 ~/Desktop/project (master)
$ ls .git/
COMMIT_EDITMSG  HEAD  ORIG_HEAD  config  description  hooks/  index  info/  logs/  objects/  refs/

# HEAD refers to current branch in use.

sri@envy MINGW64 ~/Desktop/project (master)
$ git push origin master
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 6 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 641 bytes | 320.00 KiB/s, done.
Total 7 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/rnaveensrinivas/GitTutorial
   14f64a3..667a857  master -> master


# now check GitHub - you will have all the commits in there as well.
# similarly, 

$ git log
commit 667a8572205a533da3d16e2a35daccf258209feb (HEAD -> master, origin/master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:58:40 2024 +0530

    rollno.txt file modified

commit 55dec57de847e0073ee9d864f2da69691ad6a349
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:54:20 2024 +0530

    rollno.txt file added

commit c592cffe12e1935bd1b584e5e74bcd227e224a03
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:53:41 2024 +0530

    hotel.txt file added

commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added

# now let's start working with existing projects on GitHub.

# Fork - the GitHub project to your own account. now you can do anything you want with this folde. 

# then clone to your working directory using git clone,

# Goto commclassroom/commclassroomOP
# Fork it
# then clone it in your working directory.


sri@envy MINGW64 ~/Desktop
$ git clone https://github.com/rnaveensrinivas/commclassroomOP
Cloning into 'commclassroomOP'...
remote: Enumerating objects: 10, done.
remote: Total 10 (delta 0), reused 0 (delta 0), pack-reused 10 (from 1)
Receiving objects: 100% (10/10), done.

sri@envy MINGW64 ~/Desktop
$ cd commclassroomOP/

# from where we have forked the repo
# that url is called upstream url !
# here, commclassroom/commclassroomOP

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git remote add upstream https://github.com/commclassroom/commclassroomOP

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ ls
README.md  names.txt

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ vi README.md

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ cat README.md
# Community Classrom OP

- Kunal Kushwaha says that this community is amazing.
- Naveen says that this community is amazing.

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

# !!! NEVER COMMIT ON MAIN BRANCH
# always create a new branch and work on it. 

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git branch kunal

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git checkout kunal
Switched to branch 'kunal'
M       README.md

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$

# Now look at the branch name - changed from (main) to (kunal)

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git add .

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git commit -m "Kunal and Naveen added a message"
[kunal 404aa48] Kunal and Naveen added a message
 1 file changed, 3 insertions(+), 2 deletions(-)

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git log
commit 404aa488cce5a775b987b1642be84fcbd361e8ad (HEAD -> kunal)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 13:32:34 2024 +0530

    Kunal and Naveen added a message

commit c3164c5542fc3e77e5861eff83938032d5b35f3a (origin/main, origin/HEAD, main)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message


# Now let's try to push this to the main branch of commclassroomop
# we want to push these changes present in the current branch to main branch

when we push and if the owner accepts it, we will have something like below,
<owner> merged <#> commits into <project_repo>:main from <user>:<user's branch>

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git branch
* kunal
  main

# what happens when we try to push upstream?
sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git push upstream kunal
remote: Permission to commclassroom/commclassroomOP.git denied to rnaveensrinivas.
fatal: unable to access 'https://github.com/commclassroom/commclassroomOP/': The requested URL returned error: 403

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git remote -v
origin  https://github.com/rnaveensrinivas/commclassroomOP (fetch)
origin  https://github.com/rnaveensrinivas/commclassroomOP (push)
upstream        https://github.com/commclassroom/commclassroomOP (fetch)
upstream        https://github.com/commclassroom/commclassroomOP (push)

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git push origin kunal
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 367 bytes | 183.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote:
remote: Create a pull request for 'kunal' on GitHub by visiting:
remote:      https://github.com/rnaveensrinivas/commclassroomOP/pull/new/kunal
remote:
To https://github.com/rnaveensrinivas/commclassroomOP
 * [new branch]      kunal -> kunal

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git log
commit 404aa488cce5a775b987b1642be84fcbd361e8ad (HEAD -> kunal, origin/kunal)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 13:32:34 2024 +0530

    Kunal and Naveen added a message

commit c3164c5542fc3e77e5861eff83938032d5b35f3a (origin/main, origin/HEAD, main)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message

# Now goto to your forked repo
# then goto branches and select the one you pushed
# then click on contribute
# then click "create pull request"
# then add title and description
# you are done

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ ls
README.md  names.txt

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ cat names.txt

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ vi names.txt

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ cat names.txt
Naveen

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git add .
warning: in the working copy of 'names.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git commit -m "names.txt file was modified"
[kunal b9aeb73] names.txt file was modified
 1 file changed, 1 insertion(+)

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git push origin kunal
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 293 bytes | 293.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/rnaveensrinivas/comm

# Now this new commit will be added to the existing pull request! 
# why?
# one branch - one pull request
# one feature - one branch - one pull request
# all commits - old and new - made on one branch, stays there itself. 


# now let's talk about deleting a commit that is already present in the GitHub repo

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git log
commit b9aeb73782482887a2c438731ab9f865a1763df5 (HEAD -> kunal, origin/kunal)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 13:46:44 2024 +0530

    names.txt file was modified

commit 404aa488cce5a775b987b1642be84fcbd361e8ad
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 13:32:34 2024 +0530

    Kunal and Naveen added a message

commit c3164c5542fc3e77e5861eff83938032d5b35f3a (origin/main, origin/HEAD, main)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message

commit 69bff533282f8cc1137708e5cb438b4317b7b005
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 08:49:38 2023 +0530

    Initial commit

# say we want to remove the first commit, b9aeb73782482887a2c438731ab9f865a1763df5

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git reset 404aa488cce5a775b987b1642be84fcbd361e8ad
Unstaged changes after reset:
M       names.txt

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git status
On branch kunal
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   names.txt

no changes added to commit (use "git add" and/or "git commit -a")

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git add .
warning: in the working copy of 'names.txt', LF will be replaced by CRLF the next time Git touches it

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git stash
Saved working directory and index state WIP on kunal: 404aa48 Kunal and Naveen added a message

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git status
On branch kunal
nothing to commit, working tree clean

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git log
commit 404aa488cce5a775b987b1642be84fcbd361e8ad (HEAD -> kunal)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 13:32:34 2024 +0530

    Kunal and Naveen added a message

commit c3164c5542fc3e77e5861eff83938032d5b35f3a (origin/main, origin/HEAD, main)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message

commit 69bff533282f8cc1137708e5cb438b4317b7b005
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 08:49:38 2023 +0530

    Initial commit

# now let's try to push normally

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git push origin kunal
To https://github.com/rnaveensrinivas/commclassroomOP
 ! [rejected]        kunal -> kunal (non-fast-forward)
error: failed to push some refs to 'https://github.com/rnaveensrinivas/commclassroomOP'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

# normal push doesn't work
# hence we will have to force push it.

sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git push origin kunal -f
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/rnaveensrinivas/commclassroomOP
 + b9aeb73...404aa48 kunal -> kunal (forced update)


# now let's say the upstream has made some changes to their base
# now to keep your forked base up to date you will have to "Fetch upstream"


sri@envy MINGW64 ~/Desktop/commclassroomOP (kunal)
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git log
commit c3164c5542fc3e77e5861eff83938032d5b35f3a (HEAD -> main, origin/main, origin/HEAD)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message

commit 69bff533282f8cc1137708e5cb438b4317b7b005
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 08:49:38 2023 +0530

    Initial commit

# let's get up to date
# first fetch all the changes

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git fetch --all --prune
Fetching origin
Fetching upstream
From https://github.com/commclassroom/commclassroomOP
 * [new branch]      main       -> upstream/main

# --all - get all branches
# --prune - get all deleted branches too

# second, reset the main branch of my origin to the main branch of upstream

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git reset --hard upstream/main
HEAD is now at c3164c5 Merge pull request #1 from mranjmi567/imran

sri@envy MINGW64 ~/Desktop/commclassroomOP (main)
$ git log
commit c3164c5542fc3e77e5861eff83938032d5b35f3a (HEAD -> main, upstream/main, origin/main, origin/HEAD)
Merge: 69bff53 53b8351
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 10:31:12 2023 +0530

    Merge pull request #1 from mranjmi567/imran

    imran added a message

commit 53b835125a1c4b50ce911b45c0c0042bad7fb6cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 10:19:02 2023 +0530

    names.txt file added

commit eea40196d4a69b519e6896c0a94781d81a4f20cf
Author: Mohammad Imran <webworksimran@gmail.com>
Date:   Mon Dec 25 09:41:41 2023 +0530

    imran added a message

commit 69bff533282f8cc1137708e5cb438b4317b7b005
Author: mranjmi567 <119578935+mranjmi567@users.noreply.github.com>
Date:   Mon Dec 25 08:49:38 2023 +0530

    Initial commit

# now the main branch of our current system is exactly the same as that 

# Let's talk about commit squashing
# making lot's of commit into one commit. 
# note! whenever you are creating a new branch, we are going to create it from the HEAD.


sri@envy MINGW64 ~/Desktop/project (master)
$ touch 1

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .; git commit -m "1"
[master c1d362c] 1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 1

sri@envy MINGW64 ~/Desktop/project (master)
$ touch 2

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .; git commit -m "2"
[master 08cc5f2] 2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 2

sri@envy MINGW64 ~/Desktop/project (master)
$ touch 3

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .; git commit -m "3"
[master fcf2a73] 3
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 3

sri@envy MINGW64 ~/Desktop/project (master)
$ touch 4

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .; git commit -m "4"
[master 404b609] 4
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 4

# now we want to merge 1,2,3,4 into one commit

# method 1
# reset to the commit before 1
# all the changes will be unstaged
# commit once again.

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit 404b6092d841fc92abfd52b68b18d8df5ccf86df (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:17:12 2024 +0530

    4

commit fcf2a73e6adf4af816b34bcad40a53d346c55ce5
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:17:05 2024 +0530

    3

commit 08cc5f20001973b96d00e97849a5c24ca107a0cb
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:16:58 2024 +0530

    2

commit c1d362c1dcb3e36dd464e79a9414829095cb83da
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:16:51 2024 +0530

    1

commit 667a8572205a533da3d16e2a35daccf258209feb (origin/master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:58:40 2024 +0530

    rollno.txt file modified

commit 55dec57de847e0073ee9d864f2da69691ad6a349

sri@envy MINGW64 ~/Desktop/project (master)
$ git reset 667a8572205a533da3d16e2a35daccf258209feb

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1
        2
        3
        4

nothing added to commit but untracked files present (use "git add" to track)

sri@envy MINGW64 ~/Desktop/project (master)
$ git add .; git commit -m "squash alternate"
[master eec8d7d] squash alternate
 4 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 1
 create mode 100644 2
 create mode 100644 3
 create mode 100644 4

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit eec8d7dbbbdd6b31e76914a25a724936a797f740 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:19:23 2024 +0530

    squash alternate

commit 667a8572205a533da3d16e2a35daccf258209feb (origin/master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:58:40 2024 +0530

    rollno.txt file modified

commit 55dec57de847e0073ee9d864f2da69691ad6a349
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:54:20 2024 +0530

    rollno.txt file added

commit c592cffe12e1935bd1b584e5e74bcd227e224a03
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:53:41 2024 +0530

    hotel.txt file added

commit 14f64a318ac434629e22d8a0a093d38d9c1c8f77
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 12:15:16 2024 +0530

    names.txt file added

# let's look at squash
sri@envy MINGW64 ~/Desktop/project (master)
$ touch 5; git add .; git commit -m "5"
[master c810304] 5
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 5

sri@envy MINGW64 ~/Desktop/project (master)
$ touch 6; git add .; git commit -m "6"
[master 611bd7d] 6
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 6

sri@envy MINGW64 ~/Desktop/project (master)
$ touch 7; git add .; git commit -m "7"
[master 802133a] 7
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 7

sri@envy MINGW64 ~/Desktop/project (master)
$ git log
commit 802133abe55ac1103da2cc827bec5b84be8b7462 (HEAD -> master)
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:22:24 2024 +0530

    7

commit 611bd7d1e14a52cf7b3dfd59f31f37302c097b6c
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:22:17 2024 +0530

    6

commit c810304002a1eccde69831a91f0b665c48975280
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:22:11 2024 +0530

    5

commit eec8d7dbbbdd6b31e76914a25a724936a797f740
Author: rnaveensrinivas <rnaveensrinivas@gmail.com>
Date:   Sat Dec 7 14:19:23 2024 +0530

    squash alternate


sri@envy MINGW64 ~/Desktop/project (master)
$ git rebase -i eec8d7dbbbdd6b31e76914a25a724936a797f740
hint: Waiting for your editor to close the file...

# now goto the editor; 

pick c810304 5
pick 611bd7d 6
pick 802133a 7

# Rebase eec8d7d..802133a onto eec8d7d (3 commands)
#
# Commands:
# p, pick <commit> = use commit ...
... 

# Now all you have to do for squash is
# change from "pick" to "s" for 6 and 7, they will be squashed.
# say you have 5, 6, 7, 8; 
# you can squash 6, 7 and to 5 too.
# we have that much flexibility.

# when reseting if you use hard all the changes until then will not be staged!
# in soft the changes are saved. 

sri@envy MINGW64 ~/Desktop/project (master|REBASE 3/3)
$ git reset --hard eec8d7dbbbdd6b31e76914a25a724936a797f740
HEAD is now at eec8d7d squash alternate

sri@envy MINGW64 ~/Desktop/project (master)
$ git status
nothing to commit, working tree clean

# merge conflicts
have to handle them manually.