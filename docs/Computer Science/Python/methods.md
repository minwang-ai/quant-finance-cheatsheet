## Lambda Function

| Feature | Regular Function | **Lambda** Function (alternative way for creating a simple function) |
| :--- | :--- | :--- |
| **When to use** | General purpose, especially when for **complex** expressions and **reusable** functions | When an **anonymous simple, temporary** function is needed immediately, not intended to be reused multiple times, such as when using **inline operations**, as **arguments to higher-order functions** (map, filter, sorted) |
| **Syntax** | `def fn_name(arguments):` <br>&nbsp;&nbsp;&nbsp;&nbsp;`block of code`<br>&nbsp;&nbsp;&nbsp;&nbsp;`return expression_or_var` | `lambda arguments: expression` |
| **Syntax details** | Starts with `def` keyword followed by the function name, arguments, and a block of code for multiple expressions, optionally explicit return statement. | Starts with `lambda` keyword followed by parameters, a colon, and a **single expression**.<br><br>* **arguments**: A comma-separated list of parameters<br>* **expression**: A single expression that is evaluated and returned automatically. |
| **Example** | `def add(x, y):` <br>&nbsp;&nbsp;&nbsp;&nbsp; `return x + y` | `lambda x, y: x + y` |
| **Scope of Variables** | Can define local variables for use within the function. | Cannot define new variables; can only use function arguments and existing variables. |
---

Figure: Regular Function vs Lambda Function
![Lambda](figures/lambda_function.jpeg)