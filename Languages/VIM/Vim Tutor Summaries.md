
# Lesson 1
1. The cursor is moved using the hjkl keys.
	- h (left)
	- j (down)
	- k (up) 
	- l (right)
2. `vim FILENAME <ENTER>` to edit a file with Vim
3. vim
4. To delete the character at the cursor type: `x`
5. To insert or append text type:
	- `i`    insert before the cursor
	- `a`    append after the cursor
	- `A`    append at the end of the line

Pressing `<ESC` will place you in Normal mode, or cancel partially completed commands

# Lesson 2
1. To delete from the cursor up to the next word type:    `dw` 
2. To delete from the cursor up to the next word type:    `de` 
3.  To delete from the cursor up to the next word type:    `d$`
4. To delete a whole line type:                                         `dd`

5. To repeat a motion prepend it with a number:    `2w`
6. The format for a change command is:
	- `operator [number] motion`
7. To move to the start of the line use `0`
8. Undo
	1. To undo previous actions, type: `u    (lowercase u)`
	2. To undo all the changes on a line, type: `U    (capital U)`
	3. To undo the undos, type: `CTRL-R`

# Lesson 3
1. To put back text that has just been deleted, type `p`. This puts the deleted text AFTER the cursor (if a line was deleted it will go on the lines below the cursor).
2. To replace the character under the cursor, type `r` and then the character you want to have there.
3. The change operator allows you to change from the cursor to where the motion takes you. eg. Type `ce` to change from the cursor to the end of the word, `c$` to change to the end of a line.
4. The format for change is:
	- `c [number] motion`

# Lesson 4
1. `CTRL-G` displays your location in the file and the file status.
	- `G` moves to the end of the file.
	- `[number] G` moves to that line number
	- `gg` moves to the first line.


