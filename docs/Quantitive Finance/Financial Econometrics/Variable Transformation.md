[TOC]

## Table of Contents
* [Table: Variable Transformation](#variable-transformation)
* [Code: Variable Transformation]



## Variable Transformation
**Variable transformation is an iterative process.**  <br> Examine scatter plots and/or histograms <br> → apply a transformation <br>  → use the transformed variable in the model <br> → re-check model fit <br>  → try another transformation until the model result is good.


### Term Definition
| Term | Meaning |
|-------|-----------------------|
| **Raw data**| the dataset that comes straight from the data source. There might be missing values, outliers, wrong data input, etc. |
| **Raw Variable** | a variable from the cleaned dataset that has not otherwise been manipulated. Example: stock price X. |
| **Transformed Variable** | A variable created by manipulating a raw variable (i.e., f(X)). |

### When to Transform Variables? 
| Situation | Explanation |
|----------------------------------------|-------------|
| **Situation 1: Raw variables not in proper form** | Different raw variables may be on very different scales (e.g., *different stock price*). Transforming (e.g., price → price return) puts variables on the **same scale**, making them easier to compare and analyze. You may also create new variables to gain new insights (e.g., *Sales per Trip*). |
| **Situation 2: Raw variables do not meet model assumptions** |financial models require assumptions (e.g., **linear relationships** or **normal distribution**). If scatter plots show non-linearity or histograms show skewed distributions, transformation is needed. |


### Methods to Transform Variables
| Methods | Explanation |
|-----------------------------------|-------------|
| **Method 1: Transformation for Linear Relationship** | Apply transformations (log, square root, cube root) to make the relationship between X and Y more **linear**. These transformations: (1) preserve the order of data points, (2) reduce the impact of outliers.|
| **Method 2: Transformation for Normal Distribution** | Used when a model requires a variable to be **normally distributed**. Apply transformations (log, sqrt, cube root) or **remove outliers** on the tail. <br> use **Box–Cox Transformation** to systematicly transform a non-normal variable into a more normally distributed one. Formula: 
$$
\text{newY} =
\begin{cases}
\dfrac{Y^\lambda - 1}{\lambda}, & \text{if } \lambda \neq 0 \\
\log(Y), & \text{if } \lambda = 0
\end{cases}
$$|







## code: Variable Transformation
```
# Generate random dataset
np.random.seed(0)  # to make reproducible example
Y = np.random.exponential(size=500)

# Plot distribution of data
plt.figure(figsize=(7, 7))
plt.title("Histogram of Y")
sns.histplot(Y, kde=True)
plt.show()



 
# Apply Box-Cox transformation on original data
new_Y, best_lambda = boxcox(Y)
print("Optimal Box-Cox transformation lambda:", best_lambda)

# Plot distributions of original data
plt.figure(figsize=(14, 5))
ax1 = plt.subplot(121)
sns.histplot(Y, kde=True, ax=ax1)
plt.title("Histogram of $Y$")

# Plot distribution of transformed data
ax2 = plt.subplot(122)
sns.histplot(new_Y, kde=True, ax=ax2)
plt.title("Histogram of $newY$")
plt.show()
```
