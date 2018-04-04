---
layout: post
title:      "SQL: Joining 2 or More Tables"
date:       2018-04-04 16:05:32 +0000
permalink:  sql_joining_2_or_more_tables
---


The joining of two tables in SQL is fairly straight-forward if one of the tables contains a foreign key column that relates to the primary key in the other table.

However, tables may also rely on a join table, a table that relates two separate tables by listing together their primary keys in the same row.  In this situation, this will require the joining of three tables.

SQL queries can contain more than one JOIN clause.  The number of JOIN clauses needed is N-1, where N is the number of tables to be joined.

**Example**

There are three tables: movies, actors, and a movie_actors table.  Below are the table attributes:

**movies**
* id
* title

**actors**
* id
* name

**movie_actors**
* movie_id
* actor_id

To get the names of all the actors in a specific movie, all three tables need to be joined. To query this, let's join the actors table with the movie_actors table:

```
SELECT name
FROM actors A
INNER JOIN movie_actors MA
ON A.id = MA.actor_id;
```

Then, let's connect the movies table by inner joining it with the movies table:

```
SELECT name
FROM actors A
INNER JOIN movie_actors MA
ON A.id = MA.actor_id
INNER JOIN movies M
ON MA.movie_id = M.id;
```

Now that the three tables are joined, let's narrow the results with a WHERE clause to return only the actors' names from the movie "Titanic":

```
SELECT name
FROM actors A
INNER JOIN movie_actors MA
ON A.id = MA.actor_id
INNER JOIN movies M
ON MA.movie_id = M.id
WHERE M.title = 'Titanic';
```

Joining more than two tables can be made easy by joining the tables in order by connecting with the join table first and then joining that with the last table.  Here, with N = 3, the SQL query utilizes two (2) join statements to successfully link up all three tables.

**The Implicit Join**

The above query can be simplified even further by using an implicit join.  An implicit join connects tables without a JOIN clause by listing out all the tables in the FROM clause and specifies on which columns to "join" in the WHERE clause.

```
SELECT name
FROM actor A, movie M, movie_actor MA
WHERE A.id = MA.actor_id
AND M.id = MA.film_id
AND M.title = 'Titanic';
```

Here, the implicit join helps clean up the query.  However, this approach may clutter up the WHERE clause, especially if there are multiple WHERE conditions applied.
