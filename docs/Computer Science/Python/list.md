
[TOC]

# [Lists](https://docs.python.org/3/library/stdtypes.html#lists)


## Characteristics & Definition
Lists are a data type used to store a collection of items in a specific order.

| Feature | Description |
| :--- | :--- |
| **Sequence** |  **finite, ordered, mutable** sequence of elements   |
| **Mutable (changeable)** | We can **modify, add, or remove items** after creation  |
| **Element Types** | List can contain elements of same types and even **different types** (e.g., strings, integers, or even dictionaries, lists.) |
| **Creation Syntax** | enclosed by square brackets `[]` with elements separated by commas `list = [elem_1, elem_2, ..., elem_n]`. |
| **When to Use List** | - When we want to return multiple values, we can pack them into a list <br> - When the value should be able to be changed |

## Creation
| Operation | Syntax | Description | Complexity |
| :--- | :--- | :--- | :--- |
| **Create** a list with $n$ **same** objects | `list = [value] * n` | Creates a list of length `n`. This is fine for immutable objects (e.g. `int`, `str`). | $O(n)$  |
| **Create** a list with $n$ **distinct** mutable objects | `list = [[] for _ in range(n)]` | Use list comprehension for distinct sub-lists or other mutable objects. <br> `[[]] * n` would create the same sub-list referenced $n$ times. | $O(n)$ |

## Accessing & Modifying Elements
Python list uses **0-based indexing**, meaning the first item is at position 0.

| Action  | Detail | Syntax  | Complexity |
| :--- | :--- | :--- | :--- |
| **Access**  | Retrieve the value at the $i$-th position | `list[i]` | $O(1)$|
| **Reassign** | Change a value by accessing value via its position index and assigning a new value. |  `list[i] = new_value` | $O(1)$|
| **Check** if an item is **in** list| In the worst case: Python checks **each** element. For membership tests, consider using a set if we need repeated lookups.| `if item in lst:` | $O(n)$|


## General Operations (Polymorphic Tools)
These tools work on multiple data types, including **strings, lists, and more**.

| Tool | Purpose | Syntax | Parameters | Return Value | Notes | Complexity|
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`len()`** | Return the number of items/characters in an object. | `len(obj)` | An iterable (list, string, etc.) | `int` | Essential for dynamic loops like `range(len(list))`. |
| **`+` operator** | **Concatenate** two sequences of the same type. | `s1 + s2` | Two sequences (2 lists or 2 strings) | New sequence | Creates a **new** object; does not modify the originals in-place. | $O(len(a) + len(b))$|
| **`*` operator** | Repeat a sequence a specified number of times. | `s * n` | A sequence and an `int` | New sequence |  |





## [List build-in methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)


| Method | Purpose | Syntax | Parameters | Return Value | Complexity | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`.append()`** | Add **an item** to the **end** of the list. | `list.append(value)` | `value`: Any object | `None` | Amortized $O(1)$ | `lst = [1, 2, 3]` `lst.append([4, 5])` <br> output: [1, 2, 3, [4, 5]]|
| **`.extend()`** | **Unpack an iterable** and **adds all its items** to the **end** of list. | `list.extend(iterable)` | `iterable`: the iterable (e.g., list/tuple, string) | `None` | $O(k)$ where $k$ is length of the iterable | `l1 = [1, 2, 3]`<br>`l2 = [4, 5]`<br> `l1.extend(l2)`<br> output: [1, 2, 3, 4, 5] |
| **`.insert()`** | Insert an item at a **specific index**. | `list.insert(index, value)` | - `index`: Position where the element will be inserted. <br> - `value`: Item to be added to the list. | `None` | $O(n)$ | `a = [1, 2, 5]` <br> `a.insert(2, [3, 4])`<br> output: [1, 2, [3, 4], 5] |
| **`.remove()`** | Remove the **first occurrence** of a specific value. <br> It raises a ` ValueError`  if there is no such item. | `list.remove(value)` | `value`: Value to find | `None` | $O(n)$ | `lst = [5, 10, 5, 15, 5]`<br>`lst.remove(5)`<br> output: [10, 5, 15, 5] |
| **`.pop()`** | **Remove** the item at **given** **index** $i$(default is **last**) and **return** it. <br>  It raises an `IndexError` if the list is empty or the index is outside the list range.| `list.pop(index=-1)` | `index`: (Optional) Position of the element to remove. | The removed item | - $O(1)$ (at the end)<br>- $O(n)$ (random index) | `lst = ["red", "blue", "green", "yellow"]`<br>`val = lst.pop(1)`<br> output: ['red', 'green', 'yellow']|
| **`.clear()`** | **Remove all items** from the list. | `list.clear()` | None | `None` | $O(n)$ | `l.clear() # results in []` |
| **`.reverse()`** | Reverses the elements of the list **in-place**. | `list.reverse()` | None | `None` | $O(n)$ | `lst = [1, 2, 3, 4, 5]`<br>`lst.reverse()`<br> output[5, 4, 3, 2, 1]|
| [**`list.sort()`**](https://docs.python.org/3/library/stdtypes.html#list.sort) | Sort **list** **in-place**. **Only** defined for **lists**. Uses Timsort. s|`list.sort(key=None, reverse=False)` | - **key** (Optional): A **function or callable** taking one argument as **sorting criteria**. Note: just function name **without()**. **Default**: **lexicographical order** for nested lists (i.e., first sort by `x[0]`, if `x[0]` is the same, further sorts by `x[1]`). <br>  •  [*Multi-level of sorting*](https://docs.python.org/3/howto/sorting.html): <br>`from operator import itemgetter, attrgetter`<br>  `key = itemgetter(obj_idx_1, obj_idx_2)` or <br>  `key = attrgetter(obj_attr_1, obj_attr_2) ` <br>  •  [*use partial() to reduce arugments*](https://docs.python.org/3/library/functools.html#functools.partial):  <br> `from functools import partial`<br>  `key=partial(multi_argument_func)` <br> - **reverse** (Optional): : Boolean flag for order. **Default**: **ascending** (`False`); descending (`True`). | Return `None` (modifies list in place) | Time: $O(n \log n)$<br>Space: $O(n)$ |
| **`.count()`** | Return the number of times a value appears. | `list.count(x)` | `x`: Value | `int` | $O(n)$ | `num = l.count("Gryffindor")` |




