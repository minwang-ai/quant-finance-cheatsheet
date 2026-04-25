## Table of Contents
* [Table: Covariance vs. Correlation](#covariance-vs-correlation)
* [Table: Collinear Variables](#collinear-variables)
* [Table: Impact of Multicollinearity in Regression Model](#impact-of-multicollinearity-in-regression-model)
* [Table: Methods to Address Multicollinearity](#methods-to-address-multicollinearity)
    * Principal Component Analysis (PCA)
* Code
    * [Code: Correlation](#code-correlation)
    * [Code: PCA](#code-pca)


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
|**covariance matrix**| a matrix that contains all pairwise covariances from all variables.| The diagonal elements of the covariance matrix are also the variance of the variables|
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
| **Method 3: Use principal components from Principal Component Analysis (PCA)** | 1. Use PCA to **create new variables (principal components)** that are **independent** (uncorrelated/ orthogonal), and select the first few components to replace the original correlated variable. <br> 2. Choose the top k principal components explain most (e.g.about 95%+) of the total variance. <br> 3. For the k principal components, choose the **original variable with the highest absolute value of the coefficient** in the linear combination as a **proxy** of that principal component or  <br> look for a financial theme from the loadings of a principal component and select original variables related to the theme. <br> 4. rerun to the revised model with **fewer independent variables** to see the difference. | <br>• Each principal components is a linear function of the original variables <br>•  PCs preserve as much information (variation) as possible.  <br>• PCA also ranks each principal component's ability to explain the dataset variation. The first principal component has the highest ability to explain the variation of the dataset.  <br> • It allows reducing many variables to a smaller set (**dimension reduction**) <br> •  Note: By selecting the top variables from PCA for data analysis, there is a **trade-off** between reducing multicollinearity and losing data explaining accuracy, which will depend on a researcher's experience in data analysis.|
---

### Principal Component Analysis (PCA)
**Baic idea:**
PCA rotates the original coordinate system into a new one whose axes (principal components) capture the most variance and are uncorrelated, allowing us to reduce dimensionality and remove multicollinearity.

#### Derivation of Principal Components
| Step | What You Do | Explanation / Formula |
|------|--------------|--------------------------------|
| **1. Standardize the Dataset** | Convert each variable to standardized form. <br> • Ensures all variables have the same scale <br> Mean = 0 and variance = 1   | $ \text{Standardized Variable} = \frac{\text{Original Variable} - \text{Mean}}{\text{Standard Deviation}} $ |
| **2. Calculate the Covariance Matrix** of the Standardized Variables| Compute pairwise covariances between all standardized variables | $\text{Covariance} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{N} $  <br> Diagonal elements = variances of the variables <br> $Var(X) = E[(X - E(X))^2]= Cov(X,X)$|
| **3. Calculate Eigenvectors and Eigenvalues** from the covariance matrix | Use linear algebra to obtain eigenvectors and eigenvalues of the covariance matrix. <br> Note: most software doesn't readily provide eigenvalues. They instead provide a proportion of the total variance explained by the principal component. This proportion is calculated from the eigenvalue of the principal component. | • Eigenvectors are the **direction** of the principal components <br> • Eigenvalues show **how much variance** each principal component explains <br> • The component with the **largest eigenvalue** = **PC₁** <br> • The second largest = **PC₂**, etc. |
| **4. Transform the Original Variables into Principal Components** | generate PCs by linear combination of eigenvectors, i.e., Multiply the standardized data by the transformation matrix $PC = W^TX$ | Transformation matrix  (stacking eigenvectors, columns = eigenvectors, e.g., $(a_1, a_2)$ for PC₁): <br> $W = \begin{pmatrix} a_1 & b_1 \\ a_2 & b_2 \end{pmatrix}$  <br> $PC_1 = a_1 Var_1 + a_2 Var_2$ <br> $PC_2 = b_1 Var_1 + b_2 Var_2$ |
---

## code
### code: Correlation
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



### code: PCA
```
# Libraries
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import statsmodels.formula.api as smf
from scipy.stats import boxcox
from sklearn import preprocessing
from sklearn.decomposition import PCA



# Load the dataset
data_set = pd.read_csv("data_set_name.csv")



# Select n variables and standardise
pc = data_set[
    [
    "variable_1",
    "variable_2",
    "variable_3",
    "variable_4",
    ...,
    "variable_n",
    ]
]
pca_data = preprocessing.scale(pc)
pca = PCA(n_components=n)
pca.fit(pca_data)


# Get proportions of variance and cumulative proportion of variance for PCA
pr_var = pca.explained_variance_ratio_
cum_pr = np.cumsum(pca.explained_variance_ratio_)
ind = ["Proportion of variance", "Cumulative proportion of variance"]
cols = ["PC1", "PC2", "PC3", "PC4", "PC5", "PC6", "PC7", "PCn"]
pd.DataFrame(np.vstack((pr_var, cum_pr)), ind, columns=cols)


# Coefficients (Loadings) of n Principal Components
pc_res = pd.DataFrame(pca.components_.T, index=list(pc.columns), columns=cols)
pc_res


# choose the original variable with the highest absolute value of the coefficient in the linear combination as a proxy of that principal component
# OLS for revised model
model_4 = smf.ols(
    "Y ~ Proxy_X1 + Proxy_X2 + Proxy_X3 + ... + Proxy_Xn",
    data=data_set,
).fit()
model_4.summary()
```