# Git

This is the Git course note Udemy: [Git Complete](https://www.udemy.com/course/git-complete)
 ---

<br/>

## Section 1: Introduction

>What is Git:  
Distributed source control system (Not required to be decentralized). [Wiki](https://en.wikipedia.org/wiki/Git)

>Key Concepts:  
Repository contains all files, history, config managed by Git.

>Three local states of Git:  
    1. Working directory hold  
        *Includes all files may or not managed by Git, has a hidden document /.git to save actual git repository  
    2. Staging area (pre-commit holding area)  
        * Git index, a holding area for queueing up changes for next commit.  
    3. Commit - Git Repository (history)  
        * The Git repository manages the Git commit history.

>Remote repository (maybe the forth state --- Github)

>Branches: other source control systems, timeline contains changes. (Master Branch)
---
<br/>

## Section 2: Git Installation

> Mac: terminal type: git version
---
<br/>

## Section 3: Git Quick Start

> Set up local git user name and email.

```
git version
git config --global user.name "YourName"
git config --global user.email "EmailAddress@gmail.com"
git config --global --list
```

>Clone the Github repository and check status  
Plase first use terminal to go the correct directory. cd../ and pwd command

```
git clone https://github.com/RunzheZ/Git.git
git status
```

git status will report the changes between working directory and staging area, local repository and remoate repository.

>Create a new start.txt file in the project file.

```bash
echo "Test Git Quick Start Demo >> start.txt
ls
cat start.txt
git status
```

>Git **add** file, to move start.txt from working directory to staging area (committed)

```bash
git add start.txt
git status
```

>Git **commite** file. The new file is moved from staging area into local repository. **The file still in local**

```bash
git commit -m "Adding start text file"
git status
```

>Git **push** file to remote (online). "origin" is the remote name when clone the repository. "master" is the branch name.

```bash
git push origin master
```

---
<br/>

## Section 4: Text Editor Installation

>Windows Text Editor: Notepad ++

>MacOS Text Editor: [TextMate](https://macromates.com/)  
Setup: TextMate --> Preference --> Terminal --> Install Shell Support  
Test: Open terminal --> type "mate" to open TextMate.

>Set TextMate is the default editor for Git

```
git config --global -e
# This is using default editor (Vim) to show the Git config file (Quit: ESC, then ":q" or ":wq" )

git confit --global core.editor "mate-w"
# This is modify the default editor to TextMate

git config --global -e
# Check the config file again, this time it should use Textmate open config file. "Command + Q" to quit.
```

>Set TextMate profile

```
# In terminal open or create .tm_properties for TextMate
mate .tm_properties
```

```
# In .tm_properties file
# General Settings
fontName = "Menlo"
fontSize = 24
# "Command + S" to save, "Command + Q" to quit
```

## Section 5: Basic Git Commands (Core)

- [1. Staring a project with Git in three ways:](#1-staring-a-project-with-git)  
    1. [Fresh (no source yet)](#511-fresh)  
    2. [Existing source locally](#512-existing-source-locally)  
    3. [GitHub project (Fork and clone)](#513-github-project-clone)

- [2. Basic Workflow:](#52-basic-git-workflow-add-commit-pull--push)
    1. Adding and editing files;  
    2. Adding files to Git's staging area;  
    3. Committing to Git repository;  
    4. Push & pull changes back to Git.  

- [3. File Management:](#53-file-management-remane-move--deletet-files)
  - Remane, move & deletet files.

- [4. History and Aliases:](#54-history-and-aliases)
  - Git log command to display the repository history, "git alias"

### 5.1 Staring a project with Git in three ways

#### 5.1.1 Fresh

Start generate some filler text from [hipster ipsum](http://hipsum.co/)

Create a fresh new Git repository:

```bash
pwd
cd  # choose the project directory
git init fresh-project
ls
ls -al
cd .git/
cd ..
git status
mate hipster.txt
git status
git add hipster.txt
git commit      ### This will open a TextMate for this commit, input the commit message, Ctrl+S, Ctrl+Q
rm- rf fresh-project/       # Remove the Git Repository
```

#### 5.1.2 Existing Source locally

In this section, we will use [Initializr](http://initializr.com) to generate files as our locally Git.
Download a .zip file to project directory.

```bash
pwd
cd GitHub
unzip ~/Downloads/initializr-verekia-4.0.zip
ls
mv initializr web-project       # rename project 
cd web-project
ls                              # assume this is our project
git status
git add .                       # add all the new files
git commit -m "My first commit, inline"
git status
rm -rf .git                      # remove .git documents, can't manage the files by Git
cd ..
rm -rf web-project
```

#### 5.1.3 Github Project Clone

1. Sign in Github;
2. Find the project repository, and click **"Fork"** to copy the repository to your own Github;
3. Find the **"Clone"** options, and copy the **"HTTPS"**;
4. Using the following command to clone the repository local.

```bash
pwd
cd Github
git clone https://github.com/RunzheZ
```

### 5.2 Basic Git Workflow (add, commit, pull & push)

This section introduce how to clone GitHub repository and update new file.

```bash
# In Git clone local repository
pwd
git status
mate test.txt
git add test.txt
git status
git commit              # use mate to command or git commit -m "This is commit"
git pull origin master  # git config pull.rebase false(merge)/true(rebase)
git push origin master
```

### 5.3 File Management (Remane, move & deletet files)

Modify **".gitconfig"** file

```bash
mate ~/.gitconfig
```

> Tracked Files: the tracked files are the files are already added to Git list, not the new create file.
>> If we create a new file, we need to use "git add xxx.txt" to add the new file to git tracked list.

```bash
git status
mate test.txt               # modify test.txt
git status
git ls-files                # To check the tracked files list
git commit -am "Test tracked files"
```

> **Eidting Files**      
>>Best way to update files to remote repository is to add all the modification or new files to staging area first, then commit together.

> **Recursive Add**  
>>If we create a new deep nesting folder, such as level1/level2/level3, and each level has other new files. We need use **"git add ."** to add the recursive folders to staging area.

```bash
git add .
```

> **Backing Out Changes**
>> This backing out is only works for the modification in staging area. This is **unstage** and **checkout** process.

```bash
git add test.txt
git status
git reset HEAD test.txt                 # unstage the added document
git checkout -- test.txt                # reload the previous test.txt
```

> **Renaming and Moving Files** 
>>  There are two ways to remane or move files. One is using Git command; another is using bash command.
``` bash
# git command renaming and moving files
git mv test.txt test_new.txt
git status          # it will appear rename
git commit -m "renaming test.txt file"      # rename the file, before other modification
```

``` bash
# bash command renaming and moving files
mv test.txt test_new.txt
git status          # it will appear delete original file and have another new file
git add -A          #  -A will recursively add any changes(renamed, moved or deleted)
git status          # it will appear rename file
git commit          # add commit in mate
```

Rename the file then back out.

``` bash
# git command renaming and moving files
git mv test.txt test_new.txt
git status          # it will appear rename
git mv test_new.txt test.txt
git status
```

``` bash
# git command and moving files to another directory
git mv test.txt newFolder
cd newFolder
git status          # it will appear rename
git commit
```

``` bash
# bash command and moving files to another directory
mv test.txt ..      # moveing the test.txt to the up folder
cd ..
git status          # it will appear rename
git add -A
git commit
```

We also can modify the file name in Finder. In this condition, there will be ".DS_Store" operating system level file. We want to git add the individual our modification file.

``` bash
# bash command renanme file in Finder
git add newFileName.txt     # Git add specific file
git add -u                  # update git list
git commit
```
> **Deleting Files**
>> Case 1. Delete the untracked file
``` bash
mate test_delete.txt        # create a new file and untracked by Git
rm test_delete.txt          # because it's untracked file, only need to use bash command rm to remove
```

>> Case 2. Delete the Git tracked file
``` bash
mate test_delete.txt            # create a new file and untracked by Git
git add test_delete.txt
git commit -m "Add test_delete.txt"
git ls-files                    # check the tracked files
git rm test_delete.txt          # for the tracked files, we can use git rm to remove them
git commit -m "Deleting new file"
```

> **How to back out a staged deletion**
``` bash
git ls-files                    # check the tracked files
git rm test_delete.txt          # remove file
git reset HEAD test_delete.txt  # begin back out
ls                              # the file is still missing
git check out -- test_delete.txt    # check out the deleted file
ls                              # the deleted file will be back out
```

> **Remove folder and its subfiles**
``` bash
rm -rf folder                    # r is recursive f is force deletion
git status
git add -A
git commit -m "deleting the folder and all children"
```

### 5.4 History and Aliases
> **Check Git Log History**
``` bash
git help log                            # Press q to out the help window
git log                                 # check log history
git log --abbrev-commit                 # short name log history 
git log --oneline --graph --decorate    # ** Very Useful, oneline log
git log --since="3 days ago"            # 3 days log
git log -- test.txt                     # specific document log
git log --follow -- test.txt            # rename or moving log
git show 4fbe838de2fc0fab561a0a7a91f187a3fa285257git commit -m 
# detial of a specific log information
```

> **Git Alias**  
> Sometimes the Git commands are too long, such as
```bash
git log --all --graph --decorate --oneline
```
It's very useful, but it's too long for everytime to use.
We prefer to create some alias for these useful command.
```bash
git config --global alias.hist "log --all --graph --decorate --oneline"
# setup alias
git hist
mate ~/.gitconfig       # check .gitconfig
```

> **Git Ignore (Avoid unwanted files)**  
> This section will show how to exclude unwanted files, such as ".DS_Store".  
> We will use the Git text file **".gitignore"**, which to recored all the files and floders that Git should ignore. (We can use "ls -al" to list all files and folders, including dot files and folders)

```bash
mate .gitignore
```

The format for this ".gitignore" file is one expression per line. The expression could be the name of a specific file, the name of folder, or a pattern like "*.txt".

```bash
# This is in mate .gitignore file
MyFile.ext      # Specific File
*.ext           # File Pattern
my-folder/      # Folder

# Examples
.DS_Store       # ignore specific ".DS_Store" file
*.log           # ignore all ".log" file
log/            # ignore log folder and its files

# Finally, Cleanup and Back to Origin
git pull origin master      # pull first
git push origin master      # push, origin is the name of remote repository, master is the default branch in Git repository
```

## Section 6: Visual Merge/Diff Tool Installation

### 6.1 Install **P4Merge**
Open the [PERFORCE](http:www.perforce.com).   
DOWNLOADS --> Downloads --> LATEST RELEASES --> Clients --> [P4MERGE: VISUAL MERGE TOOL](https://www.perforce.com/downloads/visual-merge-tool)  
Choose the correct family system. Then, download.  
Open the downloaded "P4V.dmg" file, and move the "p4merge.app" to Applications folder.  
Open "Launchpad" to open the new installed "p4merge.app", "command+q" quit.

> Simple solution will match local master branch HEAD to origin.master branch HEAD.
```
git reset --hard origin/master
```

### 6.2 P4Merge for Mac Git Configuration
1. Confirm the specific P4Merge executable.
```bash
cd  ~/Applications/p4merge.app/Contents/MacOS/
ls -al
./p4merge       # Run p4merge
pwd
```
2. Set up p4merge as Git diff tool and set p4merge path. Also, we need disable the prompt.
```bash
git config --global diff.tool p4merge       # Set p4merge as diff.tool
git config --global difftool.p4merge.path /Applications/p4merge.app/Contents/MacOS/p4merge  # Set p4merge path
git config --global difftool.prompt false   # Disable the prompt
```
We can use the similar method to set up p4merge as Git merge tool.
```bash
git config --global merge.tool p4merge
git config --global mergetool.p4merge.path /Applications/p4merge.app/Contents/MacOS/p4merge
git config --global mergetool.prompt false
```
Then, we can check all the Git config set up.
```bash
git config --global --list
git config --global -e          # edit the .gitconfig file
```
## Section 7: Comparisons

**Basic Git Workflow Life Cycle Table**  
| Local | Local | Local  | Remote  |
| :------: | :------: | :------: | :------: |
| Working Directory | Staging Area | Repository (.git folder) |Server (Github)| 

### 7.1 Comparisons Working Dir VS. Staging Area
We use the **"git diff"** to no what's the modification in "git status" result. This difference is betwwen the **Working Directory** and **Staging Area**.  

We also can use the Git's **"difftool"** command to visually see the modification.
```bash
git diff            # prompt command to show the difference, use q to quit
git difftool        # visually method to see difference using p4merge, use command + q to quit
```

### 7.2 Comparisons Working Dir VS. Repository
We can use the **"git diff HEAD"** to compare the difference between **Working Directory** and **Local Repository**.  

We also can use the Git's **"difftool"** command to visually see the modification.
```bash
git diff HEAD           # prompt command to show the difference, use q to quit
git difftool HEAD       # visually method to see difference using p4merge, use command + q to quit
```

### 7.3 Comparisons Staging Area Dir VS. Repository
We can use **"git diff --staged HEAD"** to compare the difference between **Staging Area** and **Local Repository(.git folder)**. The **HEAD** means the last commit on the current branch (Local).
We also can use the Git's **"difftool"** command to visually see the modification.

```bash
git diff --staged HEAD      # prompt to check the diff, use q to quit
git difftool --staged HEAD  # visually to check the diff, use command + q to quit
```

### 7.3 Comparisons Limit for One File

We can add the specific file name in the "git diff" command to check one specific file difference.

```bash
git diff -- Git_Udemy.md        # we only check the README.md file difference
git difftool -- Git_Udemy.md    
```

### 7.4 Comparisons Between Commits

We compare the arbitrary commit and  the last commit. We need to use **"git log --oneline"**. It will show all the commits and the abbreviating label for each commit. Then, we use **"git diff reference1 reference2"** to compare two different commits.

```bash
git log --oneline
git diff ae6f872 HEAD   # HEAD means the last commit
git diff HEAD HEAD^     # compare HEAD and HEAD-1 commits
git difftool HEAD HEAD^
```

If one side is referenced by "dev/null/", that means that this file didn't exist prior, followed by the other side.

If there are several files modificaiton between two commits, the **difftool** shows file difference one by one, once we close the top one.

### 7.5 Comparisons Local VS Remote

We want to compare the difference between two branches. It's similar to compare the local master branch and remote master branch.

```bash
git diff master origin/master
git difftool master origin/master
```

**"origin"** is the name of the remote reference that points back to GitHub (online), and **"/master"** is just the master branch on the Git repository on GitHub. The **"master"** is the local committed master branch, and it's also called **"HEAD"**.



## Section 8: Branching and Merging

### 8.1 Branch Basic
In this section, we begin to create a new branch and do modification, then, merge the stable modification to the master branch. We use **"git branch -a"** to list all the local and remote branches.
```bash
git branch -a
```
The asterisk(*) labels the current active branch.  
> We use the **"git branch newBranchName"** to create a new branch.  
> Use **"git checkout mynewbranch"** to switch branches.
```bash
git branch mynewbranch      # Create a new branch called "nynewbranch"
git branch -a               # Will show the new branch in the list
git checkout mynewbranch    # Switch to mynewbranch as active branch
git branch -a               # The asterisk will label "mynewbranch"
```

Let's check the history of Git.
```bash
git log --oneline --decorate    # It will appear the history log

# The first line will looks like
e060xxx (HEAD, origin/master, origin/HEAD, mynewbranch, master)
# HEAD usually points to the last commit on the current branch;

git checkout master             # Switch back to the master branch
git branch -m mynewbranch newbranch # Rename the branch
git branch -a
git branch -d newbranch         # Delete branch, we can't delete current branch
```

### 8.2 Happy Path: Fast Forward
> Faster Forward merge: there are no changes being made on the target branch (master).
> Git places all the commites on the master branch, as if we never branched away. 
```bash
git branch                      # list all local branch
git branch -a                   # list all branches including remote branches

git checkout -b title-change    # build a new branch called title-change and checkout it
mate test.txt                   # change one file
git status
git commit  -am "Changing XXX file"
git log --oneline --decorate   

# Move the modification from title-change brach to master
git checkout master             # change branch back to master
git diff master title-change    # Show the difference between master brach and title-change branch
git difftool master title-change # visual version to show difference
git merge title-change          # merge the title-change branch to master
git log --oneline --graph --decorate
git branch 
git branch -d title-change
git branch
```

### 8.3 Happy Path: w/0 Faster Forward

```bash
# commits in add-copyright branch 
git checkout -b add-copyright   # create and switch to add-copyright branch
mate test.txt                   # modification in add-copyright branch
git commit -am "Adding text"    # add-copyright branch commit
git log --oneline --grapy --decorate

 # merge to master branch w/o faster forward
git checkout master
git merge add-copyright --no-ff # --no-ff means w/o faster forward
git log --oneline --graph --decorate --all
git branch -d add-copyright     # when we check the log, the commit still there, but no branch name label.
```

### 8.4 Automatic Merges

> Automatic merge: Both of the sub-branch and master-branch has modification commits, but there are no conflicts. It can merge automatically.

```bash
# Create the simple-changes branch and do some modification
git checkout -b simple-changes
mate test.txt
git commit -am "Modification in simple-changes branch test.txt"

# Switch back to master branch and do some modification not conflict with simple-changes branch modification
git checkout master
mate start.txt
git commit -am "Modification in master branch start.txt"

# Check difference and automatic merge
git log --oneline --graph --decorate --all
git merge simple-changes -m "Merging changes from simple-changes branch"
# the -m means this merge will result in a commit
git log --oneline --graph --decorate --all
git branch -d simple-changes
```

### 8.5 Merge Conflict and Resolution

> If two branches have the modification in the same area of same file, the merge will conflict and we need to use the difftool to check the difference and choose what we want.

```bash
# Creat a new branch and do some modification
git checkout -b realwork
mate test.txt
git commit -am "Making changes in realwork branch"

# Switch back to master bracn and do modification in the same area of realwork branch
git checkout master
mate test.txt
git commit -am "Making changes in master branch"

git log --oneline --graph --decorate --all

# Check the difference between two branches
git diff master realwork
git difftool master realwork

# Merge conflict
git merge realwork                      # will report a conflict problem
git mergetool                           # use p4merge software to merge conflict
git commit -m "Complete merge conflict" # commit the merge 

# Ignore all the .orig files
mate .gitignore                         # open .gitignore file and add *.orig

# Delete the realwork branch and check log
git branch -d realwork
git log --oneline --graph --decorate --all

git pull origin master
git push origin master
```

## Section 9: Rebasing

### 9.1 Simple Rebase Example


## Section 10: Stashing

## Section 11: Tagging

## Section 12: Bonus: Office Hour Sessions

## Section 13: Updates and Errata

## Section 14: Bonus: Resources and Special Offers
