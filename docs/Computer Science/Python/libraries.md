# CS50P Lecture 4: Libraries 
Instead of copying and pasting code from an old project of yours or others, you can **share** functions or features by **creating modules** and **import** modules/functions to your new project. 

## [Import Functions, Classes, Variables](https://www.pythontutorials.net/blog/from-import-vs-import/#key-differences-a-side-by-side-comparison)
| keywords | Purpose | Syntpurposeax |  Notes | Pros and Cons| When to Use|
| :--- | :--- | :--- | :--- | :--- | :--- | 
| **`import`** (**preferred**)| import the entire module (**all** the functions, classes, variables)  into the current namespace | `import <module>` <br> optional:<br> `import <module> as <alias>`| When we call the functions, we need to **specify the module name as a prefix** `module.function()`| + **Clarify the origin of names** of functions and variables to the module. Keep namespace clean, as it **prevents potential naming conflicts**. <br> + **Avoid ImportError** in case of **circular imports** <br> <br>- **Calling multiple times** of `module.function` makes the code **longer, ugly and annoying** |- not use the functions/classes/variables frequently <br> - want to clarify the origin of names|
| **`from ... import ...`**|  Case 1. only import some **specific functions/classes/variables** of a module into the current namespace <br><br> Case 2. import **submodules**| `from <module> import <function>,<class>, <variable>` <br> <br> ` from <module> import <submodule>` | When we call the functions, we simply call the function `function()` **without** specifying the module name as a prefix<br><br> Note:<br> **Avoid** using  `from <module> import *` because they make it unclear which names are present in the namespace (hide the origin of names, and risk overwriting built-in functions), confusing both readers and many automated tools. |- Without the module prefix leads to **cleaner code** when using that function multiple times <br> - We **cannot use** the same name for the variable or functions name as the one from the libraries, otherwise cause potential **naming conflicts**. | - Use a name **frequently** <br> - The **module name is long**|
---
Note:
- **Both** methods load the **entire module**.
- Group Imports Logically:
    - Standard library imports (e.g., `import os`).
    - Third-party imports (e.g., `import requests`).
    - Local/application-specific imports (e.g., `from mypackage import utils`).

## Built-in Modules

### [`random`](https://docs.python.org/3/library/random.html) & [`statistics`](https://docs.python.org/3/library/statistics.html)

| Method | Purpose | Syntax | Parameters | Return Value | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`random.choice()`** | Pick a **random element** from a sequence. | `random.choice(seq)` | `seq` (list/tuple/string) | A single random element | Use case: "Heads/Tails" logic. |
| **`random.randint()`** | Generate a **random integer** between two values inclusive. | `random.randint(start, end)` | - `start`, `end`: **inclusive** range [`start`, `end`] | `int` |  |
| **`random.shuffle()`** | **Reorder** a **list** randomly **in-place**. | `random.shuffle(x)` | `x` (a list) | `None` Modifies the original list |
| **`statistics.mean()`** | Calculate the arithmetic mean (average). | `statistics.mean(data)` | `data` (list of numbers) | `float` |  |
---



##  Command-Line Arguments: [`sys`](https://docs.python.org/3/library/sys.html)

The `sys` is a module that allows us to take user input from the command line when we automate running Python scripts quickly.

| Variable | Purpose | Syntax | Parameters (as input) | Return Value | Example/Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`sys.argv`** <br> stands for **arg**ument **v**ector | Access **a list of all the arguments** that user typed at the command line as inputs to the program when running python script to influence the behavior of the program. | `sys.argv[i]` | **`i` (index)**: An integer representing the position of the argument in the list. | `str` | - `sys.argv[0]` is always the python **file_name.py** <br> -  `sys.argv[1]` is the **first user input**. Using **slicing** `sys.argv[1:]` to skip the file name. <br><br> - Use **conditions**, e.g., `if len(sys.argv) == 2` to avoid **IndexError** (list index out of range) when accessing `sys.argv` <br><br> - Use **quote** for string `"str"` to pass a string as one argument |
| **`sys.exit()`** | **Exit** the whole program **earlier**  and optionally print an error message if an error arises. | `sys.exit(msg)` | **`msg` (string)** (optional): A message displayed to the user when the program terminates. |  | Used to stop a program gracefully if the user provides incorrect inputs. |
---
 





## Packages & APIs: [`requests`](https://docs.python-requests.org/) & [`json`](https://docs.python.org/3/library/json.html)

Third-party packages (installed via package manager `pip install package_name`) allow us to interact with external data and functionalities. [PyPI](https://pypi.org/) is a repository or directory of all available third-party packages currently  available.

**APIs** (application program interfaces) refer to **third-party services** that we can write code to connect to **download data**.
`requests` is a package that allows our program to make internet request using python code behave as a web browser. We can constructe URL by reading any API documentation.

The format in the downloaded text file is called **JSON** (javascript object notation) , a **language agnostic text-based** format that is used to exchange text-based data between applications. Python has a built-in `json` library that can help us interpret the  data received.

| Method | Purpose | Syntax | Parameter | Return Value | 
| :--- | :--- | :--- | :--- | :--- | 
| **`requests.get()`** | **Download** data from a URL and store it into response object, like typing url in a web browser and enter. | `Response = requests.get(url)` | url: in string format | `Response` object | 
| **`response.json()`** | Converts that JSON response into a Python dictionary so that we can extract specific information | `response.json()`| | `dict` or `list` | Converts JSON text into a format Python can use. |
| **`json.dumps()`** | Format JSON data for **nice printing**. | `json.dumps(obj, indent=2)` | - obj <br> - `indent`: Indentation making nested data more readable.| `str` |  |
---


## Making Your Own Libraries  
Use the following structure to **prevents the `main()` function from executing** if we `import` any function into another project. 

**Pattern: The Main Guard**
```python
def main():
    # Code to run only when executing this file directly
    ...

def my_function():
    # Reusable library function
    ...

if __name__ == "__main__":  # special variable __name__ is automatically set to be "__main__" when we run the python file from the command line
    main()
```

