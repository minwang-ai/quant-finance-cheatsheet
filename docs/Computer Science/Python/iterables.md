# Iterables
Anything you can **loop over** with a for loop is an iterable.
- **ordered sequences (string, list, tuple)**: support indexing and slicing. 
- **unordered collections (dictionary, set)**: support indexing but not slicing. 

## Slicing for Ordered Sequences
a universal technique in Python used to extract parts of **ordered sequences (string, list, tuple)**. 
| Syntax | Meaning | Note | 
| :--- | :--- | :--- |
| `data[start: stop: step]` | - `:` separate start, stop, and step <br> - Inclusive Start, Exclusive Stop, i.e., [start, stop) |  - optional: Omitting start means "from beginning" <br> - optional: Omitting stop means "to end" |
| **Negative indices** means **count from the end** |  **-1** means the **last** element <br>  -2 means the last 2nd element |
| `step` | determine selection intervals | **Negative step reverses order** |
---

### Slicing cheat sheet

| Operation | Syntax | Meaning | Example (`"Python"`) | Output | Complexities |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Basic Slicing** | `data[start:stop]` | Extract elements from `start` to `stop-1`. | `"Python"[1:4]` | `"yth"` | $O(k)$ |
| **Omitting start** | `data[:stop]` | start from the beginning up to `stop-1`. | `"Python"[:4]` | `"Pyth"` | $O(k)$ |
| **Omitting stop** | `data[start:]` | From `start` to the end. | `"Python"[2:]` | `"thon"` | $O(k)$ |
| **Using step** | `data[start:stop:step]` | Extract with step intervals. | `Python"[::2]` | `"Pto"` | $O(k)$ |
| **Full Slice** | `data[:]` | Return the entire sequence. | `"Python"[:]` | `"Python"` | $O(n)$ |
| **Negative Indexing** | `data[-start:-stop]` | Count from the end (-1 is the last element). | `"Python"[-5:-2]` | `"yth"` | $O(k)$ |
| **Reverse a Sequence** | `data[::-1]` | Reverse the sequence. | `Python"[::-1]` | `"nohtyP"` | $O(n)$ |
| **Skipping Elements** | `data[::k]` | Select every k-th element. | `"Python"[::3]` | `"Ph"` | $O(n/k)$ |
| **Negative Step** | `data[start:stop: -step]` | Pick elements in reverse order. | `"Python"[4:1:-1]` | **`"oht"`** | $O(k)$ |
---
**Note**: 
slicing **create new lists** -> space O(n)

## Build-in Methods for Iterables

| Method | Purpose | Scope | Syntax | Parameters | Return Value | Complexities |
| :--- | :--- | :--- | :--- | :--- | :--- |:--- |
| [**`list.sort()`**](https://docs.python.org/3/library/stdtypes.html#list.sort) | Sort **list** **in-place**. **Only** defined for **lists**. Uses Timsort. | only **list** |`list.sort(key=None, reverse=False)` | - **key** (Optional): A **function or callable** taking one argument for **sorting criteria**. **Default**: **lexicographical order** for nested lists (i.e., first sort by `x[0]`, if `x[0]` is the same, further sorts by `x[1]`). <br>  •  [*Multi-level of sorting*](https://docs.python.org/3/howto/sorting.html): <br>`from operator import itemgetter, attrgetter`<br>  `key = itemgetter(obj_idx_1, obj_idx_2)` or <br>  `key = attrgetter (obj_attr_1, obj_attr_2) ` <br>  •  [*use partial() to reduce arugments*](https://docs.python.org/3/library/functools.html#functools.partial):  <br> `from functools import partial`<br>  `key=partial(multi_argument_func)` <br> - **reverse** (Optional): : Boolean flag for order. **Default**: **ascending** (`False`); descending (`True`). | Return `None` (modifies list in place) | Time: $O(n \log n)$<br>Space: $O(n)$ |
| [**`sorted()`**](https://docs.python.org/3/library/functions.html#sorted) | Build a **new sorted list** from **any iterable**. Uses Timsort. | any **iterable** | `sorted(iterable, key=None, reverse=False)` | - **iterable**: **Any** iterable object.<br> - **key / reverse**: Same as `list.sort()`. | **New** sorted list | Time: $O(n \log n)$<br>Space: $O(n)$ |
| [**`zip()`**](https://docs.python.org/3/library/functions.html#zip) | **Combine multiple iterables** element-wise into **tuples**.<br><br>**Additional Tricks:**<br>• *Unzip*: <br> `var1, var2 = zip(*var)`<br>• *Chunking a list into equal size n*: <br> `zip(*[iter(s)] * n, strict=True)`| any **iterable** | `zip(*iterables, strict=False)` | - ***iterables**: Two or more **any iterable** inputs.<br> - **strict** (Optional): Boolean flag for equal length. <br> If `True`, forces equal length check. **Default** `False` (stops when the shortest iterable is exhausted, ignore the remaining items in the longer iterables). If iterables must to be of equal length, set strict=True | A iterator of tuples, one tuple per index position (a lazy iterator, so no actual tuples are created until you iterate or convert it using `list()`, `set()`, etc.) | Time: $O(n)$<br>Space: $O(1)$ (lazy, unless cast) |
|[**`.index()`**](https://docs.python.org/3/library/stdtypes.html#sequence.index) | Return the **index** of the **first occurrence** of value in sequence. | any **sequence** (list, string, tuple)| `sequence.index(value[, start[, stop]])` | - `value`: value to find <br> -`start`/`end`: (optional) search range  (efficient searching of subsections **without copying any data**.)<br> Caution: **Not all** sequence types support passing the `start` and `stop` arguments. | `int` (index of match); raises **`ValueError`** if not found | $O(n)$ |
---