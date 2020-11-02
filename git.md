# Git cheat sheet  
  
## Branch  
1. #### get the local branch list, star is marked for current branch  
	  ```$ git branch   ```  
  
2.  ####  create new branch  
	  ```$ git checkout -b <branch-name> ``` 
  
  3. #### list all branch  
	  ```$ git branch -a```   
       
 >list remote branches  
	 ```$ git branch -r``` 
  
3. #### create anew branch from current code  
	  ```$ git branch <branch-name> ```  
  
4. #### create branch from remote  
	  ```$ git checkout -b <local_branch> origin/<remote_branch>``` 
  
5. #### switch to another branch  
	```$ git checkout <branch_name>```  
#  
  
## Create  
1. #### Clone   
	 ```$ git clone ssh://username@repos.git```  
 
2. #### Create  
	  ```$ git init```  
3. #### Push local branch to remote  
	  ```$ git push -u origin <branch_name>``` 
##  
## Local changes
1. #### Files changed  
	  ```$ git status``` 
2. #### Add file to local repo 
	  ```$ git add <file_name>```  
	  ##### Add multiple files to local repo  
	  ```$ git add <file1> <file2> <file3>...```  
	  ###### Add all the files  
	  ```$ git add .```  
 3. #### Difference between edited file and local repo  
	  ```$ git diff <file_name>```  
 4. #### Commit all files to local repo  
	  ```$ git commit -m <commit message>```  
  
 5. #### Change the last commit  
	  ```$ git commit --amend```     
6. #### Change the author infomration of last commit  
  ```$ git commit --amend --author "Sushil Kotnala <sushil.kotnala@gmail.com>```	
 
 7.  #### Change the last commit message  
	  ```$ git commit --amend```  
	  > in the editor window, change the commit messages   
##  
## Commit history  
1. #### list the last commit messages  
	  ```$ git log```  
2. #### Show changes of specific file  
	  ```$ git log -p <file>```  
3. #### Who changed and when in file  
	  ```$ git blame <file>``` #  
 ## 
## Update and publish  
1. ##### List all configure remotes  
	  ```$ git remote -v```  
2. #### Get information about remote  
	  ```$ git remote show <remote>```  
3. #### Add new remote  
	  ```$ git remote add <shortname> <url>```  
4. #### Download changes from remote but dont merge with local  
	  ```$ git fetch <remote>``` 
5. #### Download remote changes and merge with local  
	  ```$ git pull <remote> <local_branch_name>``` 
6. ##### Publish local changes to remote  
	  ```$ git push <remote> <branch_name>```  
7. ##### Delete local branch  
	  ```$ git branch -d <branch_name>```  
8. #### Delete remote branch  
	  ```$ git branch -D <branch_name>```  
9. #### Publish local tags  
	  ```$ git push --tags```  
##  
## Merge and rebase  
1. ##### Merge branch into current head  
	  ```$ git merge <other_branch_name>```
 2. #### Rebase current head into branch  
	  ```$ git rebase <other_branch_name>```  
3. #### Abort a rebase  
	  ```$ git rebase --abort```  
4. #### Continue rebase after resolving conflicts  
	  ```$ git rebase --continue```  
## 
## Reset and revert  
1. #### Discard all local changes in your working directory  
	  ```$ git reset --hard HEAD```  
2. #### Discard local changes in specific file  
	  ```$ git checkout HEAD <file>```  
3. #### Revert a commit  
	  ```$ git revert <commit_id>```  
4. #### Reset your HEAD pointer to specific commit and discard all changes since then  
	  ```$ git reset --hard <commit_id>```  
5. #### Reset your HEAD pointer to specific commit and preserve all changes as unstaged  
	  ```$ git reset <commit_id>```  
6. #### Reset your HEAD pointer to specific commit and preserve uncommitted local changes  
	  ```$ git reset --keep <commit_id>```
