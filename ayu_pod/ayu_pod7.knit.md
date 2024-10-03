---
title: "AYU - Pod Week 7"
format: 
  html: 
    toc: true
editor: visual
---




### Instruction

1.  *Open the Rmarkdown file of this assignment ([link](07_ayu_pod_submission.Rmd)) in Rstudio.*

2.  *Right under each question, insert a code chunk (you can use the hotkey Ctrl + Alt + I to add a code chunk) and code the solution for the question.*

3.  *Once you are done answering all the question, Knit the file (Use: Ctrl + Shift + K or Click to Knit -\> Knit to pdf or Word) to convert the Rmarkdown file into a pdf or word file to submit to Canvas.*

------------------------------------------------------------------------


![](15.png)

(Source: seattletimes.com)

In this assignmemt, we will use the K-Nearesr Neighbor (KNN) model makes predictions on the [German Credit dataset](german_credit2.csv). 

This dataset contains 20 variables includung the classification whether an applicant is considered a Good or a Bad credit risk for 1000 loan applicants (variable: `Creditability`). A predictive model developed provides guidance for making a decision whether to approve a loan to a prospective applicant based on their profiles. 

To build a KNN model, we first need to scale all the continuous variables into the range of 0 and 1.  All the categorical variables will be decoded into multiple numeric variables associated with the catagories taking values of 0 and 1.  The function `knn_prepared` below will prepare the dataset so that it is ready for KNN. 

## KNN for Classification


::: {.cell}

```{.r .cell-code}
# dummy all categorical variables
# normalize all continuous variables to range 0 and 1
knn_prepared = function(d, target_variable)
{
  library(tidyverse)
  library(fastDummies)
  
  target = d[[target_variable]]
  
  d = d %>% select(-target_variable)
  
  d_numeric = d %>% summarise_if(is.numeric, 
                                 function(x){
                                   (x-min(x))/(max(x)-min(x))
                                   })
  
  rt = d_numeric
  
  d_category = d %>% select_if(~!is.numeric(.))
  
  if (!ncol(d_category)==0)
  {
    d_category_dummy = dummy_cols(d_category, 
                                remove_first_dummy = TRUE,
                                remove_selected_columns=TRUE)
    
    rt = as_tibble(cbind(d_numeric, d_category_dummy))
  }
  
  rt$target = target
  
  return(rt)
  
}
```
:::


We then read the dataset, applying the `knn_prepared` function to it, splitting the data into training and testing dataset, building the KNN model on the trainning dataset and evaluate the model performance on the testing dataset.   



::: {.cell}

```{.r .cell-code}
library(tidyverse)
library(caret)
library(class)

df <- read_csv('german_credit2.csv')

df = knn_prepared(df, target_variable = 'Creditability')

library(caret)
set.seed(2023)
splitIndex <- createDataPartition(df$target, p = .90, 
                                  list = FALSE)
df_train <- df[ splitIndex,]
df_test <- df[-splitIndex,]

pred = knn(select(df_train, -target), 
           test = select(df_test, -target), 
           cl = df_train$target,
           k = 7)

cm <- confusionMatrix(data = pred, 
                      reference = as.factor(df_test$target), 
                      positive = "1")
cm$overall[1]
```

::: {.cell-output .cell-output-stdout}
```
Accuracy 
    0.71 
```
:::
:::

::: {.cell}

:::


### Practice 1

Use the [Actuarial Loss dataset](actuarial_loss.csv),

- Train a KNN with `k = 3` on the training data to predict the claim cost category (i.e., `claim_cost_category` is your target variable). 

- Calculate the accuracy of the model on the test data.

## KNN for Regression

For the regression task, we will train a KNN to predict the `Credit Amount` of an applicant.  The steps for regression is very much the same as for classification as described follows. 


::: {.cell}

```{.r .cell-code}
library(FNN)
df <- read_csv('german_credit2.csv')

df = knn_prepared(df, target_variable = 'Credit Amount')


library(caret)
set.seed(2020)
splitIndex <- createDataPartition(df$target, p = .70, 
                                  list = FALSE)
df_train <- df[ splitIndex,]
df_test <- df[-splitIndex,]


pred = knn.reg(train = select(df_train, -target), 
               test = select(df_test, -target), 
               y = df_train$target, 
               k = 10)

postResample(pred = pred$pred, obs = df_test$target)
```

::: {.cell-output .cell-output-stdout}
```
        RMSE     Rsquared          MAE 
2451.3859498    0.2617057 1680.7370000 
```
:::
:::


### Practice 2

- Train a KNN with `k = 5` on the training data to predict the ultimate claim cost (i.e., `UltimateIncurredClaimCost` is your target variable).  

- Calculate the RMSE, Rsquared and MAE of the model on the test data.

## Questions

1.  Run the all the above codes show all the results

2.  Do Practice 1 and 2.
