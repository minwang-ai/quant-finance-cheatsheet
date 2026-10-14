[TOC]

# CS50P Lecture 6: File I/O 

File I/O (Input/Output) allows programs to **read from and write to files**, enabling **persistent storage** so that data is not lost and can be **used later** when the program ends. 


## Opening a File
Best practice: using **`with`** keyword to open a file-like object at the `filepath`, write some content and **automatically safely closes** after exit this code block even if exceptions occur inside the block.

```python 
with open(filepath, mode) as file:
    # Use the file-like object file 
```
  
* `filepath`: "/path/file_name.file_extension" 
    (or simplely "file_name.file_extension" if it is in the current path)
* `mode` (optional)
* as `file`: the name of the variable that should be assigned the return value of `open`
* we can actually **open multiple files at once** (use case: read one file and write another at the same time)
    ```python 
    with open(filepath, mode) as file_1, open(filepath, mode) as file_2:
        # Use the file-like object file 
    ```

### File Modes

| Mode | Syntax | Purpose | If the File Exist or Not| 
| :--- | :--- | :--- | :--- |
| **Write** | `"w"` | Write fresh content or **overwrite an existing file**. | **create** the file if missing. <br> However, if the file does exist, it will **clear any existing content** before writing new data. |
| **Safe Create** | `"x"` | create a new file **only if it does not exist** | Raise FileExistsError if the file already exists to **prevent accidental overwrites**. (handle it via try-except block)|
| **Append** | `"a"` | Append data to the **end** of the file **without deleting existing content**. | **create** the file if missing |
| **Read** | `"r"` | Read (**default** mode). | Raise an **error** `FileNotFoundError` |
| **Both read and write** |`"+"`| combine with other modes (e.g., "r+", "w+") for both reading and writing|

#### Write Mode
```python 
var = input("prompt string") 
with open(filepath, mode) as file:
    # Use the file-like object file 
    file.write(f"{var}\n")  # Writes a raw string to an opened file. It does not automatically add newlines so we must append `\n` manually.
```

#### Read Mode
```python 
with open(filepath, "r") as file:  
    for line in file:   # Iterates through line-by-line. If we want the lines to be sorted, we can use sorted(file)
        print(line.rstrip())  # Removes extra trailing line break to prevent double new line issues caused by the file's `\n` and `print()`'s default newline. 
```
If we want to further change the data, e.g., sorting, we can create a variable at the top, append info to collect it in one place.
Example:
```python 
names = []  
with open(filepath) as file:   
    for line in file:   
        names.append(line.rstrip())  
for name in sorted(names):   
    print(f"hello, {name}")  
```

##  Reading & Writing Text Files
`file` must refer to a file that has been opened via `with open(filepath, mode) as file: `  

### Writing Text Files
| Method | Purpose | Syntax | Parameters | Return Value | Pros &Cons|When to Use |
| :--- | :--- | :--- | :--- | :--- |:--- |:--- |
| **`write()`** | Writes **a string** to the end of the file. | `file.write(string)` | **`string`**: The text string to write. <br> It does not automatically add newlines so we must append `\n` manually. Building a single string and calling `write()` once, i.e., `text = "\n".join(lines) + "\n"` can be more efficient and less error-prone compared to `writelines()`. | None | + Safe and predictable.  <br><br> - Cannot write lists/iterables natively without manual conversion. | Best for writing **individual strings or custom-formatted blocks**. |
| **`writelines()`** | Writes each line as an item in **a list (or any iterable sequence) of strings** to the end of the file.  | `file.writelines(list)` | **`list`**: A list or iterable of strings. <br><br> It does not add newlines automatically we must **include `\n`** in each string in the list. | None |   + Dumps an entire sequence of lines in a single call.<br><br>- **Highly error-prone.** Beginners often forget that it doesn't auto-add newlines, resulting in all list items squished onto a single line. | Use when you already **have a pre-formatted list of strings that already contain newline characters** at the end. |

