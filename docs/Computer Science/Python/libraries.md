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

### [`random`](https://docs.python.org/3/library/random.html) 

| Method | Purpose | Syntax | Parameters | Return Value | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`random.seed()`** | By setting a **fixed** seed value, **randomness becomes reproducible**, which is essential for debugging, testing and scientific experiments. | `random.seed(a=None, version=2)` | - `a` (Optional): it's the seed value (integer, float, str, bytes or bytearray). If None, the system time is used.<br> - `version`(Optional): defaults value is 2, using a more advanced seeding algorithm. version=1 uses an older method. | None | **Important** for reproductivity |
| **`random.choice()`** | Choose **a** random element from a sequence. | `random.choice(seq)` | `seq` (list/tuple/string) | A single random element | Use case: "Heads/Tails" logic. |
| **`random.choices()`** | Choose **multiple** random elements from a sequence (sampling **with replacement**, meaning each time only choose one and put it back). | `random.choice(seq, k)` | -`seq` (list/tuple/string) <br> - `k`: the number of items to randomly choose <br> - `weights`: (optional) a list of weights in percentage (add up to **100**) for each item in the sequence | A list of random elements |  |
| **`random.samples()`** | Choose **multiple** random elements from a sequence (sampling **without replacement**, meaning choose one shuffling the remaining and choose again without putting the chose one back). | `random.sample(seq, k)` | -`seq` (list/tuple/string) <br> - `k`: the number of items to randomly choose | A list of random elements |  |
| **`random.randint()`** | Generate a **random integer** between two values inclusive. | `random.randint(start, end)` | - `start`, `end`: **inclusive** range [`start`, `end`] | `int` |  |
| **`random.randrange()`** | Generate a **random integer** within a specified range.  | `random.randrange(start, stop, step)` | - `start` (optional): The starting number of the range. Default is 0. <br> - `stop` (required): The upper limit (**exclusive**) for the generated number <br> - `step` (optional): The step size. Default is 1 and cannot be zero (raises `ValueError`).| `int` | - Even or odd Numbers <br> - Dice roll - <br> Random selection from a list: random index |
| **`random.shuffle()`** | **Reorder** a **list** randomly **in-place**. | `random.shuffle(x)` | `x` (a list) | `None` Modifies the original list |
---

### [`statistics`](https://docs.python.org/3/library/statistics.html)
| Method | Purpose | Syntax | Parameters | Return Value | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`statistics.mean()`** | Calculate the arithmetic mean (average). | `statistics.mean(data)` | `data` (list of numbers) | `float` |  |
---

### `datetime`


#### [`date`](https://docs.python.org/3/library/datetime.html#date-objects)

