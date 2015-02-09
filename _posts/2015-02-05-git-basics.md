---
layout: post
title:  "Git Basics"
date:   2015-02-05 21:01:15
categories: git basics
---

#Creating and managing your Git project (locally and remotely)

More details about this subject can be found at [Git Reference Documentation](http://git-scm.com/docs).

##How to install Git?

Check out [how to install Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git), at Git Documentation page.

##How to start a Git project?

Basicaly, to start versioning your project with Git, you just need to:

1. Go to your project's folder (on console) and type `git init`. 
2. Add your files to the index (The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit.) using `git add <files>` or `git add --all` (to add all your files).
3. Stores the current contents of the index in a new commit along with a log message from the user describing the changes with `git commit -m "<message>"`.

###Example:

``` bash
# create project's folder or use an existing one
mkdir hello 		
# go to project's folder
cd hello 			
# enable Git on your project 
git init
# create a file sample
touch readme.md
# add the file to the Git repository index
git add readme.md
# commit the file along with the message "My first commit!"
git commit -m "My first commit!"
```

That is it! You have your first commit in your Git project.

To further changes, adding or updating files, you just need to repeat the **steps 2** and **3**. These steps will commit your changes locally, to know how to make it remotely take a look at **@**.

##How to clone, or download, a remote repository in a local folder?

There are two approaches that can be used: with `git clone` or `git init`. `git clone`, as the name suggest, is used to clone a remote repository in a local folder. `git init` can reach the same goal with more control. Both cases will be discussed below.

`git clone <repository-url> <local-folder-name>`

The above code will clones `<repository-url>` into `<local-folder-name>`, creates remote-tracking branches for each branch in the cloned repository (visible using git branch -r), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

Using `git init` to clone a remote repository is a little bit tricky.

1. Create an empty folder.
2. Get inside the folder.
3. Run `git init`.
4. Run `git remote add <name> <remote-repository-url>` to add a reference name to a remote repository.
5. Run `git fetch -all` to update all remote-tracking branches.
6. Run `git pull <remote-repository> <remote-branch>` to merge the remote master branch into the current master branch.

##How to create a local branch that tracks a remote branch?

**`git checkout -b <local-branch> --track <remote-repository>/<remote-branch>`**

Is a shortcut to `git branch --set-upstream-to=<remote-repository>/<remote-branch> <local-branch>` followed by `git checkout <local-branch>`


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

##What is Git Submodule?





