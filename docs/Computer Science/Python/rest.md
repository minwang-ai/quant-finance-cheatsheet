
# CS50P Lecture 9: Et Cetera

## Functional Programming
**Functions** themselves can be **passed** around as arguments/values.


taken a list and produced another list from it that contains either a subset of the items or a transformed version of each item. 

* When each item is **transformed**, we say that the operation is a mapping, or just a map of the original list. 
* When some items are **omitted**, we call it a **filter**.


| Method | Purpose | Syntax | Parameters | Return Value | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **[`map()`](https://docs.python.org/3/library/functions.html#map)** (**not preferred**) | Applies a specified **function** to **every element** across a sequence. | `map(transform_function, iterable)` | - **`transform_function`**: The function to apply to each element to transform each element to a new element.<br> - **`iterable`**: One or more iterable objects (list, tuple, etc.) whose elements will be processed. | A **`map` iterator** containing the transformed items. | `words = ["this", "is", "cs50"]`<br>`uppercased = map(str.upper, words)` |
| **[`filter()`](https://docs.python.org/3/library/functions.html#filter)**(**not preferred**)  | Extracts a **subset** of a sequence for which a conditional function returns `True`. | `filter(filter_function, iterable)` | - **`filter_function`**: A function or `lambda` expression returning **boolean `True`/`False`** for each item.<br> - **`iterable`**: The target sequence to filter. | A **`filter` iterator** containing only the matching items. | `students = [{"name": "Harry", "house": "Gryffindor"}, ...]`<br>`gryffindors = filter(lambda s: s["house"] == "Gryffindor", students)`  |

Note that:

- Only **pass the function name without ()**, because we do not call the functions there; the functions will be called for each items later.
- Return a **iterator** -> we need to **cast** it to **list** , e.g., `list(map())` or `list(filter())`

## Comprehension
### List Comprehension
a concise way to **create new lists from other lists** in one elegant one-liner, optionally combine **map and filter operation** together.
```python
my_list = [transform_expression for item in iterable if filter_condition]
```

* The `if` clause (optional) is for a **filter** operation.
* The `transformer_expression` is for **mapping** operation.

| When to use |	Code syntax |
| :--- | :--- |
| init 2D matrix (m rows and n columns) |	`[[default_value] * n for _ in range(m)`]

### Dictionary Comprehension 
(similar to List comprehension)
a concise way to **create a new dictionary from other lists**, optionally combine **map and filter operation** together.
```python
my_dict = {key_expression : value_expression for item in iterable if filter_condition}
```

* The `if` clause (optional) is for a **filter** operation.
* The `key_expression` and ` value_expressionis`  are for **mapping** operation.
* e.g., `
counts = {word : words.count(word) for word in words}
`

## Generators 
We can **define a function as generators** whereby it can still generate a massive amount of data by **returning one item at a time** instead of storing everything in memory, preventing **memory exhaustion** or crashing.


### Syntax
```python
def generator_name():
    for i in range(n):
        yield object

my_generator = generator_name()
next(my_generator)
# do something else
next(my_generator)
```
Details:  
To create the next successive, we can simply call `next()` on the generator object, and it will yield the next iteration. After yield is called, everything in the state of the generator function freezes, and the value is returned. When the generator is called again with `next()`, it picks back up right where it stopped at yield from before.

### Python [Generators](https://docs.python.org/3/howto/functional.html#generators) vs. Functions
| Feature | Function | Generator |
| :--- | :--- | :--- |
| **When to use** | Standard tasks where the data fits in memory and can be computed and returned all at once. | Dealing with very large collections of data that we cannot store in memory all at once (which leads to program hanging or crush). |
| **Functionalities** | Return a value and exiting the this function. | Pause the process, save its state for next time, [optionally do other things] and continue|
| **Biggest difference** | `return` keyword: return **all at once**| `yield` keyword: <br> return **one item  at a time** while the  `for ` loop keeps working. <br> (return an [**iterator**](https://docs.python.org/3/howto/functional.html#iterators) so we can use for loop to **iterate over** the generated value one at a time) |


### Flattened Generator Expression 

| Feature | Description |
| :--- | :--- |
| **What It Is** | A generator expression that **iterates through nested 2D structures** (e.g., **list of lists** for grid, matrix, game board) and yields items as a **single 1D stream**. |
| **Why Use It** | Processes elements lazily (one by one) to save memory instead of building a full intermediate list in RAM. |
| **Common Use Case** | Feeding flattened elements directly into aggregator functions (e.g., `Counter()`, `sum()`, `set()`, `"".join()`). |
```python
from collections import Counter 
# 2D Grid / Board 
board = [
    ["🍪", "🍪", "🐍"], ["🐍", "🍪", "🍪"],
]   

# using a Flattened Generator Expression (Memory Efficient): 
counts = Counter(char for row in board for char in row) 

print(counts) # Output: Counter({'🍪': 4, '🐍': 2}) 


# The exact same behavior written with a explicit generator function: 
def stream_board(grid): 
    for row in grid: 
        for char in row: 
            yield char 

counts = Counter(stream_board(board))  
```

### Generator Expression vs. List Comprehension for Flattening
| Approach | Syntax Example | Memory Overhead | Execution Behavior |
| :--- | :--- | :--- | :--- |
| **Generator Expression** | `(char for row in board for char in row)` | **Low** <br> **$O(1)$** RAM | Generates and yields items lazily one at a time on demand. |
| **Nested `yield` Loop** | `for row in board:`<br />    `for char in row:`<br />        `yield char` |  **Low** <br> **$O(1)$** RAM | Standard multi-line function logic equivalent to the generator expression. |
| **List Comprehension** | `[char for row in board for char in row]` |  **High** <br> **$O(N)$** RAM | Allocates and constructs the full flattened list in memory immediatelys. |
