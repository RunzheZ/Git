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
> We will use the Git text file **".gitignore"**, which to recored all the files and floders that Git should ignore.
> 
> 

## Section 6: Visual Merge/Diff Tool Installation

## Section 7: Comparisons

## Section 8: Branching and Merging

## Section 9: Rebasing

## Section 10: Stashing

## Section 11: Tagging

## Section 12: Bonus: Office Hour Sessions

## Section 13: Updates and Errata

## Section 14: Bonus: Resources and Special Offers
