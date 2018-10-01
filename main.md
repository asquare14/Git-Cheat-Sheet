# GIT CHEATSHEET

## Initializing Git
These commands are related to the inizialitazion process for git repositories on your local machine.

`$ git init`
- It will create a new git repository in the current directory.

`$ git init --bare`
- It will create a new bare repository.

A bare repository is a bit different from a regular one, it doesn't .git folder, history is stored in the project root, also if you try to `git clone --bare` from a remote repository (e.g. github) you will lost track of it's origin since usually bare repositories are supposed to be served at the users as remote endpoints.

## Cloning Repositories

`$ git clone <link to repo>`
- Clones repository to local machine.

### Shallow cloning
`$ git clone <link> --depth=1`

Git supports the notion of a “shallow clone”, which is a more succinctly meaningful way of describing a local repository with history truncated to a particular depth during the clone operation. By providing an argument of --depth 1 to the clone command, the process will copy only the latest revision of everything in the repository. This can be a lifesaver for Git servers that might otherwise be overwhelmed by CI/CD automation.

## Common local commands
`$ git log`
 - Shows history of past commits

`$ git log --oneline`
 - Shows history of past commits in summary which contains only commit id and commit message. 

`$ git status`	
 - Shows the last modified files 

`$ git stash`	 
 - Git stash temporarily shelves or stashes changes made to your working copy so you can work on something else, and come back and re-apply them later on.

`$ git stash pop`	 
 - Get back stashed commits
 
`$ git stash list` 
 - Lists all stashed changesets
 
 `$ git stash drop` 
 - Discards the most recently stashed changeset
 

`$ git commit --amend -m “updated commit msg”`	
 - Updates commit message

`$ git commit --amend --author “new author name <new author’s email id>”`
- Update the author of that commit        

## How to commit changes to a particular branch .

`$ git add .` or `git add -A`
 - Add all untracked files.

`$ git commit -m “name of commit”`
 - Commit Files

`$ git commit --amend (if you want to amend your commit message)`
 - If you want to edit your commit message.

`$ git push origin <branch name>`	
 - (eg: $ git push origin master). Push your changes.

## Commands related to branching
It is a good practice to make a new branch for every new PR you make. Also,name the branches according to the work you are doing. It will be easier.

`$ git checkout -b mybranch`
 - Creates a new branch named mybranch.

`$ git checkout mybranch`
 - Move to a different branch. 

`$ git branch`
- Check if you're on the right branch. Now,you’re on the new branch ! Commit your changes here.

`$ git branch -d branch-name`
- Delete branch temporarily

`$ git branch -D branch-name`
- Delete branch permanently

`$ git merge branch-name`
- Merge branch with the current branch.

## Squashing X commits together

`$ git rebase -i <after-this-commit>`	  
- Eg: ( $ git rebase -i HEAD~2 ) => (rebasing 2 commits starting from HEAD)
- Then edit the ‘pick’ to ‘squash’ in front of all those commits which you want to squash.
- Commit your new squashed commits.

## Removing a commit from in between the commit history

  If you need to delete more than just the last commit use rebase.

  Example-

  Number	Hash	    Commit Message	
  1	     2c6a45b	 (HEAD) Adding public method to access protected method	
  2	     ae45fab	 Updates to database interface	
  3	     77b9b82	 Improving database interface	
  4	     3c9093c	 Merged develop branch into master	
  5	     b3d92c5	 Adding new Event CMS Module	
  6	     7feddbb	 Adding CMS class and files	
  7	     a809379	 Adding project to Git	

  Using the git log above we want to remove the following commit; 2 (ae45fab).

  `$ git rebase --onto <branch name>~<first commit number to remove> <branch name>~<first commit to be kept> <branch name>`

  e.g to remove commit 2 above

  `$ git rebase --onto repair~2 repair~1 repair`

## Making sure your repository is up-to-date with the original/upstream repository
Note: `< >` should not be included in commit message. Example, `git fetch upstream master`.

`$ git remote add upstream <link of original repo>`
 - Note that "upstream" is the name I chose to give the repo, you can name it anything. 

`$ git fetch upstream <branch name>`
 - Fetch the latest changes. Alternatively, you can do `git pull upstream <branch name>` but it adds an extra merge commit.

`$ git rebase upstream/<branch-name>`	
 - Puts your changes on top.

`$ git push origin <ur branch-name u want to push to> --force` 	

`$ git log`
 - To make sure rebase is done and you can see the commits.
 
 `git diff origin/master`
 - See differences between local changes and master


## Rebasing
`$ git rebase --abort`	
 - To quit the rebase process
 
`$ git rebase --continue`	
 - To finish the rebase process

## How to undo a mistaken git rebase
- To undo a rebase, first find the head commit of the branch before the rebase began:

`$ git reflog <branch-name>` 

`>> 73d836b testBranch@{0}: rebase finished: refs/heads/testBranch onto e806e41f1fe22624e6546abd65c332c934214891`

`>> 129e6d3 testBranch@{1}: commit: some sort of commit message`

- Then return to that commit using `git reset`

`$ git reset --hard <commit>` 		

- For example, in this case the command would be

`$ git reset --hard testBranch@{1}`

### Checking the difference between any two particular commits 

`$ git diff <commit-id> <commit-id>`	
 - To check difference between any two commits by using their commit id. One can also use short git commit id which is provided by using `$ git log --oneline'` command

`$ git diff <commit-id>`
- To check difference between the latest commit relative to a particular old commit.

`$ git diff --cached`
- To check difference between changed staged for the next commit relative to the latest commit.

`$ git diff --cached <commit-id>`
- To check difference between changed staged for the next commit relative to a particular commit.

