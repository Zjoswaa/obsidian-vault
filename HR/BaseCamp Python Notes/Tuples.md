---
reference: "[[Introducing Python - Book]]"
chapter: "7"
---
# Tuples
- Are *immutable*
- *"too-pull"* or *"tub-pul"* ?
``` Python
# Creating an empty tuple
>>> empty_tuple = ()
>>> empty_tuple = tuple()


# Initializing a tuple
>>> filled_tuple = ("Item",)

# Or
>>> filled_tuple = "Item",

# This does not work
>>> filled_tuple = ("Item")
>>> type(filled_tuple)
<class 'str'>
```
## Tuples let you assign multiple variables at once
``` Python
>>> animals = ("Dog", "Cat", "Fish")
>>> a, b, c = animals
>>> b
'Cat'
```
## Converting from other items to a tuple with `tuple()`
``` Python
>>> names = ["John", "Max", "Bob"]
>>> my_tuple = tuple(names)
```
## Combining tuples with `+`
- Similar to combining [[Text Strings]]
``` Python
>>> ("Dog") + ("Cat", "Fish")
('Dog', 'Cat', 'Fish')
```
## Duplicate items with `*`
``` Python
>>> ("Yada") * 3
('Yada', 'Yada', 'Yada')
```
## Comparing tuples
- The `<`, `<=`, `>`, `>=` operators compare tuple sizes
``` Python
>>> ("Cat", "Dog") == ("Cat", "Dog", "Fish")
False
>>> ("Cat", "Dog") < ("Cat", "Dog", "Fish")
True
```
## Tuple unpacking
``` Python
>>> for row, col in cells:
...     print(row, col)
...
1 1
1 2
2 1
2 2
```
## Tuple Comprehension
- Note that the type is not of class `tuple`
- You can however, create a tuple from this `generator` with the `tuple()` function
``` Python
>>> numbers = (number for number in range(1, 6))
>>> type(numbers)
<class 'generator'>

>>> numbers_tuple = tuple(number for number in range(1, 6))
>>> numbers_tuple
(1, 2, 3, 4, 5)
```