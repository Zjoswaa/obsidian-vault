> [!info] Reference
> [[Introducing Python - Book]] - Chapter 5.
## Multiline Strings with triple quotes
``` Python
>>> text = """Line 1
	Line 2
	Line 3"""
```
## Raw Strings ignore escape characters, useful for Regular Expressions
``` Python
>>> raw_string = r"Not escaping\n"
```
## Creating Strings
``` Python
>>> str(98.6)
'98.6'

>>> str(1.0e4)
'10000.0'
```
## Substring with slice
- Entire string with `[:]`
- From index `start` to end with `[start:]`
- From start to index `end` with `[:end]`
- From index `start` to index `end` with `[start:end]`
- From index `start` to index `end`, taking steps of size `step` with `[start:end:step]`
## Search and select
``` Python
>>> word = "abcde"
>>> sentence = "This is a sentence"

>>> len(word)
5

>>> word.startswith("abc")
True

>>> word.endswith("bc")
False

>>> sentence.find("is")
2

>>> word.index("de")
3

>>> sentence = "A duck goes into a bar..."
>>> setup.strip(".")
'A duck goes into a bar'


>>> import string
>>> string.whitespace
' \t\n\r\x0b\x0c'

>>> string.punctuation
'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

>>> word = "What?!?"
>>> word.strip(string.punctuation)
'What'
```
## Other String functions
- Find rightmost occurrence with `sentence.rfind(word)`
- Find rightmost index with `sentence.rindex(word)`
- `sentence.find(word)` and `sentence.rfind(word)` return `-1` if `sentence` doesn't contain `word`
- `sentence.index(word)` and `sentence.rindex(word)` raise an error if `sentence` doesn't contain `word`
- Count substring occurrences with `.count()`
- Check if string contains only letters and numbers with `.isalnum()`
- `.upper()` returns a string in all uppercase
- `.lower()` returns a string in all lowercase
- `.swapcase()` swaps upper- and lowercase
- Align a string with `ljust()` and `rjust()`