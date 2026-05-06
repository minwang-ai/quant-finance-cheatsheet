# String (`str`)

## String Operators
| Syntax | Application | 
| :--- | :--- | 
| **Concatenation (+)** | chain strings together. |
---


## Output Formatting (f-strings)

| Feature | Meaning | Syntax | Examples |
| :--- | :--- |  :--- | :--- | 
| **Interpolation** | **Injects variables** into strings. |`f"other_text, {variable_name}"` |
| **Thousands** | Formats **large number** variable `num` with commas (e.g., 1,000,000). | `f"{num:,}"` | `print(f"{num:,}")`  |
| **Precision** | **rounds** the output variable `num` to the **nearest `n` decimal points**. Here `n` is a number. |`f"{num:.nf}"`  | `print(f"{num:.2f}")`|
---

## [String build-in methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
|---|---|---|---|---|---|---|
| `len()` | Returns the length of the string. | `len(str)` | `str`: The input string. | Returns an integer representing the number of characters in the string. |  |
| `strip()` | **Stripes oﬀ** (Removes) any **leading** and **trailing** whitespace (or **specified characters**). | `str.strip([chars])` | `chars` (optional): specified characters to remove. | Returns a new string with characters removed from both ends. | | `str_variable_name = str_variable_name.strip()` |
| `lstrip()` | Removes leading (**left**) whitespace or specified characters. Note: not remove characters in between | `str.lstrip([chars])` | Same as `strip()`. | Returns a new string with leading characters removed. |  |
| `rstrip()` | Removes trailing (**right**) whitespace or specified characters. <br> Note: not remove characters in between | `str.rstrip([chars])` | Same as `strip()`. | Returns a new string with trailing characters removed. |  |
| `capitalize()` | **Capitalizes** the **first** character of the **string**. | `str.capitalize()` | None | Returns a new string with only the first letter capitalized. |  | `str_variable_name = str_variable_name.capitalize()` |
| `title()` | Capitalizes the first letter of **each word**. | `str.title()` | None | Returns a new string with each word's first letter capitalized. |  | `str_variable_name = str_variable_name.title()` |
| `lower()` | Converts all characters in a string to lowercase. | `str.lower()` | None | Returns a new string with all lowercase characters. |  |
| `upper()` | Converts all characters in a string to uppercase. | `str.upper()` | None | Returns a new string with all uppercase characters. |  |
| `split()` | Splits a string into **a list of substrings** based on a specified **delimiter**. Any two adjacent delimiter will generate an empty string. | `str.split(sep, maxsplit)` | - `sep` (optional): separator delimiter - string or char, such as `','`. Default: **whitespace**. <br><br> -`maxsplit` (optional): Maximum number of splits. Default: `-1` means **no limit**. | Returns a list of substrings. | Time: `O(n)`, Space: `O(n)` | `str_variable_name_1, str_variable_name_2, ... str_variable_name_n = str_variable_name.split()`|
| `join()` | Joins elements of an iterable into a single string with a specified delimiter placed between each element. | `sep.join(iterable)` | `sep`: separator delimiter.<br>`iterable`: A sequence of strings (e.g., list, tuple, dict etc) to join together. When using it with a dict, it will only join the keys, not the values. | Returns a concatenated string. | Time: `O(n)`, Space: `O(n)` |
| `replace()` | Return a copy of the string with all occurrences of an **old substring** **replaced** by a **new substring**; <br><br> case-sensitive (it treats uppercase and lowercase characters as distinct). | `str.replace(old, new, count=-1)` |- `old`: Substring to replace.<br> -`new`: Replacement string.<br> -`count` (optional): If `count` is given, only the first count occurrences are replaced. If `count` is not specified or `-1`, then **all occurrences** are replaced. | Returns a new string with replacements applied. | |`str_content = str_content.replace(":)", "🙂")`|
| `find()` | Returns the lowest index of the first occurrence of a substring. | `str.find(sub, start, end)` | `sub`: Substring to search. `start`, `end` (optional): Index range to search. | Returns index if found, `-1` if not found. |  |
| `index()` | Similar to `find()`, but raises an error if not found. | `str.index(sub, start, end)` | Same as `find()`. | Returns index if found; raises `ValueError` if not found. |  |
| `startswith()` | Checks if a string starts with a specified prefix. | `str.startswith(prefix, start, end)` | `prefix`: Prefix to check. `start`, `end` (optional): Index range to check. | Returns `True` if it starts with prefix, otherwise `False`. |  |
| `endswith()` | Checks if a string ends with a specified suffix. | `str.endswith(suffix, start, end)` | `suffix`: Suffix to check. `start`, `end` (optional): Index range to check. | Returns `True` if it ends with suffix, otherwise `False`. |  |
| `count()` | Counts occurrences of a substring. | `str.count(sub, start, end)` | `sub`: Substring to count. `start`, `end` (optional): Index range to search. | Returns the number of occurrences of `sub`. |  |
| `isdigit()` | Checks if all characters are digits. | `str.isdigit()` | None | Returns `True` if all characters are digits, otherwise `False`. |  |
| `isalpha()` | Checks if all characters in the string are letters (English (`A-Z`, `a-z`), also including Unicode letters for other languages). | `str.isalpha()` | None | Returns `True` if every character in the string is a letter; `False` if the string contains any numbers, spaces, or special characters. | Time: `O(n)`, Space: `O(1)` |
| `isalnum()` | Checks if all characters are alphanumeric (letters or digits). | `str.isalnum()` | None | Returns `True` if all characters are alphanumeric, otherwise `False`. |  |
| `isspace()` | Checks if all characters are whitespace. | `str.isspace()` | None | Returns `True` if all characters are whitespace, otherwise `False`. |  |
| `swapcase()` | Swaps case for all characters. | `str.swapcase()` | None | Returns a new string with uppercase converted to lowercase and vice versa. |  |
| `ljust()` | Left-aligns a string, padding with spaces or specified characters. | `str.ljust(width, fillchar)` | `width`: Total width. `fillchar` (optional): Padding character. | Returns a left-aligned string. |  |
| `rjust()` | Right-aligns a string, padding with spaces or specified characters. | `str.rjust(width, fillchar)` | Same as `ljust()`. | Returns a right-aligned string. |  |
| `center()` | Centers a string, padding with spaces or specified characters. | `str.center(width, fillchar)` | Same as `ljust()`. | Returns a centered string. |  |
| `zfill()` | Pads the string with zeros on the left. | `str.zfill(width)` | `width`: Total width. | Returns a zero-padded string. |  |
| `sorted()` | Returns a sorted list of characters from the string. | `sorted(str)` | `str`: The input string. | Returns a sorted list of characters. |  |
| `format()` | Formats a string by converting the argument as a formatted string. | `str.format(args...)` | `args...`: Values to format into the string. | Returns a formatted string. |  |
| `removeprefix()` | Removes a specific prefix from the string (Python 3.9+). | `str.removeprefix(prefix)` | `prefix`: The prefix to remove. | Returns a new string without the prefix. |  |
| `removesuffix()` | Removes a specific suffix from the string (Python 3.9+). | `str.removesuffix(suffix)` | `suffix`: The suffix to remove. | Returns a new string without the suffix. |  |
---