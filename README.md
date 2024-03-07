# ProjectTitle: BCG-DATA-SCIENCE-VIRTUAL-INTERNSHIP---CHURN-BUSTER-PREDICTIVE-MODELING-TO-CUSTOMER-RETENTION

Dataset link:https://www.theforage.com/virtual-experience/Tcz8gTtprzAS4xSoK/bcg/data-science-ccdz/business-understanding-hypothesis-framing

*************************************************************************************************************************************

## OBJECTIVE:
  The objectives of the BCG  Virtual Experience Program:

      1. Analyze provided data to understand customer behavior and patterns. And address data quality issues and engineer relevant features for analysis.

      2. Develop machine learning models to predict customer churn. Evaluate and fine-tune models for accuracy and effectiveness.

      3. Interpret model results to identify key factors influencing churn. Extract actionable insights to inform customer retention strategies.

## VARIABLES:

**client_data.csv**

* id = client company identifier
* activity_new = category of the company’s activity channel_sales = code of the sales channelcons_12m = electricity consumption of the past 12 months
* cons_gas_12m = gas consumption of the past 12 months
* cons_last_month = electricity consumption of the last month 
* date_activ = date of activation of the contract
* date_end = registered date of the end of the contract 
* date_modif_prod = date of the last modification of the product
* date_renewal = date of the next contract renewal 
* forecast_cons_12m = forecasted electricity consumption for next 12 months
* forecast_cons_year = forecasted electricity consumption for the next calendar year 
* forecast_discount_energy = forecasted value of current discount
* forecast_meter_rent_12m = forecasted bill of meter rental for the next 2 months * forecast_price_energy_off_peak = forecasted energy price for 1st period (off peak)
* forecast_price_energy_peak = forecasted energy price for 2nd period (peak) 
* forecast_price_pow_off_peak = forecasted power price for 1st period (off peak)
* has_gas = indicated if client is also a gas client imp_cons = current paid consumption
* margin_gross_pow_ele = gross margin on power subscription 
* margin_net_pow_ele = net margin on power subscription
* nb_prod_act = number of active products and services 
* net_margin = total net marginnum_years_antig = antiquity of the client (in number of years) 
* origin_up = code of the electricity campaign the customer first subscribed.
* pow_max = subscribed power *churn = has the client churned over the next 3 months


**price_data.csv**

* id = client company identifier
* price_date = reference date
* price_off_peak_var = price of energy for the 1st period (off peak)
* price_peak_var = price of energy for the 2nd period (peak)
* price_mid_peak_var = price of energy for the 3rd period (mid peak)
* price_off_peak_fix = price of power for the 1st period (off peak)
* price_peak_fix = price of power for the 2nd period (peak)
* price_mid_peak_fix = price of power for the 3rd period (mid peak)

## LIBRARIES USED:

   - Pandas, Matplotlib, Seaborn, Scikit-learn, datetime, Tensorflow, Numpy, Keras.


## TABLE OF CONTENTS:

