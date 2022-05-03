# Git tutorial

## Configuration Git

system: all users.
global: all repositories of the current user.
local: the current repository.

config username and email address of our github account:
`git config --global user.name "USER NAME"`
`git config --global user.email "EMAIL ADDRESS"`

use VSCode as defaul editor:
`git config --global core.editor "code --wait"`

open default editor to see all configuration:
`git config --global -e`

config end of line for git input for linux / true for mac:
`git config --global core.autocrlf input`

full help:
`git config --help`

short summery:
`git config -h`

## Creating snapshot

initalize a directory for git:
`git init`

add file to staging area:
`git add <FILES>` multiple or single file.
`git add *.txt` to add all files with ending of .txt.
`git add .` to add all files in directory.

then use commit to store this chenges:
`git commit -m "COMMIT MESSAGE"`
`git commit` it opens the default editor, if we need long message we use this command. in editor we type short description the an new line then a long description.

git store ID, Message, Date/time, Author, Complete snapshot in a commit.
to see status of working directory and staging area:
`git status`

if we are sure that our code dont need to be reviewed we can skip staging area and commit changes with following command:
`git commit -am "COMMIT MESSAGE"` use `-a` for all tracked modifed files so it does not work for untracked files `-m` for message as before.

remove files from working directory as well as staging area:
`git rm <files>`

rename or moving files with git:
`git mv file1 file2` rename file1 to file2

create .gitignore file in root of repository to ignore files or directories:
`touch .gitignore`

adding ignore stuff in this file like patterns below:

- log/ --> ignore directory
- main.log --> ignore file
- *.log --> ignore patterns

add .gitignore file to staging area and do a commit:
`git add .gitignore`
`git commit -m "add gitignore"`

show files in staging area:
`git ls-files`

if add a file to staging area then add it to .gitignore git do not ingnore it so if we want to ignore it we must remove it from staging area with following command:
`git rm --cached -r <files>` -r if we need recursive removal ex. we want to remove a nonempty directory.

