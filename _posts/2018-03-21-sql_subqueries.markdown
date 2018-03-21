---
layout: post
title:      "SQL Subqueries"
date:       2018-03-21 19:20:45 +0000
permalink:  sql_subqueries
---


SQL subqueries are SQL queries nested inside another SQL query.

There may be situations where a first query is needed in order to provide data for a condition in a subsequent query.  Rather than run two separate queries, one of the queries can be inserted inside the outer query.  Because the subquery runs first, it can then pass on its result immediately to that parent query.

Subqueries are usually added in WHERE clauses to provide a value or set of values for comparison by the outer query.  For example, the typical syntax to run a subquery in a WHERE clause would be:

```
SELECT list_name
FROM table
WHERE expression operator
     (SELECT list_name or aggegrate_value
     FROM table);
```

When using subqueries, the general guidelines are:

- Subqueries need to be wrapped in parenthesis
- Must be on the right side of a comparison operator
- Cannot internally manipulate the subquery results (i.e. apply an ORDER BY to the subquery results)

**Example 1: Return list of movies titles from a collection of movies that have a user rating higher than the overall average rating**

In this situation, we have a single table with the following columns:

movies
* id
* title
* rating

To return the above query, we would first need to find the average rating, and then return the movie titles which are higher than the average rating.  If run as 2 queries, it would look like this:

```
SELECT AVG(rating)
FROM movies;
```

Let's say that query returns a value of 3.5.  To get the list of movies that exceed that value, a second query would be run applying that value in the WHERE clause below:

```
SELECT title
FROM movies
WHERE AVG(rating) > 3.5;
```

With subqueries, this can be compacted into a single query:

```
SELECT title
FROM movies
WHERE (
     SELECT AVG(rating)
     FROM movies
);
```

**Example 2: Return a list of movies titles from a collection of movies that was released after the year 2000 and revenue was greater than $1 million**

In this situation, we have 2 additional tables with the following columns:

release
* id
* year
* movie_id

revenue
* id
* amount
* release_id

First, we would need to get the list of movie ids that were released after the desired year and had a certain revenue by joining the release and revenue tables:

```
SELECT release.movie_id
FROM release
INNER_JOIN revenue ON release.id = revenue.release_id
WHERE release.year > 2000 AND revenue.amount > 1000000;
```

This should return a list of movie_ids that match the above conditions.  Now in order to return the list of movies that meet this condition, we can use it as a subquery in there WHERE clause along with IN to have the outer query return only those titles with movie_ids that were provided by the subquery:

```
SELECT title
FROM movies
WHERE id IN (
SELECT release.movie_id
FROM release
INNER_JOIN revenue ON release.id = revenue.release_id
WHERE release.year > 2000 AND revenue.amount > 1000000);
```

Subqueries help make the query overall easier to read and debug.  However, subqueries can get much more complicated.  Other situations include multiple column subqueries and nested subqueries.
