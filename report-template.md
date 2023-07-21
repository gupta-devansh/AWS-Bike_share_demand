# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Devansh Gupta

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
while submitting the predictions we need to take care of the negative value predictions as kaggle does not allow negative values for predictions. for negative values, we can set them to 0.

### What was the top ranked model that performed?
the top ranked model was WeightedEnsemble_L3 with rmse = 53.106404

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
upon doing exploratory analysis we found out that faetures like seasons,weather,holiday,workingday were used as integer, when they really are categorical data type,apart from that we can see the information in the datetime column from which we extract multiple features such as day,month, hour.
Also there were two columns : registered and casual ,which were not present in test dataset therefore they needed to be dropped before training.

### How much better did your model preform after adding additional features and why do you think that is?
the kaggle score before adding the new featues was: 1.79190 . After adding the new features{extracted from datetime: day,month,hour} the kaggle score improved significantly to : 0.65234 .This addition of features with changing datatype of some columns{weather,seasons} as categorical allowed model to look for seasonal/time dependencies of the demand,which then improved the model performance.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
the kaggle score before tuning the hyperparameters was : 0.65234 andd after tuning the hyperparameters the kaggle score improved slightly to : 0.53304.
most parameters were kept as default,with more time we could definitely look into chosing which and how to tune the hyperparameters which woulf further improve the kaggle score.

### If you were given more time with this dataset, where do you think you would spend more time?
I think i would spend more time on two things:
1.) extensive EDA: i would like to understand the data better by plotting charts,etc. would try to tackle outliers, maybe perform PCA.
2.) better hypertuning the autogluon , as there are many hyperparameters, I would spend time to look for the parameters which improves the model the most.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|default|default|default|1.79190|
|add_features|default|default|default|.65234|
|hpo|GBM:{extra_trees: True,num_boost_round: 250,num_leaves: 37,ag_args: {name_suffix: XT}}, {}, GBMLarge|{'CAT': {'iterations': 9000}}|{'RF':{'n_estimators': 250},'XT': {'n_estimators': 250}}|0.533004|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](D:\AIML\udacity\bike_share\model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](D:\AIML\udacity\bike_share\model_test_score.png)

## Summary
during this project I performed the following steps:
studied the AutoGluon AutoML framework for Tabular Data and used it in bike sharing demand prediction project.
the model performance was improved by doing some EDA and feature engineering without tuning the hyperparameters.
then after tuning some of the hyperparameters we could see some improvements in the model score on the raw initial score as well as the score produced after the previous step.
Given more time we can look into the hyperparameters of autogluon more deeply and also spend some more time during the EDA phase of the ML lifecylce.
