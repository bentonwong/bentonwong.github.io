---
layout: post
title:  "SQL Joins In a Nutshell"
date:   2017-09-14 14:02:16 -0400
---


SQL joins are used to combine data from two or more tables based on a common column between the tables.  Typically, at least one of the related tables has a foreign key column, which typically contains the id number of the associated object from the other table.

For example, we have two tables: a Books table and a Authors Table.   Books has the following three columns: *id*, *title*, and *author_id*.  Authors has the following two columns: *id*, *name*.

Books and Authors would be associated by the author_id column, which is the foreign key.  Because of this association, SQL queries can be written to return the name of books by a specific author, such as:
```
     SELECT title
     FROM Books
     WHERE author_id = 1;
```
This query would return all the book titles that have an author id of 1.  What if we want to get a list of all the books with the author's names next to it or only books where we have author names?  We can, using a SQL JOIN statement using the author_id (i.e. foreign key) column to relate the tables.

**Types of SQL joins**

There are different join statements that can be inserted into a SQL query.  Each produces different results:

* INNER JOIN: Will return all rows from both tables where the queried condition is met
* LEFT JOIN: Will return all rows from the left (first) table regardless of whether the queried condition is met, while returning any matched data from the right (second) table
* RIGHT JOIN: Will return all rows from the right (second) table regardless of whether the queried condition is met, while returning any matched data from the left (first) table.
* FULL JOIN: Will return all rows where the queried condition is met in one of the tables

**Applying Joins**

The basic format for inserting joins into a SQL query is:
```
SELECT column(s)
FROM first_table
INNER JOIN second_table
ON first_table.column = second_table.column;
```
Getting a list of all books only with authors via Inner Join

Using the following query:
```
SELECT Books.title, Authors.name
FROM Books
INNER JOIN Authors
ON Books.author_id = Authors.id;
```
we are specifying that we want:

* a list containing the title of the book from the Books table, with the author's name from the Authors table with SELECT
* connect the Books and Authors table with FROM...INNER JOIN
* connect them on the foreign key or table id with ON

Because inner join will only return a result if there is a foreign key value for a book, any book without a foreign key will not be returned.  Books without a foreign key will not meet the inner join condition and thus, they will not be displayed.

**Getting a list of all books and any authors via Left Join**

Using the following query:
```
SELECT Books.title, Authors.name
FROM Books
LEFT OUTER JOIN Authors
ON Books.author_id = Authors.id;
```
we are specifying that we want to display all the book titles from the Books table.  We are also specifying that we want to display the author's name.  Since we are using a LEFT JOIN, all Books titles will be displayed regardless of whether there is an associated author or not for that book (i.e. no foreign key).

**Getting a list of all authors and any books via Right Join**

Using the following query:
```
SELECT Books.title, Authors.name
FROM Books
RIGHT OUTER JOIN Authors
ON Books.author_id = Authors.id;
```
Since we are using a RIGHT JOIN, all Author names will be displayed regardless of whether there is an associated book or not in the Books table.

**Getting a list of any books and any authors via Full Outer Join**

Using the following query:
```
SELECT Books.title, Authors.name
FROM Books
FULL OUTER JOIN Authors
ON Books.author_id = Authors.id;
```
Full Outer Joins will return all the books and all the authors in both tables and associate both if there is a foreign key. Nothing is excluded.  Therefore, the results will also include books without authors and authors without books.
