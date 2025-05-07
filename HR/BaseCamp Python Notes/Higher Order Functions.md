# A function that has a function as input / output
- At least one of input or output has to be a function to be a HOF, can also be both.
## Functions like `map()`, `filter()`
- They accept a function as parameters.
## Importance
- Enables functional programming.
- Promotes code reusability and abstraction.
### `map()`
- Applies a certain function to every item in the iterable.
``` Python
def double(x):
    return x * 2

my_list = [1, 2, 3, 4]
print(list(map(double, my_list)))
# Prints [2, 4, 6, 8]
```
- You can use a [[Lambda Functions|lambda function]] as a parameter too
``` Python
my_list = [1, 2, 3, 4]
print(list(map(lambda x : x * 2, my_list)))
# Prints [2, 4, 6, 8]
```
### `filter()`
- Filters a list based on a function, items that don't evaluate to `True` are not added.
``` Python
my_list = [1, 2, 3, 4, 5, 6]
print(list(filter(lambda x : not x % 2, my_list)))
# Prints [2, 4, 6]
```
### `reduce()
- Applies a **rolling computation** to **sequential pairs** of values in an iterable.
- In Python 3, it is no longer a built-in function, you need to [[Modules, Packages & Libraries|import]] it.
``` Python
from functools import recuce

def add(x, y):
	return x + y

my_list = [1, 2, 3, 4, 5]
print(reduce(add, my_list))
# Prints 15
```
## Functions as arguments
``` Python
def greet(name):
	return f"Hello, {name}!"

def custom_greet(func, name):
	return func(name)

print(custom_greet(greet, "Joshua"))
# Prints "Hello, Joshua!"
```
``` Python
def multiplier(factor):
	def multiply_by_factor(number):
		return number * factor
	return multiply_by_factor

double = multiplier(2)
triple = multiplier(3)

print(double(5)) # Prints 10
print(triple(5)) # Prints 15
```
