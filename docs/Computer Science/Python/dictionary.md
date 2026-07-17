# [Dictionary](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)

## Characteristics & Definition
data structure that allows us to store associated info - **associate keys with  values**.  


| Feature | Description |
| :--- | :--- |
| **Sequence** |  **unordered, mutable (changeable)** collection of **key-value pairs**   |
| **Mutable (changeable)** | We can modify, add, or remove items after creation  |
| **Key** is **unique**| cannot have two same keys |
| **Element Types** | keys and values can contain elements of same types and even **different types** (e.g., strings, integers) |
| **Creation Syntax** | enclosed by curly braces `{}` with key-value pairs `key: value` separated by commas `,`|
---

- If value == **`None`** : Indicates no data is assigned to that key. 
- Clean formatting:
Separate into multiple lines
```python
dict = {
    key_1: value_1, 
    key_2: value_2, 
    ... , 
    key_n : value_n
}
```

        

## Accessing & Modifying Elements
accessing **keys** (not via position index) 

| Action | Syntax / Example | Detail |
| :--- | :--- | :--- |
| **Access Value** | - `dict[key]` <br> - `dict.get(key, default_value)` | Retrieves the value for the key. <br> - `dict[key]` might get key error if key is not existing <br> - **`dict.get()`** (preferred) method **won't get key error**   |
| **Reassign** | `dict[key] = new_value` | changing values by accessing **keys** (not via position index) and resigning a new value |
| **adding new key and new value** |`dict[new_key] = new_value`  | resigning a value to a new key|
---

## Dictionary Comprehension 
(similar to List comprehension)
a concise way to **create a new dictionary from other lists**, optionally combine **map and filter operation** together.
```python
my_dict = [key_expression : value_expression for item in iterable if filter_condition]
```
* The `if` clause (optional) is for a filter operation.
* The `key_expression` and ` value_expressionis`  are for mapping operation.
* e.g., `
counts = {word : words.count(word) for word in words}
`



## [Dict build-in methods](https://docs.python.org/3/library/stdtypes.html#dict)

### Standard Dictionary (`dict`) Methods

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`get()`** | Retrieve value for the key safely - never raises `KeyError`. | `d.get(key, default = None)` | - `key` <br> - `default` (optional) | Return the value for key if key is in the dictionary, otherwise `default` if key is missing| $O(1)$ | `d.get("apple", 0)` |
| **`keys()`** | Return a new view of all keys in the dictionary. | `d.keys()` | None | Return a new view of the dictionary’s keys.  | $O(1)$ | `d.keys()` |
| **`values()`** | Return a view of all values in the dictionary.  <br><br> Note: An equality comparison between one dict.values() view and another will always return False. This also applies when comparing dict.values() to itself. | `d.values()` | None | Return a new view of the dictionary’s values.  | $O(1)$ | `d.values() == d.values()` -> False |
| **`items()`** | Return key-value pairs for iteration. | `d.items()` | None | Return a new view of the dictionary’s items, i.e., (key, value) pairs | $O(1)$ | `for k, v in d.items():` |
| **`pop()`** | Remove key and return its value. | `d.pop(key, default)` | `key`, `default` (optional) | Value or `default` | $O(1)$ | `d.pop("milk")` |
| **`popitem()`** | Remove/return last inserted key-value pair. | `d.popitem()` | None | `(key, value)` pair | $O(1)$ | `k, v = d.popitem()` |
| **`update()`** | Update dict with another dict or iterable. | `d.update(other)` | Another `dict`/iterable | `None` | $O(len(other))$ | `d.update({"bread": 1})` |
| **`setdefault()`** | Get value if key exists, else set/return default. | `d.setdefault(k, def)` | `key`, `default` | Value | $O(1)$ | `d.setdefault("eggs", 1)` |
| **`clear()`** | Remove all items from the dictionary. | `d.clear()` | None | `None` | $O(1)$ | `d.clear()` |
| **`copy()`** | Create a shallow copy of the dictionary. | `d.copy()` | None | New `dict` | $O(n)$ | `new_d = d.copy()` |

***

### Specialized Collections (`collections` module)
Requires: `from collections import defaultdict, Counter`

| Method | Purpose | Syntax | Parameters | Return Value | Complexities | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`defaultdict()`** | Create dict with default factory for missing keys. | `defaultdict(factory)` | `factory` (e.g., `int`) | `defaultdict` object | $O(1)$ | `d = defaultdict(int)` |
| **`Counter()`** | Count hashable elements in an iterable. | `Counter(iterable)` | `iterable` or `mapping` | `Counter` object | $O(n)$ | `c = Counter(list)` |
| **`most_common()`** | Return k most frequent elements. | `c.most_common(k)` | `k` (optional) | List of `(elem, count)` | $O(n \log k)$ | `c.most_common(1)` |

***






