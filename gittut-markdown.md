# Git Tutorial

## Configuration Git

system: all users.
global: all repositories of the current user.
local: the current repository.

config username and email address of our GitHub account:

`git config --global user.name "USER NAME"`

`git config --global user.email "EMAIL ADDRESS"`

use VSCode as the default editor:

`git config --global core.editor "code --wait"`

open default editor to see all configurations:

`git config --global -e`

config end of the line for git input for Linux / true for mac:

`git config --global core.autocrlf input`

full help:

`git config --help`

short summary:

`git config -h`

## Creating Snapshot

initialize a directory for git:

`git init`

add files to the staging area:

`git add <FILES>` multiple or single file.

`git add *.txt` to add all files with the ending of .txt.

`git add .` to add all files in the directory.

then use commit to store these changes:

`git commit -m "COMMIT MESSAGE"`

`git commit` opens the default editor, if we need a long message we use this command. in the editor, we type a short description of the new line then a long description.

git store ID, Message, Date/time, Author, and Complete snapshot in a commit.

see the status of the working directory and staging area:

`git status`

if we are sure that our code doesn't need to be reviewed we can skip the staging area and commit changes with the following command:
`git commit -am "COMMIT MESSAGE"` use `-a` for all tracked modified files so it does not work for untracked files `-m` for the message as before.

remove files from the working directory as well as the staging area:

`git rm <files>`

rename or move files with git:

`git mv file1 file2` rename file1 to file2

create a .gitignore file in the root of the repository to ignore files or directories:

`touch .gitignore`

adding ignore stuff in this file like patterns below:

- log/ --> ignore directory.
- main.log --> ignore file.
- *.log --> ignore patterns.

add .gitignore file to the staging area and do a commit:

`git add .gitignore`

`git commit -m "add gitignore"`

show files in the staging area:

`git ls-files`

if add a file to the staging area then add it to .gitignore git do not ignore it so if we want to ignore it we must remove it from the staging area with the following command:

`git rm --cached -r <files>` -r if we need recursive removal ex. we want to remove a non-empty directory.

