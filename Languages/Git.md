(i know git isnt a language bit whatever)

apart from obvious stuff i already know, here are some other useful things
- git show -> view last commit details
- .gitignore file: put stuff in here to not get tracked, obvious but i wasnt using this for notes and i should have been
- git reset \<file\> -> remove file from commit but keep changes

# Branches

How to create a new branch
- `git branch NAME` to create a new branch
- `git checkout -b NAME` to create a new branch and also switch to it

How to switch branches
- `git checkout NAME` to switch to a branch

How to view branches
- `git branch` will show you your local branches
- `git branch --all` shows all branches
	- important because if you download a project, the branches on it are 'remote tracking' until they are checked out on your computer

How to merge branches
- `git merge BRANCH` wil make commits from the BRANCH a part of the currently checked out branch
- `git merge --no-edit BRANCH` will make git automatically create a message for the merge, doesn't open the editor

