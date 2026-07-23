
# [Lists](https://docs.python.org/3/library/stdtypes.html#lists)


## Characteristics & Definition
Lists are a data type used to store a collection of items in a specific order.

| Feature | Description |
| :--- | :--- |
| **Sequence** |  **finite, ordered, mutable** sequence of elements   |
| **Mutable (changeable)** | We can modify, add, or remove items after creation  |
| **Element Types** | List can contain elements of same types and even **different types** (e.g., strings, integers, or even dictionaries, lists.) |
| **Creation Syntax** | enclosed by square brackets `[]` with elements separated by commas `list = [elem_1, elem_2, ..., elem_n]`. |
---

## Accessing & Modifying Elements
Python list uses **0-based indexing**, meaning the first item is at position 0.

| Action  | Detail | Syntax  |
| :--- | :--- | :--- |
| **Access**  | Retrieve the value at the $i$-th position | `list[i]` |
| **Reassign** | Change a value by accessing value via its position index and assigning a new value. |  `list[i] = new_value` | 
| **Join** | Perform a `+` operation to combine two lists into one. | `list1 + list2` | 
---


## General Operations (Polymorphic Tools)
These tools work on multiple data types, including **strings, lists, and more**.

| Tool | Purpose | Syntax | Parameters | Return Value | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`len()`** | Return the number of items/characters in an object. | `len(obj)` | An iterable (list, string, etc.) | `int` | Essential for dynamic loops like `range(len(list))`. |
| **`+` operator** | Concatenate two sequences of the same type. | `s1 + s2` | Two sequences (2 lists or 2 strings) | New sequence | Creates a **new** object; does not modify the originals in-place. |
| **`*` operator** | Repeat a sequence a specified number of times. | `s * n` | A sequence and an `int` | New sequence |  |
---


## List comprehension
a concise way to **create new lists from other lists**, optionally combine **map and filter operation** together.
```python
my_list = [transformer_expression for item in iterable if filter_condition]
```
* The `if` clause (optional) is for a filter operation.
* The `transformer_expression` is for mapping operation.

| When to use |	Code syntax |
| :--- | :--- |
| init 2D matrix (m rows and n columns) |	`[[default_value] * n for _ in range(m)`]
---


## [List build-in methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)


| Method | Purpose | Syntax | Parameters | Return Value | Complexity | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`.append()`** | Add **a single item** to the end of the list. | `list.append(x)` | `x`: Any object | `None` | $O(1)$ | `l.append("Harry")` |
| **`.extend()`** | **Unpack an iterable** and **adds its items to the end**. | `list.extend(iter)` | `iter`: Another list/tuple | `None` | $O(k)$ | `l.extend(["Ron", "Ginny"])` |
| **`.insert()`** | Insert an item at a **specific index**. | `list.insert(i, x)` | `i`: Index, `x`: Item | `None` | $O(n)$ | `l.insert(0, "Hermione")` |
| **`.remove()`** | Remove the **first occurrence** of a specific value. | `list.remove(x)` | `x`: Value to find | `None` | $O(n)$ | `l.remove("Draco")` |
| **`.pop()`** | **Remove and Return item at index** (default is **last**). | `list.pop([i])` | `i`: (Optional) Index | The removed item | $O(1)$ (end), $O(n)$ (index) | `last = l.pop()` |
| **`.clear()`** | **Remove all items** from the list. | `list.clear()` | None | `None` | $O(n)$ | `l.clear() # results in []` |
| **`.reverse()`** | Reverses the elements of the list **in-place**. | `list.reverse()` | None | `None` | $O(n)$ | `l.reverse()` |
| **`.count()`** | Return the number of times a value appears. | `list.count(x)` | `x`: Value | `int` | $O(n)$ | `num = l.count("Gryffindor")` |
---




