
# output examples
what each tool should be doing

understand what kind of output each tool makes when given good inputs, and bad inputs

cat
- What it does: concatenate one or more files into one output on the screen, in the order they are given as arguments
- accepts any number of filename arguments greater than 0

tac
- What it does: works just like cat, but each file's information is printed out backwards. The files are still printed in order of the arguments given, but their contents are reversed

nl
- What it does: works like cat, but adds line numbers on the left side of the output. *The count does not restart when a new file is encountered.*
- by default, only non-blank lines are numbered. Blank lines are printed without a number and the count does not increase
- blank lines are counted when `-ba` option is given

paste
- joins files together by inserting commas in between the lines of each file. For example, the first lines from each file all get pasted together in one big 'super line' for line 1. line 2 would be a 'super line' consisting of each second line from each file, printed next to each other with a comma in between them.
- useful with CSV files specifically

cut
- prints out specific columns from a CSV file
- use the `-f` flag to specify which column to extract by it's position, or multiple specific columns

grep
- searches for any lines in the file that has the characters we give as an argument
- can also do the opposite, where it searches for any lines in the file that don't have the characters we give

head
- prints the first 10 lines of a file
- can print out more or less than 10 lines, if `-n` argument is given
- if multiple files are give, identify each with a banner that looks like `==> FILENAME <==`

tail
- prints the last 10 (or N) lines of a file
- if multiple files are give, identify each with a banner that looks like `==> data/filename <==`

sort
- prints all contents from file in lexical order
- if mulitiple files given, all lines are mixed together into one sorted output

wc
- word count
- outputs: lines, words, character, filename