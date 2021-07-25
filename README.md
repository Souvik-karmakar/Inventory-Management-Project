# Inventory-Management-Project(Backorder Prediction)
For Dataset Click the provided link below:-
https://drive.google.com/file/d/1Z-vEb91E9zVkqlb3N5COJvM_T-pSALyS/view?usp=sharing


1. Introduction :
A Backorder is an order which can’t be fulfilled at the given time due to lack of supply or the product is currently out of stock or not in inventory but can guarantee delivery of the goods or service requested by a certain date in the future because the production of goods  is underway. Unlike in the situation of Out-of-stock where the delivery date of the goods can’t be promised , in the Backorder scenario the customers are allowed to shop for the products and order. Simply put Backorder can be thought of as an order with a delayed delivery date.

2. Why do Backorders happen ?
When there is a sudden increase in demand 
Poor Supply chain Management
Improper Inventory Management

3.Effects of Backorders:
If many items are going on Backorders consistently it is a sign that companies operations are not properly planned and also there is a very high chance of missing out business on the products.
Also if the customers frequently experience Backorders they switch their loyalities to your competitors.
Backorders(unpredicted) also affect the production planning, Transportation management and logistics management etc.


4.What to do to avoid Backorders ?
Increasing inventory or stock of produts is not a solution as it increases storage costs and extra costs means they have to be included in the product prices which might result in losing business to competitors.
A well planned Suppply Chain Management , Warehouse management and inventory management can avoid Backorders to some extent.
5.Need for Having Backorder prediction system:
Backorders are inevitable but through prediction of the items which may go on backorder planning can be optimized at different levels avoiding un expected burden on production , logistics and transportation planning.
ERP systems produce a lot of data (mostly structured) and also would have a lot of historical data , if this data can be leveraged correctly a Predictive model can be developed to forecast the Backorders and plan accordingly.

Problem Statement :
Classify the products whether they would go into Backorder(Yes or No) based on the historical data from inventory, supply chain and sales.


Task:
The task at hand is classifying whether a product would go to Backorder given input data.
The target variable to predict consists of two values:
“Yes” - If the Product predicted to go to Backorder
“No”- If the Product predicted to be not going to Backorder

Dataset Analysis :
In the Train dataset we are provided with 23 columns(Features) of data.
Sku(Stock Keeping unit) : The product id — Unique for each row so can be ignored
National_inv : The present inventory level of the product
Lead_time : Transit time of the product(it is the amount of time spent when moving goods from one point to another)
In_transit_qty : The amount of product in transit
Forecast_3_month , Forecast_6_month , Forecast_9_month : Forecast of the sales of the product for coming 3 , 6 and 9 months respectively
Sales_1_month , sales_3_month ,sales_6_month , sales_9_month : Actual sales of the product in last 1 , 3 ,6 and 9 months respectively
Min_bank : Minimum amount of stock recommended
Potential_issue : Any problem identified in the product/part
Pieces_past_due: Amount of parts of the product overdue if any
Perf_6_month_avg , perf_12_month_avg : Product performance over past 6 and 12 months respectively
Local_bo_qty : Amount of stock overdue
Deck_risk , oe_constraint, ppap_risk, stop_auto_buy, rev_stop : Different Flags (Yes or No) set for the product
Went_on_backorder : Target variable

UNDERSTANDING(Data Description)
The class ratio of Products that went to Backorder(‘Yes’) to those which didn’t go to Backorder(‘No’) is 1:148.
The dataset is highly imbalaced which should be addressed for accurate predictions by the model.
Out of the 23 features given in the dataset 15 are numerical and 8(including the target variable) are categorical features. The first column ‘sku’ corresponds to product identifier which is unique for each datapoint in the dataset. So this feature can be dropped as it adds no value in output prediction.
There are in total 1687861 datapoints and 23 features in the dataset
Out of the 23 features 22 are indpendent features and 1 is dependent feature ( Target variable)
The target variable column name is "went_on_backorder"
The last row of the dataset consists of NaN values for all features.
Dataset has 15 columns of data type float and 8 coumns are string ( including target variable)
Only the column lead_time has a few null values.
It seems the firt column sku consists of productids , if all of them are unique then this column can be dropped.

PREPROCESSING
Remove Null/Duplicate Rows
Remove sku (all unique values)
Impute NAs in lead_time to mean
Normalize the quantity columns
Convert categorical binary attributes to numeric attributes (Yes/No to 1/0)
Drop unused levels (When creating a subset of a dataframe
Remove the SKUs for which forecast and sales are 0 and the target class “Went to Back order is also “No” . Remaining No of records = 1015940


Feature Selection
Features were selected by applying domain knowledge of Supply chain
Forecasts and Sales were analyzed for 3, 6 and 9 months data
We can see that the relationship between the variables are linear
We also observed that the backorders happen only when the value of sales and forecast is very low
Linear relation was observed between sales and forecast data
Due to the good correlations and sufficiently linear relationships between these features we concluded that sales_1_month can represent all forecast and sales data

Approach to handle Imbalanced Data (only 0.7% went on backorder)
Oversampling
Minority class is randomly replicated.
Increases the overall size of the data
Under Sampling
Randomly eliminating the majority class
This method help improve run time and the storage problems by reducing the sample size
There can be loss of potentially useful information which could be important 
SMOTE (Synthetic Minority Over-sampling Technique)
Used to avoid overfitting which can occur when replicating the minority class
SMOTE is an oversampling technique where the synthetic samples are generated for the minority class. This algorithm helps to overcome the overfitting problem posed by random oversampling.
it is found not effective for high dimensional data.
SMOTE works by selecting examples that are close in the feature space, drawing a line between the examples in the feature space and drawing a new sample at a point along that line.

Algorithm Selection - Random Forest
Random Forest is based on the bagging algorithm and uses Ensemble Learning technique. It creates as many trees on the subset of the data and combines the output of all the trees. In this way it reduces overfitting problem in decision trees and also reduces the variance and therefore improves the accuracy.
Random Forest can automatically handle missing values.
Robust to outliers and missing values
Perform well with large dimensional datasets
Can handle thousands of input variables without variable deletion.
 Gives estimates of what variables are important in the classification
 We compared the model by varying number of leaves and the minimum support.

K-fold Cross Validation(Resampling procedure)
The original data is randomly partitioned into k equal sized subsamples.
A single subsample is used as the validation data for testing the model, and the remaining k-1 subsamples are used as the training data.
The advantage of K-Fold Cross validation is that all the observations in the dataset are eventually used for both training and testing
Reduces bias as we are using most of the data for fitting, and also significantly reduces variance as most of the data is also being used in validation set



