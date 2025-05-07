---
reference: "[[Introducing Python - Book]]"
chapter: "14"
---
# Create or open with `open()`
- `file = open(<filename>, <mode>)`
- `filename` is the name of the file as a string.
- `mode` is the mode in which you want to open the file and the type of file.
	- The first letter of `mode` indicates the operation:
		- `r` - Read
		- `w` - Write
			- If the file doesn't exist, it is created
			- If the file exists, it is first cleared and then written to.
		- `x` - Write, but only if the file **does not** already exist.
		- `a` - Append
			- Add to the end of the file, original file content is preserved.
	- The second letter of `mode` indicates the file's type:
		- `t` (or nothing) - Text file
		- `b` - Binary
		- `+` - Updating, read & write
- After opening a file, you can call functions to read or write data.
- After you are done with the file, you need to ==**free the memory**== with `close()`.
# Write a text file with `print()`
``` Python
>>> my_file = open("file.txt", "wt")
>>> print("This is some text", file=my_file)
>>> my_file.close()
```
# Write a text file with `write()`
``` Python
>>> my_file = open("file.txt", "wt")
>>> my_file.write("Hello")
5
>>> my_file.close()
```
# Read a text file with `read()`, `readline()` or `readlines()`
## Using `read()`
- Reads the entire file into a string. Large files will consume a lot of memory using this method.
## Using `readline()`
- Reads one line and returns it, can be used in a loop
``` Python
>>> file = open("file.txt", "rt")
>>> while True:
...     line = file.readline()
...     if not line:
...         break
...     print(line)
...
>>> file.close()
```
## Using `readlines()`
- Reads the whole file into a list of strings, each string is one line of the file.
# Close files automatically using `with`
``` Python
>>> with open("file.txt" , "wt") as file:
...     file.write("Hello")
...
```