- [Introduction](#introduction)
- [Data Preprocessing](#data-preprocessing)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Feature Engineering](#Feature-Engineering)
- [Model Building](#Model-Building)
- [Model Evaluation Metircs](#Model-Evaluation-Metircs)
- [Insights](#insights)
      
## Introduction:

  In today's competitive business landscape, retaining customers is paramount for sustained growth and profitability. Customer churn, or the loss of customers over a given period, poses a significant challenge for companies across various industries. To address this challenge, businesses must proactively identify at-risk customers and implement targeted retention strategies. Leveraging predictive modeling techniques and advanced analytics, this project seeks to uncover underlying patterns and factors contributing to churn, enabling businesses to implement proactive measures to retain customers.

## Data Preprocessing:

   In this part, I have inquired about the data quality such as missing values with missing values plot for all the features, inconsistent column and names, infered the proper format for datetime and inquired about the duplicated rows in the dataset. Also did descriptive statistics for both categorical and numerical features. Also analyzed the tails and shape of distributions of data using kurtosis and skewness.

## Data Visualization:
   
   For Data visualization part,

   * Barplots for Churners and non Churners - Sales channel_sales, Contract_type, Gender, nb_prod_act, origin_up, num_years_antig.

   * Boxplots for all  numerical features to asses the outliers or anomalies in the dataset notablly for cons_gas_12m, cons_last_month with has_gas features

   * Histograms and KDE plots for the numerical features to asses the spread or the distributions of the dataset which includes cons_gas_12m, cons_last_month,imp_cons, con_12m and others 
 
   * Aso did Correlation matrix for all the features to know about its relationships.

## Price Sensitivity Analysis:

PRICE SENSITIVITY or PRICE ELASTICITY:

* A simple measure in which calculates how much the change in price of goods and services affect the willigness to buy the particular product or brand.

* Price sensitivity,Ps= (% change in Quantity demand)/(% change in price of the brand or product )

      * If Ps > 1: Demand is elastic (price-sensitive).
      * If Ps = 1: Demand is unitary elastic.
      * If 0 < Ps < 1: Demand is inelastic (less price-sensitive).
      * If Ps = 0: Demand is perfectly inelastic (not price-sensitive).


# Feature Engineering:

 Tried to create  lot of new features to capture the variations by Peak features offered from the Price.csv file  based on id's, Max price for id based on entire period by months and Minimum price  also simultaneously. Some other features are No of days of subscription , lead time to renewal and etc...

 Then from the insights obtained from the EDA most of the features were not in normal. So in order to  convert the features to normal, I have utilized the One of the Power Transformation technique from sklearn library called Yeo-Johnson method.

 Before entering into Feature Engineering part, data must be cleaned from the outliers. For outliers cleansing, I have used the Z-score method.
    
 After these transformation and cleaning of data, compared the visualizations boxplot and Histogram with KDEplot for  before and after transformation changes.

 Converted the categorical features to numerical coding using LabelEncoders and other few categorical variables for One-Hot Encoding techniques.

 Due to Class Imbalance in Churners and Non-Churners, Ml models cannot be able to generalize and capture the patterns of customer behaviors. So inorder to balance the class, I used the SMOTE(Synthetic Minority Over Sampling technique) from imblearn library of python. Created the artifical Synthetic points to balance the imblance problem only in the Train dataset. It should not be imposed on Test dataset. 

For Independent features tried to know about the which are the features are more import using Mututal Information technique for Classification for features.

## Model Building

* For Train-test split done. Size of test is 20% percent of data with shuffled ones.

* To build a Ml model with well optimal model to generalize the unseen data K Fold Cross validation. 

* BEST MODELS INTERMS OF F1 SCORES PERFORMANCES:

   * Neural Network-logistic Regression Model
   * Categorical Boost Classifier
   * XGBoost Classifier
   * GradientBoost Classifier
   * KNeighbors Classifier

## Model Evaluation Metircs

   * F1 Score
   * Precision
   * Recall
   * Accuracy

## Insights

* Most of the features are right skewed and followed by heavly tailed distributions.
* Dataset contains more number of outliers
* People who dont own the Gas contract Churned a lot when compared to the people who own the Gas contract.
* Forecasted value of current discount for the pople own Gas contract have the much less churn rate.
* comparison between the owning the Gas contract: 

      @ People who does not own the contract will be retained around 82% and who own the contract likely to be retained 18%

      @ People who does not own the contract will be churned around 85% and who own the contract likely to be churned 15%.

* Around 10% people are like to be churned and 90% will be retained.

* Number of active products and services only the products 1,2,3,4 and 5 contains the people with churned behaviour and other products have 100% retention rate.

* People with 1 year of subscription have 100% retention rate. similar for the people who with 9 years of subcription. Higher churning rate with the people with 2 years of subscription. Some attention needed here to address this issue.

* price sensitive analysis using correlation method churning is likely to be have weak relationship with the price sensitivity. And Higher inter correlation found between the price sensitivity features
