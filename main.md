# GIT CHEATSHEET

## Help and Documentation
`$ git help <command>`
- Display help information about Git.
- With no options and no COMMAND or GUIDE given, the synopsis of the git command and a list of the most commonly used Git commands are printed on the standard output.
- Note that `git --help ...` is identical to `git help ...`

## Converting a folder into a working Git repository

- For projects using repositories on GitHub
 - `cd <localdir>` to change to the directory you want to use as a repository
 - `git init` to initialize the repository
 - `git add .` to prepare all of the local files to be sent to the remote repository
 - `git commit -m "message"` to name your commit
 - `git remote add origin <url>` to set the remote location of your repository
   - *This can be found on the primary Code tab of a GitHub project on the web. Repositories not hosted through services like GitHub or BitBucket require setting up a git daemon*
 - `git push -u origin master` to submit your commit to the remote repository

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

 `$ git blame <file>`
 - Shows what revision and author last modified each line of a file upto the last commit.

`$ git status`
 - Shows the last modified files

`$ git stash`	 
 - Git stash temporarily shelves or stashes changes made to your working copy so you can work on something else, and come back and re-apply them later on.
 
 `$ git stash save "message"`
 - Same as above but also annotates the stash with a description. This will be shown when running `$ git stash list` and helps provide context if you have multiple stashes at a time.

`$ git stash pop`	 
 - Get back stashed commits

`$ git stash pop stash@{<index>}`
 - Pop only a specific index from the stash. You can find the index by running `git stash list`.

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

`$ git commit -a --amend -C HEAD`
 - Add all the untracked files to the last commit without changing the commit message.

`$ git push origin <branch name>`
 - (eg: $ git push origin master). Push your changes.

## Commands related to branching
It is a good practice to make a new branch for every new PR you make. Also,name the branches according to the work you are doing. It will be easier.

`$ git checkout -b mybranch`
 - Creates a new branch named mybranch.

`$ git checkout mybranch`
 - Move to a different branch.

`$ git checkout -`
- Return to the previously checked out branch.

`$ git branch`
- Check if you're on the right branch. Now,you’re on the new branch ! Commit your changes here.

`$ git branch -a`
- To list all the local and as well as the remote branches.

`$ git fetch -p`
- Delete local branches which doesn’t exist on remote anymore.

`$ git branch -d branch-name`
- Delete branch temporarily

`$ git branch -D branch-name`
- Delete branch permanently

`$ git merge branch-name`
- Merge branch with the current branch.

`$ git mergetool`
- Run merge conflict resolution tools to resolve merge conflicts.


## Renaming branch

If you want to rename branch you have to run this set of commands.

`$ git branch -m old_branch new_branch`
- Rename branch locally.

`$ git push origin :old_branch`
- Then delete the old branch from origin.

`$ git push --set-upstream origin new_branch`
- Push the new branch and set local branch to track the new remote.


## Squashing X commits together

`$ git rebase -i <after-this-commit>`	  
- Eg: ( $ git rebase -i HEAD~2 ) => (rebasing 2 commits starting from HEAD)
- Then edit the ‘pick’ to ‘squash’ in front of all those commits which you want to squash.
- Commit your new squashed commits.


## Squashing all commits up to root

`$ git rebase -i --root master`
- This will ‘squash’ all commits up to Initial (first) commit.


## Removing a commit from in between the commit history

   If you need to delete more than just the last commit use rebase.
  
  Example-

  ```
  commit 1	     2c6a45b	  Adding public method to access protected method(HEAD)	
  commit 2	     ae45fab	  Updates to database interface	
  commit 3	     77b9b82	  Improving database interface	
  ```

  Using the git log above we want to remove the following commit; 2 (ae45fab).
  
  `$ git rebase --onto repair~2 repair~1 repair`
  
  - This command will delete commit 2
  
    Generalized Format for writing command is as follows:
   
  `$ git rebase --onto <branch name>~<first commit number to remove> <branch name>~<first commit to be kept> <branch name>`
  
   - Use rebase tool to rebase a series of commits onto the HEAD they were originally based on instead of moving them to another one.
   
   - Then give branch name along with first commit to be removed.
   
   - Then give branch name along with first commit to be kept.
   
   - Above command could also be used to remove one or more consecutive commits.For example if you want to remove commit 2&3, command        would be as follows:
   
    ` $ git rebase --onto repair~3 repair~1 repair `
     
     
## Going back to a previous commit in commit history
`$ git reset --hard <HEAD^ sha1-commit you want to go-key>`
- The ^ symbol after HEAD defines the selected commit. HEAD is the current one, so for each '^' it goes back 1 commit in history before the current.
- Note that this command will move the HEAD pointer to the specified commit and all uncommitted changes to files will be discarded.

`$ git reset --soft <HEAD^ sha1-commit you want to go-key>`
- The ^ symbol after HEAD defines the selected commit. HEAD is the current one, so for each '^' it goes back 1 commit in history before the current.
- Note that this command will move the HEAD pointer to the specified commit and all files that differ from the version in the selected commit will be moved to the staged area.


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
`$ git reflog <branch-name>`

```
>> 73d836b testBranch@{0}: rebase finished: refs/heads/testBranch onto e806e41f1fe22624e6546abd65c332c934214891

>> 129e6d3 testBranch@{1}: commit: some sort of commit message
```
- Find the head commit of the branch before the rebase began, in this case `testBranch@{1}`

`$ git reset --hard <commit-id>`
- Return to that commit using `git reset`
- For example, in this case the command would be `$ git reset --hard testBranch@{1}`


## Checking the difference between any two particular commits

`$ git diff <commit-id> <commit-id>`
 - To check difference between any two commits by using their commit id. One can also use short git commit id which is provided by using `$ git log --oneline'` command

`$ git diff <commit-id>`
- To check difference between the latest commit relative to a particular old commit.

`$ git diff --cached <commit-id>`
- To check difference between changed staged for the next commit relative to a particular commit ie its `<commit-id>` or `HEAD` if relative to the latest commit.
