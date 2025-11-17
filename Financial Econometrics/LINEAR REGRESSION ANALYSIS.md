
## Table of Contents
* [Table: Overview of the Linear Regression Project Setup](#overview-of-the-linear-regression-project-setup)

## Overview of the Linear Regression Project Setup
| Step | Meaning / Examples | Key Actions |
|------|---------------|-------------|
| **1.1 Identify potential factors** that impact the stock price and **collect data** |  e.g., sales, whole stock market movement trends | Research economic, market, and company-specific factors, Collect relevant data |
| **1.2 Quantify relationships** between stock price and selected factors by **building a model** | e.g., linear regression analysis | select models|
| **1.3 Predict** future stock price | e.g., simulate how much the stock price would change given a 0.5% increase, 1% increase, and 2% increase in revenue. | Convert selected factors into measurable numerical variables and convert the variables into comparable returns or ratios. , e.g., **quarterly excess returns** and **quarterly** sales growth | 
|2. **Decide Y (dependent) and X (independent) variables**| <br> • **Y**: An endogenous variable, also called a dependent variable: whose value is determined by the model. <br> • **X**: An exogenous variable, also called an independent variable: whose value is determined outside of the model or is given to us.  |
|**3. Check relationship between Y (dependent) and X (independent) variables**|use scatter plot; use Pearson Correlation | For **scatter plot:** <br> • If draw a straight line where most of the points will be around the line (oval shape) <br> => linear relationship  <br> •  if the straight line drawn is either a horizontal line or a vertical line  <br> => The exogenous variable is independent of the endogenous variable <br> => we should drop this exogenous variable from the model.<br> • If find extreme points that are well-separated from the other points., <br> e.g., 1. An outlier is a point that doesn't follow the general trend of the other points. <br> 2. A leverage point has extreme value for exogenous variables. Both types may or may not impact the estimated result of the regression model. <br> =>Try to run one model with them and another model without them.<br> => Then, compare the two model results to see if these extreme points are crucial to the final model result. <br> For **Pearson Correlation [-1, 1]:**  <br> • If the value of two variables tends to move in the **same direction**, the correlation is **positive**. A correlation towards **$1$** means the two variables have a **perfectly** positive linear relationship, while towards 0 means less and less linear relationship. <br> • If the two variables tend to move in **opposite directions**, the number is **negative**.  |
|**4. build the regression model.** |||
|**5. Assess the Model fit**  |||
---

**Note:**
* Why excess return? 
    * Finance theory tells us a stock **excess return** is a better variable to analyze than the actual price. The **excess return** is the actual return minus risk-free interest rate (usually Treasury Bill Rates),to explain the part of the return that comes from taking additional risk than deposit it in banks with zero risk.
* Why quarterly data?
    * Because daily data is noisy. Quarterly data matches how real economic factors move (Many important financial things only change every 3 months, such as: company earnings, interest rate policy, GDP growth, inflation trends, industry performance). 


## 



##





## Code
```
python

# Libraries
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import statsmodels.api as sm
import statsmodels.formula.api as smf

plt.rcParams["figure.figsize"] = (12, 9)




# Load the dataset
data_set = pd.read_csv("dataset_name.csv")




# Create scatter plot
scatt = data_set.plot.scatter(
    x="x_variable_index",
    y="x_variable_index",
    title="Scatterplot XXX Stock Excess Return vs X variable Excess Return",
)
scatt.set(xlabel="... Excess Return", ylabel="... Excess Return")
plt.show()




# Function to calculate correlation coefficient between two arrays
def corr(x, y, **kwargs):
    # Calculate the value
    coef = np.corrcoef(x, y)[0][1]
    # Make the label
    label = r"$\rho$ = " + str(round(coef, 2))

    # Add the label to the plot
    ax = plt.gca()
    ax.annotate(label, xy=(0.3, 0.15), size=20, xycoords=ax.transAxes)




# Create the default pairplot
# (a grid of plots showing every variable against every other variable)
grid = sns.pairplot(
    data_set, vars=["variable_1", "variable_2", "variable_3", "variable_4", ...], height=3
)

# Map a scatter plot and Pearson correlation coefficient to the upper triangle
grid = grid.map_upper(plt.scatter)
grid = grid.map_upper(corr)

# Map a histogram to the diagonal 
# (shows the distribution of each variable, not comparisons)
# grid = grid.map_diag(plt.hist)

# Map a smooth density heatmap plot (showing where data points cluster) and regression line to the lower triangle
grid = grid.map_lower(sns.kdeplot)
grid = grid.map_lower(sns.regplot, lowess=True, line_kws={"color": "red"})






# OLS Linear regression result 
result = smf.ols(
    "endogenous variable ~ exogenous_variable_1 + exogenous_variable_2 + exogenous_variable_3", data=data_set
).fit()
result.summary()


# Show Parameters with 6 significant digits
result.summary2().tables[1]
```
