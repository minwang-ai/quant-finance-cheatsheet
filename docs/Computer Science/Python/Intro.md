# CS50P Lecture 0: Introduction

## Environment & Workflow

### Command line interface (CLI)
| CLI Command | When to use | Example | Note |
| :--- | :--- | :--- |:--- |
| `code` |  Create or open a file in VS Code to start coding |`code file_name.py`| `.py` means Python file|
| `python`| Run a Python script.  | `python file_name.py`| Python is not only a **language** but also a **interpreter** software, which will interpret the text and translate it into the zeros and ones that the computer can understand.  |
| enter **Interactive Mode** | Type `python` alone to run live code in terminal. |`python` | (rarely used in this course)|
| **Up-arrow key**  | recall recent terminal commands. | |
| **tab**| auto-complete current command|
| `..` | parent directory |
---


### Basic Linux CLI Commands

| Command | Purpose | Parameters / Options | Example |
|---|---|---|---|
| `ls` |**L**i**s**ts files and directories in the current directory or a specified path. | -`path` (optional): directory to list | `ls`<br>`ls /home/user` |
| `cp` | **C**o**p**ies a file or directory to another location. | -`source`: file/directory to copy<br>- `destination`: target path<br> - `-r`: copy directories recursively | `cp notes.txt backup.txt`<br>`cp -r folder1 folder2` |
| `mv` | **M**o**v**es or **renames** a file or directory. |-`source`: file/directory to move<br> - `destination`: target path or new name | `mv old.txt new.txt`<br>`mv file.txt docs/` |
| `rm` | **R**e**m**oves files or directories. | `file`: file to remove<br>`-r`: remove directories recursively<br>`-f`: force removal | `rm temp.txt`<br>`rm -r old_folder` |
| `mkdir` | **M**a**k**e a new **dir**ectory (folder). | - `directory_name`: name of the new directory<br> - `-p`: create parent directories as needed | `mkdir projects`<br>`mkdir -p week1/src` |
| `cd` | **C**hanges the current working **d**irectory. | - `directory` (optional): target directory, <br>, e.g.,`..` means parent directory <br> and `~` means home directory | `cd documents`<br>`cd ..`<br>`cd ~` |
| `rmdir` | **R**e**m**oves a **dir**ectory. | `directory_name`: empty directory to remove | `rmdir empty_folder` |
| `clear` | **Clears** the terminal screen. | None | `clear` |
---


## Escape Character - backslash \ 
Treats the next character as a literal (e.g., `\"` for quotes `"`).


## Core Programming Concepts
| Concept | Description | Notes |
| :--- | :--- | :--- |
| **Bugs** | Natural **normal** mistakes or problems in code to be solved. | **Error messages** can often inform you of your mistakes and provide clues on how to fix them. However, there will be many times when the interpreter is not this helpful. <br> **Avoid using global variables**.|
| **Variables** | **Containers** for **storing** values within your program in the computer memory. |**Avoid hard coding**! Use variables to store the values to use them later|
| **Assignment `=`** | Assign (copy) the value on the **right** to the variable on the **left**. |
| **Comments** | Developer notes are used to track **intentions** for a block of code and write **todo list (pseudo code)** to break a bigger program down into small tasks and structure your code | - single line: `#` or  <br> - multiple lines: Three Double quotes `""" comments """` |
| **Readability** and **simplicity**| Prioritize simple code and use comments to clarify logic. | Do not nest too much with multiple parentheses `((()))` |
| **Consistency**| use a consistent coding style | We can use either double quotes `" "`  or single quotes `' '` as long as it is consistent |
| **naming** | **snake_case** (words are separated by underscores `_`, with all letters in lowercase. )|
----

## Function Terminology 
| Term | Definition | Notes |
| :--- | :--- | :--- |
| **Function** | verbs or actions that let we do something that the computer or computer language already know how to perform | Functions takes intput (arguments/ parameters) as input and produce output (return value). |
| **Arguments** | The actual input values passed to a function to influence its behavior. |  Parameters and arguments are the **same** thing, but using different terms in different places. |
| **Parameters** (input) | Placeholders in the function definition determining what it can take. | - Positional parameters: passing with orders <br> - Named parameters: optional, e.g., `sep`, `end`.   |
| **Return Value** (output)| A value "passed back" from a function when function ends | we can use it directly or store it in a variable to use it later in the program. |
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
if __name__ == "__main__":
    main()
```


