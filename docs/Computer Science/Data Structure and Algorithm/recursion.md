# Recursion

## Iterative vs Recursion
| Aspects |  Iterative | Recursion |
|:--:|:--:|:--:|
| Connection|  any iterative algorithm can be written recursively.|
| Why to use it | | It is easier to do analysis and prove correctness on the smaller constant amount of work and info maintaining some invariant.|
| **Idea**| | break down a problem into smaller **subproblems**, whose solutions can then be combined to solve the original problem.|
| **implementation** - simulate **repetition**  | use for or while **loops** | use a **function that calls itself** <br> - The **base case** is the condition at the start of any recursive function that **terminate** the recursive calls. <br> **recurrence relation** - an equation that **connects** solutions to subproblems. |
| the **order** of code execution| start at the top, and go line by line | We start with the first call. In each function call, we check if it reaches base case, if so, trigger the **base case** and return; if not, execute the function code, then move to a next function call, the old one waits until the new one returns. The order in which the calls happens is remembered, and the lines within the functions are executed in order. When we reach the base case, return and then the recursion **"moves back up"** - move to the next line, return the current function, and so on, until we eventually return from the first call and the algorithm terminates. <br> <br> Note that each function call also has its **own local scope**. |
---