git basics starts with this :

1. first create a repository = use (git init ) to create a repo

2. after that if u want to add html,css and js in one step = use (touch index.html style.css script.js)

3. to check the username and user-email = use git config user.name and git config user.email

4. to make a directory = user mkdir (add-file name) = eg : mkdir git-folder

5. if u want to move a files to a folder = use mv  index.html style.css script.js project/

- mv = move
- project/ = target folder

eg : mv index.html style.css script.js git-folder/ 

6. if you u want to inspect history = use git log --oneline --all --graph

7. if u want to know difference between the last 2 commits u made = use git diff HEAD~1 HEAD

8. if u want to know the last commit details = use git show HEAD


9. if u want to create a branch = use git checkout g-b (new branch name) = eg : git -b feature

10. if u want to check the branches = use git branch 

11. if u want to delete a branch = use git branch -d (existing branch name) = eg : git -d OR D feature

12. if u want to rename a branch name = use git branch -M main = eg : main branch name is (master) => after using this master branch name will change into main branch name.

13. if u want to add git file to github first u need to connect with github repo :

- first step : git remote add origin https://github.com/username/practicing-git.git

-second step : 



14. if you want to merge a branch to the main branch = use git merge (mention the file name that you want to merge,) when u are merging the file don't merge the current file , for eg : if u want merge feature in main branch then mention => git merge feature in main branch as the current file.

15. if u want to checkout out in the old commits = > use git checkout (mention the previous id commit)

16. if u see a file in the normal stages section it means that the code is untracked.

17. Revert the merge:

git revert -m 1 <merge-commit-hash>


-m 1 tells Git to keep the first parent (main) and undo the changes from the merged branch.

This creates a new commit that undoes everything from that merge, including the file.


18. if u want to know where ur local repo is connected to remote repo = use git remote show origin

19. if u want to push ur file from local repo to remote repo = use git push -u origin main

20. if sync changes shows in the source control it means that if u have update anything in local repo they ask you to update in remote repo

21. if u want to add the main branch code to the default branch use git push (main branch name)

22.  the head gets detached from the main when u checkout through the deleted commits and u want and it will come to the main :

- when u enter this git checkout head , it will still detach from the main 
- when u enter this git checkout --hard head!~1 it will still detach from the main 

- so , therefore u have to add 2 or more commits and then prompt : git reset --hard head~2 , then point it to main branch

- then the head will attach to the main

23. git 

there are 3 methods to reset a commit u made :

1. git reset --hard, this method will delete the commit and put the head section to the previous main section
2. git reset --soft, by this method it will delete the commited changes and bring it back to the staged changes section
3. git reset , by this method it will delete the commited changes and bring it back to the changes section

4. if you want to recover or revert a commit that u have deleted u can find it by the
- first step : git reflog 
- second step : take the id of the commit u want to recover 
- third step : git --hard (enter the id);
- when u are using this method make sure that your code stays in the local and not push to the GitHub

5. git checkout head - this code will point out to the current directory u are

6. git checkout head~0 - this code will point out to the current directory u are

7. git checkout head~1 - head section will step down to the below directory from the current directory

8. git revert (id) - 

9. git revert head3..head

10. git revert --no-commit head~5 

11. git revert --continue => 	


12. if u want to revert 2 or more from above to below : use like this  = git revert head~3..head

13. if u want to revert 2 or more from above to below at once : use like this  = $ git revert --no-commit head~2..

14.  if u want to abort the commit use : git revert --abort

15. if u want to continue the commit : git revert --continue 