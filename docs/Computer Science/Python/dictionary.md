# [Dictionary](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)

## Characteristics & Definition
data structure that allows us to **associate keys with  values**.  


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
| **Access** | `dict[key]` | Retrieves the value for the key |
| **Reassign** | `dict[key] = new_value` | changing values by accessing **keys** (not via position index) and resigning a new value |
| adding new value |`dict[new_key] = new_value`  | resigning a value to a new key|
---

