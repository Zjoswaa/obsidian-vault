# Three types
- [[In-Band SQL Injection]]
	- Error-Based
	- Union-Based
- [[Blind SQL Injection]]
	- Authentication Bypass
	- Boolean-Based
	- Time-Based
- Out-of-Band SQL Injection
# Detecting SQL Injection
- Enter a `'`, if the application returns a database error, the input is likely being inserted into a SQL query without proper handling.
- Try a `"`.
- Enter `;--`, if the application behaves differently (e.g., returns different content), the comment syntax is being processed.
- Test `OR 1=1`, if it changes the results, the input is directly in the query's logic.