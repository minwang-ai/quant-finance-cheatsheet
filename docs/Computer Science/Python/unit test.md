
# CS50P Lecture 5: Unit Tests
Best practice: write a little extra code to test the code we wrote, testing individual units or functions.  


## Manual Testing vs Unit Testing

| Concept | Description | Typical Pattern / Command | Key Takeaway |
| :--- | :--- | :--- | :--- |
| **Manual Testing** | Running your program manually and typing in inputs to check if the outputs are correct. | `python filename.py` | Slow, error-prone, and doesn't scale as codebases grow. |
| **Unit Testing** (best practice) | Writing separate program(s) that call your individual functions with specific inputs and test if the returned values match expectations. | `python test_filename.py` | Most common in industry; allows you to **automate testing and catch "corner cases"**. |

Note:
Ensuring `if __name__ == "__main__": main()` so that testing file or program don't execute  the `main()` in the tested file when imported. 




## Keyword [`assert`](https://docs.python.org/3/reference/simple_stmts.html#assert)

The `assert` statement claims a boolean expression is true. If the boolean expression is true, nothing will happen; if the expression is false, Python raises an `AssertionError`.

| Feature | Syntax | Behavior on Failure | Example |
| :--- | :--- | :--- | :--- |
| **Basic Assert** | `assert boolean_expression` | Raises `AssertionError` and halts execution of subsequent tests in that function. | `assert square(2) == 4` |
| **Assert with Message** | `assert condition, "Error Msg"` | Raises `AssertionError` displaying the custom error message. | `assert square(2) == 4, "2 squared was not 4"` |
| **Catching AssertionError** | `try:` <br> `...`<br> `except AssertionError:` | Catch the failure for the test cases to log details without crashing the testing script. | `try:` <br>`assert square(2) == 4 except AssertionError:` <br>`...` |

### Why `assert` alone can be bloated:
Using manual `try...except AssertionError` blocks for dozens of test cases makes your testing code extremely bloated and repetitive. This is why automated third-party frameworks like `pytest` are used to handle these `try...except AssertionError` blocks.


## Automated Testing with [`pytest`](https://docs.pytest.org/en/7.1.x/getting-started.html)

`pytest` is a popular third-party testing framework that automates running unit tests and provides detailed, structured reports on which tests passed or failed.
Based on the results of the test, we can go correct our code.

| Command |  Purpose | Syntax / Action  | Notes |
| :--- | :--- | :--- | :--- |
| **Installation** |  Installs the `pytest` package from PyPI. |`pip install pytest` | Run once in your terminal. |
| **Run Single File**  | Runs all functions prefixed with `test_` in the specified test file.|`pytest test_filname.py` | Displays a summary of **passes (green dots .)** and **failures (red `F`)** with the **red `E`** providing hints about the **errors** detailed traceback. |
| **Dividing Tests** | Break each original function into **smaller bite-sized functions** and write separate `test_function()`. Divide one `test_function()` into different **groups** of tests   | `def test_function_groupname():` <br>`assert function(input) == true_value` | `pytest` runs **every** test function; a failure in one won't stop others from running so that **more errors are being displayed** allowing us to further explore the bugs.  |
| **Testing Exceptions** | Express we expect a specific error to be **raised** when running the block. | `import pytest` <br> `def test_function():`<br>`with pytest.raises(ErrorType):` <br> `# code that should raise the exception` |Requires `import pytest` at the top of the testing file. |

| Function | Purpose | Syntax | Parameters | Return Value | Common Scenario |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [**`pytest.approx()`**](https://docs.pytest.org/en/stable/reference/reference.html#pytest-approx) | Compare **floating-point numbers** safely with approximated value by allowing a small margin of error (**tolerance**) to bypass binary precision limitations. | `pytest.approx(expected, abs=None)` | - **expected**: The number (or list/dictionary of numbers) you expect. <br> - **abs** (Optional): Absolute tolerance (maximum allowed difference). *Set this tolerance based on specifications first; do not expand it just to force a failing test to pass.* | An **approximation wrapper object** that handles the margin of error calculations during comparisons. | Testing **float** calculations where minor rounding issues occur |

### Example: Testing Returns and Exceptions
```python
import pytest
from calculator import square

# Testing different groups e.g., positive, negative, zero
def test_positive():
    assert square(2) == 4
    assert square(3) == 9

def test_negative():
    assert square(-2) == 4
    assert square(-3) == 9

def test_zero():
    assert square(0) == 0

def test_float():
    assert square(0.231) == pytest.approx(0.0536, abs = 1e-5)

# Asserting that an exception is expected to be raised when passing wrong arguments
def test_error():
    with pytest.raises(TypeError):
        square("cat")   # code that should raise the exception
```






## Designing Code for Testability

To unit test a function effectively, the function **should return a value** rather than just having side effects, e.g., printing to the console. Only `main()` should call print.



## Organizing Tests into Folders

As programs grow, you should isolate your tests into a dedicated folder. `pytest` allows you to execute all tests in a directory with a single command.

| Step | Terminal Command / Filename | Purpose / Behavior |
| :--- | :--- | :--- |
| **1. Create Folder** | `mkdir test` | Creates a new directory named `test` to house all test files. |
| **2. Write Tests** | `code test/test_filename.py` | Put your test files inside the `test` directory (prefixed with `test_`). |
| **3. Package Marker** | `test/__init__.py` | **Mandatory.** An empty file with double underscores. Tells `pytest` that the folder can be treated as a package of tests. |
| **4. Run All Tests** | `pytest test` | Runs every test file found inside the `test` directory with a single terminal command. |
