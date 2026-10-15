
# Tuples

## Characteristics & Definition
| Feature | Description |
| :--- | :--- |
| **Ordered and <br> Immutable** (unchangeable) | the **values cannot be changed** by accessing it via the position index and resigning new value |
| **Memory Effient** | tuple takes less memory compared to list |
| **Creation Syntax** | enclosed by parentheses `()`  with elements separated by commas <br> `my_tuple = (element_1, element_2, ...,  element_n)` |
| **When to Use Tuple** | - When we want to return multiple values, we can pack them into a tuple <br> - When the value should not be changed |



## Accessing 
Python tuple uses **0-based indexing**, meaning the first item is at position 0.

| Action | Purpose | Syntax|
| :--- | :--- | :--- |
| **index** | Retrieves the value at the  $i$-th position | `tuple[i]`|
| **unpack** (preferred) | unpack the tuple into n distinct variables| `element_1, ... , element_n = tuple`  | 
| **adding new value** by | perform `+` operation |
