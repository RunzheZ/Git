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
        * Includes all files may or not managed by Git, has a hidden document /.git to save actual git repository   
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
```
echo "Test Git Quick Start Demo >> start.txt
ls
cat start.txt
git status
```

>Git **add** file, to move start.txt from working directory to staging area (committed)
```
git add start.txt
git status
```

>Git **commite** file. The new file is moved from staging area into local repository. **The file still in local**
```
git commit -m "Adding start text file"
git status
```

>Git **push** file to remote (online). "origin" is the remote name when clone the repository. "master" is the branch name.
```
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

- 4. History and Aliases:   
    - Git log command to display the repository history, "git alias"

### 5.1 Staring a project with Git in three ways

#### 5.1.1 Fresh

Start generate some filler text from [hipster ipsum](http://hipsum.co/)

Create a fresh new Git repository:
```
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
```
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
   ```
   pwd
   cd Github
   git clone https://github.com/RunzheZ
   ```

### 5.2 Basic Git Workflow (add, commit, pull & push)
This section introduce how to clone GitHub repository and update new file.
```
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
```
mate ~/.gitconfig
```
> Tracked Files: the tracked files are the files are already added to Git list, not the new create file.   
> If we create a new file, we need to use "git add xxx.txt" to add the new file to git tracked list.
```
git status
mate test.txt               # modify test.txt
git status
git ls-files                # To check the tracked files list
git commit -am "Test tracked files"
```

>Eidting Files  
Best way to update files to remote repository is to add all the modification or new files to staging area first, then commit together.

>Recursive Add  
If we create a new deep nesting folder, such as level1/level2/level3, and each level has other new files. We need use **"git add ."** to add the recursive folders to staging area.
```
git add .
```

> Backing Out Changes  
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


