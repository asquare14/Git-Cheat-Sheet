<!--                     File Style Guide

- One sentence per line: Since Markdown doesn't mind newlines,
- splitting the paragraph into one sentence per line improves 
- readability of raw file while generating the same output

- use grip - https://github.com/joeyespo/grip
- to preview your changes before you submit

- You can find the Markdown cheat sheet here
- https://guides.github.com/features/mastering-markdown/
-->

# Git-Cheat-Sheet

## What is Git?

[Git](https://github.com/git/git) is the most widely used modern version control system in the world today.
Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds -
the famous creator of the Linux kernel.

## What is this repo about?

A cheatsheet for git commands. 
[`main.md`](./main.md) contains commonly used git commands. 
[`resources.md`](./resources.md) contains resources for learning git. 

## Contributing

Git-Cheat-Sheet welcomes any contribution. Please refer to our style guide for submitting patches and additions.

### Installation
1. Fork our repo from [here.](https://github.com/aSquare14/Git-Cheat-Sheet)
2. In the console, download a copy of your forked repo with `git clone https://github.com/your_github_username/Git-Cheat-Sheet.git`.
3. Enter the **Git-Cheat-Sheet** directory with `cd Git-Cheat-Sheet`.
4. Make changes to the file you want, commit your changes and submit your Pull Request.

Note: Since this is an active project please rebase from master before submitting a Pull Request to avoid merge conflicts.  

### Style guide
How to add git commands in `main.md`:
 
* **Case 1: The command's category already exists.**  
This should be the markdown format.
```
`$ git command`
- Command Description
```
* **Case 2: The command's category does not exist.**  
This should be the markdown format.
```
## Category
`$ git command`
- Command description.
```

### Tracking Issues

Please post any bugs, questions, or ideas on our
[issues page](https://github.com/aSquare14/Git-Cheat-Sheet/issues). 

### Labelling Issues

If you create an issue, please tag it with the appropriate label. 