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
