# CS50P Lecture 3: [Exceptions](https://docs.python.org/3/tutorial/errors.html)
Handle **something out of the ordinary** (exceptional).
All errors in Python are dealt with using exceptions, but **not all exceptions are errors**.

## Error Categories
| Error Type | Definition | When to be Caught | Example | Solution |
| :--- | :--- | :--- | :--- |:--- |
| **Syntax Error** | Errors in the **"grammar"** of the code. | caught before the program runs | - Missing quotes, unclosed parentheses (`unterminated`: started something but didn't stop it; `literal`:something we literally typed) <br> - Typos | Double-check typing; the interpreter usually points to the line. |
| **Runtime Error** | Errors that occur while the **program is running** due to **unexpected behavior**. |  caught during execution.| - Unexpected user input (ValueError: e.g., entering "cat" when a number is expected). | Implement "defensive programming" using try-except blocks. |
---

## Use `try/except` block to catch errors
These keywords allow you to `try` to run some code `except` if something goes wrong, to handle errors caused by unexpected events gracefully **without crashing**.

| Keyword | Defination | Behavior |  Purpose | Note |
| :--- | :--- | :--- |:--- |:--- |
| **`try`** | Try to execute a block of code that might cause errors. | If the whole block of code executes without any run-time errors, just run the code after the `try-except` block (e.g., `else` block if it exists).| testing out code before something goes wrong| - Only include the **fewest lines of code** possible that are **likely to fail** (because the error will be **catched immediately** and then the program **skip the rest of the `try`  block** and **jump to `except` block**) <br> - combine with **while loo**p** when handling **incorrect user input**: ask for input again.  |
| **`except`** | Defines the code to run to handle the error if a specific error occurs in the `try` block. | | Prevents the program from crashing by allowing a defined response to errors. | - It is a **bad practice to catch all runtime error in one except** using `except Exception:` <br> - **Better** practice: figure out what **kind of errors** could happen and handle them **seperately** explicitly. |
| **`else`** | Defines code to run **if no exceptions** were raised in the `try` block. || For logic that depends on the successful execution of the `try` block. |
---


| Keyword | Purpose | Behavior |
| :--- | :--- | :--- | 
| [**`pass`**](https://docs.python.org/3/tutorial/controlflow.html#pass-statements)| Silently **ignores** an exception. Acts as a **null placeholder**. The program will catch the error but take no action  | Execution continues to **the next line of code** immediately following the current block. |
| **`continue`** | **Interrupts** the current loop iteration. | Jumps directly **back to the top of the loop** (the `while True` line) and starts a new cycle|
---

### Syntax template - try-except block
```python
try:
    # Fewest lines of code that might raise errors
except SpecificErrorType:
    # Handle the specific type of error or simply pass the error without handling it
else:
    # code to run when there is no error raised
```

Note:
The exception code can **access a variable** that contains **information about exactly what the error was**.
Example:
```python
try:
    items = ['a', 'b']
    third = items[2]
    print("This won't print")
except Exception as e: # specify a variable name e then the exception clause code can refer to that variable name.
    print("got an error")
    print(e) # print out the information that would normally be printed as an error message

print("continuing")
```

### Example Implementation
The `get_int` Function demonstrates the "Pythonic" way to ensure a user provides a **valid input** integer without crashing the program.

```python
def main():
    # Pass the prompt as an argument for flexibility
    percentage = get_valid_fraction("Fraction: ")
    print(f"Fuel level: {percentage:.0%}")

def get_valid_fraction(prompt):
    while True:
        fraction = input(prompt)
        try:
            # Attempt parsing and conversion
            x_str, y_str = fraction.split("/") 
            percentage = int(x_str) / int(y_str)
        except (ValueError, ZeroDivisionError): 
            # Handle non-integers or division by zero by re-prompting
            continue
        except EOFError:
            # Move to a new line and exit when user hits Control-D
            print()
            break
        else:   # If the user enters a input in correct format, further validate it here
            if 0 <= percentage <= 1:
                return percentage
            # Otherwise, re-prompting again for invalid logic
            continue

if __name__ == "__main__":
    main()
```

## Common Error Type 
Understanding specific error names allows us to target error handling.

All exceptions are objects. The classes that define the objects are organized in a **hierarchy** - the **parent** class of a set of related exceptions will catch all exception messages for **itself and its child** exceptions. 
For example, an ArithmeticError exception will catch itself and all FloatingPointError, OverflowError, and ZeroDivisionError exceptions.

| Exception | Meaning | Common Scenario |
| :--- | :--- | :--- |
| **`ValueError`** | A function receives an argument of the right type but inappropriate value. | Using `int()` on a string that isn't a **numeric integer**, e.g., `int("1.5")`, `int("three")`, `int("cat")`. |
| **`NameError`** | Attempting to use a variable that has not been defined. | Accessing `x` after the line `x = int(input())` failed and skipped assignment. |
|**`ZeroDivisionError`**|The second argument of a division or modulo operation is zero| Calculating percentage `x/y` when the denominator `y` is 0|
| **`KeyError`**| Attempting to access a dictionary key that does not exist| access dictionary using `dict[key]` instead of `.get()`|
|[**`EOFError`**](https://docs.python.org/3/library/exceptions.html#EOFError)|"End of File" error, occurs when the user inputs **Control-D**| Used as a standard way for a user to signal they are finished with input|
| **`FileNotFoundError`**|Raised when a file or directory is requested but does not exist. | Attempting to open or read a file that is not in the current directory. |
| **`IndexError`** | Occurs when attempting to access an index that is outside the bounds of a list. | Accessing list index but index is **out of range**, e.g.,`sys.argv[1]` when the user forgot to provide a **command-line argument**. |
| **`requests.RequestException`** | The base class for all exceptions raised by the `requests` library. | A "catch-all" to prevent a crash if an **API query** fails due to network or connection issues. |
| **`AssertionError`**| Raised when an `assert` statement's boolean condition evaluates to `False`. | Raised during unit testing when checking if a function's returned value is not equal to its expectations |
---

## When to Use Exception
* Error Handling:
    * Handle Common Error Exceptions:
    * Graceful Degradation: Allow the program to continue running with reduced functionality rather than crashing.
* Cleanup Resource:
    * Ensure resources such as files, network connections, or hardware interfaces are properly closed or released in the event of an error.
* Graceful Shutdown when users Interrupt:
    * Handle user-generated interrupts (e.g., KeyboardInterrupt) to shut down processes cleanly, providing feedback to the user
* Maintain robustness of Long-Running Processes:
    * involving loops, sleep methods, or long-running tasks by handling potential interruptions or errors.



## Use `raise` to manually trigger an error

| Keyword | When to Use | Behavior | Syntax | Example |
| :--- | :--- | :--- | :--- |:--- |
| **`raise`** | **Alter** programmers and users when something is **wrong** or they use it in an incorrect way.| Manually triggers a specific exception. | `raise SpecificErrorType("ErrorMessage")` | `raise ValueError("Invalid age")` |
---

### Why use `raise`?
*   **Enforce Logic**: Python doesn't mind if an age is `-5`, but your program should. 
*   **Better Debugging**: It provides specific error messages that help you find bugs faster.

### Example Implementation
```python
def main():
    user_age = get_age()

def get_age():
    age = int(input("Age: "))
    if age < 0:
        # Trigger an error manually
        raise ValueError("Age cannot be negative!")
    return age

main()
```
