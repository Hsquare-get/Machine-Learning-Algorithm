# 데이터 누수(Data Leakage)

- Reference

  - [Data Leakage-Rafael Pierre](https://mlopshowto.com/data-leakage-part-i-think-you-have-a-great-machine-learning-model-think-again-ad44921fbf34)
  - [Data Leakage-Kaggle](https://www.kaggle.com/alexisbcook/data-leakage)
  - [Data Leakage-DACON](https://dacon.io/competitions/official/235720/support/403125?page=1&dtype=recent)

<hr/>

> ### **Think You Have a Great Machine Learning Model? Think Again**
>
> You were presented with a challenging problem.
>
> As a driven, gritty, aspiring data scientist, you used all tools that were within your reach.
>
> <br/>
>
> You gathered a reasonable **amount of data**. You have got a considerable **amount of features**. You were even able to come up with **many additional features** through feature engineering.
>
> You used **fanciest possible machine learning model**. You made sure your model didn't overfit. You properly **split your dataset** in training and test sets. You even used **K-Folds validation**.
>
> <br/>
>
> You were able to get an impressive **99% AUC score** for your classification problem. Your model has outstanding results when it comes to predicting labels for your testing set, properly detecting **True Positives, True Negatives, False Positives and False Negatives**.
>
> Or, inthe case you had a regression problem, your model was able to get **excellent MAE, MSE and R-Squared**.
>
> <br/>
>
> As a result of your efforts and the results you obtained, everyone at the office admires you. You have been lauded as the next machine learning genius.
>
> <br/>
>
> But before that, it is time for showdown: your model is going **into production**.
>
> However, when it's finally time for your model to start doing some perfect predictions out on the wild, something weird happens. Your model is simply not good enough.

<hr/>

## 1. What is Data Leakage?

- **Data leakage** happens when your **training data contains information about the target**, but similar data will not be available when the model is used for prediction. This leads to high performance on the training set (**and possibly even the validation data**), but the model will perform **poorly in production**.

- when the data used **for model training contains the information to be predicted**, it happens data leakage.
- data leakage can lead to completely **erroneous predictive models** or **overly optimistic results**, in other words, **overfitting problems**.
- **Data Leakage** happens a lot when we are dealing with data that has <u>**Time Series**</u> characteristics.

<hr/>

## 2. Data Leakage Types

### (1) Target Leakage

![Target Leakage](https://mblogthumb-phinf.pstatic.net/MjAyMDAyMTdfMjEg/MDAxNTgxODY3MTA5ODE1.vShDBNEugwqJ-Gt_THKHHpkZRN55GtlAOvbNthb8TZQg.BKeIWJgrQ3KZQinV2spDSooEw3TUZRcQd1ALf77YYYog.PNG.hongjg3229/image.png?type=w800)

**Target leakage** occurs when your predictors include data that will not be available at the time you make predictions.

To prevent this type of data leakage, **any variable created after the target value** is realized **should be excluded**.

<br/>

### (2) Train-Test Contamination

**Train-Test Contamination** occurs when you aren't careful to distinguish training data from validation data.

If you run preprocessing before calling `train_test_split()`, your model may get good validation scores.

But the model perform poorly when you deploy it.

If your validation is based on a simple train-test split, **exclude the validation data** from any type of fitting, including the fitting of preprocessing steps. This is easier if you use **scikit-learn pipelines**.

<hr/>

## 3. How to Avoid Data Leakage?

There is no silver bullet for avoiding data leakage.

But the first step, in case you have a time-series dataset, is removing time-related features.

### (1) Remove Time-Related Features

Typical forecasting problems, such as **weather**, **cryptocurrencies** and **stock market price prediction** require time series data analysis.

You might feel tempted to remove time-related features from your dataset.

However, depending on the number of features in your dataset, this could prove to be a more complicated task, and you might end up removing features that could benefit your model.

But apart from that, tackling **data leakage** involves more of a **mindset change** when it comes to **cross validation** rather than **feature selection.**

<br/>

### (2) Nested, Forward Chaining Cross-Validation

![Nested Cross-Validation](https://sebastianraschka.com/images/faq/evaluate-a-model/nested-k-fold.png)

**Nested Cross Validation** is the most appropriate method to evaluate performance when conceptualizing a predictive model for time-series data.

**Predicting the second half** is an easy and straightforward nested **cross validation** method for avoiding data leakage. It is also closer to the real-word, production scenario, but it comes with some caveats.

Depending on the splitting approach, **bias could be introduced**, and as a result, biased estimates of prediction error could be produced for an independent dataset.

![Forward Chaining](https://miro.medium.com/max/700/1*eQbqtaZYPmy70aCm8GIRBQ.png)

**Forward chaining** involves creating many different folds within your dataset, in a way that you predict the second half for each of these folds.

This exposes the model to different points in time, thus **mitigating bias**.
