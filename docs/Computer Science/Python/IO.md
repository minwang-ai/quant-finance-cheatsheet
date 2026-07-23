# Input / Output (I/O)


## build in methods
| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Examples |
|---|---|---|---|---|---| --- |
| [`print()`](https://docs.python.org/3/library/functions.html#print) | Outputs one or more objects to the console or another text stream. Useful for displaying values, debugging, and writing formatted text. | `print(*objects, sep=' ', end='\n', file=None, flush=False)` | -`*objects`: `*` means the method can take multiple arguments, i.e., arbitrary number of objects to print. Here we can also take a big argument using + to concatenate strings. <br> <br>  - `sep` (optional): Seperator inserted between objects automatically. Default: blank space `' '`.  <br><br> - `end` (optional): String appended for line ending. Default: new line `'\n'`. <br><br> - `file` (optional): A file-like object with a `write()` method. Default: standard output.<br><br> - `flush` (optional): If `True`, forcibly flushes the stream. Default: `False`. | Return `None`. | Time: `O(n)`, Space: `O(1)` |
| [`input()` ](https://docs.python.org/3/library/functions.html#input)| Reads a line of text from standard input, usually entered by the user, and optionally displays a prompt before reading. | `input([prompt])` | `prompt` (optional): A string displayed to the user before input is read. Default: no prompt. | Return the user input as a **string**, excluding the trailing newline.<br><br> Note: Use `int()` or `float()` to **convert data type** if the input is a number and will be used in calculation. | Time: `O(n)`, Space: `O(n)` | `input_variable_name = input("text prompt")`|
----
