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

11. if u want to delete a branch = use git branch -d (existing branch name) = eg : git -d feature

12. if u want to rename a branch name = use git branch -M main = eg : main branch name is (master) => after using this master branch name will change into main branch name.

13. if u want to add git file to github first u need to connect with github repo :

- first step : git remote add origin https://github.com/username/practicing-git.git

-second step : 



14. if you want to merge a branch to the main branch = use git merge (mention the file name that you want to merge,) when u are merging the file don't merge the current file , for eg : if u want merge feature in main branch then mention => git merge feature in main branch as the current file.

