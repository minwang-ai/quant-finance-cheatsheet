# CS50P Lecture 0

## Environment & Workflow

### CLI Command
| CLI Command | When to use | Example | Note |
| :--- | :--- | :--- |:--- |
| `code` |  Create or open a Python file in VS Code to start coding |`code file_name.py`|
| `python`| Run a Python script.  | `python file_name.py`| Python is not only a language but also a interpreter software, which will interpret the text and translate it into the zeros and ones that the computer can understand.  |
| **Interactive Mode** | Type `python` alone to run live code (rarely used in this course). |`python` |
| **Up-arrow key**  | recall recent terminal commands. | |
---

## Terminology 
### Core Programming Concepts
| Concept | Description | Notes |
| :--- | :--- | :--- |
| **Bugs** | Natural normal mistakes or problems in code to be solved. | Error messages can often inform you of your mistakes and provide clues on how to fix them. However, there will be many times when the interpreter is not this helpful. |
| **Variables** | Containers for storing values within your program in the computer memory. |**Avoid hard coding**! Use variables to store the values and return the values to use it later|
| **Assignment `=`** | Assigns the value on the right to the variable on the left. |
| **Comments** | Developer notes used to track intentions for a block of code and write todo list (pseudo code) to break a bigger program down into small tasks | - single line: `#` or  <br> - multiple lines: Three Double quotes `""" comments """` |
| **Scope** | A variable only exists within the context (block) where it is defined. | we can only use the variables there |
| **Readability** | Prioritize simple code and use comments to clarify logic. |, |
----

### Function Terminology 
| Term | Definition | Notes |
| :--- | :--- | :--- |
| **Function** | verbs or actions that let we do something that the computer or computer language already know how to perform | Functions takes arguments. |
| **Arguments** | The actual input values passed to a function to influence its behavior. |
| **Parameters** | Placeholders in the function definition determining what it can take. | Parameters and arguments are the **same** thing, but using different terms in different places |
| **Return Value** | A value "passed back" from a function to the rest of the program. |,, |
| **Nesting** | Running functions on functions; the inner one executes first. |,, |

## String Methods (`str`)
| Method / Syntax | Application | Source |
| :--- | :--- | :--- |
| `input("prompt")` | Prompts the user; always returns input as a string. |,,, |
| **Concatenation (+)** | Joins two strings together. |,,, |
| **Multiple Args (,)** | Passes separate values; `print()` automatically inserts a space. |,, |
| `.strip()` | Removes all whitespace from the left and right sides of a string. |,,, |
| `.title()` | Capitalizes the first letter of every word (Title Case). |,, |
| `.split()` | Splits a string into multiple variables based on a separator. |, |
| **Chaining** | Combine methods for efficiency: `name.strip().title()`. |,, |
| **Escape (\)** | Treats the next character as a literal (e.g., `\"` for quotes). |,, |

## Numbers and Operators
| Category | Items | Source |
| :--- | :--- | :--- |
| **Data Types** | `int` (integers/whole numbers), `float` (decimal/real numbers). |,,,,, |
| **Basic Operators** | `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponent). |,, |
| **Type Casting** | `int(variable)` or `float(variable)` to change data types. |,, |
| **Math Functions** | `round(n, [digits])` rounds; `pow(n, e)` raises to power. |,,,,, |

## Output Formatting (f-strings)
| Feature | Syntax Example | Source |
| :--- | :--- | :--- |
| **Line Ending** | `print(..., end="")` overwrites the default `\n`. |,,, |
| **Separator** | `print(..., sep=":")` overwrites the default space. |, |
| **Interpolation** | `f"hello, {variable_name}"` - injects variables into strings. |,,, |
| **Thousands** | `f"{z:,}"` formats number with commas (e.g., 1,000). |,, |
| **Precision** | `f"{z:.2f}"` rounds the output to two decimal places. |,, |

## Custom Functions (`def`)
| Element | Description | Source |
| :--- | :--- | :--- |
| **Keyword** | `def` is used to define your own special function. |,, |
| **Indentation** | Python uses whitespace to define blocks within a function. |,, |
| **Defaults** | Parameters can have default values: `def hello(to="world"):`. |,, |
| **Main Pattern** | Define a `main()` function and call it at the bottom of the script. |,,, |

```python
def main():
    x = int(input("What's x? "))
    print("x squared is", square(x))

def square(n):
    return n * n

main()
```
*(Source:)*


I have converted the previous list-based sections into detailed tables as requested, drawing directly from the lecture notes to ensure all key concepts like string methods, CLI commands, and function anatomy are clearly categorized and cited. I also included the recommended `main()` function structure as a reference code block.