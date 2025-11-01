
`aaaaa`
aaaaa
iiiii
`a`a`a`aaaaa
aaaa`aaa`aa
a`aa`aa`aa`a
# Navigation
- Simple navigation
	- `0` beginning of line
- `G`
	- `CTRL-G` to show location in the file
	- `[line number]G` to jump to a specific line
- Searching
	- `/[phrase]` to search for a phrase
	- `?[phrase]` to search for a phrase backwards
	- `n` to jump to next match, `N` to go to previous match
	- `CTRL-o` to jump to previous location of cursor
- Finding
	- `f[character]` to search forward in a line for the first character
	- `F[character]` goes backwards
	- `t[character]` searches like `f`, but stops before the character
	- Repeat with `;` and go backwards with `,` 
- Matching Parentheses
	- `%` to find a matching open/closed `(, [, or {`
- In help pages
	- Using `CTRL-]` on text that looks like `|text|` will take you to a page about that thing *italic*
- Scrolling
	- `CTRL-E` to scroll one line down, `CTRL-Y` to scroll down one line
	- `CTRL-F` to scroll one screen forwards, `CTRL-B` to go backwards one screen
- Centering
	- `zz` centers the cursor
	- `zt` puts cursor at the top
	- `zb` puts cursor at the bottom
# Editing
- Deletion
	- `x` to delete the character under the cursor
	- `d` delete operator
	- `dd` and `D` delete line
		- Will store line in a Vim register (clipboard)
	- `daw` will delete a word, regardless of where the cursor is
		- `aw` is a text object, stands for "A Word"
- Insertion
	- `i`  insert text before cursor, `I` insert text at beginning of line
	- `a` insert text after cursor, `A` insert text at the end of line
	- `o` to open line below cursor, `O` to open line above cursor
- Replacing
	- `r` to replace one character
	- `R` to replace multiple characters
	- `c` is change operator
	- `cc` and `S` delete line and go into insert mode
- Undo
	- `u` undo last command
	- `U` undo entire line at once
	- `CTRL-R` to redo commands (undo undos)
- Substitution
	- `:s/[old]/[new]/g` replaces `[old]` with `[new]` on a line, if the `g` flag is included
		- `:[start line #],[end line #]s/[old]/[new]/g` to replace within a range of lines
		- `:%s/[old]/[new]/g` to change every occurence in an entire file
		- `:%s/[old]/[new]/gc` to change every occurrence in a file, but prompt first
- Copy Paste
	- `p` to put a stored line below cursor
	- `y` copy operator 
- Visual mode
	- `v` starts Visual Selection. You can use operators on selected text
- Join
	- `J` brings the next line up to the current one, and joins them
- `.`
	- Means to repeat the last command


# Misc
- Exiting files
	- `:q!` to quit without saving
	- `:wq` to save and exit
		- `w` stands for "write", and if you type `:write` on its own it will save without quitting
	- `ZZ` saves and exits too
- Operators
	- `d` delete
	- `c` change (delete + place into insert mode)
	- `y` copy operator
- Motions
	- `w` until start of next word, excluding first character
	- `e` to end of current word, including last character
	- `$` to end of line, including last character
- Options
	- You can set options with `:set [option]` and unset them with `:set no[option]`
	- `ic` Ignore case
	- `hlsearch` highlight search
	- `incsearch` 'incremental search', jump to first occurrence immediately
	- `showmode` to always show mode
	- `number` shows line numbers
- `:syntax enable`
	- Vim will automatically detect and show syntax highlighting with this