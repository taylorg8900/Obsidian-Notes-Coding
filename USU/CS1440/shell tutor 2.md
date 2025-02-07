
# shortcuts
shortcuts
	- Ctrl + A : move cursor to start of line
	- Ctrl + E : move cursor to end of line
	- Alt + B : move cursor backward one word
	- Alt + F : move cursor forward one word
	- TAB : autocomplete
	copy and paste
		- Ctrl + W : 'kill' / cut backward from cursor to beginning of word
			- use to delete entire words
		- Ctrl + K: 'kill' / cut forwaard from cursor to end of line
		- Ctrl + Y : 'yank' / paste text to the right of the cursor
		- Ctrl + U: 'kill' entire line, and store in yank buffer
	- Ctrl + L : clear screen, while preserving command line
	- 

notations
	- ^ symbol means CTRL
	- M- symbole means ALT
		Alt key is also called 'Meta'

# redirection
cat
	why doesn't cat change files and actually join them together like its name suggests?
	
redirection
	makes a new file called FILENAME, and sends output there instead of the screen
	add > FILENAME to the command line
	example: cat first.md second.md > final.md
	#important if a file 'final.md' already exists, it will get overwritten completely which is called #term clobbering
	
appending
	adds new content to the end of FILENAME
	add '>> FILENAME' to the command line
	example: 'cat third.md >> final.md'

output
	ordinary vs error output
	ordinary output is also called standard output, or STDOUT
	error output is also called standard error, or STDERR
	'2>' redirects only error messages to a file, leaving STDOUT to the terminal

python
	two 'files' are automatically created each time you run a program, one that corresponds to STDOUT and one for STDERR. The variables that hold these files are in the sys package, named sys.stout and sys.stderr
	print() sends it's output to sys.stdout by default
		can be make explicit by saying print(file=sys.stdout)
	'&>' operator sends both stdout and stderr to the same file
	can redirect stdout and stderr to different places on same command by using both '>' and '2>' together

summary
	\> redirects stdout to a file
	\>> redirects stdout to a file, appends
	2> redirects stderr to a file
	&> redirects both stdout and stderr to a file
	/dev/null : special file that is basically a black hole and eats all info given to it apparently

# submit
process of submitting
	- add files to be committed, using git add
	- commit using git commit -m
	- view where origin URL points with git remote -v
	- rename origin to old-origin by saying 'git remote rename origin old-origin'
	- run 'git remote add origin URL', with origin being the shorthand for our URL, which is the git@gitlab.cs.usu.edu:a02296587/cs1440-Gebhard-Taylor-assn1.1 link
	- run 'git push -u origin master' to submit 