---
layout: post
title:  "Git Basics"
date:   2015-02-05 21:01:15
categories: git basics
---

**`git remote add -f [-t <branch>] [-m <master>] <name> <remote-repository-url>`**

Creates a remote repository named as `<name>` for the `<remote-repository-url>`.
`-m <master>` sets the master branch to `<master>`.
`-t <branch>` set branch that will be tracked. You can give more than one `-t <branch>` to track multiple branches without grabbing all branches.
`-f` will fetch the remote repository after adding it.

**`git remote `**

Shows all remote repository in the project.

**`git branch -r`**

Shows all remote branches in the project.

**`git branch -list`**

Shows all local branches in the project.

**`git checkout -b <local-branch> <remote-branch>`**

Is a shortcut to `git branch <local-branch> <remote-branch>` followed by `git checkout <local-branch>`


**`git branch -d <local-branch>`**

Delete a `<local-branch>`.

**`git add <files> (or --all)`**

Add `<files>` to the index.
(The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit.)

**`git status`**

Displays paths that have differences between the index file and the current `HEAD` commit, paths that have differences between the working tree and the index file, and paths in the working tree that are not tracked by Git.

**`git commit -m “<message>”`**

Stores the current contents of the index in a new commit along with a log message from the user describing the changes.

**`git fetch --all`**

Fetch branches and/or tags (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. Remote-tracking branches are updated (see the description of `<refspec>` below for ways to control this behavior).

**`git push <remote-repository> [<branch>]`**

Updates remote refs using local refs, while sending objects necessary to complete the given refs.
If `<branch>` is not provided, it will push to master.

**`git pull <remote-repository> <branch>`**

Incorporates changes from a remote repository into the current branch. In its default mode, `git pull` is shorthand for git fetch followed by `git merge FETCH_HEAD`.

**`git merge [-s <strategy> <commit>...] [-m “<message>”]`**

Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch. This command is used by `git pull` to incorporate changes from another repository and can be used by hand to merge changes from one branch into another.

**`git pull -r <remote-repository> <branch>`**

Replace local branch with `<remote-repository> <branch>` files.

**`git checkout -b <local-branch> <remote-repository>/<local-branch-origin>

**`git push origin -u <local-branch> 
