
# Lists


## Characteristics & Definition
Lists are a data type used to store a collection of items in a specific order.

| Feature | Description |
| :--- | :--- |
| **Sequence** |  **finite, ordered, mutable** sequence of elements   |
| **Mutable (changeable)** | We can modify, add, or remove items after creation  |
| **Element Types** | List can contain elements of same types and even **different types** (e.g., strings, integers, or even dictionaries) |
| **Creation Syntax** | enclosed by square brackets `[]` with elements separated by commas `list = [elem_1, elem_2, ..., elem_n]`. |
---

## Accessing & Modifying Elements
Python uses **0-based indexing**, meaning the first item is at position 0.

| Action | Syntax / Example | Detail |
| :--- | :--- | :--- |
| **Access** | `list[i]` | Retrieves the value at the $i$-th position |
| **Reassign** | `list[i] = new_value` | Changes a value by accessing value via its position index and assigning a new value. |
| **Join** | `list1 + list2` | Performs a `+` operation to combine two lists into one. |
---


## General Operations (Polymorphic Tools)
These tools work on multiple data types, including strings, lists, and more.

| Tool | Purpose | Syntax | Parameters | Return Value | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`len()`** | Returns the number of items/characters in an object. | `len(obj)` | An iterable (list, string, etc.) | `int` | Essential for dynamic loops like `range(len(list))`. |
| **`+` operator** | Concatenates two sequences of the same type. | `s1 + s2` | Two sequences (2 lists or 2 strings) | New sequence | Creates a **new** object; does not modify the originals in-place. |
| **`*` operator** | Repeats a sequence a specified number of times. | `s * n` | A sequence and an `int` | New sequence | Used in the "Mario" examples to print multiple bricks: ` "#" * 3`. |



## [List build-in methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)


| Method | Purpose | Syntax | Parameters | Return Value | Complexity | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`.append()`** | Adds a single item to the end of the list. | `list.append(x)` | `x`: Any object | `None` | $O(1)$ | `l.append("Harry")` |
| **`.extend()`** | Unpacks an iterable and adds its items to the end. | `list.extend(iter)` | `iter`: Another list/tuple | `None` | $O(k)$ | `l.extend(["Ron", "Ginny"])` |
| **`.insert()`** | Inserts an item at a specific index. | `list.insert(i, x)` | `i`: Index, `x`: Item | `None` | $O(n)$ | `l.insert(0, "Hermione")` |
| **`.remove()`** | Removes the first occurrence of a specific value. | `list.remove(x)` | `x`: Value to find | `None` | $O(n)$ | `l.remove("Draco")` |
| **`.pop()`** | Removes and returns item at index (default is last). | `list.pop([i])` | `i`: (Optional) Index | The removed item | $O(1)$ (end), $O(n)$ (index) | `last = l.pop()` |
| **`.clear()`** | Removes all items from the list. | `list.clear()` | None | `None` | $O(n)$ | `l.clear() # results in []` |
| **`.sort()`** | Sorts the list in-place (ascending by default). | `list.sort()` | `key`, `reverse` (optional) | `None` | $O(n \log n)$ | `l.sort(reverse=True)` |
| **`.reverse()`** | Reverses the elements of the list in-place. | `list.reverse()` | None | `None` | $O(n)$ | `l.reverse()` |
| **`.index()`** | Returns index of the first item matching the value. | `list.index(x)` | `x`: Value | `int` | $O(n)$ | `pos = l.index("Harry")` |
| **`.count()`** | Returns the number of times a value appears. | `list.count(x)` | `x`: Value | `int` | $O(n)$ | `num = l.count("Gryffindor")` |
---




## List-Related Global Functions
| Function | Purpose | Syntax | Return Value | Difference from Methods |
| :--- | :--- | :--- | :--- | :--- |
| **`sorted()`** | Returns a new sorted list from any iterable. | `sorted(list)` | New `list` | Unlike `.sort()`, it does **not** modify the original list. |
