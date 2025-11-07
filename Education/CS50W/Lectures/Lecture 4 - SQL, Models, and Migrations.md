Quick summary of opening
- We can store data inside of a relational database, using tables (composed of rows and columns)
- Each column in the table is called a field

Types in SQL
- TEXT - Strings
- NUMBERIC - Things similar to numbers, such as dates
- INTEGER - Integers including negative
- REAL - Numbers that have decimals
- BLOB - Stands for Binary Large Object, lets you store things like audio files

Types in MySQL
- This has a lot more types
- CHAR(size) - Lets you allocate a specific amount of characters for strings
- VARCHAR (size) - For strings that will be up to a certain amount of characters
- SMALLINT
- INT
- BIGINT
- FLOAT
- DOUBLE - These all use different amounts of bytes

Commands we can execute on our database
- `CREATE` lets us create our table

Example with explanation
- [SQL Contraints](https://www.w3schools.com/sql/sql_constraints.asp) are things like `NOT NULL`
-  [Normal Forms](https://en.wikipedia.org/wiki/Database_normalization) for information on best practices for organizing data in databases (referencing DATA3300)
- Each comma separated value is a field in the table
- `PRIMARY KEY` is the way that we uniquely identify each flight
- `NOT NULL` lets us add a constraint, where we make sure that each cell is never empty
- `AUTOINCREMENT` will make SQL automatically create the next ID for us
```MySQL
CREATE TABLE flights (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	origin TEXT NOT NULL,
	destination TEXT NOT NULL,
	duration INTEGER NOT NULL
)
```

Example of `INSERT`
```MySQL
INSERT INTO flights
	(origin, destination, duration)
	VALUES ("New York", "London", 415);
```

Examples of `SELECT`
- Simplest example is `SELECT * FROM flights;` which would just select every single column in the entire table
- `SELECT origin, destination FROM flights;` would only select origin and destination from the flights table
- `SELECT * FROM flights WHERE id = 3;`
- `SELECT * FROM flights WHERE origin = "New York";`

Creating a SQLite database
1. `touch flights.sql`
2. `sqlite3 flights.sql`