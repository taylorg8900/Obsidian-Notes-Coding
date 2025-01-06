more specialized than python or C
domain specific language, with databases
#term flatfile database
	just using a text file
	need a way to dileneate the information in the file
	#term CSV files - comma separated values
		data stored row by row and line by line, columns are separated by commas
		can export things like excel files into csv because its just rows and columns really
		first row are the headers for columns, special
			#term metadata
		having a comma within double quotes ignores it so it isnt accidentally taken as a new column
		import csv in python, for built in support and functions like csv.reader()
how do we make sure we are accessing the correct columns in the csv file, even if the data has been shifted around?
	turn it into a dictionary, and use strings to access the columns instead of accessing by index or something
sorted function in python for sorting dictionaries
	can give it an argument for what the key is as well, or reversing the order
#term relational database
#term SQL
	Structured Query Language, specifically designed for databases
	supports 4 key pieces of functionality, referred to as #term CRUD
		C - create, create data in a database
		R - read, access data from the database
		U - update, change data in the database
		D - delete
		CREATE, INSERT
		SELECT
		UPDATE
		DELETE, DROP
#term tables
	what the data in databases are stored inside, has rows and columns
sqlite3
	stores all data in a file on hard drive or in the cloud
	just a more lightweight version of SQL that is used in cs50 and a lot of other mini use cases for it
	sqlite3 FILE, like sqlite3 favorites.db 
		.mode csv
			having a period at the start is specific to sqlite, and saying csv is specifying what type of file we are going to import
		.import favorites.csv favorites
			we already have favorites.csv, and we want to create a table names "favorites" to store it in
		.quit
			gets you  back to the dollar sign prompt in the vs code shell
		.schema
			tells you the structure of the sql file, and tells you the type datatype of the headers
		example on how to access data: SELECT columns FROM table;
		SELECT \* FROM favorites;
			the \* is basically saying get all of the columns
		SELECT language FROM favorites;
built in functions
	AVG
	COUNT 
	DISTINCT
	LOWER
	MAX
	MIN
	UPPER
	\*
		gets everything
	%
		used with LIKE, to represent 'something' so to speak
	etc
	examples of usages
		SELECT COUNT(\*) FROM favorites;
		SELECT DISTINCT language FROM favorites;
			gives you the different unique values for what is in the language column
		SELECT COUNT(DISTINCT language) FROM favorites;
use single quotes in sqlite for strings, not double quotes
other keywords
	GROUP BY
	LIKE
	LIMIT
	ORDER BY
	WHERE
	example usages
		SELECT COUNT(\*) FROM favorites WHERE language = 'C';
		SELECT COUNT(\*) FROM favorites WHERE language = 'C' AND problem = 'hello world';
		SELECT COUNT(\*) FROM favorites WHERE language = 'c' AND problem LIKE 'hello, %';
		SELECT language, COUNT(\*) FROM favorites GROUP BY language;
		SELECT language, COUNT(\*) FROM favorites GROUP BY language ORDER BY COUNT(\*) DESC;
#important to avoid the program having a single quote mess things up, instead of escaping using a backslash, use two single quotes together to denote that you only want one of them to be there
	super weird but it is what it is

next day
giving aliases in sql
	use something like AS n
using LIMIT
	just say LIMIT 1/2/3 whatever to get only 1/2/3 results
using INSERT
	INSERT INTO table (column, ...) VALUES(value,...);
using DELETE
	DELETE FROM table WHERE condition;
		like WHERE Timestamp IS NULL; for example
	#important dont ever say DELETE from table; because it will delete everything lmao
using UPDATE
	UPDATE table SET column = value WHERE condition;
	UPDATE favorites SET language = 'SQL', problem = 'Fiftyville'

IMDb
	in the world of relational databases, it is good practice to hvae separate 'bricks' of info in separate tables, like shows/people/stars (entities)
	also good practice to assign things IDs, a number
		this is so we use ints and not strings, more lightweight
	#term one-to-one 
		each show only having one rating for example
	#term one-to-many
		each show having multiple genres
	data types during CREATE
		INTEGER, NOT NULL, NUMERIC,  TEXT, REAL(which is like a float), BLOB (binary large object), UNIQUE
		PRIMARY KEY(id), 
		FOREIGN KEY(show_id) REFERENCES shows(id)
			where show_id is the name of the key here, and shows is the name of the table  we are pulling the id from
	#term nested query
		using the output of one query as an input to another query
		#important if you hit enter without putting a semicolon, you can have multiple lines to avoid wrapping
	JOIN
		joining two tables together
		SELECT \* FROM shows JOIN ratings
			how do we tell where we want to 'join' or stitch together the things?
		SELECT \* FROM shows JOIN ratings ON shows.id = ratings.show_id
		SELECT \* FROM shows JOIN ratings ON shows.id = ratings.show_id WHERE rating >= 6.0 LIMIT 10;
		SELECT title, rating FROM shows JOIN ratings ON shows.id = ratings.show_id WHERE rating >= 6.0 LIMIT 10;
indexes
	can create indexes to speed up querying
	CREATE INDEX title_index ON shows(title);
		don't really get how this worked, uses trees somehow and its super fast
	.timer on
		sqlite command that tells you how long a query takes
	#term B-tree
		NOT  a binary tree
		essentially very wide, and not tall so the distance between the root node and leaf nodes is very short
using python and SQL
	from cs50 import SQL
	[cs50 SQL documentation](https://cs50.readthedocs.io/libraries/cs50/python/#cs50.SQL)
	? is a placeholder we use, because we don't use f strings for some reason
		include a second argument in the .execute method to tell it what the ? is 
	.execute method to be used on the return value of SQL(file)
race conditions
	jugs of milk example 
	changes to a database at the same time
	functionality in SQL
		BEGIN TRANSACTION
			dont make any changes until a query is done
		COMMIT
			at the end of the block that started with BEGIN TRANSACTION
SQL injection attacks
	similar to prompt injection attacks on AI where people try to get the AI to misbehave with specific inputs
	"--" is the start of a comment in SQL 
	using a f string in python lets it get fucked up because if a single quote is part of the variable within brackets, it breaks everything lol
	"'--" breaks f strings in SQL lines, because the first \' closes an f string and -- makes everything else a comment
typical order of queries
	SELECT, FROM, JOIN, WHERE, GROUP BY, HAVING, ORDER BY