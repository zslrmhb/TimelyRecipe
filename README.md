# TimelyRecipe

by Hongbin Miao

---

## Framing the Problem

> Prediction Problem: The number of minutes to prepare recipes.

> Problem Type: Regression

> Response Variable: minutes
>>Reason of Choice: I want to see if more ingredients and more steps in a recipe will correspond with a longer preparation time

> Evaluation metric: Root Mean Square Error
>> Reason of Choice: First, Root Mean Squared Error is a common metric for regression problem. Second, I am more familiar with analyzing the performance of a regression problem on this metric than other metrics.

---
## Baseline Model

> Model Description: A multi-variable linear regression model with no preprocessing

> Quantitative Feature(s): minutes, calories, n_steps, n_ingredients, avg_rating

> Ordinal Feature(s) : rank

> Necessary_encoding: None (i.e treat all features as quantitative)

> Model Performance: 
rmse_train:   79.47983440541547 
rmse_test:  82.61487736608815

> Comment: The current model is decent as the gap between the rmse_train and rmse_test is fairly close. Plus, this model should have a better performance than a single variable regression on a particular feature of the dataset because of the fact that the  model complexity generally increase as the number of linearly independent feature increases.
---

## Final Model

> Added Features and Why?
>> parsed "rank" to the OneHotEncoder(): since "rank" is ordinal, we should treat it as a categorical feature

>> standardized 'n_steps', 'n_ingredients', "avg_rating",  "calories": By drawing scatter plots, we can observed that there is a non-linear relationship between minutes and each of the features described above. Furthermore, a linear relationship is only apparent in a small subsection of the plot. Hence, it is reasonable to standardize each features based on their distribution

>> polynomial_features on "n_steps", "n_ingredients", "avg_rating",  "calories", "rank": To better capture the nonlinear relationship described in the bullet point above, I created polynomial features for a subset of my features to increase my model complexity




---

## Fairness Analysis


