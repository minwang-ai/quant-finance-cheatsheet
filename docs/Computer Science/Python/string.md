# String (`str`)

## String Operators
| Syntax | Application | Example |
| :--- | :--- | :--- | 
| **Concatenation (+)** | chain strings together. | ` str1 + str2` |
| **multiplicaton (*)** | repeat strings n times | ` print(str_variable * n)` |
---


## Output Formatting (f-strings)
`f"{value:format}"`
| Parts | Meaning|
| :--- | :--- |
| value | The variable or expression we want to print.|
| colon : | The separator that tells Python everything after this is a formatting instruction.|
|format| Special codes that tell Python how to display that value.|
---

### f-strings Patterns Cheat Sheet
| Feature | Meaning | Syntax | Examples |
| :--- | :--- |  :--- | :--- | 
| **Interpolation** | **Injects variables** into strings. |`f"other_text, {variable_name}"` |
| **Thousands** | Formats **large number** variable `num` with commas `,` | `f"{num:,}"` | `print(f"{num:,}")` <br> 1000000 -> 1,000,000 |
| **Precision** | **rounds** the output variable `num` to the **nearest `n` decimal points**. Here `n` is a number and it could not be `0`. |`f"{num:.nf}"` | `print(f"{num:.2f}")` <br> 3.1415926 -> 3.14 |
|**Percentage**| automatically convert float output variable `num` to percentage, add `%`sign and keep the **nearest `n` decimal points**.  | `f"{num:.n%}"`  | `f"{num:.0%}"`<br> 0.75 -> "75%" | 
---

## Slicing

| Syntax | Meaning | Note | 
| :--- | :--- | :--- |
| `str[start: stop: step]` | - `:` separates start, stop, and step <br> - Inclusive Start, Exclusive Stop, i.e., [start, stop) |  - optional: Omitting start means "from beginning" <br> - optional: Omitting stop means "to end" |
| **Negative indices** means **count from the end** | * -1 means last element <br> * -2 means last 2nd element |
| `step` | determines selection intervals | **Negative step reverses order** |
---

### Slicing cheat sheet

| Operation | Syntax | Meaning | Example (`"Python"`) | Output | Complexities |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Basic Slicing** | `data[start:stop]` | Extracts elements from `start` to `stop-1`. | `"Python"[1:4]` | `"yth"` | $O(k)$ |
| **Omitting start** | `data[:stop]` | starts from the beginning up to `stop-1`. | `"Python"[:4]` | `"Pyth"` | $O(k)$ |
| **Omitting stop** | `data[start:]` | From `start` to the end. | `"Python"[2:]` | `"thon"` | $O(k)$ |
| **Using step** | `data[start:stop:step]` | Extracts with step intervals. | `Python"[::2]` | `"Pto"` | $O(k)$ |
| **Full Slice** | `data[:]` | Returns the entire sequence. | `"Python"[:]` | `"Python"` | $O(n)$ |
| **Negative Indexing** | `data[-start:-stop]` | Counts from the end (-1 is the last element). | `"Python"[-5:-2]` | `"yth"` | $O(k)$ |
| **Reverse a Sequence** | `data[::-1]` | Reverses the sequence. | `Python"[::-1]` | `"nohtyP"` | $O(n)$ |
| **Skipping Elements** | `data[::k]` | Selects every k-th element. | `"Python"[::3]` | `"Ph"` | $O(n/k)$ |
| **Negative Step** | `data[start:stop: -step]` | Pick elements in reverse order. | `"Python"[4:1:-1]` | **`"oht"`** | $O(k)$ |
---
**Note**: 
slicing **create new lists** -> space O(n)