[for more .gitignore templates visit this](https://github.com/github/gitignore)

short status:

`git status -s` the left column shows the staging and the right column shows the working directory.

shows unstaged changes:

`git diff`

shows staged changes:

`git diff --staged`

set our editor for diff:

`git config --global diff.tool VSCode`

`git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $ REMOTE"`

check if these lines are added correctly to your .gitconfig file with the `git config --global -e` command.

```.gitconfig
[diff]
 tool = vscode
[difftool "vscode"]
 cmd = "code --wait --diff $LOCAL $REMOTE"
```

lunch our visual diff tools we command bellow:

`git difftool` changes between unstaged changes and our current working directory.

`git difftool --staged` changes between staged changes and our current working directory.

look at our history of commits:

`git log`

`git log --oneline` for short log.

`git log --oneline --reverse` see commit in reverse order.

see what exactly we have changed in a commit:

`git show <ID>` or a few letters of id which makes it unique from other commits.

`git show HEAD~<number-of-steps-to-go-back>` ex. `git show HEAD~3`

shows the version of file.js stored in the third last commit:

`git show HEAD~3:<PATH-TO-file.js>`

if we want to see all files and directories in a specific commit:

`git ls-tree HEAD~3` shows the unique object id for a file or dir so we can see it with git show `<object-id>`

Git objects :

- commits
- Blobs (Files)
- Trees (Directories)
- Tags

upstaging files (undoing git add command):

`git restore --staged file.js` Copies the last version of file.js from the repository to the index.

discarding local changes:

`git restore file.js` Copies file.js from index to working directory.

restores multiple files in the working directory:

`git restore file1.js file2.js`

discards all local changes (except untracked files):

`git restore .`

removes all untracked files:

`git clean -fd` use `git clean -h` for more help.

restoring an earlier version of a file:

`git restore --source=HEAD~2 <PATH-to-file>`

## Browsing History

we will learn:

- search for commit. (by author, date, message, etc.)
- view a commit.
- restore your project to an earlier point.
- compare commits.
- view the history of a file.
- find a bad commit that introduced a bug.

viewing the history to show the list of modified files

`git log --stat`

shows the actual changes (patches):

`git log --patch`

see the last three commits:

`git log -3`

search commits by author:

`git log --author=“Kristen”`

search commits by date:

`git log --before=“2022-10-25”`

`git log --after=“one week ago”`

commits with “GUI” in their message(this command is case sensitive):

`git log --grep=“GUI”`

commits with “GUI” in their patches it means to add "GUI" to our code or removed it:

`git log -S“GUI”`

`git log _S"GUI" --patch`

range of commits:

`git log hash1..hash2`

commits that touched file.txt

`git log file.txt`

**note** if git complained about the file name we separate the file with `--` e.g. `git log --oneline -- toc.txt`

**note** if we want to see actual changes for a touched file we use `-- patch` e.g. `git log --oneline --patch -- toc.txt`

formatting the log output:

`git log --pretty=format:”%Cgreen%an%Creset committed %H”` note that `%an` for the author name and `%Cgreen` to Change color of author name in green and `%Creset` to resort color after green.

placeholders that expand to information extracted the commit:

- %H --> commit hash.
- %h --> abbreviated commit hash.
- %T --> tree hash.
- %t --> abbreviated tree hash.
- %P --> parent hashes.
- %p --> abbreviated parent hashes.

[for more visit this link](https://git-scm.com/docs/pretty-formats)

creating an alias:

`git config --global alias.lg “log --oneline"`

open the editor to check the alias we set:

`git config --global -e`

viewing a commit:

`git show HEAD~2`

shows the version of the file stored in this commit:

`git show HEAD~2:file1.txt`

shows only names of the files that were deleted or modified or added in this commit:

`git show HEAD~2 --name-only`

shows names and status of the files that were deleted or modified or added in this commit:

`git show HEAD~2 --name-status`

comparing commits which shows the changes between two commits:

`git diff HEAD~2 HEAD`

changes to file.txt only:

`git diff HEAD~2 HEAD file.txt`

shows only the name of files that changed between two commits:

`git show HEAD~2 HEAD --name-only`

shows the name and status of files that changed between two commits:

`git show HEAD~2 HEAD --name-status`

to see a complete snapshot of our project we Check out a commit, and it restores our directory to that commit.

**note** that we must not modify or change the file in a commit when we face with "detached HEAD" warning that if we commit on as detached HEAD the git automatically removes it.

checks out the given commit:

`git checkout lhe433a`

checks out the master branch:

`git checkout master`

if we are in a previous commit the fit log just shows the committed massage till that commit but we can see all the commits we follow the trick below:

`git log --oneline --all`

finding bugs or bad commits by dividing commits in half and examining the code in that commit and running git bisect good if it is a good commit or git bisect bad if it is a bad commit and do this to the remaining half and so on till we found the commit that caused the bug.

first start bisect :

`git bisect start`

marks the current commit as a bad commit:

`git bisect bad`

marks the given commit as a good commit:

`git bisect good am48547`

terminates the bisect session (attached the head to the master branch):

`git bisect reset`

finding contributors:

`git shortlog` also we can use `git shortlog -h` to find helpful parameters.

for viewing the history of a file and showing the commits that touched file.txt:

`git log file.txt`

shows statistics (the number of changes) for file.txt:

`git log --stat file.txt`

shows the patches (changes) applied to file.txt:

`git log --patch file.txt`

if we remove a file accidentally and want to restore it so we must look at the logs with:

`git log --online -- deletedfile.txt`

and to restore this file we have to look at the parent of the latest commit and make checkout on that commit and file with:

`git checkout b633f47 deletedfile.txt`

finding the author of each line in file.txt:

`git blame file.txt`

if we want also find out the email of the author of each line in file.txt:

`git blame -e file.txt`

if we want to search based on the lines:

`git blame -L 1,3 file.tx` e.g. first three lines

tagging or bookmark a commit to tag the last commit as v1.0:

`git tag v1.0`

tags an earlier commit:

`git tag v1.0 sfe2857`

we can check out a commit with it tag:

`git checkout v1.0`

we can associate a message `-m` with a tag using annotated `-a` tag:

`git tag -a v1.1 -m "this is version1.1"`

to see the tag messages:

`git tag -n`

lists all the tags:

`git tag`

deletes the given tag:

`git tag -d v1.0`

## Branching & Merging

diverge from the mainline of work and work on something else in isolation.

in this section we'll learn :

- use branches.
- compare branches.
- resolve conflicts.
- undo a faulty merge.
- essential tools. (stashing, cherry-picking.)

creates a new branch called bugfix:

`git branch bugfix`

see list of branches:

`git branches`

switches to the bugfix branch:

`git checkout bugfix`

same as the above:

`git switch bugfix`

rename a branch:

`git branch -m <old-name> <new-name>` better to use bugfix/signup-form so its more specefic.

view commit across all branches:

`git log --oneline --all`

creates and switches:

`git switch -C bugfix`

deletes the bugfix branch:

`git branch -d bugfix`

force to delete a branch:

`git branch -D bugfix`

for comparing branches we need to list the commits in the bugfix branch, not in the master:

`git log master..bugfix`

shows the summary of changes:

`git diff master..bugfix`

shows the summary of changes between the current branch and bugfix:

`git diff bugfix`

see only the name of the files that changed between the current branch and bugfix:

`git diff --name-only bugfix`

`git diff --name-status bugfix`

stashing, if we have local changes in our working directory that we have not committed yet, these changes could get lost in this situations git does not allow us to switch branches so we should stash those changes.

creates a new stash:

`git stash push -m “New tax rules”`

**note** that new untracked files do not include in our stash we can include them by `-all` or in short `-a` tag:

`git stash push -am "stash all files"`

lists all the stashes:

`git stash list`

shows the given stash:

`git stash show stash@{1}`

shortcut for stash@{1}:

`git stash show 1`

applies the given stash to the working directory:

`git stash apply 1`

deletes the given stash:

`git stash drop 1`

deletes all the stashes:

`git stash clear`

merge is all about bringing changes from one branch to another branch.

we have two types of merges:

1. fast-forward(FF)(if branches have not diverged)
2. 3-way(if branches have diverged)

merges the bugfix branch into the current branch we should be on the current branch:

`git merge bugfix`

use the following command for graphing:

`git log --oneline --all --graph`

creates a merge commit even if FF is possible:

`git merge --no-ff bugfix`

disable FF in the current directory:

`git config ff no`

disable FF globally:

`git config --global ff no`

viewing the merged and unmerged branches to show the merged branches(it is safe to delete merged branches):

`git branch --merged`

shows the unmerged branches:

`git branch --no-merged`

conflicts happen when we want to merge branches for example:

1. same lines of code have been changed in different ways in two branches.
2. if a file changes in one branch and deleted in other branches.
3. a file adds in twice in two different branches.

after resolving conflicts, we add a conflict files to the staging area.

some merge tools for resolving conflicts are :

1. Kdiff
2. P4Merge

set p4merge to the default merge tool:

`git config --global merge.tool p4merge`

set path to P4Merge:

`git config --global mergetool.p4merge.path "path-to-P4Merge"`

open merge tool after facing conflict for editing:

`git mergetool`

aborts the merge and back to the state before the merge:

`git merge --abort`

for undoing a faulty merge we have two options 1. delete the current commit which is not recommended cause its rewrites history and makes other ones confuse if we are working on share space but if we are doing this in our local its okay to do that 2. revert a commit which is recommended.

first, look at the first option. (delete the current commit, resetting the HEAD pointer.

reset the head pointer to go one step back:

`git reset --hard HEAD~1`

recover the merge that we undo in the last step:

`git reset --hard <merge-id>`

second, let's look at the revert method:

`git revert HEAD`

but we probably face errors cause we must tell the git where we want to back.

we specify the parent with a number and the first parent is the one on the master branch and also specify the target commit
`git revert -m 1 HEAD`.

**how to perform a squash merge?**

we use this method when we don't care about the history of a branch that we want to merge, so we create a commit that combines all the features in that branch and applies that commit on top of the master after that we need to commit changes and also it is important to remove the branch after we did cause squash is not a merging method and we can see that by running git branch `--merged` so if don't force delete it, it makes confusion in future.

if we end up with a conflict we solve it as before then commit the changes:

`git merge --squash bugfix`

rebasing (it results in a linear history in merging) in other words changes the base of the current branch.

we should be conscious because rebasing rewrites history so we should use rebasing only for branches or commits that are local in our repositories if we have to share these commits with other people on our team, if we have to push our changes we should not use rebasing.

first, we have to switch to our target branch:

`git rebase master`

then we switch to master and do merge:

`git merge <BRANCH-NAME>`

if we end up with a conflict we solve it as before then commit the changes.

after done conflicts we run:

`git rebase --continue`

we can skip a commit and move to the next commit by:

`git rebase --skip`

we can abort rebase if we end up with conflicts and wanna move to the stage before rebasing:

`git rebase --skip`

the P4Merge creates backup files we can remove them by git `-rm` file.orig or:

`git clean -fd`

we can set P4Merge not to save backups by:

`git config --global mergetool.keepBackup false`

cherry-picking applies the given commit on the current branch:

`git cherry-pick gtr57ws` if we end up with conflict we solve it and then commit the changes

if we are interested in a single file, not the whole commit:

`git restore --source=TARGET-BRANCH -- INTERSTED-FILE`

## Collaboration

what we will learn in this section :

- collaboration workflows
- pushing, fetching and pulling
- pull requests, issues, and milestones
- contributing to open-source projects

**types of version control systems:**

**centralized:** in centralized like SubVersion we have a single repository that is shared with all members the problem is that everyone is dependent on this repository. if the server that holds that repo goes offline no one can commit and see the history of the project
distributed: in distributed systems like Git every developer has the repository on their machine and they can work offline on the project instead of collaborating we use a centralized workflow for ease of use. so everyone has their local repository but there is also a centralized repository they use to sync as they work if the centralized repository goes offline for some time still we can sync with each other we can use a privet server or a cloud server for our centralized repository. this workflow is suitable for privet teams.

we have another workflow which is **integration-manager** and it is suitable for open-source projects. in an open-source project we have one or more maintainers and many contributors the problem is that we do not know these contributors so we can not trust them enough to access them to push or write to our repository only the maintainer of this project have to push access to project repository so if we want to contribute first we should fork the project repository to get a copy of this repository on cloud and them clone this forked repository to our local machine them we commit on the project and push that to our forked repository and next we send a pull request to the maintainer(s) of the project (we do this in GitHub) so the maintainer(s) will notify and the pull the changes form our forked repository and review them and if they want they can merge our work to their local repository and then push the merge changes to the official repository.

changing the default name of a repository when we clone it:

`git clone https://github.com/username/prj.git <another-name>`

a remote repository is a repository that is not on our machine or in other words, is not in the current directory.

list of remote repositories:

`git remote`

more info on remote repositories:

`git remote -v`

The URLs that appear with this command are the URLs that git gonna use when we talk to this remote repository.

if have a commit in our remote repository(which is GitHub) our local repository will not be aware of that.

download new commit:

`git fetch <remote> <branch>`

`git fetch origin master`

if we do not specify a branch name we will download all commits in that remote repository we can also drop the `<remote>` and git figure it out by putting origin in that place:

`git fetch`

so the git ganna downloads this commit and moves origin/master forward (not the master) even though we downloaded this new commit our working directory is not updated.

we switch to the master and merge the remote branch with the master:

`git merge origin/master`

so we ganna have a FF merge or our branches have diverged we may have conflicts and we must resolve them just like before.

see how our local and remote branches are diverging and merge them if we want:

`git branch -vv`

so to bring the changes in a remote repository into a local repository most of the time we have to fetch + merge we have the command that combines this:

`git pull`

we can do a rebase instead of merging so the git rebases our master branch on top of origin/master:

`git pull --rebase`

if in the local repository our master is ahead of origin/master by some commit we can use the push command to send commits to remote and move the origin/master pointer in the local repository to master.

pushes master to origin:

`git push origin master`

shortcut for `git push origin master`:

`git push`

Sometimes the push command will be rejected in case someone else has pushed it to the origin(remote).

some people use the bellow command which forces the git to drop other one's work and replace it with our work this is a terrible option and we should not ever do this unless we have a strong reason:

`git push -f`

the right thing is to do a pull to bring another one that works in our local repository then do a merge or a rebase if we have any conflicts we have to resolve them and then we can do a push.

by default, the push command does not transfer tags to a remote repository.

to push tag v1.0 to origin:

`git push origin v1.0`

in GitHub and on each tags page we can download our source code at that time which is automatically generated for us.

delete a tag if we have pushed it by accident:

`git push origin --delete v1.0`

**note** that this command will not delete the tag from our local repository if we want to delete it we use `git tag -d v1.0`.

we can create a release to package our software along with source code, binary files, and release notes. we can do this by going to GitHub, release section and creating a new release and we can choose a tag that was previously created or create one and let the GitHub tag our latest commit.

if we want to contribute with other ones on the branch we have to explicitly push that local branch(the same way we push tags).

shows remote-tracking branches:

`git branch -r`

shows local and remote-tracking branches:

`git branch -vv`

pushes bugfix to origin:

`git push -u origin bugfix`

removes bugfix from origin:

`git push -d origin bugfix`

**note** that the previous command does not remove the bugfix branch from the local repository so we should switch to master and run `git branch -d bugfix`.

**note** that we can also create a branch in GitHub but we have to do fetch and create a branch that is set to track the remote branch by running `git switch -C bugfix origin/bugfix`.

remove tracking branches that are not remote:

`git remote prune origin`

**What is a pull request ?**
with a pull request, we open a discussion for the team before merging to master.

to keep a forked repository up to date as the base repository. in the local repository in our machine we have a reference to our fork repository call origin, we can add another reference to the base repository and then use the pull command to bring in new commits(`git fetch <name-of-new-refrence>` and `git merge <name-of-new-refrence>/master`) and then push them to our forked repository.

shows remote repositories:

`git remote`

shows more detail about remote repositories:

`git remote -v`

adds a new remote called upstream:

`git remote add upstream <url>`

**note** that the `<url>` here is the link to the base repository that we forked.

rename a remote repository:

`git remote rename <old-name> <new-name>` e.g. `git remote rename upstream base`

remotes upstream:

`it remote rm <remote-name>` e.g. `git remote rm upstream`

