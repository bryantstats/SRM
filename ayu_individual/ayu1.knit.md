---
title: "AYU - Individual Week 1"
format: 
  html:
    toc: true
editor: visual
---





Watch the videos to see how the similar problems are solve.

### Parameter estimation

<!--

**Problem 1.** 

Given the data

| x | 2 | 3 | 5 | 6 | 1 | 9 |10| 15|
|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| y | 1 | 4 | 6 | 4 | 4 | 3 |20|25|

Write the equation of the best fitted line.

A. $y = -1.722 + 1.584x$ \
B. $y = -1.722 - 1.584x$ \
C. $y = 1.722 + 1.584x$ \
D. $y = 1.584 + 1.722x$ \
E. $y = -1.584 + 1.722x$ \


::: {.cell}

:::

---
-->

**Problem 1.** 

The regression model is $y=\beta_0 + \beta_1x+\epsilon$. There are six observations. The summary statistics are: 
\begin{align*} 
\sum{y_i} &= 58, \\
\sum{x_i}&=21, \\
\sum x_i^2 &= 91, \\
\sum x_iy_i &= 259, \\
\sum y_i^2 &= 754
\end{align*}

Calculate the least squares estimate of $\beta_1$.

(A) 3.0
(B) 3.2
(C) 3.4
(D) 3.6
(E) 3.8

---

::: {.cell}

:::



**Problem 2** 

The regression model is $y=\beta_0 + \beta_1x+\epsilon$. You are given the follows. 
\begin{align*} 
n &= 10, \\
\bar{y} &= 21.1, \\
\bar{x}&=7.5, \\
\sum x_i^2 &= 759,\\ 
\sum x_iy_i &= 2253,\\ 
\sum y_i^2 &= 7657
\end{align*}


::: {.cell}

:::


Predict $y_{11}$ given that $x_{11}=20$

A. 63.748 \
B. 62.758 \
C. 64.758 \
D. 65.758 \
E. The correct answer is not given by (A), (B), (C), or (D).

---

**Problem 3** 

You are given the following summary statistics:

\begin{align*}
\bar{x} = 6 \\
\bar{y}=13.75 \\
\sum (x_i-\bar{x})^2 = 102 \\
\sum (x_i - \bar{x})(y_i-\bar{y}) = 192 \\
\sum (y_i-\bar{y})^2 = 503.5
\end{align*}

Determine the equation of the regression line, using the least squares method. 

(A) $y = 2.456  + 1.882x$ 

(B) $y =  0.78  + 1.882x$

(C) $y =  2.456  + 0.65x$

(D) $y =  0.39  + 0.70x$

(E) The correct answer is not given by (A), (B), (C), or (D).


::: {.cell}

:::


---

### Goodness of Fit

**Problem 4** 

For a simple linear regression model the sum of squares of the residuals is 

$$
RSS = \sum_{i=1}^{25} e_i^2 = 300
$$
and the $R^2$ statistic is 0.8. Calculate the total sum of squares (TSS) for this model. 

(A) 1000
(B) 1200
(C) 1500
(D) 2000
(E) 2500


::: {.cell}

:::



---

**Problem 5** 

For a simple linear regression model the total sum of squares (TSS) is 1000

and the $R^2$ statistic is 0.7. Calculate the sum of squares of the residuals for this model. 

(A) 300
(B) 400
(C) 500
(D) 600
(E) None of the above



::: {.cell}

:::


---

**Problem 6** (SRM - Sample Question 11)

You are given the following results from a regression model.

| Observation number (i) | $y_i$ | $\hat{f}(x_i)$ |
|:------------------------|:-------|:----------------|
| 1                      | 1     | 4              |
| 2                      | 2     | 3              |
| 3                      | 6     | 7              |
| 4                      | 8     | 9              |
| 5                      | 4     | 6              |

Calculate the sum of squared errors (SSE) or sum of squares of the residuals (RSS).

(A) 10
(B) 12
(C) 14
(D) 16
(E) 46


::: {.cell}

:::


---

**Problem 7** (SRM - Sample Question 44)

Two actuaries are analyzing dental claims for a group of $n = 100$ participants. The predictor variable is sex, with 0 and 1 as possible values. 

Actuary 1 uses the following regression model: 

$$Y = \beta + \epsilon$$
Actuary 2 uses the following regression model: 

$$Y = \beta_0 + \beta_1 \times Sex + \epsilon$$

The residual sum of squares for the regression of Actuary 2 is 100,000 and the total sum
of squares is 120,000.

Calculate the F-statistic to test whether the model of Actuary 2 is a significant improvement over the model of Actuary 1. 

(A) 20.5
(B) 22.6
(C) 19.6
(D) 30.1
(E) 34.5


::: {.cell}

:::


---

**Problem 8** 

Two actuaries are analyzing dental claims for a group of $n = 100$ participants. The predictor variable is sex, with 0 and 1 as possible values. 

Actuary 1 uses the following regression model: 

$$Y = \beta + \epsilon$$

Actuary 2 uses the following regression model: 

$$Y = \beta_0 + \beta_1 \times Sex + \epsilon$$

Given $R^2 = .7$. Calculate the F-statistic to test whether the model of Actuary 2 is a significant
improvement over the model of Actuary 1. 

(A) 120.67
(B) 135.67
(C) 147.67
(D) 157.67
(E) 228.67


::: {.cell}

:::


---

**Problem 9** 

The results of fitting ten observation by the regression model, $y=\beta_0 + \beta_1x+\epsilon$, are given below.

Determine the test results of the hypothesis $H_0: \beta_1 = 0$ against $H_{\alpha}: \beta_1 \neq 0$.

|           | Estimate | Std. Error | t value | Pr(>\|t\|) |
|:-----------|:----------|:------------|:---------|:------------|
| Intercept | -4.4916  | 6.6540     | -0.675  | 0.51869    |
| x         | 3.4122   | 0.7638     | 4.468   | 0.00209    |

A. Reject at $\alpha = .2$ \
B. Reject at $\alpha = .1$ \
C. Reject at $\alpha = .05$ \
D. Reject at $\alpha = .01$ \
E. All (A), (B), (C), or (D) are correct.


::: {.cell}

:::



---

### Application of Linear Model.

**Problem 10** (SRM - Sample Question 23)

Toby observes the following coffee prices in his company cafeteria:

- 12 ounces for 1.00
- 16 ounces for 1.20
- 20 ounces for 1.40

The cafeteria announces that they will begin to sell any amount of coffee for a price that
is the value predicted by a simple linear regression using least squares of the current
prices on size.

Toby and his co-worker Karen want to determine how much they would save each day,
using the new pricing, if, instead of each buying a 24-ounce coffee, they bought a 48-
ounce coffee and shared it.

Calculate the amount they would save.

(A) It would cost them 0.40 more.
(B) It would cost the same.
(C) They would save 0.40.
(D) They would save 0.80.
(E) They would save 1.20. 


::: {.cell}

:::



---

<!--

**Problem 12** 

Peter observes the following coffee prices in his company cafeteria:

- 1 bagel for 1.00 (USD)
- 2 bagel for 1.50 (USD)

The cafeteria announces that they will begin to sell any amount of bagels for a price that
is the value predicted by a simple linear regression using least squares of the current
prices.

With the new pricing model, how much Peter would save if he bought 10 bagels instead of 5 bagels twice?

(A) It would cost him more so he would not save any money. 
(B) It would cost the same.
(C) He would save 0.5 (USD)
(D) He would save 1 (USD)
(E) He would save 1.5 (USD)

---

-->
