## Functions like `map()`, `filter()`
- They accept a function as parameters.
### `map()`
- Applies a certain function to every item in the iterable.
``` Python
>>> def double(x):
>>>     return x * 2
>>> my_list = [1, 2, 3, 4]
>>> print(list(map(double, my_list)))
[2, 4, 6, 8]
```
- You can use a [[Lambda Functions|lambda function]] as a parameter too
``` Python
>>> my_list = [1, 2, 3, 4]
>>> print(list(map(lambda x : x * 2, my_list)))
[2, 4, 6, 8]
```
### `filter()`
- Filters a list based on a function, items that don't evaluate to `True` are not added.
``` Python
>>> my_list = [1, 2, 3, 4, 5, 6]
>>> print(list(filter(lambda x : not x % 2, my_list)))
[2, 4, 6]
```