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
| [**`pass`**](https://docs.python.org/3/tutorial/controlflow.html#pass-statements) | Silently ignores an exception. | The program will catch the error but take no action | In some cases, we want to be very clear to the user what error is being produced; other times, we might decide to simply ask the user for input again. |
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
The `get_int` Function demonstrates the "Pythonic" way to ensure a user provides a valid integer without crashing the program.

```python
def main():
    # Pass the prompt as an argument for flexibility
    x = get_int("What's x? ")
    print(f"x is {x}")

def get_int(prompt):
    while True:
        try:
            # If this succeeds, the value is returned immediately, exiting the loop
            return int(input(prompt))
        except ValueError:
            # If the user enters a string, pass silently and loop again
            pass

main()
```

## Common Error Type 
Understanding specific error names allows us to target error handling.

All exceptions are objects. The classes that define the objects are organized in a **hierarchy** - the **parent** class of a set of related exceptions will catch all exception messages for **itself and its child** exceptions. 
For example, an ArithmeticError exception will catch itself and all FloatingPointError, OverflowError, and ZeroDivisionError exceptions.

| Exception | Meaning | Common Scenario |
| :--- | :--- | :--- |
| **`ValueError`** | A function receives an argument of the right type but inappropriate value. | Attempting to convert a string (like "cat") into an integer: `int("cat")`. |
| **`NameError`** | Attempting to use a variable that has not been defined. | Accessing `x` after the line `x = int(input())` failed and skipped assignment. |
| **`KeyError`**||
| **`FileNotFoundError`**||
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
