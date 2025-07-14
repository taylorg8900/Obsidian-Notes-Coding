git diff master
- 'red text are lines to erase from the master version to make it become like the current code'
- 'greeen text are lines that need to be added to the master commit to make it the same as HEAD'

git show
- shows the commit ID + author ++ commit date + commit message + everything that git diff does
- without arguments shows all of this compared to previous commit

git checkout HEAD~
- can will take you to previous commit
- can put a number after the squiggly to make it go further, like `git checkout HEAD~3` will go back 3 commits

git diff
- so when you are on a commit, I will say 'current-checked-out-commit' and you do git diff on some other commit, I will say other-commit, this is how the colored text works
	- red text needs to be deleted from the 'other-commit' version to make it match the 'current-checked-out-version'
	- green text needs to be added to the 'other-commit' to make it match the 'current-checked-out-version'

git branch
- by default only shows local branches
- until a branch is checked out on your local machine, it is a 'remote-tracking-branch'
- `git branch --all` shows all branches

git show-branch
- honestly have no idea what the fuck I am looking at here so I will take many notes for future reference
- stuff above '-----' names local branches, has a symbol that is colored in a certain column, and if you look down you can see commits belonging to each branch. they have the same color and are only in the same column as the symbol
- the `*` symbol is the currently checked out branch, and the `!` symbol are just other branches
- the bottom most line is the common ancestor of all of the branches, and anything under it is left out so you don't have a million little plus signs everywhere

git merge BRANCH_NAME
- new commits from BRANCH_NAME become a part of the currently checked out branch
- `git merge --no-edit BRANCH_NAME` makes it so that git automatically makes a message for the merge and doesn't open an editor for you to provide the message
