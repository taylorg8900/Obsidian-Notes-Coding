how to run query i have typed out in a file
	sqlite3 your_database.db < 1.sql
write a SQL query to list the names of the top 5 longest songs, in descending order of lengt

write a SQL query that lists the names of any songs that have danceability, energy, and valence greater than 0.75.

write a SQL query that returns the average energy of all the songs

write a SQL query that lists the names of songs that are by Post Malon

write a SQL query that returns the average energy of songs that are by Drake.

write a SQL query that lists the names of the songs that feature other artists
- Songs that feature other artists will include “feat.” in the name of the song.
- Your query should output a table with a single column for the name of each song.

In `7.sql`, write a SQL query to list all movies released in 2010 and their ratings, in descending order by rating. For movies with the same rating, order them alphabetically by title.
    - Your query should output a table with two columns, one for the title of each movie and one for the rating of each movie.
    - Movies that do not have ratings should not be included in the result.
JOIN
		joining two tables together
		SELECT \* FROM shows JOIN ratings
			how do we tell where we want to 'join' or stitch together the things?
		SELECT \* FROM shows JOIN ratings ON shows.id = ratings.show_id
		SELECT \* FROM shows JOIN ratings ON shows.id = ratings.show_id WHERE rating >= 6.0 LIMIT 10;
		SELECT title, rating FROM shows JOIN ratings ON shows.id = ratings.show_id WHERE rating >= 6.0 LIMIT 10;