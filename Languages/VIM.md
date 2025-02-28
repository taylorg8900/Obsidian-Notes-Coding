# [eriks talk from 2015](https://www.youtube.com/watch?v=MquaityA1SM)

things i want to know more about
- how to use whatever the vim-like-mode stuff in IDE's is
- using vim to navigate between multiple files in the shell
- multiple cursors

help commands
- `:help regexp` for example

Regular expressions
- `:help regexp`
- regexes
- find what you are looking for, count how many times it occurs, make many tedious changes in one shot
- use `/` to search for something, and use `n` to find next occurence
- use `:%s/target/replacement` to replace words

Marks
- `:help marks`
- keep track of interesting places in the file
- set mark with `m[a-z or A-Z]` command, can be one of the 26 letters
- go to marks with `'{mark name}`  
- uppercase marks persist between files
- must be in normal mode, and vim will not tell you that it set the mark successfully, but you can check with `:marks`

Ex commands
- not really sure about any of this, but `:help range` seems useful

Registers
- copy and paste / clipboard
- `:help registers` 
- i think the @ sign is how you call macros? or something
- feel like im getting lost, this all seems really cryptic and complicated

count, operation, motion

splitting windows
- ctrl + w + s = split a file into two windows
- ctrl + w + v = split vertically
- navigate between them with ctrl + w + h/j/k/l like normal vim navigation, or do ctrl + w + w to 'alt tab'
- ctrl + w + o = make the current window the only one

visual mode
- 'a flexible and easy way to select a piece of text for an operator' 'it is also the onl yway to select a block of text'
- multiple cursors
- probably have to google this one, wasn't expanded upon that much in the talk in terms of how to actually do it