`from datetime import date`
| Method / Class / Attribute | Purpose | Syntax | Parameters  | Return Value |
| :--- | :--- | :--- | :--- | :--- |
| **`date`** *(Class)* | create a calendar **date** (year, month, day) in the Gregorian calendar. | `d = date(year, month, day)` | - **`year`**: Integer (e.g., `2024`).<br>- **`month`**: Integer (`1`–`12`).<br>- **`day`**: Integer (`1`–`31`). | An instance of a **`date` object**. |
| **[`date.today()`](https://docs.python.org/3/library/datetime.html#datetime.date.today)** | Retrieves the current local calendar date. | `today_date = date.today()` | None. | a **`date` object** representing today. |
| **`date.fromisoformat()`** | Parses an ISO 8601 formatted date string (`YYYY-MM-DD`). | `d = date.fromisoformat(date_str)` | **`date_str`**: String in `YYYY-MM-DD` format. | A **`date` object** if valid; automatically; raises a **`ValueError`** if invalid. |
---

### [timedelta objects](https://docs.python.org/3/library/datetime.html#timedelta-objects)
`from datetime import timedelta`
| Method / Class / Attribute | Purpose | Syntax | Parameters  | Return Value |
| :--- | :--- | :--- | :--- | :--- |
| **Date Subtraction (`-`)** | Computes the difference between two `date` objects (operator overloading via `__sub__`). | `delta = date2 - date1` | - **`date2`**: End date object.<br>- **`date1`**: Starting date object. | a **`timedelta` object** representing the duration between the two dates, which itself comes with several (read-only) "instance attributes" |
| **`timedelta()`** | Constructs a **custom time interval** for relative date calculations/testing. | `delta = timedelta(days=365)` | **`days`**: Integer representing duration in days. | A **`timedelta` object**. |
| **`timedelta.days`** *(Attribute)* | Accesses the total number of days stored in a `timedelta` object. | `num_days = delta.days` | None (read-only attribute). | An **integer** representing the total days difference. |
---


##  Command-Line Arguments: [`sys`](https://docs.python.org/3/library/sys.html)

The `sys` is a module that allows us to take user input from the command line when we automate running Python scripts quickly.

| Variable | Purpose | Syntax | Parameters (as input) | Return Value | Example/Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`sys.argv`** <br> stands for **arg**ument **v**ector | Access **a list of all the arguments** that user typed at the command line as inputs to the program when running python script to influence the behavior of the program. | `sys.argv[i]` | **`i` (index)**: An integer representing the position of the argument in the list. | `str` | - `sys.argv[0]` is always the python **file_name.py** <br> -  `sys.argv[1]` is the **first user input**. Using **slicing** `sys.argv[1:]` to skip the file name. <br><br> - Use **conditions**, e.g., `if len(sys.argv) == 2` to avoid **IndexError** (list index out of range) when accessing `sys.argv` <br><br> - Use **quote** for string `"str"` to pass a string as one argument |
| **`sys.exit()`** | **Exit** the whole program **earlier**  and optionally print an error message if an error arises. | `sys.exit(msg)` | **`msg` (string)** (optional): A message displayed to the user when the program terminates. |  | Used to stop a program gracefully if the user provides incorrect inputs. |
| **[`os.path.splitext()`](https://docs.python.org/3/library/os.path.html#os.path.splitext)** | Splits a file path into its root name and its **file extension**. | `root, ext = os.path.splitext(path)` | **`path`**: A string representing the filename or file path. | A **tuple of two strings** `(root, ext)`. | *Example: `"photo.png"` returns `("photo", ".png")`.* |
---
 





## Packages & APIs: [`requests`](https://docs.python-requests.org/) & [`json`](https://docs.python.org/3/library/json.html)

Third-party packages (installed via package manager `pip install package_name`) allow us to interact with external data and functionalities. [PyPI](https://pypi.org/) is a repository or directory of all available third-party packages currently  available.

**APIs** (application program interfaces) refer to **third-party services** that we can write code to connect to **download and access data**.
`requests` is a package that allows our program to make internet request using python code behave as a web browser. We can **constructe URL** by reading the API **documentation** we request.

The format in the downloaded text file is called **JSON** (javascript object notation) , a **language agnostic text-based** format that is used to exchange text-based data between applications. Python has a built-in `json` library that can help us interpret the  data received.

| Method | Purpose | Syntax | Parameter | Return Value | 
| :--- | :--- | :--- | :--- | :--- | 
| **`requests.get()`** | **Download data** from a URL and store it into response object, like typing url in a web browser and enter. | `response = requests.get(url)` | url: The https url to the API in string format. Check the documentation of the API.| `Response` object | 
| **`response.json()`** | Converts that **JSON** response into a Python **dictionary** so that we can extract specific information | `content = response.json()`| | `dict` or `list` | Converts JSON text into a format Python can use. |
| **`json.dumps()`** | Format JSON data for **nice printing**. | `json.dumps(obj, indent=2)` | - obj <br> - `indent`: Indentation making nested data more readable.| `str` |  |
---

**Best practice**: using **try-except block** for requests:

**get.py**
```python
import requests

def get_item(query):
    payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
    try:
        response = requests.get(
            "https_url",
            params = payload
        )
        response.raise_for_status()  # will raise an HTTPError if the HTTP request returned an unsuccessful status code.
    except requests.RequestException:
        print("Couldnt complete request!")
        return []
    
    content = response.json()
    return [item["key"] for item in content["data"]]
```

**main.py**
```python
from package.module import functions

def main():
    item = input("Item: ")
    items = get_item(query=item)
    for item in items:
        # access data

if __name__ == "__main__": 
    main()
```
### Third-Party Library

### `inflect` Module
for **generating natural language plurals, ordinals, and converting numbers to words**.

`import inflect`

| Method | Purpose | Syntax | Parameters  | Return Value  |
| :--- | :--- | :--- | :--- | :--- |
| **`inflect.engine()`** | The important first step: creates an instance of the **inflect engine** to perform text generation. |`p = inflect.engine()` | None. | An **`inflect.engine` object**. |
| **`p.number_to_words()`** | Converts **numeric integers into English words**. | `words = p.number_to_words(number, andword="")` | - **`number`**: Number to convert.<br>- **`andword`** *(Optional)*: String to join tens/hundreds (set to `""` to **remove "and"**). | A **string** containing the number spelled out in words (in **lowercase**). |
---

### PDF Generation (`fpdf2`) 

The `FPDF` class is the primary engine for creating and exporting PDF documents.

The canvas uses a standard 2D millimeter-based coordinate system 
- Origin $(0,0)$: Located at the **top-left corner** of the PDF page
- $X$-Axis (Horizontal): Measures distance from the left edge ($0\text{ mm}$) to the right edge ($210\text{ mm}$).
- $Y$-Axis (Vertical): Measures distance from the top edge ($0\text{ mm}$) down to the bottom edge ($297\text{ mm}$).
- **Internal Cursor**: fpdf2 maintains an internal drawing cursor $(x, y)$ that tracks where the next text or image will be placed automatically unless we override it.


| Method / Constructor | Purpose | Syntax Example | Parameters / Options | Return Value / Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **`FPDF()` Constructor** | Instantiates a new PDF document object with page dimensions and units. | `pdf = FPDF(orientation="P", unit="mm", format="A4")` | - **`orientation`**: `"P"` (Portrait) or `"L"` (Landscape) or `"Letter"`, `Legal`. <br>- **`unit`**: Measure unit (`"mm"`, `"cm"`, `"pt"`, `"in"`).<br>- **`format`**: Standard page sizes (`"A4"` = 210x297mm). | Returns a new **`FPDF` instance**. |
| **`pdf.add_page()`** | Adds a **new blank page** to the PDF document. <br><br> The origin is at the **upper-left corner** and the current position is by default placed at 1 cm from the borders; the margins can be changed with `set_margins`. | `pdf.add_page()` | None. | Appends a page |
| **`pdf.set_font()`** | Before we can print text, it is **mandatory**, otherwise the document would be invalid.  | `pdf.set_font("helvetica", style="B", size=30)` | - **`family`**: Built-in fonts (`"helvetica"`, `"times"`, `"courier"`, `Symbol` and `ZapfDingbats`).<br>- **`style`**: `""` (Regular), `"B"` (Bold), `"I"` (Italic), `"U"` (Underline).<br>- **`size`**: Font size in points (`pt`). | Updates active document font settings. |
| **`pdf.set_text_color()`** | Sets the **foreground text color** using RGB or grayscale values. | `pdf.set_text_color(255, 255, 255)` | - **RGB**: Three integers (`0`–`255`) for Red, Green, Blue (e.g., **`255, 255, 255` for white**).<br>- **Grayscale**: Single integer (`0`–`255`). | Changes active text color. |
| **`pdf.cell()`** | Renders a **rectangular block** of text at the current cursor position. | `pdf.cell(w=0, h=10, text="string text", new_x= , new_y="NEXT", align="C")` | - **`w`**: Cell width (`0` stretches cell **across entire printable width**).<br>- **`h`**: Cell height in mm (negative height moves cursor upward). <br> - **`new_x`**: New current position in x after the call. <br>- **`new_y`**: Set to `"NEXT"` to automatically advance cursor to next line. - <br> center (bool): center the cell horizontally on the page. <br>- **`align`**: `"C"` (Center), `"L"` (Left), `"R"` (Right), `"X:`(center around current x position)| Draws text cell on the page. |
| **`pdf.image()`** | Embeds an image (PNG/JPEG) onto the page. | `pdf.image("image.png", x="C", y=, w=width)` | - **`name`**: Path to image file.<br>- **`x`**: Horizontal coordinate or `"C"` (Center horizontally).<br>- **`y`**: Vertical coordinate in mm (omitting `y` uses current cursor position).<br>- **`w`**: Target width in mm (height `h` **scales automatically**). | Renders image on the PDF canvas. |
| **`pdf.set_y()`** | Sets the vertical position of the **cursor** explicitly. | `pdf.set_y(140)` | **`y`**: Absolute vertical position in mm (positive value measured from top edge; negative value measured from bottom). | Moves active drawing cursor vertically. |
| **`pdf.epw`** *(Property)* | Gets the **Effective Page Width** (total width minus left and right margins). | `w = pdf.epw` | None (read-only property). | Returns float representing printable width in mm. |
| **`pdf.output()`** | Compiles and writes the PDF data to a file on **disk**. | `pdf.output("file_name.pdf")` | **`name`**: Destination filename or file path string. | Saves the generated PDF file to disk. |
---

#### Object-Oriented Subclassing with `FPDF`

| Concept | Syntax | Purpose |
| :--- | :--- | :--- |
| **Subclassing `FPDF`** | `class NewClass(FPDF):` | Extends the base `FPDF` class to encapsulate **custom PDF layouts and header** behaviors. |
| **Parent Initialization (`super()`)** | `super().__init__(orientation="P", unit="mm", format="A4")` | Invokes the constructor of the parent `FPDF` class to ensure full initialization. |
| **Method Overriding (`header`)** | `def header(self):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`self.set_font("helvetica", "B", 30)`<br>&nbsp;&nbsp;&nbsp;&nbsp;`self.cell(0, 10, "Title", align="C")` | Overrides `FPDF`'s built-in empty `header()` method to automatically print a header on every new page. |
---

## Making Your Own Modules and Packages
Create a **folder** for the **Package**: 
- `__init__.py`: An **empty file**, just helps Python realize this folder is a package including multiple modules.
- `module.py` files: about functionalities

**module.py**
```python
import package

def main():
    # Code to run only when executing this file directly

def my_function():
    # Reusable library function

if __name__ == "__main__":  # special variable __name__ is automatically set to be "__main__" when we run the python file from the command line to prevent the following `main()` function from executing if we `import` any function into another project. 
    main()
```

