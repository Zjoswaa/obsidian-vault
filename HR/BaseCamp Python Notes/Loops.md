---
reference: "[[Introducing Python - Book]]"
chapter: "6"
---
## Loop types
Main types are:
- `while` loop
- `for` loop
### `while` loop
- Repeat until condition is met, or `break` is used.
``` Python
>>> count = 1
>>> while count <= 5:
...     print(count)
...     count += 1
1
2
3
4
5
```
### `for` loop
- Specific amount of iterations
- `for` and `in` keywords
- `range(x, y)` returns an _iterable_ object from `x` to `y - 1`, you can step through its values
``` Python
>>> for i in range(0,3):
...     print(i)
0
1
2
```
> [!info]
> You can also specify `step` size in a `range` by using `range(x, y, step)`
## Common loop elements
- Initialization
- Condition
	- A boolean expression
- Iteration
	- The body of the loop
- Update
	- In a `while` loop, you need to update the condition to ensure it will evaluate to `False` eventually.