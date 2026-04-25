# I/O


## build in methods
| Method | Purpose | Syntax | Parameters | Return Value | Complexities |
|---|---|---|---|---|---|
| [`print()`](https://docs.python.org/3/library/functions.html#print) | Outputs one or more objects to the console or another text stream. Useful for displaying values, debugging, and writing formatted text. | `print(*objects, sep=' ', end='\n', file=None, flush=False)` | -`*objects`: `*` means arbitrary number of objects (values) to print.  <br> <br>  - `sep` (optional): Seperator inserted between objects. Default: space `' '`.  <br><br> - `end` (optional): String appended after the last character. Default: new line `'\n'`. <br><br>`file` (optional): A file-like object with a `write()` method. Default: standard output.<br>`flush` (optional): If `True`, forcibly flushes the stream. Default: `False`. | Returns `None`. | Time: `O(n)`, Space: `O(1)` |