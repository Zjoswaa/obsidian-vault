---
reference: "[[Introducing Python - Book]]"
chapter: "12"
---
# ASCII
- American Standard Code for Information Interchange.
- Uses 7 bits per character (128 unique values)
	- 26 Uppercase letters
	- 26 Lowercase letters
	- 10 numbers
	- Punctuation
	- Spacing characters
	- Nonprinting control codes
# There are more characters than ASCII provides
- There have been multiple attempts to put more characters in 8-bit encoding.
	- ISO 8859-1 / Latin-1
	- Windows CP-1252
- This was still not enough to store all characters, including non-European languages, mathematical symbols, emojis, etc.

# Unicode
- Unicode is an ongoing international standard to define the characters of all the world's languages, symbols, emojis, etc.
- All the characters can be found here: https://unicode.org/charts/
# Unicode in Python
- In Python 3, strings are **Unicode character sequences**.
- The characters are divided into 8-bit sets called ==**planes**==.
	- For example, plane 0 contains all the ASCII characters.
- A `\u` followed by four [[Numbers|hexadecimal]] numbers specifies a character.
		- The first two are the plane number (`00` to `FF`).
		- The last two are the index of the character within the plane.
- For characters in higher planes we need more bits. Using `\U` followed by eight [[Numbers|hexadecimal]] numbers you can access higher planes. The leftmost ones need to be `0`.
- Using `\N{<name>}`, you can print a character by its standard name. These can be found here: https://unicode.org/charts/charindex.html, or on the charts website.
``` Python
>>> print("\u0041")
A
>>> print("\U00000041")
A
>>> print("\N{LATIN CAPITAL LETTER A}")
A
```
- The Python `unicodedata` module has functions that translate in both directions
	- `lookup()` - Takes a case-insensitive name and returns a Unicode character.
	- `name()` - Takes a Unicode character and returns an uppercase name.
``` Python
# This does not work
>>> import unicodedata
>>> unicodedata.name("A")
'LATIN CAPITAL LETTER A'
>>> unicodedata.lookup("LATIN CAPITAL LETTER B")
'B'
```
- Using `lookup()`. The charindex page does not always work.
	- The character 'é' is called ==**E WITH ACUTE, LATIN SMALL LETTER**==.
``` Python
>>> unicodedata.lookup("E WITH ACUTE, LATIN SMALL LETTER")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: "undefined character name 'E WITH ACUTE, LATIN SMALL LETTER'"
```
- This is because in Python, you need to remove the comma, and place the second part first. So 'é' becomes ==**LATIN SMALL LETTER E WITH ACUTE**==.
``` Python
# Now it works
>>> unicodedata.lookup("LATIN SMALL LETTER E WITH ACUTE")
'é'
```
- Using Python functions `chr()` and `ord()`. You can convert between [[Numbers|decimal]] Unicode ID's and single-character Unicode strings.
``` Python
>>> print("\u00E9")
é
>>> chr(0x00E9)
'é'
>>> ord("é")
233
```
# UTF-8
- UTF-8 is a dynamic encoding scheme for Unicode characters.
- It uses **one to four bytes** per Unicode character
	- One byte for ASCII
	- Two bytes for most Latin-derived (but not Cyrillic) languages
	- Three bytes for the rest of the basic multilingual plane.
	- Four bytes for the rest, including some Asian languages and symbols.
# Encoding
- Using the Python's string method `encode(<encoding>)` you can encode any string into encoding schemes. `<encoding>` can be any of these
	- "**ascii**" - 7-bit ASCII encoding
	- "**utf-8**" - eight-bit variable-length UTF-8 encoding
	- "**latin-1**" - Also known as ISO 8859-1
	- "**windows-1252**" - Windows CP-1252
	- "**unicode-escape**" - Python Unicode literal format (`"\uxxxx"` or `"\Uxxxxxxxx"`)
