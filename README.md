			
    REPORT ON A PETROPHYSICAL (SPWLA-PDDA) MACHINE LEARNING COMPETITION 2020
 
    

    Problem Statement

Compressional travel-time (DTC) and shear travel-time (DTS) logs are not acquired in all the wells drilled in a field due to financial or operational constraints. Under such circumstances, machine learning techniques can be used to predict DTC and DTS logs to improve subsurface characterization. The goal of the “SPWLA’s 1st Petrophysical Data-Driven Analytics Contest” is to develop data-driven models by processing “easy-to-acquire” conventional logs from Well #1, and use the data-driven models to generate synthetic compressional and shear travel-time logs (DTC and DTS, respectively) in Well #2. A robust data-driven model for the desired sonic-log synthesis will result in low prediction errors, which can be quantified in terms of Root Mean Squared Error by comparing the synthesized and the original DTC and DTS logs.

You are provided with two datasets: train.csv and test.csv. You need to build a generalizable data-driven models using train dataset. Following that, you will deploy the newly developed data-driven models on test dataset to predict DTS and DTC logs. The data-driven model should use feature sets derived from the following 7 logs: Caliper, Neutron, Gamma Ray, Deep Resistivity, Medium Resistivity, Photo-electric factor and density. The data-driven model should synthesize two target logs: DTC and DTS logs.

The predicted values should be in the same format as sample_submission.csv, and submit together with your notebook for evaluation.

     Data Decription
Files
> #### train.csv All the values equals to -999 are marked as missing values.

CAL - Caliper, unit in Inch,
CNC - Neutron, unit in dec
GR - Gamma Ray, unit in API
HRD - Deep Resisitivity, unit in Ohm per meter,
HRM - Medium Resistivity, unit in Ohm per meter,
PE - Photo-electric Factor, unit in Barn,
ZDEN - Density, unit in Gram per cubit meter,
DTC - Compressional Travel-time, unit in nanosecond per foot,
DTS - Shear Travel-time, unit in nanosecond per foot,
> #### test.csv The test data has all features that you used in the train dataset, except the two sonic curves DTC and DTS.

> #### sample_submission.csv A valid sample submission.

     Evaluation Metric
We will be evaluated by the metirc Root Mean Squared Error.

The RMSE is calculated as:

$ ϵ=∑_i \sqrt{ ∑_n (y_p - y_t)^2 /n } $

Where:

y_p is the predicted curve for DTC and DTS
y_t is the true value for evaluation.
DTC and DTS are in the same weight during the evaluation

Understanding and optimizing the predictions for this evaluation metric was paramount for this compeition.

  
    Our solution in this competition earned us a final RMSE score of 16.412 on the final test data as shown on the leaderboard. 

After trying a lot of techniques our approach was, first we created a notebook where we tested the performance on various machine learning techniques or algorithms on the dataset. We discovered that gradient boosting techniques like LGBM, XG-BOOST etc including CATBOOST performs extremely well in predicting the target variables.

Our Final solution was a blend of two different models in predicting the two different target variables DTC and DTS. 
We used the Catboost Regressor technique in Predicting DTC with no major feature engineering applied than dropping all null values in the dataset and we used a n-fold split of 20 for training the model.
For DTS, we used LGBM regressor coupled with a Grid-Search CV for hyper-parameter tuning. The feature engineering performed here involved dealing with outliers which involve replacing the outliers with values that satisfies various conditions for each feature being considered in the train set and test-set. We also created other features through various mathematical estimations and based on our findings from research on the subject topic
For training the LGBM, we eventually used all the original features of the train-set and just one feature engineered variable in building our model for DTS prediction.

We stored the final predictions of these two models on the test data which was used for our second submission that gave an RMSE of 16.412 on the leaderboard. 

We thank SPWLA for the opportunity given to us to participate in this competition as it was indeed a great experience filled with lots of learning and fun for us.

Team Members – Ntongha Ibiang - ntongha1@gmail.com 
		       Onaneye Temilola – onaneyetemilola@gmail.com 
           
Sponsors (SPWLA-PDDA ,  SparkCognition)