### Reading Text Files
| Method | Purpose | Syntax | Parameters | Return Value | Pros &Cons|When to Use |
| :--- | :--- | :--- | :--- | :--- |:--- |:--- |
| **Direct Iteration** | Iterate line-by-line |`for line in file:` | None | Yields a **string** representing one line at a time. |+ **Extremely memory-efficient.** Only keeps one line in RAM at a time (perfect for massive files).<br><br>- Cannot access lines out of order (**no indexing or slicing**). | **Default best practice** for standard line-by-line file processing.|
| **`read()`** | Reads `n` characters, or the entire file as a single string if `n` is omitted. | `file.read(n=-1)` | - **`n`** *(Optional)*: The number of characters to read. **Defaults** to `-1` (reads the **entire file**). | A **string** containing all the read characters. | + Gives you the entire file as one **easily searchable string**.<br><br>- **Poor memory efficiency** for large files; loads the entire file into RAM at once. |When we need to process **small files as a single block** (e.g., parsing JSON/XML) or **searching for substrings** across line boundaries.|
| **`readline()`** | Reads the next line of the file with all text up to and **including the newline character**. | `file.readline(n=-1)` | **`n`** *(Optional)*: **Maximum characters** to read from the line. If n is provided as a parameter, then only n characters will be returned if the line is longer than n. (Note: Parameter `n` is ignored in the browser version of Python and is rarely used). | A **string** containing the next line of tex  (includes `\n`). Returns an empty string `""` when the end of the file is reached. | + Great for grabbing a **specific single line** (e.g., reading a **header** line before starting a loop to process data).<br><br> - Clunky if you just want to loop through the whole file.|When you need precise, **manual control** over step-by-step reading. |
| **`readlines()`** | Read **all the lines** of the file | `lines = file.readlines()` | **`n`** *(Optional)*: If `n` is not provided then all lines of the file are returned. If `n` provided, characters are read up to `n` but rounded up so that an entire line is returned. (Note: Ignored in the browser version). | A **list of strings**, where each item represents **a single line of the file**. | + Gives you a standard list you can **manipulate** with list operations immediately.<br><br>- **Unsafe for large files** as it loads all lines into RAM simultaneously. |When you specifically need the lines stored in a list structure for sorting, reversing, indexing, or checking the list length. |

Note:
- **Adjust index** for slicing because txt file lines are **1-indexed** (conventionally), while Python lists/sequences are **0-indexed**.
- Use **`line.strip()`** on strings when reading from a file to **remove any leading or trailing whitespace, including newline character `\n`** before processing or printing(because print will automatically add a newline character `\n`).






## Structured Data: module [`csv`](https://docs.python.org/3/library/csv.html) for comma separated values 
**automatically** parse and deal with **corner cases** (such as handling extra commas embedded inside quoted strings)

