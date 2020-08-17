# Git Commands
Some useful commands for manage a Git Repository and interact with Github.

  - [Basic Workflow](#basic-workflow)

    - [Initialize a repo](#initialize-a-repo)
    - [Check status](#check-status)
    - [Add files](#add-files)
    - [See changes](#see-changes)
    - [Commit](#commit)
    - [Log the commit tree](#log-the-commit-tree)
    - [Show commit details](#show-commit-details)
  
  - [Backtracking](#backtracking)

    - [Checkout](#checkout)
    - [Unstage files](#unstage-files)
    - [Change HEAD commit](#change-head-commit)
  
  - [Branching](#branching)

    - [Show branches](#show-branches)
    - [Create a branch](#create-a-branch)
    - [Switch branch](#switch-branch)
    - [Merge changes](#merge-changes)
    - [Delete a branch](#delete-a-branch)
  
  - [Teamwork](#teamwork)

    - [Clone a repo](#clone-a-repo)
    - [Show connected remotes](#show-connected-remotes)
    - [Fetch changes](#fetch-changes)
    - [Merge from remote](#merge-from-remote)
    - [Push changes](#push-changes)

<br/>

## Basic Workflow


### Initialize a repo 

Initialize a local repository 

```shell
git init 
```
<br/>


### Check status 

check the status of the repository

```shell
git status 
```
<br/>


### Add files 

Add files to the staging area (before commit).

- add single files 
    ```shell
    git add [filename]
    ```

    
    
- add multiple files like so: 
    ```shell
    git add ./main.js ./index.html ./style.css 
    ```

    
    
- add all the files in the repo
    ```shell
    git add .
    ```
<br/>


### See changes 

See the changes of a defined unstaged file, compared to the last commit.

```shell
git diff [filename]
git diff .
```
<br/>


### Commit 

Commit all the changes from the staging area (add a commit message to the end)

```shell
git commit -m 'commit message'
```
<br/>


### Log the commit tree 

View all the commits tree, (logs, author and date).

```shell
git log 
```
<br/>


### Show commit details 

Show all the details about a commit and file changes.

- use HEAD to refer to the last commit 

  ```shell
  git show HEAD
  ```

- use the first 7 character of the *sha code* (use `git log`) to get a specific commit.

  ```shell
  git show [sha-code]
  ```
<br/>
<br/>



## Backtracking 


### Checkout
Restore the file changes to the commit specified.

- restore the file to the last commit
    ```shell
    git checkout HEAD [filename]
    git checkout HEAD .
    ```

- restore a file to a  specified commit (using the first 7 char of its *sha code*).
    ```shell
    git checkout [sha-code] [filename]
    ```
<br/>


### Unstage files

unstage file from staging area 
```shell
git reset [filename]
git reset .
git reset HEAD [filename]
git reset HEAD .
```
<br/>


### Change HEAD commit

change the Head commit to the specified commit using its SHA
```shell
git reset [sha-code]
```
<br/>
<br/>



## Branching 


### Show branches

show the all the available branches for the current repository
```shell
git branch
```
<br/>


### Create a branch

create a new branch with the specified  name
```shell
git branch [branch-name]
```
<br/>


### Switch branch

switch between different branches 
```shell
git checkout [branch-name]
```
<br/>


### Merge changes

merge all the changes made in the declared branch to the current branch (the command must be executed in the target branch).
```shell
git merge [branch-name]
```
<br/>


### Delete a branch

delete branches passing the branch name and after `-d` flag
```shell
git branch -d [branch name]
```
<br/>
<br/>



## Teamwork


### Clone a repo

clone a local or remote repository
```shell
git clone [remote/location] [new-repo-name]
```
<br/>


### Show connected remotes

see the remotes conneted with your repository
```shell
git remote -v
```
<br/>


### Fetch changes

fetch all the canges in a remote repo to your local
```shell
git fetch
```
<br/>


### Merge from remote

merge the changes made in the remote repo branch to your local repo branch 
```shell
git merge origin/master
```
<br/>


### Push changes

push the changes made in local to the remote master branch (or other branches) 
```shell
git push [remote-name] [branch-name]
```
<br/>