``` Python
>>> print("\u2603")
☃
>>> snowman = "\u2603"
>>> len(snowman)
1
>>> encoded_snowman = snowman.encode("utf-8")
>>> len(encoded_snowman)
3
>>> encoded_snowman
b'\xe2\x98\x83'
```
- Trying to encode a Unicode string that can't be handled by a certain encoding will throw a `UnicodeEncodeError`.
``` Python
>>> encoded_snowman = snowman.encode("ascii")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode character '\u2603' in position 0: ordinal not in range(128)
```
- You can pass a second argument to the `encode()` function to help avoid this error.
	- "**strict**" - The default value, throws a `UnicodeEncodeError` if it fails.
	- "**ignore**" - Ignores anything that won't encode.
	- "**replace**" - Replaces unknown characters with "?".
	- "**backslashreplace**" - Produces a Python Unicode character string. Like the "unicode-escape" encoding.
	- "**xmlcharrefreplace**" - Creates a HTML-safe string.
``` Python
>>> snowman.encode("ascii", "ignore")
b''
>>> snowman.encode("ascii", "replace")
b'?'
>>> snowman.encode("ascii", "backslashreplace")
b'\\u2603'
>>> snowman.encode("ascii", "xmlcharrefreplace")
b'&#9731;'
```
# Decoding
- When you get text from an external source, it is encoded as byte strings.
- It is hard to know which encoding was used, using `type()` does not reveal much.
``` Python
>>> cafe = "caf\u00E9"
>>> cafe
'café'
>>> type(cafe)
<class 'str'>

>>> encoded_cafe = cafe.encode("utf-8", "replace")
>>> encoded_cafe
b'caf\xc3\xa9'
>>> type(encoded_cafe)
<class 'bytes'>
```
- Decoding the encoded string using all encodings can produce nonsense.
``` Python
>>> decoded_cafe = encoded_cafe.decode("utf-8")
>>> decoded_cafe
'café'

>>> decoded_cafe = encoded_cafe.decode("ascii")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeDecodeError: 'ascii' codec can't decode byte 0xc3 in position 3: ordinal not in range(128)

>>> decoded_cafe = encoded_cafe.decode("latin-1")
>>> decoded_cafe
'cafÃ©'

>>> decoded_cafe = encoded_cafe.decode("windows-1252")
>>> decoded_cafe
'cafÃ©'
```
# HTML Entities
- You can also convert to and from Unicode characters using **HTML character entities**.
``` Python
>>> import html
>>> html.unescape("&egrave;")
'è'
```
- This also works with numbered entities [[Numbers|decimal]] or [[Numbers|hexadecimal]].
``` Python
>>> html.unescape("&#233;")
'é'
>>> html.unescape("&#xE9")
'é'
```
- Or you can import the named entity translations as a dictionary.
``` Python
>>> from html.entities import html5
>>> html5["egrave"]
'è'
```
- To convert a Python Unicode character to an HTML entity name.
``` Python
>>> import html
>>> char = "\u00E9"
>>> dec_value = ord(char)
>>> html.entities.codepoint2name[dec_value]
'eacute'
```
- For Python Unicode strings with more than 1 character.
	- `cafe.encode("ascii", "xmlcharrefreplace")` returns returns ASII characters as bytes.
	- `byte_value.decode()` is needed to convert `byte_value` to an HTML-compatible string.
``` Python
>>> cafe = "caf\u00E9"
>>> byte_value = cafe.encode("ascii", "xmlcharrefreplace")
>>> byte_value
b'caf&#233;'
>>> byte_value.decode()
'caf&#233;'
```
# Normalization
``` Python
>>> eacute1 = é  # UTF-8 Pasted
>>> eacute2 = "\u00E9"  # Unicode code point
>>> eacute3 = "\N{LATIN SMALL LETTER E WITH ACUTE}"  # Unicode name
>>> eacute4 = chr(233)  # Decimal byte value
>>> eacute5 = chr(0xE9)  # Hex byte value

>>> eacute1 == eacute2 == eacute3 == eacute4 == eacute5
True
```