[for more .gitignore templates visit this](https://github.com/github/gitignore)

short status:
`git status -s` the left column shows the staging and the right column shows the working directory.

shows unstaged changes:
`git diff`

shows staged changes:
`git diff --staged`

set our editor for diff:
`git config --global diff.tool vscode`
`git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $ REMOTE"`

check if these lines are add correctlly your .gitconfig file with `git config --global -e` command.

```.gitconfig
[diff]
 tool = vscode
[difftool "vscode"]
 cmd = "code --wait --diff $LOCAL $REMOTE"
```

lunch our visiual diff tools we command bellow:
`git difftool` changes between unstaged chenges and our current working directory.
`git difftool --staged` changes between staged chenges and our current working directory.

look at our history of commits:
`git log`
`git log --oneline` for short log.
`git log --oneline --reverse` see commit in reverse order.

see what exactly we have chenged in a commit:
`git show <ID>` or few letters of id which makes it uniqe between other commits.
`git show HEAD~<number-of-steps-to-go-back>` ex. `git show HEAD~3`

shows the version of file.js stored in the third last commit:
`git show HEAD~3:<PATH-TO-file.js>`

if we want to see all files and directories in a specific commit:
`git ls-tree HEAD~3` it shows the uniqe object id for a file or dir so we can see it with git show `<object-id>`

Git objects :

- commits
- Blobs (Files)
- Trees (Directories)
- Tags

unstaging files (undoing git add command):
`git restore --staged file.js` Copies the last version of file.js from repository to index.

discarding local changes:
`git restore file.js` Copies file.js from index to working directory.

restores multiple files in working directory:
`git restore file1.js file2.js`

discards all local changes (except untracked files):
`git restore .`

removes all untracked files:
`git clean -fd` use `git clean -h` for more help.

restoring an earlier version of a file:
`git restore --source=HEAD~2 <PATH-to-file>`

## Browsing History

we will learn:

- search for commit.(by autor, date, message, etc.)
- view a commit.
- restore your project to an earlier point.
- compare commits.
- view the history of a file.
- find a bad commit that introduced a bug.

viewing the history to shows the list of modified files
`git log --stat`

shows the actual changes (patches):
`git log --patch`

see last three commits:
`git log -3`

search commits by autor:
`git log --author=“Kristen”`

search commits by date:
`git log --before=“2022-10-25”`
`git log --after=“one week ago”`

commits with “GUI” in their message(this command is case sensitive):
`git log --grep=“GUI”`

commits with “GUI” in their patches it means add "GUI" to our code or removed it:
`git log -S“GUI”`
`git log _S"GUI" --patch`

range of commits:
`git log hash1..hash2`

commits that touched file.txt
`git log file.txt`

**note** if git complained about the file name we separate file with `--` e.g. `git log --oneline -- toc.txt`
**note** if we want to see actual chenges for a touched file we use `-- patch` e.g. `git log --oneline --patch -- toc.txt`

formatting the log output:
`git log --pretty=format:”%Cgreen%an%Creset committed %H”` %an for author name and %Cgreen to Change color of author name in green and %Creset to resert color after green

placeholders that expand to information extracted the commit:

- %H --> commit hash.
- %h --> abbreviated commit hash.
- %T --> tree hash.
- %t --> abbreviated tree hash.
- %P --> parent hashes.
- %p --> abbriviated parent hashes.
[for more visit this link](https://git-scm.com/docs/pretty-formats)

creating an alias:
`git config --global alias.lg “log --oneline"`

open the editor to check the alias we set:
`git config --global -e`

viewing a commit:
`git show HEAD~2`

shows the version of file stored in this commit:
`git show HEAD~2:file1.txt`

shows only names of the files that deleted or modified or added in this commit:
`git show HEAD~2 --name-only`

shows names and status of the files that deleted or modified or added in this commit:
`git show HEAD~2 --name-status`

comparing commits which shows the changes between two commits
`git diff HEAD~2 HEAD`

changes to file.txt only:
`git diff HEAD~2 HEAD file.txt`

shows only the name of files that changed between two commits:
`git show HEAD~2 HEAD --name-only`

shows the name and status of files that changed between two commits:
`git show HEAD~2 HEAD --name-status`

to see complete snapshot of our project we Checking out a commit, it restore our directory to that commit.
**note** that we must not modify or chenge file in a commit when we face with "detached HEAD" warnning if we commit on as detached HEAD the git automatically removes it.

checks out the given commit:
`git checkout lhe433a`

checks out the master branch:
`git checkout master`

if we are in privous commit the fit log just shows the commited massage till that commit but we can see all the commits we follow trick below:
`git log --oneline --all`

finding bugs or bad commit by devide commits in half and examine the code in that commit and run git bisect good if it is a good commit or git bisect bad if it is a bad commit and do this to remaining half and so on till we found the commit that caused the bug.

first start bisect :
`git bisect start`

marks the current commit as a bad commit:
`git bisect bad`

marks the given commit as a good commit:
`git bisect good am48547`

terminates the bisect session(atached the HEAD to master branch):
`git bisect reset`

finding contributors:
`git shortlog` also we can use `git shortlog -h` to find helpfull parameters.

for viewing the history of a file and shows the commits that touched file.txt:
`git log file.txt`

shows statistics (the number of changes) for file.txt:
`git log --stat file.txt`

shows the patches (changes) applied to file.txt:
`git log --patch file.txt`

if we remove a file accidently and want to restore it so we must look the logs with:
`git log --online -- deletedfile.txt`

and to restore this file we have to look at the parent of the latest commit and make checkout on that commit and file with:
`git checkout b633f47 deletedfile.txt`

finding the author of each lines in file.txt:
`git blame file.txt`

if we want also find out email of author of each line in file.txt:
`git blame -e file.txt`

if we want to search base on the lines:
`git blame -L 1,3 file.tx` e.g. first three lines

tagging or bookmark a commit to tags the last commit as v1.0:
`git tag v1.0`

tags an earlier commit:
`git tag v1.0 sfe2857`

we can checkout a commit with it tag:
`git checkout v1.0`

we can associte a message `-m` with tag using anotated `-a` tag:
`git tag -a v1.1 -m "this is version1.1"`

to see the tag massages:
`git tag -n`

lists all the tags:
`git tag`

deletes the given tag:
`git tag -d v1.0`

## Branching & Merging

diverge from main line of work and work on somthing else in isolation.

in this section we'll learn :

- use branches.
- compare branches.
- resolve conflicts.
- undo a faulty merge.
- essential tools.(stashing, cherry picking.)

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

for comparing branches we need to lists the commits in the bugfix branch not in master:
`git log master..bugfix`

shows the summary of changes:
`git diff master..bugfix`

shows the summary of changes between current branch and bugfix:
`git diff bugfix`

see only the name of the files that changed between current branch and bugfix:
`git diff --name-only bugfix`
`git diff --name-status bugfix`

stashing, if we have local chenges in our working directory that we have not commited yet,this chenges could get lost in this situations git does not allow us to switch branches so we should stash those chenges.

creates a new stash:
`git stash push -m “New tax rules”`

**note** that new untrack files does not include in our stash we can include them by `-all` or in short `-a` tag:
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

merge is all about bring chenges from one branch to another branch.

we have two types of merges:

1. fast-forward(FF)(if branches have not diverged)
2. 3-way(if branches have diverged)

merges the bugfix branch into the current branch we should be on current branch.
`git merge bugfix`

use following command for graphing:
`git log --oneline --all --graph`

creates a merge commit even if FF is possible:
`git merge --no-ff bugfix`

disable FF in current directory:
`git config ff no`

disable FF globally:
`git config --global ff no`

viewing the merged an unmerged branches to Shows the merged branches(it is safe to delete merged branches):
`git branch --merged`

shows the unmerged branches:
`git branch --no-merged`

conflicts happens when we want to merge branches for example:

1. same lines of code has been chenged in different ways in two branches.
2. if a file chenge in one branch and deleted in other branch.
3. a file add in twice in two different branches.

after resolve conflicts we add conflict file to the staging area.

some merge tools for resolving conflicts are :

1. Kdiff
2. P4Merge

set p4merge to default merge tool:
`git config --global merge.tool p4merge`

set path to P4Merge:
`git config --global mergetool.p4merge.path "path-to-P4Merge"`

open mergetool after facing conflict for editing:
`git mergetool`

aborts the merge and back to state before the merge:
`git merge --abort`

for undoing a faulty merge we have two options 1.delete the current commit which is not recommended cause its rewrites history and make other ones confiuse if we are working on share space but if we are dong this in our local its okay to do that 2.revert a commit which is recommended.

first look at first option.(delete the current commit, reseting the HEAD pointer.)

reset the HEAD pointer to go one step back:
`git reset --hard HEAD~1`

recover the merge that we undo in last step:
`git reset --hard <merge-id>`

second lets look at revert method:
`git revert HEAD`

but we probebly face error cause we must tell the git where we want to back.
we specifie the parent with number and the first parent is the one on the master branch and also specifie the target commit
`git revert -m 1 HEAD` .

**how to performs a squash merge?**
we use this method when we dont care about history of a branch that we want to merge,so we create a commit that combine all the features in that branch and apply that commit on top of master after that we need to commit chenges and also it is important to remove the branch after we done cause basically squash is not a merging method and we can see that by running git branch `--merged` so if dont force delete it, it makes confusion in future.

if we end up with a confilict we solve it as before then commit the chenges:
`git merge --squash bugfix`

rebasing (it results to a linear history in merging) in anothe word changes the base of the current branch.

we should be conscious bacause rebasing rewrites history so we should use rebasing only for branches or commits that are local in our repositories if we have to share this commits with other people on our team,if we have to push our chenges we should not use rebasing.

first we have to switch to our target branch:
`git rebase master`

then we switch to master and do merge:
`git merge <BRANCH-NAME>`

if we end up with a confilict we solve it as before then commit the chenges.

after done confilicts we run:
`git rebase --continue`

we can skip a commit and move to next commit by:
`git rebase --skip`

we can abort rebase if we end up with confilicts and wanna move to stage before rebasing:
`git rebase --skip`

the P4Merge create backup files we can remove it by git `-rm` file.orig or:
`git clean -fd`

we can set P4Merge not to save backups by:
`git config --global mergetool.keepBackup false`

cherry picking applies the given commit on the current branch:
`git cherry-pick gtr57ws` if we end up with confilict we solve it and then commit the chenges

if we interested in a single file not whole commit:
`git restore --source=TARGET-BRANCH -- INTERSTED-FILE`

## Collaboration

what we will learn in this section :

- collaboration workflows
- pushing, fetching and pulling
- pull request, issues and milestones
- contributing to open-source projects

**types of version control systems:**

**centralized:** in centralized like SubVersion we have a single repository that shares with all members the problem is that everyone are dependent on this repository.if the server that holds that repo goes offline no one can commit and see the history of the project
distributed: in distributed systems like Git every developer has the ropesitory on their machine and the can work offline on the project instead of colabrate with each other we use a centralized workflow for ease of use. so every one has their local repository but there is also a centrilized repository they use to sync as they work if the centrilized repository goes offline for a period of time still we can sync with each other we can use a privet server or a cloud server for our centrilized repository. this workflow is suitable for privet teams.

we have another workflow which is **integration-manager** and it is suitable for open-source projects. in an open-source project we have one or more maintainers and many contributors the problem is that we do not know this contributors so we can not trust them enough to access them to push or write to our repository only the maintainer of this project have push access to project repository so if we want to contribute first we should fork the project repository to get copy of this repository on cloud and them clone this forked repository to our local machine them we commit on the project and push that to our forked repository and next we send a pull request to maintaner(s) of the project (we do this in github) so the maintaner(s) will notify and the pull the changes form our forked repository and rewiew them and if they want they can merge our work to their local repository and then push the merge changes to the official repository.

changing the default name of a repository when we clone it:
`git clone https://github.com/username/prj.git <another-name>`

a remote repository is a repository that is not on our machine or in another word in is not in current directory.

list of remote repositories:
`git remote`

more info on remote repositories:
`git remote -v`

they urls that appears with this command are the urls that git gonna use when we talk to this remote repository.

if have a commit in our remote repository(which is github) our local repository will not be aware of that.

download new commit:
`git fetch <remote> <branch>`
`git fetch origin master`

if we do not specify a branch name we will download all commit in that remote repository we can also drop the `<remote>` and git figure it out by putting origin in that place:
`git fetch`

so the git ganna download this commit and move origin/master forward (not the master) even though we downloaded this new commit our working directory is not updated.

we switch to the master and merge the remote branch with the master:
`git merge origin/master`

so we ganna have a FF merge or our branches have divege we may have confilicts and we must resolve them just like before.

see how our local and remote branches are diverging and merge them if we want:
`git branch -vv`

so to bring the changes in a remote repository in to a local repository must of the time we have to fetch + merge we have command that combine this:
`git pull`

we can do a rebase instead of merging so the git rebase our master branch on top of origin/master:
`git pull --rebase`

if in local repository our master is a HEAD of origin/master by some commit we can use push command to send to commits to remote and move the origin/master pointer in the local repository to master.

pushes master to origin:
`git push origin master`

shortcut for `git push origin master`:
`git push`

sometime the push command will rejected in case that someone else have pushed to the origin(remote).

some people use the bellow command which force the git to drop other ones work and replace it with our work this a terrible option and we should not never ever do this usnless we have a strong reason:
`git push -f`

the right thing is to do a pull to bring other one works in our local repository the do a merge or a rebase if we have any confilict we have to resolve them and them we can do a push.

by default push command does not transfer tags to a remote repository.
to push tag v1.0 to origin:
`git push origin v1.0`

in github and in each tags page we can download our source code at that time which automatically generated for us.

delete a tag if we have pushed it by accident:
`git push origin --delete v1.0`

**note** that this command will not delete the tag from our local repository if we want to delete it we use `git tag -d v1.0`.

we can create a release to package our software along with source code, binary files, and release note.we can do this by going to github, release section and create a new release and we can choose a tag that previously created or create one and let the github to tag our latest commit.

if we want to contribute with other ones on branch we have to explicitly push that local branch(same way we push tags).

shows remote tracking branches:
`git branch -r`

shows local and remote tracking branches:
`git branch -vv`

pushes bugfix to origin:
`git push -u origin bugfix`

removes bugfix from origin:
`git push -d origin bugfix`

**note** that previous command does not remove the bugfix branch from local repository so we should switch to master and run `git branch -d bugfix`.

**note** that we can also create a branch in github but we have to do fetch and create a branch that is set to track remote branch by running `git switch -C bugfix origin/bugfix`.

remove tracking branche that are not the remote:
`git remote prune origin`

**what is pull request ?**
with a pull request we open a discusion for team before merging to master.

to keep a forked repository up to date as the base repository. in local repository in our machine we have refrence to our fork repository call origin, we can add another refrence to the base repository and then use pull command to bring in new commits(`git fetch <name-of-new-refrence>` and `git merge <name-of-new-refrence>/master` ) and then push them to our forked repository.

shows remote repositories:
`git remote`

shows more detail about remote repositories:
`git remote -v`

adds a new remote called upstream:
`git remote add upstream <url>`

**note** that the `<url>` here is the link to the base repository that we forked that.

rename a remote repository:
`git remote rename <old-name> <new-name>` e.g. `git remote rename upstream base`

remotes upstream:
`it remote rm <remote-name>` e.g. `git remote rm upstream`

## Rewriting History

what we will learn in this section :

- why and when to rewrite history.
- undo or revert commits.
- use interactive rebasing to drop or modify commits or combine and split commits.
- recover lost commits.

we need history to see what was changed, why, and when.

what is a bad history :

- poor commit messages.
- large commits.
- small commits.

steps to create clean and readable history :

- squash small, related commits.
- split large commits.
- reward commit messages.
- drop unwanted commits.
- modify commits.

**the golden rule of rewriting history**
don't rewrite public history it means that if we have pushed our commits to share with others those commits consider public and we should not modify them.

- for undoing a commit:

  - we have two options:

    - if we have pushed a commit to a remote repository base on the golden rule we should not remove this commit. here we should use the `revert` command to create a new commit that will do undo all
        the changes on this commit:

        `git revert HEAD`

        `git revert HEAD~2` for reverting two commits before where HEAD is pointing to.

        `git rever HEAD~3..HEAD` for reverting a range for commit(e.g. last three commits)but it makes our history very noisy so it is better to revert all these commits using a single commit we can use the command below:

        `git revert --no-commit HEAD~3..HEAD`

        git will simply add the required changes in the staging area so for every commits that we are gonna revert git figures out changes that need to be undone then it will apply those changes in the staging area. and if we do something wrong in this process we can run `git revert --abort` or if we are happy with our changes we can run `git revert --continue` and then we can push this to the origin and share it with others.

    - if we have not pushed a commit to remote and it is only on our local repository we can use the `reset` command to remove this commit from the history:

        `git reset --hard <target-position-from-HEAD-pointer>`

        for example to get back to one commit before HEAD:

        `git reset --hard HEAD~1`

        if we use the `--soft` option in this command e.g. `git reset --soft HEAD~1` git simply moves the HEAD pointer to the target location but it is not gonna touch our staging area and working directory. --> **git only removes the commit**

        if we use the `--mixed` option in this command e.g. `git reset --mixed HEAD~1` git simply move the HEAD pointer to the target location and put the latest snapshot in our stagging area but it is not gonna touch the working directory.--> **unstaged files**

        if we use the `--hard` option in this command e.g. `git reset --hard HEAD~1` git simply move the HEAD pointer to the target location and put the latest snapshot in our staging area and working directory.--> **discards local changes**
        
if we want to recover lost commits we should reset HEAD to a commit that we want to we recover it.

shows the history of HEAD:
`git reflog`

to recover the lost commit we can reset the HEAD back to the location we want using the commit id or unique identifier:
`git reset --hard af653fd`
`git reset --hard HEAD@{1}`

shows the history of bugfix pointer:
`git reflog show bugfix`

for amending the last commit, when we make a commit but then we realize that we have made a mistake, perhaps we left a typo or accidentally included a file in our commit in this situation we don't need to make another commit we can amend or modify our last commit:
`git commit --amend`
`git commit --amend -m "new-message"` to supply a new message.

if we accidentally include a file in our last commit we can remove it by:
`git reset --mixed HEAD~1`

then if we run `git status -s` we can see the untracked file, files that have `??` before them, and the run `git clean -fd` to remove untracked files from our working directory and then add files to the staging area and make a new commit.

to amending an earlier commit, we choose the parent commit id of the commit that we to amend and use interactive rebase, with rebasing we can replay a bunch of commits on top of other commits:
`git rebase -i <parent-commit-id>`

then VSCode pops up and we can edit each commit that we want then we press **start rebasing** then we back to terminal as you can see we are stopped at the commit that we choose to edit and then add or edit files that we want then run `git add .` to add changes and then `git commit --amned` (check the log to see that we diverge) then run `git rebase --continue` to continue or if we screwed up we can run `git rebase --abort` to abort the rebase operation and go back to the previous state before we started the rebase(check the log to see that we now have clean history).

to drop a commit we must be carefull, if we drop a commit we should solve conflicts we face.

start interactive rebasing by choosing the parent id of the commit we want to drop:
`git rebase -i <parent-commit-id>`

in VSCode we choose the drop for commits that we want to drop.

**note** if we are facing a conflict just run `git mergetool` and chose between modified or delete or abort and then continue the rebase operation with `git rebase --continue` or if we screwed up we can run `git rebase --abort` to abort the rebase operation and go back to the previous state before we started the rebase.

to rewording commit messages when we want to edit a commit message we start with interactive rebasing by choosing the parent id of the commit we want to edit its commit message:
`git rebase -i <parent-commit-id>`

so VSCode pops up then change the option to reword for commits that we want to edit and we **start rebasing** and continue editing commit messages in the next pop-up VSCode tabs.

tp reordering commits which means to change the order of the commits we start with interactive rebasing by choosing the parent id of the commit we want to move our commit on top of that:
`git rebase -i <parent-commit-id>`

so VSCode pops up then change the option to reorder commits that we want then we **start rebasing**.

to squashing commits which means to combine commits that are in the same unit of work, we start with the parent of the commit that we want to work on and start the interactive rebasing:
`git rebase -i <parent-commit-id>`

so VSCode pops up then change the option to squash for commits that we want to combine then we **start rebasing** and editing the commit message.
**note** if we use the fixup option in VSCode for the commits that we want to combine with the previous commit git will take the message from the previous commit and apply it to the commit that combines all the chosen commits.

to splitting a commit when we do several major updates of a project in one commit, we start with interactive rebasing by choosing the parent id of the commit we want to split:
`git rebase -i <parent-commit-id>`

so VSCode pops up then change the option to edit for commits that we want to split then we **start rebasing** and git stops the rebase operation at chosen commit and we can split that commit into two separate commits and then we go back to the state before we made this commit with `git reset --mixed HEAD~1` to unstage some changes and make new commits and after that run `git rebase --continue` to continue to rebase operation.
