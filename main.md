## GIT CHEATSHEET

### Common Commands

`$ git init`
- Initializes a new Git repository on local machine.

`$ git clone <link to repo>`
- Clones repository to local machine.

`$ git log`
 - Shows history of past commits

`$ git status`	
 - Shows the last modified files 

`$ git stash`	 
 - Git stash temporarily shelves or stashes changes made to your working copy so you can work on something else, and come back and re-apply them later on.

`$ git stash pop`	 
 - Get back stashed commits

`$ git commit --amend -m “updated commit msg”`	
 - Updates commit message

`$ git commit --amend --author “new author name <new author’s email id>”`
- Update the author of that commit        

### Shallow cloning
`$ git clone <link> --depth=1`
- Git supports the notion of a “shallow clone”, which is a more succinctly meaningful way of describing a local repository with history truncated to a particular depth during the clone operation. By providing an argument of --depth 1 to the clone command, the process will copy only the latest revision of everything in the repository. This can be a lifesaver for Git servers that might otherwise be overwhelmed by CI/CD automation		

### How to commit changes to a particular branch .

`$ git add .`
 - Add all untracked files.

`$ git commit -m “name of commit”`
 - Commit Files

`$ git commit --amend (if you want to amend your commit message)`
 - If you want to edit your commit message.

`$ git push origin <branch name>`	
 - (eg: $ git push origin master). Push your changes.

### Commands related to branching

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

### Squashing X commits together

`$ git rebase -i <after-this-commit>`	  
- Eg: ( $ git rebase -i HEAD~2 ) => (rebasing 2 commits starting from HEAD)
- Then edit the ‘pick’ to ‘squash’ in front of all those commits which you want to squash.
- Commit your new squashed commits.

### Removing a commit from in between the commit history

`$ git reset --hard <sha1-commit u want to remove-key>`

`$ git push origin <branch> --force`

### Making sure your repository is up-to-date with the original/upstream repository.

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


### Rebasing

`$ git rebase --abort`	
 - To quit the rebase process
`$ git rebase --continue`	
 - To finish the rebase process

### How to undo a mistaken git rebase

- To undo a rebase, first find the head commit of the branch before the rebase began:

`$ git reflog <branch-name>` 

`>> 73d836b testBranch@{0}: rebase finished: refs/heads/testBranch onto e806e41f1fe22624e6546abd65c332c934214891`

`>> 129e6d3 testBranch@{1}: commit: some sort of commit message`

- Then return to that commit using `git reset`

`$ git reset --hard <commit>` 		

- For example, in this case the command would be

`$ git reset --hard testBranch@{1}`

### How to turn a folder into a repository
This is useful if you have a network drive, and wish to keep your own "local" git server.

Go to the folder you wish to use as a repository
`$ git init --bare`

Now you can clone that repository from another folder as so

`$ git clone U:\\Development\\MyProject`