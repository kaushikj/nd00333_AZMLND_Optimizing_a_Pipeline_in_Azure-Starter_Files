# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Useful Resources
- [ScriptRunConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.scriptrunconfig?view=azure-ml-py)
- [Configure and submit training runs](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-set-up-training-targets)
- [HyperDriveConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.hyperdrive.hyperdriveconfig?view=azure-ml-py)
- [How to tune hyperparamters](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters)

## Summary
This dataset includes individual marketing information.The information relates to telephone-based direct marketing activities of a Portuguese banking institution. The goal of the model is categorising if a customer withh sign up or not. 

The Experiment configuration is set to maximize the accuracy as primary metric. Train test split for both models id 80-20. The autoML model uses cross validation with n =2.


The best performing model was the HyperDrive model with ID. It derived from a Scikit-learn pipeline and had an accuracy of 0.92. In contrast, for the AutoML model with ID, the accuracy was 0.916.

## Dataset
This dataset contains data about individuals applying for bank loans. The task we set out to accomplish here is to develop a model that, based on the information provided about each individual, predicts whether they will subscribe to a service.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**



-

- Evaluation interval: This represents how frequently the policy will be applied and is optional.
One interval is equal to each time the training script logs the primary metric. 

- Slack Factor: This represents how frequently the policy will be applied and is optional.
One interval is equal to each time the training script logs the primary metric. 

**What are the benefits of the parameter sampler you chose?**
 RandomParameterSampling: I selected because it is faster and allows for the early termination of low-performance runs. If money is not a concern, we might utilize BayesianParameterSampling to investigate the hyperparameter space or GridParameterSampling to thoroughly search the search space. 
**What are the benefits of the early stopping policy you chose?**
- Early stopping policy: By automatically terminating underperforming runs, an early stopping policy increases computational efficiency.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**
voting ensemble model with StandardScalerWrapper
Its an ensemble of ['XGBoostClassifier', 'XGBoostClassifier', 'XGBoostClassifier', 'XGBoostClassifier', 'LightGBM', 'LogisticRegression', 'SGD']
Badically ensemble algorithm is a voting based prediction based on prediction of individual models. The weights used here are [0.125, 0.125, 0.125, 0.25, 0.125, 0.125, 0.125].

StandardScalerWrapper Standardizes features by removing the mean and scaling to unit variance. The standard score of a sample x is calculated as: z = (x - u) / s.



## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**
HyperDrive Model
Accuracy 0.92

AutoML model
Accuracy 0.916

The final model would undoubtedly be much better if we had more time to run the AutoML.
The nice part is that AutoML would perform all required computations, trainings, validations, etc. without our involvement.
This is in contrast to the Scikit-learn Logistic Regression pipeline, where we are required to make all modifications, changes, etc. on our own and arrive at a final model through a process of numerous trials and errors. 



## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

Our data is highly imbalenced which is a very common issue in classification. accuracy is a poor representation of the performance of the model. We could look into precision, recall or AUC.

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**

clustercc.png
