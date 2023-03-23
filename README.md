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
> - rmse_train:   79.81700284197069 
> - rmse_test:    81.29661132078628

> Comment: The current model is decent as the gap between the rmse_train and rmse_test is fairly close. Plus, this model should have a better performance than a single variable regression on a particular feature of the dataset because of the fact that the  model complexity generally increase as the number of linearly independent feature increases.
---

## Final Model

> Added Features and Why?
>> parsed "rank" to the OneHotEncoder(): since "rank" is ordinal, we should treat it as a categorical feature

>> standardized 'n_steps', 'n_ingredients', "avg_rating",  "calories": By drawing scatter plots, we can observed that there is a non-linear relationship between minutes and each of the features described above. Furthermore, a linear relationship is only apparent in a small subsection of the plot. Hence, it is reasonable to standardize each features based on their distribution

>> polynomial_features on "n_steps", "n_ingredients", "avg_rating",  "calories", "rank": To better capture the nonlinear relationship described in the bullet point above, I created polynomial features for a subset of my features to increase my model complexity

> Final Model Selection: For hyperparameter search, I perform a grid search on the degree of polynomial features range from 2 to 4 for the multivariate regression model described previously

> Final model performance:
> - rmse_train:   79.51494012568425 
> - rmse_test:  80.96413993528031
>> - Small improvement over the baseline model on the test set (rmse for the training set and test set have both decreased)


---

## Fairness Analysis

> Group X: Recipe of Rank 4

> Group Y: Recipe of Rank 5

> Evaluation Metric: Root Mean Square Error

> Null Hypothesis: Our model is fair between recipe of rank 4 and rank 5. (i.e. The RMSE for Rank 4 recipe is the same as for Rank 5 recipe.)

> Alternative Hypothesis: Our model is unfair. (i.e. The RMSE for Rank 4 recipe is greater than that of Rank 5 recipe)

> Test Statistic: Signed difference between the RMSE of the Rank 4 recipe and the RMSE of the Rank 5 recipe

> Significance level: 0.05 

> Resulting p-value: 0.00

> Conclusion: Reject the null 
