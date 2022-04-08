# Git 

This is the Git course note Udemy: [Git Complete](https://www.udemy.com/course/git-complete)
 
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

## Section 2: Git Installation
> Mac: terminal type: git version

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


## Section 4: Text Editor Installation

## Section 5: Basic Git Commands

## Section 6: Visual Merge/Diff Tool Installation

## Section 7: Comparisons

## Section 8: Branching and Merging

## Section 9: Rebasing

## Section 10: Stashing

## Section 11: Tagging

## Section 12: Bonus: Office Hour Sessions

## Section 13: Updates and Errata

## Section 14: Bonus: Resources and Special Offers


