---
reference: "[[Introducing Python - Book]]"
chapter: "9"
---
# Recursion
- Recursion is a method of solving a problem where the solution depends on solving **smaller instances of the same problem**.
- A recursive function is **a function that calls itself** to solve a problem.
- Examples:
	- Factorial calculation
	- Fibonacci sequence
# Recursive Function
- **Base Case:** The condition under which the recursion ends.
- **Recursive Case:** The condition under which the recursion continues.
``` Python
def factorial(n):
	if n == 1:
		return 1  # Base case
	else:
		return n * factorial(n - 1)  # Recursive Case
```
``` Python
def fibonacci(n):
	if n == 0:
		return 0
	if n == 1:
		return 1
	return fibonacci(n - 1) + fibonacci(n - 2)
```