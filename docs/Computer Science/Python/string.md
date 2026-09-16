# String (`str`)

## String Operator Overloading
| Syntax | Application | Example |
| :--- | :--- | :--- | 
| **Concatenation (+)** | chain strings together. | ` str1 + str2` |
| **multiplicaton (*)** | repeat strings **n times** | ` print(str_variable * n)` |
---


## Output Formatting (f-strings)
prefixing a string with `f`, expressions inside {} are evaluated at runtime, making it simple to embed variable values and expressions directly within string literals. 

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
| **Interpolation** | **Inject variables** into strings. |`f"other_text, {variable_name or expression}"` |
| **Thousands** | Formate **large number** variable `num` with commas `,` | `f"{num:,}"` | `print(f"{num:,}")` <br> 1000000 -> 1,000,000 |
| **Precision** | **round** the output variable `num` to the **nearest `n` decimal points**. Here `n` is a number and it could not be `0`. |`f"{num:.nf}"` | `print(f"{num:.2f}")` <br> 3.1415926 -> 3.14 |
|**Percentage**| automatically convert float output variable `num` to percentage, add `%`sign and keep the **nearest `n` decimal points**.  | `f"{num:.n%}"`  | `f"{num:.0%}"`<br> 0.75 -> "75%" | 
| **Padding** | **Pad or fill** a string with the specified **padding character** `pad_char` to a specific **total width** `total_width`:| - Center the string and **pad both sides using `^`:** <br>`f"{str:{pad_char}^total_width}"` <br> - Padding from the **right**  using `<`:<br> `f"{str:{pad_char}<total_width}"` <br> - Padding from the" **left**  using `>`:<br> `f"{str:{pad_char}>total_width}"` - **zero-padding** for **numbers**: `f"{num:0total_width}"` | - `f"{str:{pad_char}^{width}}"` string "GFG" pad with character "-" becomes "----GFG-----" <br> - zero-padding: `f"{num:02}"`  "9" becomes "09"|
---


