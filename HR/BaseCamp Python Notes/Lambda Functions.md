---
reference: None
---
## What is a lambda function
- A lambda function is a small anonymous [[Functions & Arguments|function]].
- A small, unnamed [[Functions & Arguments|function]] that can be defined in one line.
- A lambda function can take **any number of arguments**, but can only have **one expression**.
## Why use a lambda function?
- Best suited for *small*, *simple* function that can be defined in a single line.
- They are often used for *short-lived*, *one-time* operations where you don't need to give the function a name.
- Commonly used in functional programming constructs using [[Higher Order Functions|higher order functions]] like `map()` and `filter()` because they allow you to define inline functions.
## Creating a lambda function
- `lambda <arguments> : <expression>`
- `<variable> = lambda <arguments> : <expression>`
``` Python
>>> lambda a : a + 10
```

``` Python
>>> x = lambda a : a + 10
>>> print(x(5))
15
```

``` Python
>>> x = lambda a, b : a * b
>>> print(x(5, 6))
30
```

``` Python
>>> (lambda a : a + 10)(5)
15
```