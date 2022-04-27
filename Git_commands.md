# Git Commands

# Table of Contents
1. [What is this document](#purpose)
1. [Basic Syntax](#basicSyntax)

---
# What is this document <a name="purpose"></a>
This document outlines the quick git syntax. 

# Basic Syntax <a name="basicSyntax"></a>
## Clone a project
- git clone https://github.kyndryl.net/DataMngmnt/MCDMS.git 
- git branch 
- git checkout -b <branch_name>    
- git pull origin <branch_name>    

## Push code to remote git branch
- git status     
- git add docs/DataOps/Kyndryl-IAM.md  
- git commit -m "kyndryl IAM implementation approach"  
- git push origin DataOps

## Stash local changes and pull from remote branch
- git stash
- git pull
- git stash pop 
- git stash list

## Add Existing project to a Repository    
- Create an empty repo in GitHub.com
- Open terminal inside the project folder
- Configure local git repo:
    - Remove all git related files: 
        - rm -Rf .git .gitignore
        - rd .git /S/Q
    - git init
    - git add .
    - git commit -m “Initial commit”
- Sync your local git repo with the remote one
    - git remote add origin https://github.kyndryl.net/DataMngmnt/go_service_broker.git
    - git push -u origin master <br> 

Note: reference link: https://www.youtube.com/watch?v=OVL7R0eT8jw

## Check current branch
- git branch
    
## Switch Branch using git checkout
- git checkout <existing_branch> <br>
- git checkout -b <new_branch> 

## Switch branch using git switch
- git switch <existing_branch>
- git switch -c <non_existing_branch>

<br>

# Table
| Col-1 | Col-2 | Col-3 | Col-4 |
| ---- | ---- | ---- | ---- |
| Val-1 | Val-2| Val-3 | Val-4 |
| Val-1 | Val-2| Val-3 | Val-4 |


