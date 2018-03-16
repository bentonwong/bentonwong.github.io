---
layout: post
title:      "SQL: WHERE versus HAVING"
date:       2018-03-16 17:22:01 +0000
permalink:  sql_where_versus_having
---


In SQL, WHERE and HAVING are filtering clauses, filtering out rows that contain data that do not meet a condition.   It can be confusing since they have similar functionality.  However, there is a difference.

To remember the difference:

* WHERE clause usually comes **before** calling GROUP BY, to filter **individual** rows that do not meet a specific condition
* HAVING clause comes with and **after** calling GROUP BY, to filter **grouped** rows that do not meet a specific condition

For example, we have a table containing store purchases with the columns: id, customer_name, transaction_amount, store_id

If we wanted a list of all transactions greater than $100, then we would simply apply a WHERE clause:

```
SELECT *
FROM transactions
WHERE transaction_amount > 100;
```

Say we want to reward customers who have spent more than $500, we would need to generate a list of customer names in order to identify which customers should be rewarded, along with the total spend to confirm that it is over $500.  As a start, to get the list of all customers and their total spend, we get each customers' total spend using the aggregate function SUM and GROUP BY:

```
SELECT customer_name, SUM(transaction_amount)
FROM transactions
GROUP BY customer_name;
```

To get a list of customer's whose total spend is greater than $500, HAVING is called after GROUP BY to apply a filter to those grouped results:

```
SELECT customer_name, SUM(transaction_amount)
FROM transactions
GROUP BY customer_name
HAVING SUM(transaction_amount) > 500;
```

Now if we wanted to get a list of customers whose spend is greater than $500 at a certain store (e.g. store_id =1), we can apply both WHERE and HAVING in the same query:

```
SELECT customer_name, SUM(transaction_amount)
FROM transactions
WHERE store_id = 1
GROUP BY customer_name
HAVING SUM(transaction_amount) > 500;
```

WHERE and HAVING are useful filtering clauses.  Keep in mind that HAVING has a close relationship to the GROUP BY clause, and should only be used when rows are grouped and their results are aggregated.