## [String build-in methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
|---|---|---|---|---|---|---|
| `len()` | Returns the length of the string. | `len(str)` | `str`: The input string. | Returns an integer representing the number of characters in the string. |  |
| **`.strip()`** | **Stripes oﬀ** (Removes) any **leading** and **trailing specified characters** (default: whitespace). | `str.strip([chars])` | `chars` (optional): specified characters to remove. | Returns a new string with characters removed from both ends. | | `str_variable_name = str_variable_name.strip()` |
| `.lstrip()` | Removes leading (**left**) whitespace or specified characters. Note: not remove characters in between | `str.lstrip([chars])` | Same as `strip()`. | Returns a new string with leading characters removed. |  |
| `.rstrip()` | Removes trailing (**right**) whitespace or specified characters. <br> Note: not remove characters in between | `str.rstrip([chars])` | Same as `strip()`. | Returns a new string with trailing characters removed. |  |
| **`.capitalize()`** | **Capitalizes** the **first** character of the **string**. | `str.capitalize()` | None | Returns a new string with only the first letter capitalized. |  | `str_variable_name = str_variable_name.capitalize()` |
| **`.title()`** | **Capitalizes** the **first** letter of **each word**. | `str.title()` | None | Returns a new string with each word's first letter capitalized. |  | `str_variable_name = str_variable_name.title()` |
| **`.lower()`** | Converts all characters in a string to **lowercase**. | `str.lower()` | None | Return a copy of the string with all the cased characters converted to lowercase. | `str_variable_name = str_variable_name.lower()`  |
| **`.upper()`** | Converts all characters in a string to **uppercase**. | `str.upper()` | None |  Return a copy of the string with all the cased characters converted to uppercase. | `str_variable_name = str_variable_name.upper()`  |
| **`.split()`** | Splits a string into **a list of substrings** based on a specified **delimiter**. Splitting an empty string with a specified separator returns `['']`.| `str.split(sep=None, maxsplit=-1)` | - `sep` (optional): separator delimiter - string or char, such as `','`. Default: **whitespace**. <br> > If sep is **not specified or is `None`**, runs of consecutive whitespace are regarded as a single separator, and the result will contain **no empty strings** at the start or end if the string has **leading or trailing whitespace**. Consequently, splitting an empty string or a string consisting of just whitespace with a None separator returns `[]`. In addition, if `maxsplit==0`, **only leading runs of consecutive whitespace** are considered.  <br> > If `sep` is **given**, consecutive delimiters are deemed to delimit **empty strings**. <br><br> -`maxsplit` (optional): Maximum number of splits. Default: `-1` means **no limit** (all possible splits are made). | Returns a list of substrings. | Time: `O(n)`, Space: `O(n)` | `str_variable_name_1, str_variable_name_2, ... str_variable_name_n = str_variable_name.split()` <br><br> `'1,2,,3,'.split(',')` <br> ['1', '2', '', '3', ''] <br> `'   1   2   3   '.split()` <br> ['1', '2', '3'] <br> `"".split(None, 0)` <br> [] <br> `"   ".split(None, 0)`<br> [] <br> `"   foo   ".split(maxsplit=0)`<br>['foo   ']|
| `.rsplit()` | Behaves like `split()`, except for splitting from the **right**. | `str.rsplit(sep=None, maxsplit=-1)` | - `sep` (optional): separator delimiter - string or char, such as `','`. Default: **whitespace**. <br> -`maxsplit` (optional): at most maxsplit splits are done, the rightmost ones. Default: `-1` means **no limit** (all possible splits are made). | Returns a list of substrings. | Time: `O(n)`, Space: `O(n)` | |
| **`.join()`** | Joins **elements of an iterable** into a **single string** with a **specified delimiter** placed between each element. | `sep.join(iterable)` | - `sep`: separator delimiter.<br> -`iterable`: A sequence of strings (e.g., list, tuple, dict etc) to join together. When using it with a dict, it will only join the keys, not the values. | Returns a concatenated string. | Time: `O(n)`, Space: `O(n)` |
| **`.replace()`** | Return a copy of the string with all occurrences of an **old substring** **replaced** by a **new substring**; <br><br> case-sensitive (it treats uppercase and lowercase characters as distinct). | `str.replace(old, new, count=-1)` |- `old`: Substring to replace.<br> -`new`: Replacement string.<br> -`count` (optional): If `count` is given, only the first count occurrences are replaced. If `count` is not specified or `-1`, then **all occurrences** are replaced. | Returns a new string with replacements applied. | |`str_content = str_content.replace(":)", "🙂")`|
| `.find()` | Returns the lowest **index of the first occurrence** of a substring. | `str.find(sub, start, end)` | - `sub`: Substring to search.  <br> - `start`, `end` (optional): Index range to search. | Returns index if found, `-1` if not found. |  |
| **`.index()`** | Similar to **`find()`**, but **raises an error if not found**. | `str.index(sub, start, end)` | Same as `find()`. | Returns index if found; raises `ValueError` if not found. |  |
| **`.startswith()`** | Checks if a string **starts** with a specified prefix. | `str.startswith(prefix[, start[, end]]` | -`prefix`: Prefix to check. It can also be a **tuple** of prefixes to look for. <br> - `start`: (optional) test string beginning at that position. <br> - `end`: (optional) stop comparing string at that position.| Returns `True` if it starts with prefix, otherwise `False`. | `'Python'.startswith('Py')`<br> True <br>`'a tuple of prefixes'.startswith(('at', 'a'))` <br>True <br> `'Python is amazing'.startswith('is', 7)` <br>True |
| **`.endswith()`** | Checks if a string **ends** with a specified suffix. | `str.endswith(suffix[, start[, end]])` | -`suffix`: Suffix to check. It can also be a **tuple** of suffixes to look for. <br> - `start`: (optional) test string beginning at that position. <br> - `end`: (optional) stop comparing string at that position. Note: Using start and end is equivalent to `str[start:end].endswith(suffix)`| Returns `True` if it ends with suffix, otherwise `False`. |  `'Python'.endswith('on')` <br> True <br> `'a tuple of suffixes'.endswith(('at', 'in'))`  <br> False <br>`'a tuple of suffixes'.endswith(('at', 'es'))` <br> True <br> `'Python is amazing'.endswith('is', 0, 9)` <br> True <br> |
| **`.count()`** | Counts occurrences of a substring. | `str.count(sub, start, end)` | `sub`: Substring to count. `start`, `end` (optional): Index range to search. | Returns the number of occurrences of `sub`. |  |
| **`.isupper()`** | Checks if **all** cased **characters** in the string are **uppercase**.  | `str.isupper()` | None | `bool`: Return True if all cased characters in the string are uppercase and there is **at least one cased character**, `False` otherwise. | $O(n)$ | `"BANANA".isupper()` True <br> `' '.isupper()` False|
| **`.islower()`** | Checks if all cased characters in the string are **lowercase**. | `str.islower()` | None | `bool`: Return True if all cased characters in the string are lowercase and there is **at least one cased character**, `False` otherwise. | $O(n)$ | `"hello".islower()` True |
| `.isspace()` | Checks if the string contains only whitespace characters. | `str.isspace()` | None | `bool`: Returns `True` if all characters are whitespace, otherwise `False`.  | $O(n)$ | `"   ".isspace()` |
| **`.isdigit()`** | Checks if **all** characters are **digits**. | `str.isdigit()` | None | Returns `True` if all characters are digits, otherwise `False`. |  |
| **`.isalpha()`** | Checks if **all character**s** in the string are **letters (English (`A-Z`, `a-z`)**, also including Unicode letters for other languages). | `str.isalpha()` | None | Returns `True` if every character in the string is a letter; `False` if the string contains any numbers, spaces, or special characters. | Time: `O(n)`, Space: `O(1)` |
| **`.isalnum()`** | Checks if **all** characters are alphanumeric **(letters or digits)**. | `str.isalnum()` | None | Returns `True` if all characters are alphanumeric, otherwise `False`. |  |
| `.swapcase()` | Swaps case for all characters. | `str.swapcase()` | None | Returns a new string with uppercase converted to lowercase and vice versa. |  |
| `.ljust()` | Left-aligns a string, padding with spaces or specified characters. | `str.ljust(width, fillchar)` | `width`: Total width. `fillchar` (optional): Padding character. | Returns a left-aligned string. |  |
| `.rjust()` | Right-aligns a string, padding with spaces or specified characters. | `str.rjust(width, fillchar)` | Same as `.ljust()`. | Returns a right-aligned string. |  |
| `.center()` | Centers a string, padding with spaces or specified characters. | `str.center(width, fillchar)` | Same as `ljust()`. | Returns a centered string. |  |
| `.zfill()` | Pads the string with zeros on the left. | `str.zfill(width)` | `width`: Total width. | Returns a zero-padded string. |  |
| `.format()` | Formats a string by converting the argument as a formatted string. | `str.format(args...)` | `args...`: Values to format into the string. | Returns a formatted string. |  |
| `.removeprefix()` | Removes a specific prefix from the string (Python 3.9+). | `str.removeprefix(prefix)` | `prefix`: The prefix to remove. | Returns a new string without the prefix. |  |
| `.removesuffix()` | Removes a specific suffix from the string (Python 3.9+). | `str.removesuffix(suffix)` | `suffix`: The suffix to remove. | Returns a new string without the suffix. |  |
---