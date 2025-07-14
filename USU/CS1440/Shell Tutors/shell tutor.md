'tutor hint' command if ever get stuck
'tutor bug' if bug
files are in my user/Taylo folder
'sh tutorial.sh' to run it i think could be wrong
./tutorial.sh

important things
	commands
		cat FILENAME
		clear
		reset (when terminal is corrupted)
		ctrl C
		less FILENAME (pager command)
		man COMMAND_NAME
		nano
		git status
		git add
		git commit -m "message"
		git push
		



lesson 1
	Unix CLI environment is called the #term Shell
		prioritizes interactivity, designed tobe easy to type
		commands have short names, minimal puncuation required, only string data type
	commands
		have structure -> command \[argument ... ]
		spaces separate arguments from each other, not commas
		echo 
			like print() in python, having 0 arguments prints empty line
		ls
			lists files
			can take an option '-a' to make it show ALL files, even hidden ones
		cat
			short for 'concatenate'
			meant to join several files into one
			takes as arguments names of files and prints their contents onto the screen
			#important standard text viewer in unix
		clear
			just clears screen, like ctrl L in visual studio code
		reset
			makes terminal re-initialize itself
			takes no arguments
			use when terminal gets corrupted
		Ctrl-C
			cancel current running program, like when infinite loop same as in visual studio code
	dotfiles
		file names starting with a dot '.' are hidden by ls command
		user now use this bug to clean up home directories by keeping files out of sight
	corrupted terminal
		shit looks crazy bro
		type reset (even though it won't look like you're typing anything legible)
	common errors
		"no such file or directory"
		"permission denied"
		"command not found"
	summary
		using the unix CLI
		commands and arguments
		hidden files
		difference between shell and terminal
		how to clear and reset terminal
		CRTL C to cancel a runaway command
		understanding messages and recovering from errors
lesson 2 - commands
	if you cat a really big file it will flood the screen and show you the stuff at the bottom which is annoying
	commands
		#important less
			a program called a 'pager', like 'cat' command, but only shows one page at a time and waits for you to hit a button fbefore showing the next page
			can scroll with keyboard
			press q to quit
			press j or down arrow to scroll down by one line
			press k or up arrow to scroll up by one line
			presss spacebar to scroll down by one page
			h opens help screen q closes it again
			called less because first version of it was called more, but didn't support scrolling back
		man
			system manual
			when you install programs the most up to date instructions are installed at the same time
	options
		command line arguments beginning with a '-'
	man cat -1 -S for example
	man -k manual
	apropos
		replacement for google
	summary
		write and run even more complicated commands
		use the less pager to read large documents in the terminal
		learn the difference between arguments and options
		find out how to get help in the shell
lesson 2 - files
	will learn how to: 
		make copies of files
		move and rename files
		take advantage of tab completion
		remove files
		refer to multiple files with wild cards
	#important he did some black magic and opened up file explorer where we are in the lesson? how he do that? must find out
		#important 'start .'
		might be the coolest thing so far tbh that is crazy
	commands
		cp
			copies one file and pastes it with the name you specify
			example: cp text1.txt text2.txt <- will create text2.txt in current directory as a copy of text1.txt
		mv
			moves from SOURCE to DESTINATION
			mv SOURCE DESTINATION
			basically makes a copy, pastes it, and removes the original
			how we rename files also
		rm
			remove/delete
			rm \[-f] FILENAME
			#term wild card
				a command line pattern that is replaced with matching filenames
			wild card with rm is \*
				rm \*.txt = run rm on all files ending with .txt
				rm l\*.txt = run rm on all files beginning with the letter l and ending in .txt
				rm \*t\* = run rm on all files with t anywhere in their name
				rm \* = rm on every file
			include '-f' as an option to force delete instead of having to hit 'y' after every delete, good to know
	#important tab
		autocomplete lets go baby
		saves a lot of typing
	#important USING RM IS PERMANENT, NO RECYCLE FOLDER OR ANYTHING
lesson 3 - directories
	will learn how to:
		navigate directories
		create new directories
		remove empty directories
		forcibly remove directories without regard for their contents
	commands
		cd
			use to go into directories
			can also include mulitiple subdirectories with forward slashes if you already know where to go
			'cd ..' to go back by one directory
			#important'cd' alone takes you back to home directory
			~ is short for home directory, if you say cd ~/Desktop for example it will do that
			'cd -' takes you back to previous directory, like hitting back button in web browser
			'/' is the rootmost directory in unix, typing 'cd /' takes you there
		mkdir
			mkdir \[-p] DIRECTORY
			-p option is telling it to make parent directories as needed, for when you are making multiple parent/child directories
			such as mkdir -p dir1/dir2
		rmdir
			if you want to delete a directory and all of it's children, use rm -r 'exampledir' to recursively delete everything in there
			use rm -rf, rm -fr, rm -r -f, rm -f -r to delete absolutely everything without getting a confirmation message
