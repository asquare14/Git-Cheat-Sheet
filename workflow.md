<!--                     File Style Guide

- One sentence per line: Since Markdown doesn't mind newlines,
- splitting the paragraph into one sentence per line improves 
- readability of raw file while generating the same output

- use grip - https://github.com/joeyespo/grip
- to preview your changes before you submit

- You can find the Markdown cheat sheet here
- https://guides.github.com/features/mastering-markdown/
-->
# Workflow

This file explains the basic GitHub workflow for collaboration.

**TLDR;**
* Fork from `upstream`
* Clone your `origin`
* Make a branch and play in it
* Push your branch to your `origin`
* Make a pull request from your branch in `origin` to master in `upstream`

## Fork a repository

For example, fork this repository - `aSquare14/Git-Cheat-Sheet` and it becomes `your-username/Git-Cheat-Sheet`.
Each developer creates their own forks this way.


`aSquare14/Git-Cheat-Sheet` will be called 'upstream' and your fork is called 'origin', btw.


## Clone your fork

Clone `origin` - _your_ fork to get a local copy on your computer.

`git clone https://github.com/your-username/Git-Cheat-Sheet.git`

## Add the upstream repository as remote

```
cd Git-Cheat-Sheet
git remote add upstream https://github.com/aSquare14/Git-Cheat-Sheet.git
```

This allows you to fetch changes from the upstream and merge them.
You can fetch with `git fetch upstream` and
merge them locally using `git merge upstream/master`.

## Making changes

Whatever change you want to do, do it in a separate branch. Keep your master clean.
To create a new branch, use this command
`git checkout -b branchName`

`git checkout` is a command used to move between branches.
`-b` is a shortcut to create a new branch and move to it.

You can commit in this branch and you can push the branch to `origin`.

## Create a pull request

When you are done with your branch, create a pull request from your branch in origin to master of upstream.

