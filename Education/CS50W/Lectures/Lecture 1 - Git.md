Anything that isn't already contained inside of cs1440 will be here (and probably added there too)

Typing `code .` in the terminal will open the current directory in vscode

`git commit -am` will add all currently tracked files and add to staging branch, ignoring untracked files

Example of a merge conflict:
```commandline
a = 1
<<<<< HEAD
b = 2
=====
b = 0
>>>>> 57656c636f6d652074.... (conflicting commit)
c = 3
d = 4
```

Everything between `<<<<<` and `=====` is from your changes, and between `=====` and `>>>>>` is what exists on the remote branch

`git reset` is how you go back to a previous commit
- `git reset --hard [commit]` to go back to a specific commit
- `git reset --hard origin/master` to go back to what is on the remote

## Git Branches

Common Commands
- `git branch` tells you what branch you are currently on
- `git checkout -b [new branch name]` creates a new branch with `-b` flag
- `git merge [other branch name]` will take your current branch, and merge another branch to it

## GitHub Features

***Forking*** on GitHub lets you clone the repository to your account (not just downloading the code to your computer), and lets you open a pull request so you can contribute to codebases

***GitHub Pages*** lets you deploy a website with a naming like `bpy28.github.io` so anybody can see it