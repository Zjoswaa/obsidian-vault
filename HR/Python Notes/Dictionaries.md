> [!info] Reference
> [[Introducing Python - Book]] - Chapter 8.
# Dictionaries
- A *dictionary* is similar to a [[Lists|list]], but the order of items doesn't matter, and they aren't selected by index. Instead you specify a unique *key* to associate with each *value*. This key is usually a string, but can be any of Python's immutable types.
- Dictionaries are mutable, you can `add`, `delete` and change their key-value elements.
## Create with `{}` or `dict()`
``` Python
>>> dictionary = {
...             "Day": "24 Hours",
...             "Week": "Seven days",
...             "Fortnight": "Two weeks"
...             } 

>>> dictionary = dict(Day="24 Hours", Week="Seven days", Fortnight="Two weeks")
```
## Converting from other items to a dictionary with `dict()`
``` Python
>>> list_of_lists = [['a', 'b'], ['c', 'd'], ['e', 'f']]
>>> dictionary = dict(list_of_lists)
>>> dictionary
{'a': 'b', 'c': 'd', 'e': 'f'}
```
- This works with a list of tuples, tuple of lists, list of strings, tuple of strings too.
## Change an item by `[key]`
``` Python
>>> dictionary["a"] = "abc"
>>> dictionary
{'a': 'abc', 'c': 'd', 'e': 'f'}
```
## Get an item by `[key]` or `get()`
- Using `[key]` raises an error if the dictionary does not contain an element with the given key.
- Using `get()` returns `None` if the dictionary does not contain an element with the given key.
``` Python
>>> dictionary["c"]
'd'

>>> dictionary["h"]
# Error

>>> dictionary.get("c")
'd'

>>> dictionary.get("h")
# No error, just returns None which prints as nothing
```
- You can specify an optional value in `get()` to return that instead of `None` in the case of a mismatch.
``` Python
>>> dictionary.get("h", "Not there")
'Not there'
```
## Get all keys with `keys()`
- This returns a `dict_keys()` object, which you can iterate through.
- Use `list(dictionary.keys())` to get a list of keys.
## Get all values with `values()`
- Same as `keys()`, but returns the values.
## Get all key-value pairs with `items()`
- Returns each key-value pair as a tuple.
## Delete an item with `del` or `pop()`
## Dictionary Comprehension
- `{<key>:<value> for <variable> in <iterable>}`
- You can also specify a condition
	- `[<expression> for <item> in <iterable> if <condition>]`
``` Python
>>> numbers = range(10)
>>> dictionary = {n:n**2 for n in numbers}
>>> dictionary
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
>>> dictionary = {n:n**2 for n in numbers if not n % 2}
>>> dictionary
{0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```