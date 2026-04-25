## Table of Content
* [Table: Deterministic Models vs Stochastic Models](#deterministic-models-vs-stochastic-models)
* Monte Carlo Simulation
    * [Table: Fundation](#monte-carlo-simulation--foundation)
    * [Table: Overview](#monte-carlo-simulation--overview)
    * [Table: Steps](#monte-carlo-simulation--steps)
* code


## Deterministic Models vs Stochastic Models

| Model Type | Meaning  | Key Characteristics | Examples |
|------------|-------------------------------|-----------------|---------------------|
| **Deterministic Model** | A model where the **output is fully determined** by the input variables. It does not have **random term**| • No randomness involved. <br>• Same inputs always produce the **same output**. <br>• Results are predictable and fixed. | principal component analysis; factor analysis; classification or cluster analysis|
| **Stochastic Model** | A model that has random and unknown component in it with a probability distribution| <br>• Same inputs can produce **different outputs** due to randomness. <br>• Results are expressed as multiple possible outcomes or a **distribution** of outcomes. | linear regression|

## Monte Carlo Simulation
### Monte Carlo Simulation — Foundation
| Concept | Meaning / Statement | Formula | Role in Mote Carlo|
|--------|----------------------|--------------|----------|
| **Weak Law of Large Numbers (WLLN)** | The sample mean converges to the true population mean as sample size is large enough. | For i.i.d. $X_1,..., X_n$ with finite mean $\mu$ and variance $\sigma^2$: <br> sample mean $M_n = \frac{X_1+X_2+ ... +X_n}{n} \rightarrow E[X] = \mu$  as $n \to \infty$  <br> specifically: <br>  For $\epsilon>0$, $P(\|M_n - \mu\| \ge \epsilon) \to 0$ as $n \to \infty$. | **Estimator of expected outcome**: using the sample average of model outcomes as an approximation of the unknown true expected outcome.|
| **Central Limit Theorem (CLT)** | The CDF of standardized sample mean $Z_n$ converges to the CDF of a standard normal distribution <br> (Not about statement about convergence of PDFs or PMFs). | $Z_n = \frac{(M_n - \mu)}{\frac{\sigma}{\sqrt{n}}} $ <br> For every c: $P(Z_n \le c) \to P(Z\le c)$ <br> where $Z \sim N(0,1)$.  | Gives the approximate distribution of the sample mean, which we use to build confidence intervals for the unknown expected value of the stochastic model.|
| **Confidence intervals (CIs)**| A range of values along with a secified confidence level, which is used to estimate an unknown statistical parameter, such as a population mean. Provide the distribution of estimated $\hat{\Theta}_n$, how likely are they to fall on top of the true value $\theta$ (typically 95%), as opposed to how likely they are to fall outside. | A random interval $[\hat{\Theta}_n^+, \hat{\Theta}_n^-]$ s.t. $P(\hat{\Theta}_n^+ \le \theta \le \hat{\Theta}_n^-) \ge 1-\alpha$ where $\alpha$ is the probability of a large error, typically $\alpha = 0.05$, $1-\alpha = 0.95$ <br> **Example: CI in estimation of the population mean:** <br> $\Phi(z) = 1-\alpha /2$ where The number $z$, we get from the normal table by looking up the probability $(1-\alpha)/2$ <br> Apply CLT we have: $P(\frac{\|\hat{\Theta}_n - \theta\|}{\sigma/\sqrt{n}} \le z) \approx 1-\alpha $<br> **The CI:**  <br> $[\hat{\Theta}_n - \frac{z\sigma}{\sqrt{n}}, \hat{\Theta}_n + \frac{z\sigma}{\sqrt{n}}]$ <br> For 95% confidence interval for the unknown mean $z=1.96$| Quantify the precision of the Monte-Carlo estimate: narrow CI → more precise. <br> To increase the precision of the Monte Carlo simulation, we can either **increase the number of simulations or reduce the variance of the outcome variable**. |
|**Estimate the unknown variance $\sigma$**| unbiased |$\frac{1}{n-1}\sum_{i=1}^n(X_i - \hat{\Theta}_n) \to \sigma^2$| When variance is unknown in the CI formula|
---



### Monte Carlo Simulation — Overview
| Topic | Summary |
|-------|---------|
| **What Monte Carlo Simulation Is** | A method that uses repeated random sampling to estimate the expected value and distribution of a model's output. Applicable when the model contains randomness or uncertain inputs. |
| **Why MC Is Needed** | Real-world models often produce different outcomes due to randomness. MC captures the distribution of possible outcomes by running the model many times. |
| **Key Idea** | Simulate the model repeatedly using independently drawn random inputs → collect many outcomes → use sample statistics (mean, variance, CI) to estimate the true unknown quantity. |
---


### Monte Carlo Simulation — Steps
| Step | Description |
|------|-------------|
| **1. Define the stochastic model** | Specify how the model’s output depends on random input variables (e.g., returns, interest rates, prices). |
| **2. Identify probability distributions** | Choose or estimate the distributions for all random variables in the model (e.g., normal, lognormal, Bernoulli). |
| **3. Generate one random scenario** | Sample random inputs from the chosen distributions and run the model once to produce a single outcome. |
| **4. Repeat the simulation n times** | Produce many independent outcomes by repeating Step 3 (e.g., 100, 1,000, 10,000, 100,000 or more like 1 Million). |
| **5. Collect outputs** | Store all simulated outcomes. These outcomes form an empirical distribution. |
| **6. Summarize outcomes** | Compute sample mean, variance, construct confidence interval and examine distribution (histogram, density). |
| **7. Interpret results** | A narrow CI indicates high precision; a wide CI suggests either high model variance or insufficient simulations. Increase n if needed. |
---

## code
```
# Load libraries
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams["figure.figsize"] = (12, 9)  # Figure size and width


# Monte Carlo Simulation

# Helper function that plots histogram and prints statistics
def Hist(trials):
    res = []

    # Simulate Monte Carlo sample
    # Example model
    for j in range(trials):
        int = np.random.normal(0.4, 0.7, 12)
        bal = []

        for i in range(12):
            bal.append(10 * (1 + int[i] / 12) ** (12 - i))

        res.append(sum(bal))

    # Plot Histogram
    plt.hist(res, bins=30, density=True, histtype="stepfilled", alpha=0.7)
    plt.title("Histogram of {} Simulations".format(trials))
    plt.xlabel("Cumulatice Account Balance")
    plt.ylabel("Frequency")

    # Add statistics
    avg = np.mean(res)  # Mean
    sigma = np.std(res)  # Std
    lowb = avg - 1.96 * sigma / np.sqrt(trials)  # Low Bound
    upb = avg + 1.96 * sigma / np.sqrt(trials)  # Upper Bound
    width = upb - lowb

    textstr = "{0} trials\n Average: {1:.2f}\nStandard Dev: {2:.2f}\
\n Upper Bound: {3:.2f}\n Low Bound: {4:.2f}\n Width: {5:.2f}".format(
        (trials), (avg), (sigma), (upb), (lowb), (width)
    )
    return textstr

    # Plot four histograms
plt.figure(figsize=(16, 12))

# No. trials = 100
ax1 = plt.subplot(221)
fig1 = Hist(100)
plt.text(
    0.95,
    0.85,
    fig1,
    ha="right",
    va="center",
    fontsize=10,
    bbox={"facecolor": "orange", "alpha": 0.5},
    transform=ax1.transAxes,
)

# No. trials = 1,000
ax2 = plt.subplot(222)
fig2 = Hist(1000)
plt.text(
    0.95,
    0.85,
    fig2,
    ha="right",
    va="center",
    fontsize=10,
    bbox={"facecolor": "orange", "alpha": 0.5},
    transform=ax2.transAxes,
)

# No. trials = 100,000
ax3 = plt.subplot(223)
fig3 = Hist(100000)
plt.text(
    0.95,
    0.85,
    fig3,
    ha="right",
    va="center",
    fontsize=10,
    bbox={"facecolor": "orange", "alpha": 0.5},
    transform=ax3.transAxes,
)

# No. trials = 1,000,000
ax4 = plt.subplot(224)
fig4 = Hist(1000000)
plt.text(
    0.95,
    0.85,
    fig4,
    ha="right",
    va="center",
    fontsize=10,
    bbox={"facecolor": "orange", "alpha": 0.5},
    transform=ax4.transAxes,
)
plt.show()

```