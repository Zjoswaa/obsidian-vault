# Grouping data
- **Aggregate functions**: Perform a calculation on a set of rows and return a single row
- **Group by**: Divides rows into groups and applies an aggregate function on each
- **Having**: Applies the condition for groups
## Aggregate functions
### SQL
`SELECT aggregate_function(column) FROM <table_name>`

``` SQL
SELECT count(*) FROM Departments
```

``` SQL
SELECT SUM(Salary), MAX(Salary), MIN(Salary), AVG(Salary) FROM Employees
```
### LINQ
`context.dbset.agg_function()`

``` C#
dbCOntext.Departments.Count();
```

``` C#
dbContext.Employees.Sum(e => e.Salary)
```
## Group by
- The `GROUP BY` clause divides the rows returned from the `SELECT` statement into groups
- For each group, you may apply an aggregate function. Without aggregate function, `GROUP` is similar to `DISTINCT`
- The `GROUP BY` must appear right after the `FROM` or `WHERE` clause
### Having
- `HAVING` clause is used in conjunction with the `GROUP BY` clause to filter group rows that do not satisfy a specified condition
- `HAVING` clause can only refer to columns from withing aggregate functions
- `HAVING` clause sets the condition for **group rows** created by the `GROUP BY` clause **after** the `GROUP BY` clause applies
- `WHERE` clause sets the condition for **individual rows before** `GROUP BY` clause applies
### Group by (LINQ)
- The grouping operators create a group of elements based on the given key
- This group is contained in a special type of collection that implements an `IGrouping<TKey,TSource>` interface where `TKey` is a key value on which the group has been formed and `TSource` is the collection of elements that matches with the grouping key value

``` C#
var q5 = dbContext.Employees.ToList()
	.GroupBy(x => x.DNo, x => x, (Key, Rows) => new { Key, Rows });

foreach (var group in q5) {
	Console.WriteLine($"{group.Rows.Count()} employees in DNo: {group.Key}:");
	foreach (var item in group.Rows) {
		Console.WriteLine($"{item.Dno}, {item.fName}, {item.Super_ssn}");
	}
}
```
