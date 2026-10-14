[TOC]

# CS50P Lecture 1: Conditionals
Conditions allows us to ask questions and take different paths depending on the answers to those questions.
<br> Conditions are **Boolean** values (`True` or `False` from evaluating a **function call (return value)** or a **boolean expression**)  which is used to decide whether or not to execute code in one path over another. 



## Comparison Operators
Conditionals can use operators to compare the left-hand term to the right-hand term, resulting in a **Boolean** (`True` or `False`).

| Operator | Meaning | Usage | Note |
| :--- | :--- | :--- | :--- |
| `>` | Greater than | `x > y` | |
| `<` | Less than | `x < y` | |
| `>=` | Greater than or equal to | `x >= y` | |
| `<=` | Less than or equal to | `x <= y` | |
| `==` | **Equals**| `x == y` | - Double `==` compares values <br>- single `=` assigns a value. |
| `!=` | **Not equal to** | `x != y` | Return `True` if values are different. |

## Control Flow: if, elif, and else
Control flow determines which path the program takes based on the evaluation of conditions.

| Keyword | Logic | Efficiency |
| :--- | :--- | :--- |
| `if` | Starts a conditional block. | Always evaluated.  |
| `elif` | **"Else if"** making the conditions **mutually exclusive** - checked only if preceding `if`/`elif` were `False`. | Increases efficiency by avoiding unnecessary checks when preceding `if`/`elif` were `True`. |
| `else` | A "catch-all" default outcome for any case not met by `if` or `elif`. | No need to evaluate the last case |
### Template
```python
if condition_1:
    # action_1
elif condition_2:
    # action_2
elif condition_3:
    # action_3
# ...
else:
    # action_default
```

### Logical Operators
Used to combine multiple comparisons into a single statement.,

| Operator | Behavior | Example |
| :--- | :--- | :--- |
| `or` | `True` if **at least one** condition is true. | `if x < y or x > y:` |
| `and` | `True` only if **all** conditions are true. | `if score >= 90 and score <= 100:` <br> Note: Python allow us to **chain together** the operators and conditions in a  way quite uncommon to other programming languages: <br>  `if 90 <= score <= 100:` |
|`not` | negate the boolean expression after the keyword `not`| `if not (players == "multiplayer or players == "single-player")`


### Pythonic Patterns
Python offers unique, "Pythonic" ways to write more readable and concise code.

| Pattern | Description | Example |
| :--- | :--- | :--- |
| **Chained Comparison** | Chaining operators like in mathematics. | `if 90 <= score <= 100:` |
| **simplify if statement** | `True if condition else False`| `return True if n % 2 == 0 else False`|
| **Boolean Return** | **Directly** returning the result of a comparison. | `return n % 2 == 0` (Return `True` or `False`). |

## Match Statements
An alternative to `if/elif/else` for matching a variable against specific values, i.e., compares the value following the `match` keyword with each of the values following the `case` keyword. In the event a match is found, the  respective indented code section is executed, and the program stops the matching.  

| Keyword | Syntax | Purpose |
| :--- | :--- | :--- |
| **Match** | `match variable:` | Defines the variable to be checked. |
| **Case** | `case value:` | Code to run if the variable equals a specific value. |
| vertical bar `\|` | `case value_1 \| value_2:` | like `or` keyword: allows matching multiple values. |
| `_` | `case _:` | like `else` keywrod: catch-all default case. |

### Tamplate
```python
match condition_variable:
    case value_1:
            action_1
    case value_2:
            action_2
    ...
    case _:
            action_default 
```

## Reference Implementation: Parity Function
```python
def main():
    x = int(input("What's x? "))
    if is_even(x):
        print("Even")
    else:
        print("Odd")

# A Pythonic implementation of a parity check
def is_even(n):
    return n % 2 == 0

main()
```
