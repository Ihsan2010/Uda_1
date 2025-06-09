# Report: Predict Bike Sharing Demand with AutoGluon Solution
In this project, we predicted the bike sharing demand based on the features such us the date and time, the temperature, the humidity, and the windspeed.     
We worked in local Jupyer Notebook environment in VS Code and used AutoGluon. We experimented three models, which were submitted to Kaggle for evaluation.

> **Report date : June, 2025**     
> **Written by : [Md Amimul Ihsan](https://www.linkedin.com/in/amimul-ihsan-zami010763/)**



## Initial Training
When the predictions were submitted to kaggle, they were rejected each time they contain negative value. So we needed to check negative value, and replace them with zero.


### What was the top ranked model that performed?
The top ranked model was the first one: it was trained using the default parameters of AutoGluon and got a score of `1.80121` from Kaggle for `WeightedEnsemble_L3`.


## Exploratory data analysis and feature creation
EDA showed us the distribution of the numerical features, which allowed us to spot the skew in `windspeed, registered, casual and count`. 
Another action we did take is to engineer new features (`year, month, day, hour`) based on the feature `datetime`, in order to try improving our model results.


### How much better did your model preform after adding additional features and why do you think that is?
After introducing our new features (year, month, day, hour) and removing the original datetime column—since its information is now captured by the engineered features—we observed a drop in the Kaggle score to `0.5365` for `WeightedEnsemble_L2` using autgluon, compared to `1.80121` when using the datetime column directly. It's worth noting that the datetime column was of type datetime. This suggests that AutoGluon is capable of automatically preprocessing and extracting valuable features from datetime columns in various ways, selecting the most effective transformations to optimize model performance.


## Hyper parameter tuning
After tuning the model hyper-parameters, the models performance dropped to `1.3044` for `WeightedEnsemble_L3` with autoglion from `1.80121` when we left the hyper-parameters untouched.


### If given more time with this dataset, where would we spend more time?
If given more time, I will spend more time on the first model, the baseline one (its hyper-parameters were not tuned, and `datetime` features were not engineered in the data fed to it).
That choice is based on the fact that clearly, AutoGluon is very good at predicting well on our dataset without our intervention, so we should give it more time to train (for e.g., doubling the training duration and observing the results).

### Create a table with the models we ran, the hyperparameters modified, and the kaggle score.
|model|timelimit (seconds)|presets|others|score|
|--|--|--|--|--|
|initial|10x60|best_quality|-|1.80121|
|add_features|10x60|best_quality|-|0.5365|
|hpo|12x60|best_quality|nn:activation -- dropout_prob; gmb:num_boost_round -- num_leaves; scheduler; searcher|1.3044|

### Create a line plot showing the top model score for the three (or more) training runs during the project.
![model_train_score.png](F:\Udu\New\model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.
![model_test_score.png](F:\Udu\New\model_test_score.png)

## Summary
Three models were developed and evaluated:

Model 1: Baseline Model
Used as the reference point for comparison

Trained for 600 seconds with best_quality presets

Evaluation R²: 0.8852290511131287

Evaluation Pearson correlation: 0.8852290511131287

Kaggle Score: 1.80121

Model 2: Feature-Engineered Version of Model 1
Built by updating the data used in Model 1

Performed feature engineering on the datetime column, extracting new features: year, month, day, and hour

Categorical type was explicitly set for: season, workingday, and weather

Trained for 600 seconds with best_quality presets

Evaluation R²: 0.9629054069519043

Evaluation Pearson correlation:0.9812943816620183

Kaggle Score: 0.5365

Model 3: Extended Version of Model 1
Retained the original dataset (with the unmodified datetime column)

Trained on more data than Model 1

Trained for 720 seconds with best_quality presets

Evaluation R²:  0.6282198429107666

Evaluation Pearson correlation: 0.8038187102583518

Kaggle Score: 1.3044

