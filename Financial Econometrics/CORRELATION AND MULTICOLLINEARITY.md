## Table of Contents
* [Table: Covariance vs. Correlation](#covariance-vs-correlation)
* [Table: Collinear Variables](#collinear-variables)
* [Table: Impact of Multicollinearity in Regression Model](#impact-of-multicollinearity-in-regression-model)
* [Table: Methods to Address Multicollinearity](#methods-to-address-multicollinearity)
* [Code](#code)


## Covariance vs. Correlation
| Metric | Meaning | Formula | Range | How to Interpret |
|--------|-------------------------------|---------------------------|--------|---------------------------------------------|
| **Covariance** | Measures the amount of movement the two variables exhibit together. <br> **Downside:** value changes when variable scales change | $ \mathrm{Cov}(X, Y) = \\ E[(X - E[X])(Y - E[Y])] $ | (−∞, +∞) | • **Positive sign:** move in the same direction<br>• **Negative sign:** move in opposite directions<br>• **0:** linearly uncorrelated<br>• **Higher absolute value:** stronger positive or negative relationship |
| **Correlation** | Measures the co-movement of two variables but removes the scale issue | $ \mathrm{Corr}(X, Y) = \frac{\mathrm{Cov}(X, Y)}{\sqrt{\mathrm{Var}(X)\,\mathrm{Var}(Y)}} $ | −1 to +1 | • **> 0:** positively correlated. **1**: Perfect positively correlated <br>• **< 0:** negatively correlated **-1**: Perfect negatively correlated <br>• **0:** linearly uncorrelated|
---



## Collinear Variables
| Concept | Meaning (Notebook Summary) | How to Detect / How to Read |
|---------|------------------------------|------------------------------|
| **Collinearity** | When **two variables move together** in systematic ways; they are correlated | Check their correlation value: if they move together → correlated (collinear) |
| **Multicollinearity** | When **more than two variables** are correlated | Use the **correlation matrix** to see all pairwise correlations among many variables |
| **Correlation Matrix** | A matrix showing the **correlation between every pair of variables** | Upper-right triangle shows correlations; lower-left triangle provides the same correlation information as the upper right triangle; diagonal is 1 (variable correlated with itself) |



## Impact of Multicollinearity in Regression Model
If independent variables are highly correlated
| Effect of Multicollinearity | Indication | Why It Matters |
|-----------------------------|--------------------------------|----------------|
| Large variances & standard errors and covariances of the coefficients | Regression cannot distinguish which correlated X variable drives Y | Coefficients become unstable and noisy |
| Wide confidence intervals** for the coefficient estimates  | Estimates become less precise | Hard to trust the coefficient values |
| High p-values (less significant) | Even important variables may appear insignificant | May drop variables incorrectly |
| R² and Adjusted R² may still be high | The model as a whole still explains Y well | Good overall prediction even if individual betas are unreliable |
| Hard to isolate each variable’s individual effect | Correlated variables “share credit” | Interpretation becomes difficult |
| Model may still forecast well | If future Xs of test data have the same correlation patterns as training data | Good for prediction, bad for explanation |
---




## Methods to Address Multicollinearity
| Method | What to do| Notes  |
|--------|-------------------------|--------------------------|
| **Method 1: Drop Highly Correlated Variables** | Identify independent variables with **high correlation** **(usually 0.8–0.9)**, then drop one and re-run the regression model to see if the model improves | • Only considers pairwise relationships (two variables at a time) <br>• Cannot detect multicollinearity involving >2 variables <br>• using correlation alone cannot find this issue. 
| **Method 2: to determine if any of the independent variables can be explained by the other independent variables** | Treat one independent variable as dependent as a dependent variable and run a regression with the rest of the independent variables. Use **variance inflation factor (VIF)** to determine if an independent variable has a multicollinearity issue <br> $VIF = \frac{1}{(1 − R²)} $ | • VIF starts at 1 and has **no upper limit** <br>• When R² = 0 → VIF = 1 → no multicollinearity <br>• higher R² → Higher VIF = more multicollinearity <br>• VIF 1–5 → no severe multicollinearity <br>• **VIF > 5 → severe multicollinearity**
| **Method 3: use information from a principal component analysis**||
---



## code

```
# Libraries
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import statsmodels.formula.api as smf
from statsmodels.stats.outliers_influence import variance_inflation_factor

plt.rcParams["figure.figsize"] = (12, 9)

# Load the dataset
data_set = pd.read_csv("data_set_name.csv")




# Correlation plot of all the variables
data = data_set[
    [
        "variable_1",
        "variable_2",
        "variable_3",
        "variable_4",
        ...
        "variable_n"
    ]
]
c = data.corr()
sns.heatmap(c, annot=True)
plt.show()





# Regression Model with Independent Variables
model_1 = smf.ols(
    "Y ~ X_1 + X_2 + ... + X_n",
    data=data_set,
).fit()
model_1.summary()


# Parameters with high precision
model_1.summary2().tables[1]


# Regression model to check multicollinearity among independent variables
model_dow = smf.ols(
    "X_i ~ X_1 + X_2 + ... + X_n",
    data=data_set,
).fit()
model_dow.summary()




# show the list of the VIF values of all independent variables
labels = [
    "Intercept",
    "variable_1",
    "variable_2",
    "variable_3",
    "variable_4",
    ...
    "variable_n"
]

variables = model_1.model.exog
vif = [variance_inflation_factor(variables, i) for i in range(variables.shape[1])]

pd.DataFrame(vif[1:], labels[1:], columns=["VIF"])
```