`import csv`
### Reading CSV Files
within `with open("file_name.csv") as file:`
| Method | Syntax  | Purpose | Return Value |
| :--- | :--- | :--- | :--- |
| **`csv.reader()`** |  `reader = csv.reader(file)` | Reads a CSV file. | Returns a reader object that yields **each row as a list of strings** accessed by index where each value in the list corresponds to an element in that row, e.g., `row[0]` is the first element of the given row, `row[1]` is the second element. |
| **[`csv.DictReader()`](https://docs.python.org/3/library/csv.html#csv.DictReader)** | `reader = csv.DictReader(file)` | Reads a CSV file with **header rows** dynamically, making your program much more **flexible and robust if columns are added or reordered**. | Returns a reader object that yields **each row as a dictionary**, mapping header titles to row values (e.g., `row["header_1"]`. |

### Writing CSV Files
within `with open("file_name.csv", mode) as file:`
| Method  | Syntax | Purpose | Parameters | Return Value |
| :--- | :--- | :--- | :--- |:--- |
| **`csv.writer()`** | `writer = csv.writer(file)`  | Creates a writer object to write data to a CSV file.| **`file`**: An opened file object (typically in `"w"` or `"a"` mode). | Returns a standard writer object. |
| **[`csv.DictWriter()`](https://docs.python.org/3/library/csv.html#csv.DictWriter)** | `writer = csv.DictWriter(file, fieldnames=["header_1", "header_2"])` | Prepares a CSV file for structured writing mapped to specific keys.|- **`file`**: An opened file object.<br>- **`fieldnames`**: A list of strings representing **column headers**. <br><br>*Note: To add a column dynamically, we can use **list concatenation `+`*** | Prepares a CSV file for structured writing mapped to specific dictionary keys. | Returns a dictionary-based writer object. |
| **[`writeheader()`](https://docs.python.org/3/library/csv.html#csv.DictWriter.writeheader)** | `writer.writeheader()` <br><br> ***Only** used with `DictWriter`.* | Writes a row with the column names specified in the `fieldnames` list to the file as the **header** row of the CSV.|None | returns `None` |
| **`writerow()`** | `writer.writerow(data)` <br><br> data: Takes a **list** `[var1, var2]`(for standard writer) or a **dictionary** (for DictWriter). I| Writes a single structured line of data into the CSV file.|**`data`**: Takes a **list** `[var1, var2]` (for standard writer) or a **dictionary** mapping fieldnames to values (for `DictWriter`). <br><br>*Note: If we just want to **add a new column**, simply append the value to the list/dict `row` then pass it to `writer.writerow(row)`.*  | Writes the fields to the corresponding columns and returns `None`. |

### Comparison: Standard vs. Dictionary CSV Methods

Best practice: **dictionary-based** methods for writing defensive Python code.

| Feature | Standard Version (`csv.reader` / `writer`) | Dictionary Version (`csv.DictReader` / `DictWriter`) |
| :--- | :--- | :--- |
| **Data Representation** | Handles rows as **lists** of strings. | Handles rows as **dictionaries**. |
| **Access Method** | Numerical indices: `row[0]`, `row[1]`. | Header-name keys: `row["header_1"]`, `row["header_2"]`. |
| **Robustness to Changes** | **Fragile.** If someone adds, swaps, or deletes columns, your index references will point to the wrong data and break your code. | **Highly Robust (Defensive).** As long as the header names in the CSV remain consistent, the code will not break even if columns are added or swapped. |
| **CSV Headers** | Does not require or assume a header row. | Requires a header row on the first line (or explicit `fieldnames` parameters when writing). |

#### Example code: csv File without Header
**reader**
```python 
import csv

items = []

with open("file_name.csv"), "r" as file:
    reader = csv.reader(file)
    for attr_1, attr_2 in reader:   # A reader works in a for loop, where each iteration the reader gives us another row from our CSV file. We can unpack attributes directly
        items.append({"attr_1": attr_1, attr_2: attr_2})

for item in sorted(items, key=lambda item: item["attr_1"]):
    # ...
```
**writer** 
```python 
import csv

attr_1 = input("string_prompt ")
attr_2 = input("string_prompt ")

with open("file_name.csv", "a") as file:
    writer = csv.DictWriter(file)  
    writer.writerow([attr_1, attr_2])
```

#### Example code: csv File with Header
```csv
header_1, header_2
header_1_value, header_2_value
```
**DictReader**
```python 
import csv

items = []

with open("file_name.csv") as file:
    reader = csv.DictReader(file)
    for row in reader:
        list.append(row)

for item in sorted(items, key=lambda item: items["attr_1"]):
    # ...
```

**DictWriter** 
```python 
import csv

header_1 = input("string_prompt")
header_2 = input("string_prompt")

with open("file_name.csv", "a") as file:
    writer = csv.DictWriter(file, fieldnames=["header_1", "header_2"])  
    writer.writeheader()

    writer.writerow({"header_1": header_1, "header_2": header_2})   # Write each row. Since it is a dictionary, the order does not matter
```
### Pretty-print tabular data: `tabulate` Package
`pip install tabulate` 

| Function | Purpose | Syntax | Parameters | Return Value | 
| :--- | :--- | :--- | :--- | :--- | 
| **`tabulate()`**  | Formats tabular data (like lists of lists or lists of dictionaries) into a beautiful, human-readable ASCII art table. | `from tabulate import tabulate`<br><br>`print(tabulate(data, headers=(), tablefmt="simple"))` | - **`tabular_data`**: The table content (e.g., a list of lists or a list of dictionaries).<br>- **`headers`**: Specifies what to use as column headers (e.g., `"firstrow"` if using a list of **lists**, or `"keys"` if using a list of **dictionaries**).<br>- **`tablefmt`**: A string representing the table design style (e.g., `"grid"`). | A formatted **string** containing the ASCII table layout. |

## Binary Files

A binary file is a collection of **ones and zeros** representing **compiled data (like images or music or video)** rather than text characters.

###  Image Handling ([`PIL`](https://pillow.readthedocs.io/))
A popular third-party library used for reading, writing, and manipulating image files.
`from PIL import Image, ImageOps`
#### Open and Save
| Method | Purpose | Syntax | Parameters | Return Value |
| :--- | :--- | :--- | :--- | :--- |
| **`Image.open()`**  | Opens an image file for processing. | `with Image.open("file_path") as image:` | **`file_path`**: A string representing the filename or path to the input image file. Supports formats like`.gif`, `.jpeg`, and `.png`| An `Image` object |
| **`image.save()`**  | Saves the image to a specified **output** file path. Can also compile multiple frames into animated **GIFs**. | `images.save(file_path, format=None, **params)` <br><br>*For animated GIFs:*<br>`image.save(file_path, save_all=True, append_images=[...], duration=200, loop=0)` | - **`file_path`**: String representing the output file path. <br> **params**: <br>- **`save_all`** *(Optional)*: Set to `True` to save all frames of a GIF.<br>- **`append_images`** *(Optional)*: List of subsequent Image frames to append.<br>- **`duration`** *(Optional)*: Frame display duration in milliseconds.<br>- **`loop`** *(Optional)*: Loop count (0 for infinite). | Returns `None`. |

#### Image Processing
| Method | Purpose | Syntax | Parameters | Return Value |
| :--- | :--- | :--- | :--- | :--- |
| **`image.rotate()`** | Rotates the image counter-clockwise by the specified angle. | `rotated_image = image.rotate(degrees)` | **`degrees`**: An integer representing the counter-clockwise rotation angle (e.g., `90`, `180`, `270`). | A new, rotated **`Image` object**. |
| **`image.filter()`** | Applies a specified visual effect or processing filter to the image. | `from PIL import ImageFilter`<br>`filtered_image = image.filter(ImageFilter.filter_name)` | **`filter_name`**: An ImageFilter, e.g., `BLUR`, `FIND_EDGES`, `CONTOUR`, or `SHARPEN`. | A new, filtered **`Image` object**. |
| **`image.size`**  *(Attribute)* | Retrieves the horizontal and vertical dimensions of the image. | `width, height = image.size` | None. | A **tuple of integers** `(width, height)` representing the size. |
| **`ImageOps.fit()`**  | **Crops and resizes** an image to match a target size and aspect ratio using a default center-cropping method. | `cropped_image = ImageOps.fit(image, size)` | - **`image`**: The source Image object.<br>- **`size`**: A tuple of integers representing the target size `(width, height)`. | A new, resized and cropped **`Image` object**. |
| **`image.paste()`** | **Overlays** another image on top of the current image, using an optional transparency mask. | `background.paste(foreground, box=None, mask=None)` | - **`foreground`**: The Image object to overlay.<br>- **`box`** *(Optional)*: A tuple `(x, y)` indicating top-left placement.<br>- **`mask`** *(Optional)*: An Image object used as a mask to determine which pixels in the background to update (We can pass the foreground image itself preserves its transparency). | Returns `None` (modifies the original image **in-place**). |

Example: create gif memes / animations
```python
import sys
from PIL import Image

images = [] # accumulate all the images
for arg in sys.argv[1:]:    # the images paths are provided as command-line arguments
    with Image.open(arg) as image:
    images.append(image)

images[0].save(
    "output.gif", save_all = True, append_images = [images[1], duration = 200, loop = 0]
)   # save the first image while append the other images, to compile a list of individual images into an animated, looping GIF.
```

Example: Overlay a foreground picture on top of the background
```python
def overlay():
    with Image.open(background_filepath) as background, Image.open(foreground_filepath) as foreground:
        # 1. Resize and crop the background to match the shirt's size (no copy needed)
        background_cropped = ImageOps.fit(background,foreground.size)

        # 2. Paste the shirt on top using the shirt itself as a transparency mask
        background_cropped.paste(foreground, foreground)

        # 3. Save the finished image
        background_cropped.save(output_file)
```