[TOC]

# Numbers
## Numbers 
| Category | Items | Examples |
| :--- | :--- | :--- | 
| **Data Types** | `int` (integers), <br> `float` (decimal/real numbers), <br> `complex(a,b)` (complex number a+bi). |
| **Type Casting** | **convert data types**  |e.g., after getting input from command line via `input()`, remember to use `int(variable)` or `float(variable)` to convert data types **from string to numbers**. |
| **Readable Big Numbers** | use **underscores** `_` as the seperator | `n = 100_000_000`|


## Python Arithmetic Operators

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
|---|---|---|---|---|---|---|
| `+` | **Adds** two numbers. | `x + y` | `x`, `y`: numeric values | Sum of `x` and `y` | Time: `O(1)`<br>Space: `O(1)` | `3 + 2 -> 5` |
| `-` | **Subtracts** the second number from the first. | `x - y` | `x`, `y`: numeric values | Difference of `x` and `y` | Time: `O(1)`<br>Space: `O(1)` | `5 - 2 -> 3` |
| `*` | **Multiplies** two numbers. | `x * y` | `x`, `y`: numeric values | Product of `x` and `y` | Time: `O(1)`<br>Space: `O(1)` | `4 * 3 -> 12` |
| `/` | **Divides** the first number by the second. Always Return a float in Python 3. | `x / y` | `x`, `y`: numeric values, `y != 0` | Quotient as `float` | Time: `O(1)`<br>Space: `O(1)` | `5 / 2 -> 2.5` |
| `//` | Performs **floor division**. | `x // y` | `x`, `y`: numeric values, `y != 0` | Floor of the division result | Time: `O(1)`<br>Space: `O(1)` | `5 // 2 -> 2`<br>`-5 // 2 -> -3` |
| `%` | **Modulo**: check if two numbers divide  evenly or have a **remainder**. It is essential for determining **Parity** (whether a number is even or odd) | `x % y` | `x`, `y`: numeric values, `y != 0` | Remainder of `x` divided by `y` | Time: `O(1)`<br>Space: `O(1)` | `5 % 2 -> 1` <br><br> - even: `n % 2 == 0` <br> - odd: `n % 2 != 0`|
| `**` | **Exponent**: Raises the first number to the power of the second. | `x ** y` | `x`: base value<br>`y`: exponent | `x` raised to the power `y` | Depends on operand size | `2 ** 3 -> 8` |

## Python Built-in Numeric Functions

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
|---|---|---|---|---|---|---|
| `abs()` | Return the **absolute value** of a number. | `abs(x)` | `x`: integer, float, or another numeric object | Absolute value of `x` | Time: `O(1)`<br>Space: `O(1)` | `abs(-7) -> 7` |
| `int()` | **Converts** a number or numeric string **to** an **integer**. For floats, it truncates toward `0`. | `int(x, base=10)` | - `x`: number, string, `bytes`, or `bytearray`<br> - `base` (optional): base of the input when `x` is a string-like value | Integer value | Time: `O(n)` for string input; `O(1)` for numeric input<br>Space: `O(1)` | `int("42") -> 42`<br>`int(3.9) -> 3` |
| `float()` | Converts a number or numeric string **to** a **floating-point** number. | `float(x)` | `x`: number or string | Floating-point value | Time: `O(n)` for string input; `O(1)` for numeric input<br>Space: `O(1)` | `float("3.14") -> 3.14` |
| `round()` | Rounds a number to the **nearest integer** or to the nearest **specified decimal points**. | `round(number[, ndigits])` | - `number`: value to round <br> - `ndigits` (optional): number of decimal places to keep | Rounded value | Time: `O(1)`<br>Space: `O(1)` | `round(3.14159, 2) -> 3.14`<br>`round(2.5) -> 2` |
| `pow()` | **Exponent**: Raises a base to a **power**; optionally computes modulo efficiently. | `pow(base, exp[, mod])` | - `base`: base value <br> - `exp`: exponent <br> - `mod` (optional): modulus | `base ** exp`, or modular exponentiation result | Depends on numeric type and operand size | `pow(2, 5) -> 32`<br>`pow(2, 5, 3) -> 2` |
| `divmod()` | Return the quotient and remainder together. | `divmod(a, b)` | `a`: dividend<br>`b`: divisor | Tuple `(quotient, remainder)` | Time: `O(1)`<br>Space: `O(1)` | `divmod(17, 5) -> (3, 2)` |
| `max()` | Return the largest item in an iterable or the largest of multiple arguments. | `max(iterable, *[, key, default])`<br>`max(arg1, arg2, *args, key=None)` | `iterable`: iterable to inspect<br>`arg1, arg2, ...`: values to compare<br>`key` (optional): function for comparison key<br>`default` (optional): fallback for empty iterable | Largest item | Time: `O(n)`<br>Space: `O(1)` | `max([3, 1, 9]) -> 9` |
| `min()` | Return the smallest item in an iterable or the smallest of multiple arguments. | `min(iterable, *[, key, default])`<br>`min(arg1, arg2, *args, key=None)` | `iterable`: iterable to inspect<br>`arg1, arg2, ...`: values to compare<br>`key` (optional): function for comparison key<br>`default` (optional): fallback for empty iterable | Smallest item | Time: `O(n)`<br>Space: `O(1)` | `min([3, 1, 9]) -> 1` |
| `sum()` | Adds items of an iterable from left to right, starting from an optional initial value. | `sum(iterable[, start])` | `iterable`: iterable of numbers<br>`start` (optional): initial value, default `0` | Total sum | Time: `O(n)`<br>Space: `O(1)` | `sum([1, 2, 3]) -> 6` |
----