## [String build-in methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
|---|---|---|---|---|---|---|
| `len()` | Return the length of the string. | `len(str)` | `str`: The input string. | Return an integer representing the number of characters in the string. |  |
| **`.strip()`** | **Stripe oﬀ** (Removes) any **leading** and **trailing specified characters** (default: whitespace). | `str.strip([chars])` | `chars` (optional): specified characters to remove. | Return a new string with characters removed from both ends. | | `str_variable_name = str_variable_name.strip()` |
| `.lstrip()` | Remove leading (**left**) whitespace or specified characters. Note: not remove characters in between | `str.lstrip([chars])` | Same as `strip()`. | Return a new string with leading characters removed. |  |
| `.rstrip()` | Remove trailing (**right**) whitespace or specified characters. <br> Note: not remove characters in between | `str.rstrip([chars])` | Same as `strip()`. | Return a new string with trailing characters removed. |  |
| **`.capitalize()`** | **Capitalize** the **first** character of the **string**. | `str.capitalize()` | None | Return a new string with only the first letter capitalized. |  | `str_variable_name = str_variable_name.capitalize()` |
| **`.title()`** | **Capitalize** the **first** letter of **each word**. | `str.title()` | None | Return a new string with each word's first letter capitalized. |  | `str_variable_name = str_variable_name.title()` |
| **`.lower()`** | Convert all characters in a string to **lowercase**. | `str.lower()` | None | Return a copy of the string with all the cased characters converted to lowercase. | `str_variable_name = str_variable_name.lower()`  |
| **`.upper()`** | Convert all characters in a string to **uppercase**. | `str.upper()` | None |  Return a copy of the string with all the cased characters converted to uppercase. | `str_variable_name = str_variable_name.upper()`  |
| **`.split()`** | Split a string into **a list of substrings** based on a specified **delimiter**. Splitting an empty string with a specified separator Return `['']`.| `str.split(sep=None, maxsplit=-1)` | - `sep` (optional): separator delimiter - string or char, such as `','`. Default: **whitespace**. <br> > If sep is **not specified or is `None`**, runs of consecutive whitespace are regarded as a single separator, and the result will contain **no empty strings** at the start or end if the string has **leading or trailing whitespace**. Consequently, splitting an empty string or a string consisting of just whitespace with a None separator Return `[]`. In addition, if `maxsplit==0`, **only leading runs of consecutive whitespace** are considered.  <br> > If `sep` is **given**, consecutive delimiters are deemed to delimit **empty strings**. <br><br> -`maxsplit` (optional): Maximum number of splits. Default: `-1` means **no limit** (all possible splits are made). | Return a list of substrings. <br> If **failed**, raise **`ValueError`**: not enough values to unpack | Time: `O(n)`, Space: `O(n)` | `str_variable_name_1, str_variable_name_2, ... str_variable_name_n = str_variable_name.split()` <br><br> `'1,2,,3,'.split(',')` <br> ['1', '2', '', '3', ''] <br> `'   1   2   3   '.split()` <br> ['1', '2', '3'] <br> `"".split(None, 0)` <br> [] <br> `"   ".split(None, 0)`<br> [] <br> `"   foo   ".split(maxsplit=0)`<br>['foo   ']|
| `.rsplit()` | Behave like `split()`, except for splitting from the **right**. | `str.rsplit(sep=None, maxsplit=-1)` | - `sep` (optional): separator delimiter - string or char, such as `','`. Default: **whitespace**. <br> -`maxsplit` (optional): at most maxsplit splits are done, the rightmost ones. Default: `-1` means **no limit** (all possible splits are made). | Return a list of substrings. | Time: `O(n)`, Space: `O(n)` | |
| **`.join()`** | Join **elements of an iterable** into a **single string** with a **specified delimiter** placed between each element. | `sep.join(iterable)` | - `sep`: separator delimiter.<br> -`iterable`: A sequence of strings (e.g., list, tuple, dict etc) to join together. When using it with a dict, it will only join the keys, not the values. | Return a concatenated string. | Time: `O(n)`, Space: `O(n)` |
| [**`.replace()`**](https://docs.python.org/3/library/stdtypes.html#str.replace) | **Replace all** occurrences of an **old substring** by a **new substring**. Use case: **reformating** string (e.g., phone number, date). <br><br>**case-sensitive**: It treats uppercase and lowercase characters as different. | `str.replace(old, new, count=-1)` |- `old`: old substring that needs to be replaced.<br> -`new`: new substring that will replace old substring.<br> -`count` (optional): Specifies the **maximum number of replacements** to perform. <br> If `count` is given, only the first `count` occurrences are replaced. If `count` is **not specified or `-1`**, then **all occurrences** are replaced. | Return a **new string** with replacements applied. <br> (The original string is not modified because strings in Python are immutable.) | |`str_content = str_content.replace(":)", "🙂")`|
| `.find()` | Return the **lowest index** in the string where substring `sub` is found within the slice `s[start:end]`. <br> <br> <br>**`.index()`** is similar to **`find()`**, but can be used for **all sequence** and **raises an error if not found**.| `str.find(sub[, start[, end]])` | - `sub`: Substring to search.  <br> - `start`, `end` (optional): Index range to search. | Return index if found; return `-1` if not found. |  |
| **`.startswith()`** | Check if a string **starts** with a specified prefix. | `str.startswith(prefix[, start[, end]]` | -`prefix`: Prefix to check. It can also be a **tuple** of prefixes to look for. <br> - `start`: (optional) test string beginning at that position. <br> - `end`: (optional) stop comparing string at that position.| Return `True` if it starts with prefix, otherwise `False`. | `'Python'.startswith('Py')`<br> True <br>`'a tuple of prefixes'.startswith(('at', 'a'))` <br>True <br> `'Python is amazing'.startswith('is', 7)` <br>True |
| **`.endswith()`** | Check if a string **ends** with a specified suffix. | `str.endswith(suffix[, start[, end]])` | -`suffix`: Suffix to check. It can also be a **tuple** of suffixes to look for. <br> - `start`: (optional) test string beginning at that position. <br> - `end`: (optional) stop comparing string at that position. Note: Using start and end is equivalent to `str[start:end].endswith(suffix)`| Return `True` if it ends with suffix, otherwise `False`. |  `'Python'.endswith('on')` <br> True <br> `'a tuple of suffixes'.endswith(('at', 'in'))`  <br> False <br>`'a tuple of suffixes'.endswith(('at', 'es'))` <br> True <br> `'Python is amazing'.endswith('is', 0, 9)` <br> True <br> |
| **`.count()`** | Count occurrences of a substring. | `str.count(sub, start, end)` | `sub`: Substring to count. `start`, `end` (optional): Index range to search. | Return the number of occurrences of `sub`. |  |
| **`.isupper()`** | Check if **all** cased **characters** in the string are **uppercase**.  | `str.isupper()` | None | `bool`: Return True if all cased characters in the string are uppercase and there is **at least one cased character**, `False` otherwise. | $O(n)$ | `"BANANA".isupper()` True <br> `' '.isupper()` False|
| **`.islower()`** | Check if all cased characters in the string are **lowercase**. | `str.islower()` | None | `bool`: Return True if all cased characters in the string are lowercase and there is **at least one cased character**, `False` otherwise. | $O(n)$ | `"hello".islower()` True |
| `.isspace()` | Check if the string contains only whitespace characters. | `str.isspace()` | None | `bool`: Return `True` if all characters are whitespace, otherwise `False`.  | $O(n)$ | `"   ".isspace()` |
| **`.isdigit()`** | Check if **all** characters are numeric **digits (0-9)** . | `str.isdigit()` | None | Return `True` if all characters are digits, otherwise `False`. |  |
| **`.isalpha()`** | Check if **all character**s** in the string are **letters (English (`A-Z`, `a-z`)**, also including Unicode letters for other languages). | `str.isalpha()` | None | Return `True` if every character in the string is a letter; `False` if the string contains any numbers, spaces, or special characters. | Time: `O(n)`, Space: `O(1)` |
| **`.isalnum()`** | Check if **all** characters are alphanumeric **(letters or digits)**. | `str.isalnum()` | None | Return `True` if all characters are alphanumeric, otherwise `False`. |  |
| `.swapcase()` | Swaps case for all characters. | `str.swapcase()` | None | Return a new string with uppercase converted to lowercase and vice versa. |  |
| `.ljust()` | Left-aligns a string, padding with spaces or specified characters. | `str.ljust(width, fillchar)` | `width`: Total width. `fillchar` (optional): Padding character. | Return a left-aligned string. |  |
| `.rjust()` | Right-aligns a string, padding with spaces or specified characters. | `str.rjust(width, fillchar)` | Same as `.ljust()`. | Return a right-aligned string. |  |
| `.center()` | Centers a string, padding with spaces or specified characters. | `str.center(width, fillchar)` | Same as `ljust()`. | Return a centered string. |  |
| `.zfill()` | Pads the string with zeros on the left. | `str.zfill(width)` | `width`: Total width. | Return a zero-padded string. |  |
| `.format()` | Formats a string by converting the argument as a formatted string. | `str.format(args...)` | `args...`: Values to format into the string. | Return a formatted string. |  |
| `.removeprefix()` | Removes a specific prefix from the string (Python 3.9+). | `str.removeprefix(prefix)` | `prefix`: The prefix to remove. | Return a new string without the prefix. |  |
| `.removesuffix()` | Removes a specific suffix from the string (Python 3.9+). | `str.removesuffix(suffix)` | `suffix`: The suffix to remove. | Return a new string without the suffix. |  |
---