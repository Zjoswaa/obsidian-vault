> [!info] Reference
> [[Introducing Python - Book]] - Chapter 3.
## Bases
- `0b` or `0B` for binary (base 2)
- `0o` or `0O` for octal (base 8)
- `0x` or `0X` for hexadecimal (base 16)
``` Python
# Decimal to Binary
>>> bin(65)
'0b1000001'


# Decimal to Octal
>>> oct(65)
'0o101'


# Decimal to Hexadeximal
>>> hex(65)
'0x41'


# Binary to Decimal
>>> int(0b1000001)
65


# Octal to Decimal
>>> int(0o101)
65


# Hexadecimal to Decimal
>>> int(0x41)
65
```
## Type Conversions
``` Python
# Boolean to Integer
>>> int(True)
1

>>> int(False)
0


# Integer to Boolean
>>> bool(1)
True

>>> bool(20)
True

>>> bool(-20)
True

>>> bool(0)
False


# Float to Integer
>>> int(98.632)
98


# String to Integer
>>> int('99')
99

>>> int('-23')
-23

>>> int('+12')
12


# String (non-decimal) to Integer with specified base (0, 2-36)
>>> int('11', 2)  # Binary
3

>>> int('11', 16)  # Hexadecimal
17

>>> int('11', 23)  # Other Bases
24


# Integer to Character
>>> chr(65)
'A'


# Character to Integer
>>> ord('A')
65
```
## Type Promoting
``` Python
>>> 43 + 2.0
45.0

>>> False + 0
0

>>> False + 0.0
0.0

>>> True + 0
1

>>> True + 0.0
1.0
```
