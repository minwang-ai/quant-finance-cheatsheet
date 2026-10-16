# `#include <cctype>`


## Important Notes on `<cctype>` Usage
A crucial detail for **all** `<cctype>` functions:

‼️ **always cast** `char` arguments to `unsigned char`‼️ **before passing** them to `<cctype>` functions, to avoid undefined behavior for non-ASCII characters. For example: `std::isalpha(static_cast<unsigned char>(ch))`

Reasons:
- The argument passed to these functions **must** be representable as an **`unsigned char`** or must equal `EOF`.
- However, on many platforms, the standard `char` type is **signed** (ranging from `-128` to `127`). Passing a negative `char` value (such as extended ASCII characters like `ä`, `é`, or `0x80`–`0xFF`) invokes **undefined behavior**.



## Character Classification Functions 

| Method | Purpose | Syntax | Parameters | Return Value | Complexities |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `std::isalnum` | Checks if a character is **alphanumeric** (`A-Z`, `a-z`, `0-9`) | `int isalnum(int ch);` | `ch`: character to classify (as `int`, must be converted to unsigned char by `static_cast<unsigned char>(ch)`) | Non-zero value (`true`) if alphanumeric; `0` (`false`) otherwise | Time: $O(1)$<br>Space: $O(1)$ |
| `std::isalpha` | Checks if a character is **alphabetic** (`A-Z`, `a-z`) | `int isalpha(int ch);` | `ch`: character to classify (as `int`, must be converted to unsigned char by `static_cast<unsigned char>(ch)`) | Non-zero value (`true`) if alphabetic; `0` (`false`) otherwise | Time: $O(1)$<br>Space: $O(1)$ |
| `std::isdigit` | Checks if a character is a **decimal digit** (`0-9`) | `int isdigit(int ch);` | `ch`: character to classify (as `int`, must be converted to unsigned char by `static_cast<unsigned char>(ch)`) | Non-zero value (`true`) if decimal digit; `0` (`false`) otherwise | Time: $O(1)$<br>Space: $O(1)$ |
| `std::isxdigit` | Checks if a character is a **hexadecimal digit** (`0-9`, `a-f`, `A-F`) | `int isxdigit(int ch);` | `ch`: character to classify (as `int`, must be converted to unsigned char by `static_cast<unsigned char>(ch)`) | Non-zero value (`true`) if hex digit; `0` (`false`) otherwise | Time: $O(1)$<br>Space: $O(1)$ |


## Character Transformation Functions 

| Method | Purpose | Syntax | Parameters | Return Value | Complexities |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `std::tolower`| Converts an uppercase letter **to lowercase** according to the current C locale | `int tolower(int ch);` | `ch`: character to classify (as `int`, must be converted to unsigned char by `static_cast<unsigned char>(ch)`) | Lowercase character value; returns `ch` unchanged if not uppercase | Time: $O(1)$<br>Space: $O(1)$ |
