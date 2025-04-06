# basic Concepts
| Topic | Concept | Notes|
|-------|---------|-----------------------|
| Time Value of Money | $100 today is worth more than $100 in the future. | Reason: <br>1. Immediate consumption <br> 2. Have the opportunity to invest and gain more. |
|  Interest Rates | When we take out a loan, we must repay the principal value of that loan and make periodic interest payments to the lender. It is the cost of borrowing money (from the point of view of the borrower), <br> or the return on investment (from the point of view of the lender).  <br> The lenders determine interest in terms of an annual rate. | 1. To compensat for the risks: the longer the duration, the larger the amount of the loan, the worse economic conditions (which makes the borrower less likely to repay), the higher interest will be.  <br> 2. Banks may compete with each other by offering lower interest rates to attract new business.
| Present Value (PV)|  It discounts the future amount of money back to today’s value. | Essentially asking: <br> If I will get $105 in the future, how much is that worth today?
| Future Value (FV)| It grows today’s money into the future's value. | Essentially asking: <br>  If I have $100 today, how much will I have in the future after earning interest?



# Interest Types
## Denotation
| Symbol | Meaning |
|-------|---------|
| $P$ | the principal amount |
| $PV$| present value |
| $FV$|  future (or forward) value |
| $n$| the number of years (integer count), used in simple interest|
| $t$| continuous time of loan or investment in years (decimal/fractional allowed), used in compound interest|
| $r$| the (nominal) annual interest rate 
| $q$| compound frequency: number of compounding period $q$ times per year|
| $qt$| Total number of compounding periods over the investment|
| $r_q$| nominal annual rate $r$ with $q$ compound frequency| 

## Simple Interest VS Compound Interest
| Type | Concept | Formula | note |
|-------|---------|------------|-----------|
| Simple <br> Interest | Interest earned only on principal. | $$ \text{Simple Interest} = P \times r \times n $$ <br> $$FV = PV \times(1+nr)$$| Usually for Certificates of Deposits. Better when we are borrower.
| Compound Interest | Interest earned on principal + accumulated previous interest. | $ \text{Compound Interest} = P \times (1 + r)^t - P$ <br> $$FV = PV \times(1+r)^t$$ <br> $$ \Rightarrow PV = \frac{FV}{(1 + r)^t}$$  <br> $$ \Rightarrow r = \left(\frac{FV}{PV}\right)^{1/t} - 1$$| Most common type. Better when we are depositor/investor. <br> [Growth of investments over time:](https://worldquantuniversity.shinyapps.io/wqu_compound_interest_m1_ck/) <br> • the nearly linear growth with low interest rates and fewer compounding periods <br> • an exponential growth pattern when higher interest rates, more frequent compounding periods, and extended time frames are applied. 

*Figure 1: Difference between simple and compounded interest over time.*

![Difference between the simple and compounded interest](Difference_simple_compounded_interest.png "Difference between the simple and compounded interest")
Note: the compound interest grows much faster than simple interest over time






## Compound Interest


| Concept |	Explanation |	Note / Example
|-------|---------|------------|
| Compound Frequency |	How often interest is added to your account. | monthly = 12 times/year, quarterly = 4 times/year, daily = 365 times/year |
| Nominal Annual Rate |	The stated (advertised) yearly interest rate, not accounting for compounding frequency. 	| 12% annual rate compounded monthly ≠ 12% actual return. |
| Discrete Compounding| with compounding frequency: <br> $$FV = PV \times(1+r)^t = PV \times\left(1+\frac{r}{q} \right)^{qt}$$| |
| Continuous Compounding | the extrame case, when compound frequency $q$ is infinite large - interest is added at every instant $$ \lim_{q \to \infty} FV = PVe^{rt}$$ |  |
| Effective Annual Rate (EAR)	| The true annual rate, including the effect of compounding. Formula: $$\text{EAR} = \left(1 + \frac{r}{q} \right)^q - 1$$| 12% nominal annual rate compounded monthly ≈ 12.68% EAR. <br> It allows: <br> 1. fair comparison for two investment offers with different compounding frequencies <br> 2. Understanding how much you’re really earning or paying. |
| Keep EAR the Same and Convert the Nominal Rate | Keep Effective Annual Rate the same, convert from one nominal rate with its compounding frequency to another. Formula: $$\frac{FV}{PV} = \left(1 + \frac{r_{q_1}}{q_1}\right)^{q_1} = \left(1 + \frac{r_{q_2}}{q_2}\right)^{q_2}$$ $$\Rightarrow r_{q_2} = q_2 \times \left[\left(1 + \frac{r_{q_1}}{q_1}\right)^{q_1/q_2}-1\right]$$ |  |  

