
[TOC]

## Table of Contents
* [Table: Overview of the Linear Regression Project Setup](#overview-of-the-linear-regression-project-setup)
* OLS Regression
    * [Table: OLS Regression](#ols-regression)
* [Table: Assess the Model fit (Metrics)](#assess-the-model-fit-metrics)
* [Table: Extreme points and Influence](#extreme-points-and-influence)
* [Code](#code)

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

**Note:**
* Why excess return? 
    * Finance theory tells us a stock **excess return** is a better variable to analyze than the actual price. The **excess return** is the actual return minus risk-free interest rate (usually Treasury Bill Rates),to explain the part of the return that comes from taking additional risk than deposit it in banks with zero risk.
* Why quarterly data?
    * Because daily data is noisy. Quarterly data matches how real economic factors move (Many important financial things only change every 3 months, such as: company earnings, interest rate policy, GDP growth, inflation trends, industry performance). 


## OLS Regression
| Concept | Formula / Definition | Meaning |
|--------|------------------------|---------|
| **Simple OLS model** | $ Y = \beta_0 + \beta_1 X + \varepsilon $ | Estimate Y using one factor X |
| **Multiple OLS model** | $Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \epsilon $ | Estimate Y using several factors. <br> $\beta$ are called parameters or coefficients. Once the values of the parameters are obtained from the OLS calculation, we call these values estimates.|


### OLS Assumptions
| OLS Assumption | Meaning / Mathematical Form | What Violation Causes | How to Detect | How to Fix (Methods) |
|----------------|-----------------------------|------------------------|----------------|------------------------|
| **1. Linearity** (correct functional form) | Relationship between X and Y is linear:  $ Y = \beta_0 + \beta_1 X_1 + \dots + \beta_k X_k + \epsilon $ | Model misspecification → unreliable coefficients, standard errors and biased estimates | <br> • Residual plots show curvature <br> • Likelihood ratio (LR) test | Get the form correct by trial and error <br> • Add polynomial terms  <br> • Transform variables (e.g., log, sqrt, Box-Cox)  <br> • Use nonlinear models |
| [**2.No Multicollinearity**](./Correlation%20and%20Multicollinearity.md)| X variables are not correlated themselves:  $ X_1 \neq c_1 X_2  + ... $ | coefficients and standard errors of affected variables are not reliable | <br> • High correlation values between X variables <br> • High Variance Inflation Factors(VIF) > 5 | <br>  • Drop variables  <br> • principal component analysis (PCA) <br> • factor analysis   |
| **3. Independence of Errors** | Errors are independent:  $ \text{Cov}(\epsilon_i, \epsilon_j) = 0 \; (i \neq j) $ | **Autocorrelation** (occur for time series data) → unreliable standard errors | <br> • Durbin-Watson test (specifically for the autocorrelation of the first -order, i.e., t-1) <br> •  Breusch-Godfrey test (generally, beyond first-order) | <br> • Investigate omitted variables <br> • Generalised idfference equation(Cochrane-Orchutt or AR(1) methods) <br>  • Use time-series models   |
| **4. Normality of Errors** | Errors normally distributed:  $\epsilon \sim \mathcal{N}(\mu, \sigma^2)$ | if n is small, unreliable standard errors  |  <br> • histogram  (not bell shape) <br> •  QQ-plot(deviates from the line)  <br> •  Shapiro-Wilk test  <br> •  Komologorov-Smirnov test  <br> • Anderson-Darling test |  <br> • change functional form|
| **5. Zero Mean of Errors** (omiited variables) | $E[\epsilon] = 0$ <br> The error term accounts for the variation in the dependent variable that the independent variables do not explain. A non-zero average error indicates that our model systematically underpredicts the observed values and we should add that information to the regression model.  | Model can only be used for predictive purpose (cannot infer causation) | Residual mean not near zero | • using instrumental variables |
| **6. Homoscedasticity (Constant Variance)** | The variances of error terms are constant:  $\text{Var}(Y\|X) = \text{Var}(\epsilon\|X) = \sigma^2$ |  The error terms are not constant (**Heteroscedasticity**) →  coefficients remain unbiased, but standard errors are unreliable | <br> • Residual plot shows one or more fan/ cone/ megaphone shapes (Residuals are either concentrated and spread out for different values of X variable), but sometimes difficult to detect <br>  **tests:** (same rule: **p-value < 0.05**) <br> • **White test** (preferred, any form of heteroscedasticity) <br> •  Breusch-Pagan(BP) test (only linear)  |   • **Weighted Least Squares (WLS)**   <br> • White's standard errors |

**Footnote**
* **Residuals** are the differences between measured values of the dependent variables and predicted values of dependent variables from the OLS regression model.
* **Error Term Distribution and Variance Structure (from OLS Assumptions 4, 5, 6):**  
    >  
    > Under the OLS assumptions of **zero-mean errors**, **homoscedasticity**, and **independence of errors**,  
    > the error terms are **IID (independent and identically distributed)**:  
    >  
    > $$ e \sim N(0,\sigma^2) $$
    >  
    > The regression mean function can be written as:
    >  
    > $$ E(Y \mid X) = \beta X $$
    >  
    > And the conditional variance of error term $e$ (equivalently, of $Y$ is constant):
    >  
    > $$ \operatorname{Var}(Y \mid X) = \operatorname{Var}(e \mid X) = \sigma^2 $$
    >  
    > Because we have multiple observations, the variance of the error variance is a **covariance matrix**.  
    > * Independence ⇒ all off-diagonal elements are zero.  
    > * Homoscedasticity ⇒ all diagonal elements equal the same constant variance.
    >  
    > $$ 
    > \operatorname{Var}(e) =
    > \begin{pmatrix}
    > \sigma^2 & 0        & 0        & \cdots & 0 \\
    > 0        & \sigma^2 & 0        & \cdots & 0 \\
    > 0        & 0        & \sigma^2 & \cdots & 0 \\
    > \vdots   & \vdots   & \vdots   & \ddots & \vdots \\
    > 0        & 0        & 0        & \cdots & \sigma^2
    > \end{pmatrix}
    > $$







## Assess the Model fit (Metrics)
| Metric | Meaning (per notebook) | Range | How to Evaluate |
|--------|--------------------------|--------|-------------------------------------|
| **p-value** <br> $Pr(>\|t\|)$ for each coefficient| indicate whether each X variable can explain the change of the Y variable | 0 to 1 | The lower, the better <br> • **p < 0.05 → X variable is significant**; <br> • p > 0.05 → transform the X variable, <br> e.g, take the square root or the logarithm of it and draw the scatter plot again|
| **R-squared (R²)** | indicate model fit: the percent of the variation in Y explained by the variation of all the X variables | 0 to 1 | **Higher is better**;  <br> 1 = perfect fit. <br> too low → consider adding a new exogenous variable (X) but not too many, because it might cause the issue of model overfitting  |
| **Adjusted R²** | indicate whether adding new independent variables to the model is worth it. | 0 to 1 | Higher is better; **Adjusted R²** will **increase** if the degree of improvement from adding one exogenous variable is greater than the penalty imposed by one additional exogenous variable to the model. <br> → **best practice:** builds several versions of the regression models and then compares their  **Adjusted R²**  to pick a final model. |

##  Extreme points and Influence

| Concept | Meaning | How It Affects Regression | How to identify |
|--------|-----------------|------------------|---------------------------|
| **Outlier** | A point with an unusual **Y value** (vertical direction) | Not all of outliers and leverage points will influence the result of the regression model.| scatter plot |
| **Leverage Point** | A point with an unusual or extrame **X value** (horizontal direction) | | scatter plot  |
| **Influential Point** | An extreme point that can significantly alter the regression result if removed | **Does change** the regression result noticeably | large bubble in the influence plot: <br> we can use Cook's Distance to identify influence point in the dataset <br> → The higher the Cook's D, the greater the influence. <br> A data point with a Cook's D larger than 1 is considered an influential point.  |


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







# Influence plot
fig = sm.graphics.influence_plot(result, criterion="cooks", alpha=0.5)
fig.tight_layout(pad=1.0)

# Finding most influential points using Cook's distance 
influence = result.get_influence()
inf_sum = influence.summary_frame().sort_values("cooks_d", ascending=False)
inf_sum.head(30)

```
