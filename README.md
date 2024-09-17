#Telecom Churn Case Study


____________________________________________________________________________________________________________________________________________________________________________________
Problem Statement

Business Problem Overview 

In the telecom industry, customers are able to choose from multiple service providers and actively switch from one operator to another. In this highly competitive market, the telecommunications industry experiences an average of 15-25% annual churn rate. Given the fact that it costs 5-10 times more to acquire a new customer than to retain an existing one, customer retention has now become even more important than customer acquisition.

For many incumbent operators, retaining high profitable customers is the number one business goal.

To reduce customer churn, telecom companies need to predict which customers are at high risk of churn.

In this project, we will analyse customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn and identify the main indicators of churn.
____________________________________________________________________________________________________________________________________________________________________________________

Understanding and Defining Churn

There are two main models of payment in the telecom industry - postpaid (customers pay a monthly/annual bill after using the services) and prepaid (customers pay/recharge with a certain amount in advance and then use the services).

In the postpaid model, when customers want to switch to another operator, they usually inform the existing operator to terminate the services, and we directly know that this is an instance of churn.

However, in the prepaid model, customers who want to switch to another network can simply stop using the services without any notice, and it is hard to know whether someone has actually churned or is simply not using the services temporarily (e.g. someone may be on a trip abroad for a month or two and then intend to resume using the services again).

Thus, churn prediction is usually more critical (and non-trivial) for prepaid customers, and the term ‘churn’ should be defined carefully. Also, prepaid is the most common model in India and southeast Asia, while postpaid is more common in Europe in North America.

This project is based on the Indian and Southeast Asian market.
___________________________________________________________________________________________________________________________________________________________________________________

Definitions of Churn

There are various ways to define churn, such as:

Revenue-based churn: Customers who have not utilised any revenue-generating facilities such as mobile internet, outgoing calls, SMS etc. over a given period of time. One could also use aggregate metrics such as ‘customers who have generated less than INR 4 per month in total/average/median revenue’.

The main shortcoming of this definition is that there are customers who only receive calls/SMSes from their wage-earning counterparts, i.e. they don’t generate revenue but use the services. For example, many users in rural areas only receive calls from their wage-earning siblings in urban areas.

Usage-based churn: Customers who have not done any usage, either incoming or outgoing - in terms of calls, internet etc. over a period of time.

A potential shortcoming of this definition is that when the customer has stopped using the services for a while, it may be too late to take any corrective actions to retain them. For e.g., if we define churn based on a ‘two-months zero usage’ period, predicting churn could be useless since by that time the customer would have already switched to another operator.

In this project, we will use the usage-based definition to define churn.
___________________________________________________________________________________________________________________________________________________________________________________

High-value Churn

In the Indian and the southeast Asian market, approximately 80% of revenue comes from the top 20% customers (called high-value customers). Thus, if we can reduce churn of the high-value customers, we will be able to reduce significant revenue leakage.

In this project, we will define high-value customers based on a certain metric (mentioned later below) and predict churn only on high-value customers.
___________________________________________________________________________________________________________________________________________________________________________________

Understanding the Business Objective and the Data

Overview of the Dataset

The dataset includes customer data spanning four consecutive months: June, July, August, and September, denoted as 6, 7, 8, and 9, respectively.

The goal is to predict whether a customer will churn in September based on their data from the first three months (June, July, and August). To achieve this, it's crucial to understand typical customer behaviors leading up to churn.
___________________________________________________________________________________________________________________________________________________________________________________

Customer Behavior During Churn

Customer churn does not usually happen abruptly. Instead, it occurs over a period, particularly for high-value customers. We categorize the customer lifecycle into three distinct phases:

The ‘Good’ Phase: During this time, the customer is satisfied with the service and shows typical behavior.
The ‘Action’ Phase: Customer dissatisfaction begins here. This could be due to receiving a competitive offer, facing unjust charges, or being unhappy with service quality. Customers in this phase exhibit different behaviors from those in the ‘Good’ phase. Identifying high-risk churn customers at this stage is crucial, as corrective measures can be applied (e.g., offering a counter-promotion or improving service).
The ‘Churn’ Phase: At this stage, the customer is considered to have churned. Churn is defined based on this phase. During prediction, data from this phase is not available, so once churn is tagged, all related data is discarded.
For this dataset, the phases are defined as follows:

June and July are the ‘Good’ phase.
August is the ‘Action’ phase.
September is the ‘Churn’ phase.
___________________________________________________________________________________________________________________________________________________________________________________

Dataset and Data Dictionary

You can download the dataset [here](https://drive.google.com/file/d/1SWnADIda31mVFevFcfkGtcgBHTKKI94J/view).

The data dictionary, available for download, explains abbreviations used in the dataset. Common abbreviations include:

loc (local)
IC (incoming)
OG (outgoing)
T2T (telecom operator to telecom operator)
T2O (telecom operator to another operator)
RECH (recharge)
Attributes with suffixes 6, 7, 8, and 9 correspond to the months June, July, August, and September, respectively.
___________________________________________________________________________________________________________________________________________________________________________________

Data Preparation

Feature Engineering
Creating new features is crucial as they can significantly impact model performance. Use your understanding of the business to derive features that might be strong indicators of churn.

Filtering High-Value Customers
Focus on high-value customers for churn prediction. Define them as customers who have recharged an amount greater than or equal to X, where X is the 70th percentile of average recharge amounts from June and July. This should result in around 30,000 rows.

Tagging Churners and Removing Churn Phase Data
Tag customers as churned (churn=1) if they have neither made calls (incoming or outgoing) nor used mobile internet during September. Relevant attributes for tagging are:

total_ic_mou_9
total_og_mou_9
vol_2g_mb_9
vol_3g_mb_9
After tagging, remove all attributes related to September (with _9 suffix).
___________________________________________________________________________________________________________________________________________________________________________________

Modelling

Build models to predict churn with the following objectives:

Predicting Churn: Develop a model to forecast whether high-value customers will churn. This will help the company take proactive measures like offering special plans or discounts.
Identifying Important Predictors: Determine key variables that are strong indicators of churn. These variables can reveal why customers might switch to other networks.
To address the class imbalance (churn rates are low, around 5-10%), consider techniques to manage this imbalance. Use dimensionality reduction methods such as PCA before applying classification models. After PCA, you can use any classification algorithm.

Suggested Steps for Modelling
Preprocess Data: Convert columns to appropriate formats, handle missing values, etc.
Exploratory Analysis: Analyze the data to extract useful insights for business and modeling.
Feature Engineering: Derive new features.
Dimensionality Reduction: Use PCA to reduce the number of variables.
Model Training: Train various models, tune hyperparameters, and address class imbalance.
Model Evaluation: Use metrics that focus on identifying churners rather than non-churners, given the business importance.
Since the PCA-based model won't be able to identify important features directly, build an additional model (e.g., logistic regression or a tree-based model) to highlight significant predictors. Ensure to handle multicollinearity if using logistic regression.

After identifying key predictors, present them visually using plots or summary tables.

Finally, based on your findings, suggest strategies to manage and reduce customer churn.
___________________________________________________________________________________________________________________________________________________________________________________







