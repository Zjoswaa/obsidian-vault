Most common and easiest to exploit.

The term "In-Band" means the same communication channel used to deliver the injection is also used to receive the results. You inject through a web request and see the extracted data right there in the page response.
# Error-Based SQL Injection
Error-Based SQL Injection exploits database error messages displayed to the user. When a web application is misconfigured and shows raw database errors, these messages often leak valuable information about the query structure, table names, and even data.

For example, injecting a single quote `'` into a vulnerable parameter might produce an error like:
```sql
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''1'' at line 1
```
While Error-Based Injection can reveal structural information, **Union-Based SQL Injection** is the primary method for extracting large amounts of data.
# Union-Based SQL Injection
Union-Based SQLi uses the `UNION` operator to append your own `SELECT` query to the original one, pulling data from any table the database user has access to. The methodology follows a consistent series of steps.
- **Determine the number of columns.** The `UNION` operator requires that both queries have the same number of columns. You discover this by injecting `UNION SELECT` with an incrementing number of values until the error disappears:
```sql
1 UNION SELECT 1          -- error (wrong column count)
1 UNION SELECT 1,2        -- error (still wrong)
1 UNION SELECT 1,2,3      -- success! The table has 3 columns
```
- **Identify which columns are displayed.** Not all columns may be rendered on the page. Change the original query's value to something that returns no results (like `0`), so only the `UNION` output is displayed:
```sql
0 UNION SELECT 1,2,3
```
The numbers that appear on the page output tell you which column positions you can use for data extraction. If  `3` appears in the content area, that is your extraction column.
- **Extract the database name.** Replace the visible column position with the `database()` function:
```sql
0 UNION SELECT 1,2,database()
```
- **Enumerate tables.** Use `information_schema.tables` to list all tables in the target database:
```sql
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'database_name'
```
- **Enumerate columns.** Once you've identified an interesting table, get its column names:
```sql
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'target_table'
```
- **Extract data.** With the table and column names known, extract the actual data:
```sql
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM target_table
```
