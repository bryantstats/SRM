---
title: "AYU - Pod Week 2"
format: 
  html: 
    toc: true
editor: visual
---




## Instruction

1.  *Download the Rmarkdown submission file at [this link](02_ayu_pod_submission.Rmd)*

2.  *Once you are done answering all the question, Knit the file (Use: Ctrl + Shift + K or Click to Knit -\> Knit to pdf) to convert the Rmarkdown file into a pdf or word file to submit to Canvas.*

------------------------------------------------------------------------

## 1. Sample Codes - Term Life Insurance

![](term_life.png)

In this practice, we will study a term life insurance dataset collected by the Survey of Consumer Finances (SCF) which includes information about face values of life insurance demographic characteristics the customers such as age, income and martial status. The data and variable discription can be downloaded at the links below.

-   [Term Life Insurance](https://bryantstats.github.io/SRM/ayu_pod/data/TermLife.csv),

-   [Variable Discription](https://bryantstats.github.io/SRM/ayu_pod/data/TermLife_Descriptions.pdf)

Import the data into R


::: {.cell}

```{.r .cell-code}
library(tidyverse)
d <- read_csv("https://bryantstats.github.io/SRM/ayu_pod/data/TermLife.csv")
```
:::


### Train a MLR

We will train a linear regression where the response variable is the amount that the company will pay in the event of the death of the named insured (`FACE`) and the predictors are `EDUCATION`, `NUMHH` (Number of household members) and `INCOME`. We then report the summary of this linear regression using the `summary` function.


::: {.cell}

```{.r .cell-code}
# Filter out those with zero FACE values
d = d[d$FACE>0,] 

# Train a MLR model
MLR_model = lm(FACE ~ EDUCATION+NUMHH+INCOME, data=d)

# Report model summary
summary(MLR_model)
```
:::


### Making Predictions

-   Once the model is trained (i.e., the coefficient are determined), we can use it for prediction. Let's predict the `FACE` of a person with 14 years of education (`EDUCATION=14`), an income of 100,000 (`INCOME=100000`) and Number of household members being 3.


::: {.cell}

```{.r .cell-code}
predict(MLR_model, list(EDUCATION = 14, 
                        NUMHH = 3, 
                        INCOME = 100000))
```
:::


-   A 95% confidence interval can also be calculated


::: {.cell}

```{.r .cell-code}
predict(MLR_model, list(EDUCATION = 14, 
                        NUMHH =3, 
                        INCOME = 100000), 
        interval = 'confidence', level = 0.95)
```
:::


-   We use the Use the model to predict the `FACE` values of a list of people. For example, the below codes will give predictions for the following people.

| EDUCATION | NUMHH | INCOME |
|-----------|-------|--------|
| 14        | 3     | 120000 |
| 20        | 5     | 250000 |
| 18        | 2     | 200000 |


::: {.cell}

```{.r .cell-code}
predict(MLR_model, list(EDUCATION = c(14, 20, 18), 
                        NUMHH = c(3, 5, 2), 
                        INCOME = c(120000, 250000, 200000)))
```
:::


### Including Categorical Variables

-   Let's include a categorical predictor, `ETHNICITY`. We first check to see how many categories in this variable using the `table` function


::: {.cell}

```{.r .cell-code}
table(d$ETHNICITY)
```
:::


We observe that there are four categories of `ETHNICITY`. This means that the model will have three variables to indicator variables (dummy variables) in its equation.


::: {.cell}

```{.r .cell-code}
MLR_model <- lm(FACE ~ EDUCATION+NUMHH+INCOME + factor(ETHNICITY), data=d)
summary(MLR_model)

predict(MLR_model, list(EDUCATION = 14, 
                        NUMHH =2, 
                        INCOME = 54000, 
                        ETHNICITY=1))
```
:::


### Generalized F-test

-   Consider the two following models

    -   Model 1: Regressing `Face` on `EDUCATION` and `NUMHH`
    -   Model 2: Regressing `Face` on `EDUCATION`, `NUMHH` and `INCOME`

We will use the F-test to see if adding `INCOME` would make model 2 is significant to model 1.


::: {.cell}

```{.r .cell-code}
model1 <- lm(FACE ~ EDUCATION+NUMHH, data=d)
model2 <- lm(FACE ~ EDUCATION+NUMHH+INCOME, data=d)

anova(model1,model2)
```
:::


The p-value of this test is 0.005077, which means that at the significant level of 0.05, we should reject model 1 in favor of model 2.

-   Now let's consider two following models

    -   Model 1: Regressing `Face` on `EDUCATION` and `NUMHH`
    -   Model 3: Regressing `Face` on `EDUCATION`, `NUMHH` and `SEDUCATION`


::: {.cell}

```{.r .cell-code}
model1 <- lm(FACE ~ EDUCATION+NUMHH, data=d)
model3 <- lm(FACE ~ EDUCATION+NUMHH+SEDUCATION, data=d)

anova(model1,model3)
```
:::


The p-value of this F-test if 0.1063, which shows that adding `SEDUCATION` does not make model 3 more significant than model 1. Thus, we fail to reject model 1 in favor of model 3.

### Improving Models

In this section, we will show different ways to improve the $R^2$ of a MLR.

-   Transformation


::: {.cell}

```{.r .cell-code}
MLR_model <- lm(log(FACE) ~ NUMHH+log(INCOME) + factor(ETHNICITY), 
                data=d)
summary(MLR_model)
```
:::


-   Add more predictors


::: {.cell}

```{.r .cell-code}
MLR_model <- lm(log(FACE) ~ EDUCATION + 
                  NUMHH+
                  log(INCOME) + 
                  factor(ETHNICITY), 
                data=d)
summary(MLR_model)
```
:::


-   Add Interactions


::: {.cell}

```{.r .cell-code}
MLR_model <- lm(log(FACE) ~ EDUCATION + 
                  NUMHH+
                  log(INCOME) + 
                  factor(ETHNICITY) + 
                  EDUCATION*NUMHH*ETHNICITY, 
                data=d)

summary(MLR_model)
```
:::

::: {.cell}

```{.r .cell-code}
MLR_model <- lm(log(FACE) ~ poly(log(INCOME), 2), data=d)
summary(MLR_model)
```
:::


When you run these codes, do you observe the improvement of the $R^2$?

## 2. Questions

1.  Run the all codes in the Section 1 and show all the results.

In the next questions, we will examine the hospital cost of patients in Wisconsin in 2003 using patients' information such as their age, gender, and their length of stay at the hospital. The data and the variables description can be downloaded at the below links.

-   [Hospital Costs](https://bryantstats.github.io/SRM/ayu_pod/data/frees/HospitalCosts.csv)

-   [Variable Description](https://bryantstats.github.io/SRM/ayu_pod/data/Hospital_Cost_Descriptions.pdf)





2.  Regress the total charge (`TOTCHG`) on age and length of stay. What is the R-squared of the regression? With significant level of 5%, is there any variable not significant based on coefficient p-values of the model?





3.  Use the model to predict the total charge of a 13-year-old that stays a week at a hospital.





4.  Adding variable `GENDER` to the regression. Write the equations of this new linear model. Use the model to predict the total charge of a 13-year-old female that stays a week at a hospital.





5.  Does adding `AGE` and `APRDRG` to the model in Question 4 make it more significant? Use the F-test to address the question.





6.  Could you improve the model in 4. using the methods discussed for the term life dataset?