lesson 4 - projects
	will learn how
		create and edit text files with the nano editor
		organize files into directories
		follow the duckiecorp standard project structure
		run unit tests and interpret their results
		write project documentation
	nano
		text editor, apparently goated to know since you can use it anywhere and it isnt exclusive to anything
		shortcut keys
			^ is ctrl
			M- is Alt
		bunch of shortcuts at the bottom
	Software Development Plan
		req for every assignment in class
	Workflow for DuckieCorp
		set up work environment
		run tests
		locate bugs
		plan and document fix
		perform fix
		re run tests to see that the bug is truly squashed and to ensure no new bugs were introduced
		update projects documentation
lesson 5 - ssh key
	will learn
		create an ssh key with ssh-keygen
		learn what an ssh key is and how to put it on gitlab
		test that your ssh key is correctly set up with ssh
	ssh
		Secure SHell
		essentially lets you run commands on a remote computer, obviously needs a secure connection
			will do a lot of this once you use git
		serves as both username and password when connecting to gitlab from command line
		#important ssh-keygen -t rsa -b 2048
			-t rsa = create a key with the RSA encryption algorithm
			-b 2048 = 2046 bit random number
		creates public and private key, can give the public key to any computer you want to communicate with and when you connect to it with ssh your private and public keys are checked = secure
		create a new one for each device you want to use on gitlab, can return to lesson for it
lesson 6 - GIT
	LETS FUCKING GOOOOOOOOO
	will learn
		prepare git on compooter
		ask git for help about its commands
		clone a repo onto compooter
		check status of repo
		change a file and commit to repo
		view the git log
		submit homework to gitlab
	whats git
		system of programs that manage a repo
	how use git
		always have 'git' as command
		first argument to git is the name of a #term subcommand
		'git SUBCOMMAND \[arguments ... ]'
	git commands
		git help <- this shows up in browser lol i think it still works without internet tho
			if you want to know more about a specific subcommand do git help SUBCOMMAND, like git help help
		git status
			tells you if you are in a repo, is good to spam this
		git clone
			1) git clone https://... \[DIRECTORY]
			2) git clone git@... \[DIRECTORY]
		git restore
			git restore FILENAME
			restores a file to how it was initially on that branch
			undo button basically
		git add
			git add FILENAME
			first part of committing something
		git commit
			git commit \[-m "commit message example]
		git log
			shows histroy
			uses same system as man command if too much on screen, which means scroll with j and k, quit with q
		git remote
			tells URLS that this repo can fetch and push to/from
			git remote -v
			git remote rename OLD_NAME NEW_NAME
		git push
			git push \[-u] REPOSITORY \[--all]
	sharing projects
		1) directory of files managed by Git is called a repository
		2) cloning downloads a Git repo onto your computer
		3) pushing uploades your repo to another computer
	commits
		0) changes made to files in the project (identified by git add)
		1) your name (set with git config)
		2) your email address (set with git config)
		3) the currrent date and time
		4) a brief message describing what you changed and why
	remote repos
		have #term nicknames because typing URLS is not gonna happen lol
		custom to use 'origin' for the URL that you use most frequently (should point to gitlab acct)
lesson 7 - workflow
	markdown files
		nano README.md
			add these md features to it
				headings lvl 1 and lvl 2
				bold text
				bulleted list
				inline code (not a code block)
				pre formatted block (code block)
	questions to ask when bugs appear
		1) do i really know what the code should be doing?
		2) am i sure that this program isnt already doing the right thing?
		3) what does the right thing look like?
		4) assuming that i know what the program should do, can i point to the lines that are wrong?
		5) if i am able to point to the problem, do i even know what "better" code would look like?

md files
	headings
		preface with hashes \#
		more hashes = more smaller
	line breaks
		end a line with two or more spaces, then hit enter
	bold 
		\*\*bold text\*\*
	italicize
		\*italicized text\*
	blockquote
		> paragraph that includes blockquote
		> and another line that is part of that blockquote
		>> and a nested blockquote inside the first one
	list
		-
		-
		1.
		2.
	
		
	