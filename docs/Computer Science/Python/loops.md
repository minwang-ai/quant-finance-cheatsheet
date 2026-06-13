# CS50P Lecture 2: Loops

## Loop Fundamental Types
Loops allow you to execute a block of code **repeatedly**.

| Loop Type | Mechanism | Best Use Case | Syntax Note |
| :--- | :--- | :--- | :--- | 
| **`while`** | Repeats as long as the **while condition is `True`**. | When the **number of iterations** is  **unknown** | - Requires manual **counter updates** (e.g., `i += 1`) to avoid infinite loops. <br> - Best practice for counting: start with `0`, up to `n` (but not including n) |
| **`for`** | iterates over a iterable (**a predefined sequence**): steps through the items of lists, strings, tuples, the keys of dictionaries etc.  | When the **number of iterations** is  **known** or have a **set of items** to iterate through. | - When **loop over an iterable**, simply use: <br> `for element in sequence:`<br> e.g., `for student in students:` <br ><br>- for looping specific **`n` times**: use the `range(start, stop, step)` function as a sequence to generate a sequence of numbers from `0` up to (but not including) `n`:  <br> * `start` (optional): The starting value of the sequence. The default is 0. <br> * `stop` (**required**): The ending value of the sequence (exclusive). <br> * `step` (optional): The difference between each number in the sequence. The default is 1. <br><br> > If we also want the **position index** of  element: <br>  `for i in range(len(sequence)):` <br><br> > If a variable **won't be used later**, simply represent it as underscore `_`, e.g., <br> `for _ in range(3):` when we just need to repeat an action 3 times.   |
---

### Loop Control & Logic
Keywords that modify the behavior of a loop during execution.

| Keyword | Action | Program execution proceeds  | Practical Example |
| :--- | :--- | :--- |:--- |
| **`break`** | **Immediately exits** the loop **entirely**. | the first statement after the loop body. | Used in `while True:` loops to exit once valid input is received. |
| **`continue`** | **Skips** the rest of the **current iteration**, jump to the next iteration | jumps to the top of the loop: <br> continues to re-evaluate the condition to determine whether the loop will execute again or terminate. | Skipping specific "invalid" items in a list without stopping the whole loop. |
---

### Syntax Template 
#### while loop
```python
init_condition_variable()
while condition:
    update_condition_variable() 
    if condition:
        break/continue/return
```
#### for loop
```python
for value in sequence:
    Indented_statement
        if condition:
            break/continue/return
```


- If you also need the **index values** while iterating, use `enumerate()`
```python
for index, value in enumerate(sequence):
    Indented_statement
```

Note:
- for loop will only iterate through all the keys of dictionary,  use `dict[key]`  to find its value.
```python
for key in dict:
    Indented_statement
        if condition:
            break/continue/return
```








## Nested Data and Nested Iteration

### Lists with Complex Items
Each item/ sample could be the element of the list.
Nested lists (**A list of** list/ dictionary/ tuple/ function) can be make up of any data types but to make your debug process easier, make sure **only use one type of datatype**. 

Note: **Structuring Nested Data**
* **Do not mix types in nested data**, i.e., keep the structure consistent across each level. 
    * e.g., if you have a list of dictionaries, then each dictionary should have the **same structure**, meaning the same keys and the same type of value associated with a particular key in all the dictionaries.
* If other programmer use mix types, we can add additional if statement to deal with special cases.


### Nested Dictionaries
Storing multiple objects with multiple attributes.

| | Key | values|
| :--- | :--- | :--- |
| Meaning | Multiple features/attributes | the value of the features|
| Data types | The keys in dictionaries **must** be one of the **immutable** data types (numbers, strings, tuples), it cannot be mutable type e.g. list or dictionary, because each key map to its value via hash table| **Only** the values in dictionaries can be objects of **arbitrary type**.|
--- 





### Nested Iteration
Use **nested for loops** to **traverse nested data structures** (a list of lists/ dictionarie/ 2D array)

```python
# access a list of dictionaries
for element in list:
    print(element["key_1"], element["key_2"], element["key_3"], sep=", ") # Accessing values via keys during the loop


# Nested loop for a 2D grid
for row in range(rows):     
    for col in range(columns): 
        # access grid[row][col]
```
