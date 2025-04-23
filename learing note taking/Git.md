
# Introduction

- Git the the Version control system which is use to keep track of code changes.
- If we play any game then to save the completed stages or achievements we use the save point. these save points are used for storing history of you actions. which is noting but version control system.
# Git installation

## For Linux
Open the terminal and perform 
### Debian 
```bash
sudo apt install git
```
### RPM
```bash
sudo dnf install git
```
## For Windows 

refer URL:  [Setup Git for Windows](https://git-scm.com/download/win)
## For MacOS
```sh
brew install git
```
### MacOS GUI
```bash
brew install git-gui
```

### To check Git is installed
```bash
git --version
```
![[Pasted image 20240816145758.png]]

## Git Basic Commands.

Before initializing git create one directory to store the data.

1. To initialize to Git for a folder/project Git init is used
```bash
git init
```
2. **To check the status of Git the very helpful command.**
```bash
git status
```
3. Set up git config for user, Its used to identify who made the changes in the files. its necessary to do while setting up git for 1st time.
```bash
git config --global user.name "first-name last-name"
git config --global user.email "yourmail@example.com"
```
4. Staging area or staging files
	its used for keeping track of selected files. the file can be selected and committed to track to record.
```bash
git add .  # used for keeping all the file in present working directory
git add --all
git add <file-name> # To select file that need to tacked
```
5. Git commit 
	git commit is the snapshot of repository at a point in time. it help to git understand for which file needs to be tracked.
```bash
 git commit -m "Type the changes that you have made in the file"
```
6.  Unstaging 
	if you want to unstage some file that you don't need to track record of use unstage to remove the file from staging.
```bash
git reset HEAD <file-name>
```
7. Git logs used to check the logs of changes and action performed on registry.
```
git log
git log --patch
```
![[Pasted image 20240816155138.png]]
![[Pasted image 20240816155151.png]]
8. track folder 
	you cannot commit the empty folder add .gitkeep in the folder to commit.
	its convention not rule you can add other file also.
```bash
mkdir feature
touch feature/.gitkeep
git add .
git commit -m "added folder for tracking"
``` 
