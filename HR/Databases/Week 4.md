# LINQ Query Expression
``` C#
int[] scores = {5, -5, 4, -4, 0, -1, 1}

IEnumerable<int> scoreQuery =
	(from score in scores
	where score > 0
	orderby score descendin
	select score)
	//.ToList()
;
```
## Lazy / Deferred Execution
- Deferred execution means that the evaluation of an expression is delayed until its realized value is actually required
- It greatly improves performance by avoiding unnecessary execution
- In **lazy evaluation**, a single element of the source collection is processed during each call to the iterator
## Eager / Immediate Execution
- Immediate execution is the reverse of deferred execution
- It forces the LINQ query to execute and gets the result immediately
- The `To` **conversion operators** (`ToList()`, `ToArray()`, etc.) execute the given query and give the result immediately
- In **eager evaluation**, a single element of the source collection is processed during each call to the iterator
# Joining Tables
- Join is used to combine columns from one (self-join) or more tables based on the values of the common columns between tables
- The common columns are typically the primary key columns of the first table and foreign key columns of the second table
## Joins
- **Inner Join:** Selects rows from one table that have the corresponding rows in other tables
- **Outer Join:** Selects rows from one table that may or may not have the corresponding rows in other tables
- **Self-join:** Joins a table to itself by comparing the table to itself
- **Full outer join:** Uses the full join to find a row in a table that does not have a matching row in another table
- **Cross Join:** Produces a Cartesian product of the rows in two or more tables
- **Natural Join:** Joins two or more tables using an implicit join condition based on the common column names in the joined tables
