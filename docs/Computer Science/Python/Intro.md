# CS50P Lecture 0 Introduction

## Environment & Workflow

### Command line interface (CLI)
| CLI Command | When to use | Example | Note |
| :--- | :--- | :--- |:--- |
| `code` |  Create or open a file in VS Code to start coding |`code file_name.py`| `.py` means Python file|
| `python`| Run a Python script.  | `python file_name.py`| Python is not only a **language** but also a **interpreter** software, which will interpret the text and translate it into the zeros and ones that the computer can understand.  |
| enter **Interactive Mode** | Type `python` alone to run live code in terminal. |`python` | (rarely used in this course)|
| **Up-arrow key**  | recall recent terminal commands. | |
| **tab**| auto-complete current command|
---

## Escape Character - backslash \ 
Treats the next character as a literal (e.g., `\"` for quotes `"`).


## Core Programming Concepts
| Concept | Description | Notes |
| :--- | :--- | :--- |
| **Bugs** | Natural **normal** mistakes or problems in code to be solved. | **Error messages** can often inform you of your mistakes and provide clues on how to fix them. However, there will be many times when the interpreter is not this helpful. |
| **Variables** | **Containers** for **storing** values within your program in the computer memory. |**Avoid hard coding**! Use variables to store the values to use them later|
| **Assignment `=`** | Assign (copy) the value on the **right** to the variable on the **left**. |
| **Comments** | Developer notes are used to track **intentions** for a block of code and write **todo list (pseudo code)** to break a bigger program down into small tasks and structure your code | - single line: `#` or  <br> - multiple lines: Three Double quotes `""" comments """` |
| **Readability** and **simplicity**| Prioritize simple code and use comments to clarify logic. | Do not nest too much with multiple parentheses `((()))` |
| **Consistency**| use a consistent coding style | We can use either double quotes `" "`  or single quotes `' '` as long as it is consistent |
----

## Function Terminology 
| Term | Definition | Notes |
| :--- | :--- | :--- |
| **Function** | verbs or actions that let we do something that the computer or computer language already know how to perform | Functions takes arguments. |
| **Arguments** | The actual input values passed to a function to influence its behavior. |  Parameters and arguments are the **same** thing, but using different terms in different places. |
| **Parameters** | Placeholders in the function definition determining what it can take. | - Positional parameters: passing with orders <br> - Named parameters: optional, e.g., `sep`, `end`.   |
| **Return Value** | A value "passed back" from a function when function ends | we can use it directly or store it in a variable to use it later. |
| **Nesting functions** | Running functions inside of other functions. The inner one executes first, so the return value of the inner function becomes the argument of outer function. | e.g. `x = int(input("What's x? "))`|
| **Chain methods** | Combine methods for readability and simplicity | e.g., `name.strip().title()` | 
| **Scope** | A variable only exists within the context (block) where it is defined. | we can only use the variables there |
---


## Define Custom Functions (Keyword `def`)
To avoid repeat writing similar codes

### Tamplate
```python
# Define main function on the top
def main():
    
# Define other helper functions after main()
def method_name(parameter_1 = default_value_1, ... , parameter_n = default_value_n):
    """ comments and documentation """
    # uses indentation (tab) to define blocks within a function
    # indented code
    return return_object

# Call main() function at the bottom
main()
```


