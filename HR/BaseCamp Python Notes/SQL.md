---
reference: "[[Introducing Python - Book]]"
chapter: "16"
---
# SQL
- Structured Query Language
- Defines instructions to add, read, modify, and delete data from a [[Databases|database]].
## SQLite
- In Python, you can use the **sqlite3** [[Modules, Packages & Libraries|library]] to write and execute SQL queries.
``` Python
import sqlite3

database = sqlite3.connect("database.sqlite")
database.close()
```
## Reading columns from a table
- `SELECT <columns with a comma between them> FROM <table>`
``` SQL
SELECT name, date_of_birth FROM students
```
``` Python
query = '''SELECT name, date_of_birth FROM students'''
students = database.execute(query)
for student in students:
	print(student)
```
## Sorting output
- `SELECT <columns with a comma between them> FROM <table> ORDER BY <columns (ASC or DESC) with a comma between them>`
``` SQL
SELECT name, date_of_birth FROM students ORDER BY date_of_birth DESC
```
``` Python
query = '''SELECT name, date_of_birth FROM students ORDER BY date_of_birth DESC'''
students = database.execute(query)
for student in students:
	print(student)
```
## Conditions in a query
`SELECT <columns with a comma between them> FROM <table> WHERE <conditions in the form column="value">`
``` SQL
SELECT name, date_of_birth FROM students WHERE city="Rotterdam"
```
``` Python
query = '''SELECT name, date_of_birth FROM students SELECT name, date_of_birth FROM students WHERE city="Rotterdam"'''
students = database.execute(query)
for student in students:
	print(student)
```
- In Python, using the sqlite3 [[Modules, Packages & Libraries|library]], you can also use wildcards in the query, indicted with a `?`. You have to fill in these.
``` Python
query = '''SELECT name, date_of_birth FROM students SELECT name, date_of_birth FROM students WHERE city=?'''
students = database.execute(query, ["Rotterdam"])
for student in students:
	print(student)
```
- This is useful if you want to use the same query multiple times but with different values.
## Multiple conditions in a query
- Multiple conditions can be grouped with the `AND` and `OR` keywords.
- Comparisons can be done with `=`, `<`, `<=`, `>=`, `>`, `<>`, `IN <values>`
## Changing data
- `UPDATE <table> SET <changes in the form column="value"> WHERE <conditions>`
- The `commit()` function commits any pending changes to the database.
``` SQL
UPDATE students SET class="BC11V" WHERE city="Houten"
```
``` Python
query = '''UPDATE students SET class=? WHERE city=?'''
database.execute(query, ["BC11V", "Houten"])
database.commit()
```
## Deleting data
- `DELETE FROM <table> WHERE <conditions>`
``` SQL
DELETE FROM students WHERE city="Utrecht"
```
``` Python
query = '''DELETE FROM students WHERE city=?'''
database.execute(query, ["Utrecht"])
database.commit()
```
## Adding data
- `INSERT INTO <table> (<columns with a comma between them>) VALUES (<values with a comma between them>)`
``` SQL
INSERT INTO students (name, date_of_birth, city, class) VALUES ("Joshua van der Jagt", "20-10-2002", "Rotterdam", "BC21F")
```
``` Python
query = '''INSERT INTO students (name, date_of_birth, city, class) VALUES (?, ?, ?, ?)'''
database.execute(query, ["Joshua van der Jagt", "20-10-2002", "Rotterdam", "BC21F"])
database.commit()
```