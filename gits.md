# My notes on Git  

## Git cherry picking
Check git logs:
>$ git log --oneline
Check what the logs contain:
>$ git diff <commithash>
**Never ever merge a feature branch into another feature branch, only ever branch off the development branch.**
1. Branch off (choose commit to cherry pick to the other branch)
2. >$git cherry-pick <commithash> (obs, only works if you have no conflicts with parent branch)
3. >$git log --oneline (check if this worked)
4. Git commit for cheery pick
5. Repeat to add all cherry-picks needed i.e. $ git cherry-pick <commithashofchoice>
!!Avoid adding already merged commits.
6. >$ git push origin/pia <newbranchname>_<existingbranchname> --force
i.e. merge with force push changes into old branch

# Pull Requests  
- After forking from the other repo to your own repo, copy url and git clone into a new local repo. 
- **Always** bundle the downloaded Rails project file.  
- Run rails db:create db:migrate (in most cases, you will only need to run db:migrate. Run db:create in case no database has been created).  
- Create new development branch and check into it.
- Add upstream as a remote using the remote URL. 
- Push the repo to your own remote repo
- Create new branch for each feature you work on; one user story = one feature and one pull request.  
- Every time code is merged; you need to notify your team to pull from upstream.  
- Track the other persons branch:
1. git fetch <other_person>
2. clone name of his/her branch <other_person/branch_name> as:
git checkout -t <other_person/branch_name>
=> Then git will notify you if the person makes changes in the branch!!
- Always run **$ rake** before pushing to make sure all tests are passing.
- Use poertry mode: omitting parenthesis in one place, means you should do that everywhere etc.  
- Do not use old Ruby syntax:
```rb
fill_in field, :with => content
vs
fill_in field, with: content
```
- 

# Pivotal tracker  
**ice box:** +add story
**name** it e.g. Login
**descrition:** user story
**tasks:** feature test (we do not need to have unit test for this one because we are not saving any information, we are just using the available information)  
**activity:** comments that are useful for the rest of the team.

Drag stories to backlog manually. MAX 4 backlogs currently working on.

Then:
current iteration/backlog + start + unestimated + finished
once merged: deliver! + accept button ok for now


## Git commands in the terminal   

To create a longer, more structured commit message using VSC: 

Remove a remote git user
```
$ git remote remove <username>
````

```
$ git commit
```
To check who is remotely added to you
```
$ git remote -v
```
To check your git stashes:
```
$ git stash list
```
To erase all of your git stashes:
```
$ git stash clean
```
To set the current branch HEAD to the commit you want:  
```
$ git reset --hard <commit hash>
```
To add unneccessary things to your .gitignore file:
```
$ echo -e "node_modules/\n.DS_Store\n.vscode\n"
```

## Fork a repo and create a common pull request  
1. Fork a remote repo of choice.  
2. Clone it to your local repository using
```
$ git clone <remote_repo_url>
```
3. Create a new branch and checkout from the master branch
```
$ git checkout -b <new_branch_name>
```
4. Add changes, commit them and push to own remote
```
$ git push origin <new_branch_name>
```
5. Go to your own remote repo on GitHub and create a new pull request. Make sure to use your own forked master as the base and your new branch to merge. Then create the new pull request, using the 'create new pull request'-button.  
6. Add your title and message to the request and confirm using 'create new pull request'-button and then 'merge to master'-button. This merges the pull request with the master.  
7. Switch back to the master branch 
```
$ git checkout master
```
8. Pull the merged master branch
```
$ git pull origin master
```
9. Create a new branch
```
$ git checkout -b <new_branch_name>
```
10. Add your team mate as a remote
```
$ git remote add <team_members_name> <team_mates_github_branch_url>
```
10. Pull your team mate's branch
```
$ git pull <team_members_name> master
```
11. Resolve the merge conflict!

## React as a dependency  
Initialize React (npm i -S is the equivalent to npm install --save.):
```
$ npm i -S react react-dom
```
***JSX is a shorthand for calling React.createElement function.***

Install React Router:
```
$ npm i -S react-router-dom
```

## It's all about the Babel  
* @babel-core is the main Babel package.
* @babel-cli lets you compile files from the command line.
* @preset-env preset transpiles ES6 into more traditional JavaScript (ES5). 
* @preset-react preset transpiles JSX into more traditional JS (ES5).  

Use if Yarn security threat when using older packages (eslint-utils error on GitHub):
```
yarn add eslint-utils@^1.4.1:
``
Add axios library to read JSON file: 

```
$ npm i -S axios
```

## PSQL  
open database: 
```
$ psql <database_name>
```
find databases:
```
$ psql -l
```
close database:
```
$ \q OR ctrl+d
```