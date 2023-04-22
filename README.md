# SC1015 Mini_Project
School of Computer Science and Engineering  
Introduction to Data Science and AI  
Lab A125  
Group: 7  

**Members:**
   1. Lee Jia Xin Mildred
   2. Jace Seow Wen Hui
   3. Janice Koh Swee En
#
### Description:

This repository includes the necessary code and documents to run our Mini-Project, we have used the following softwares to program our project: Jupyter Notebook and Deepnote. 

#
### Table of Contents:
   1. [Purpose of our Project](#1-project-purpose)
   2. [Preparation of Dataset](#2-preparation-of-dataset)
   3. [Exploration of Dataset](#3-exploration-of-dataset)
   4. [Machine Learning](#4-machine-learning)
   5. [Conclusion](#5-conclusion)
   6. [Recommendations for Enhancements](#6-recommendations-for-enhancements)
   7. [Members Contribution](#7-members-contribution)
   8. [Reference List](#8-reference-list)
#
### 1. Project Purpose
It isn't uncommon for people of any age to start investing these days. However, the stock market trend is unpredictable and doesn't increase every year, resulting in many investors losing hundreds or thousands of dollars. This level of volatility may seem intimidating especially for those who just started investing, which is why we came up with this project to give people a better understanding of how the stock market might work.


With the use of Data Science and Machine Learning, we hope to: 
   1. Achieve a better understanding of the stock market
   2. Give a visualisation of the past year's stock market trend 
   3. Decrease the uncertainty of trends by using machine learning

This project is for **only** for research purposes, therefore it's advisable for users to not only rely on this project to predict the stock market trend.
#
### 2. Preparation of Dataset
For this Project, we have chosen to work with 2 Datasets: Google Stocks from Yahoo Finance, and Reuter Headlines. In this section, we will clean and prepare the dataset to have a better understanding of our data.     


**Preparation of Google Stocks from Yahoo Fiance:**  
   DataFrame Name: SP
   1. **Date Splitting:** Data extracted from 01/06/2018 to 01/06/2019
   2. **Data Cleanup:** Remove all NaN values. Used **Hodrick-Prescott** filter to remove Seasonality and Trend
   3. **Detrend:** Detrended values added to the DataFrame     
    
    
**Preparation of Reuter Headlines:**     
   DataFrame Name: sp_copy
   1. **Date Splitting:** Data extracted from 01/06/2018 to 01/06/2019
   2. **Data Cleanup:** Remove the Description Column and NaN values. Remove all weekends and Public Holidays. Remove all symbols from headlines
   3. **Individual headline:** Grouped any headlines that falls on the same day  
   4. Calculate **Subjectivity, Polarity** for each headline
   5. Using Sentiment Intensity Analyzer, we were able to get the Positive, Negative, Neutral, Compound values for each headline
    
 
**Combination of both Google Stocks and Reuter Headlines:**    
   DataFrame Name: df_merge
   1. **Data Merge:** Combined the Google Stocks and Headlines according to their dates  
    
#
### 3. Exploration of Dataset
In this section, we will delve deeper into the dataset and find which and how some variables would affect the seasonality and trend.


**Exploration of both Google Stocks and Reuter Headlines:**  
   DataFrame Name: sp_copy
   1. Analyzed the relationship between the Subjectivity, Positive, Negative, Compound, and Polarity with Adjective Close and Detrended Adjective Close:   
       - a. Subjectivity has the strongest relationship with Detrended Adjective Close  
       - b. Positive has the strongest relationship with Adjective Close  
   
   
Therefore, we'll be using the variables: Subjectivity for Machine Learning
#
### 4. Machine Learning
In this section, we have experimented with 7 machine learning algorithms to test which algorithm best fits our purposes.  


**Sarimax**  
The Sarimax model is a conventional model based on statistics that are often used to predict the stock market. This is because stock market prices are not static and would often vary over time which Sarimax is able to predict, it is basically an improved version of Arima but with seasonality and exogenous factors. Generally, 
SARIMAX is used on data sets that have seasonal cycles.

    1.	Defined an ARIMA model and fit it into the training set
    2.	Plot autocorrelation of residuals to check the randomness in the dataset
    3.	Training set -> Subjectivity variable
    4.	Test set -> Detrended Adj close price
    RMSE: 0.22  
    
    

**Random Tree Forest**  

Random forest is a supervised classification machine learning algorithm that uses ensemble method. Basically, it is a random forest made up of numerous decision trees and helps to tackle the problem of overfitting in decision trees. These decision trees are randomly constructed by selecting random features from the given dataset.  


Random forest arrives at a decision or prediction based on the maximum number of votes received from the decision trees. The outcome that it arrives at, for a maximum number of times through the numerous decision trees is considered the final outcome by the random forest.


    1.	Created a Random Tree Forest Object, with parameters: n_estimators = 100 and random states = 42
    2.	Training set -> Subjectivity variable
    3.	Test set -> Detrended Adj close price
    RMSE: 0.18


**LightGBM**  
LightGBM is a gradient boosting framework that uses tree based learning algorithms, it uses a histogram-based method to aplit the data into 'bins' and these bins are then used to iterate, calculate the gain, and split the data. 

    1.	Defined an ARIMA model and fit it into the training set
    2.	Plot autocorrelation of residuals to check the randomness in the dataset
    3.	Training set -> Subjectivity variable
    4.	Test set -> Detrended Adj close price
    RMSE: 0.17


**XGBoost**  
 XGBoost is short for extreme gradient boosting. It is a popular and efficient open-source method, well known for its ability to work complicated datasets by using various optimization method. It is based on decision trees and improving on other methods such as random forest and gradient boost, and it is also a supervised learning algorithm, which attempts to accurately predict a target variable by combining the estimates of a set of simpler, weaker models.

    1.	Created an LGBM Regressor Object, with parameters: n_estimators = 100 and random states = 42
    2.	Training set -> Subjectivity variable
    3.	Test set -> Detrended Adj close price
    RMSE: 0.20


**LSTM**  
LSTM also known as Long Short Term Memory is network with loops in it, it works like a RNN (recurrent neural network) wherebyy the algorithm uses past information before conluding a decision, but unlike RNN, LSTM has the ability to store its information for a long preiod of time.

    1.	Created a Dataframe with Subjectivity and Adj Close variable
    2.	Split the input sequence into 60-time steps
    3.	Create LSTM Model and compile using the Adam algorithm
    4.	Training set -> Subjectivity variable
    5.	Test set -> Adj close price
    RMSE: 0.15


**KNN**  
KNN, or also known as K Nearest Neighbor is a simple algorithm that stores all the available cases and classifies the new data based on a similarity calculation. It calssifies the new data points based on how its neighbors are classified.  

    1.	Used GridSearch to find the best parameters
    2.	Created KNeighborRegressor object to predict based on the local neighbors
    RMSE: 0.22


**Prophet**  
Prophet is a algorithm for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data.

    1.	Created a Prophet model and added predicted values: yhat into the DataFrame
    2.	Plotted different components of forecast
    RMSE: 0.19
#
### 5. Conclusion

#
### 6. Recommendations for Enhancements

#
### 7. Members Contribution

**Project:**  
Data Preparation: Mildred, Jace and Janice  
Data Exploration: Mildred, Jace and Janice  
Machine Learning: Mildred and Janice  


**Video Preparation:**  
Slides design and content: Jace  
Audio Recording: Mildred, Jace and Janice  

#
### 8. Reference List
1. https://towardsdatascience.com/predicting-stock-prices-using-a-keras-lstm-model-4225457f0233
2. https://stackabuse.com/k-nearest-neighbors-algorithm-in-python-and-scikit-learn/
3. https://www.kaggle.com/code/ramlalnaik/sales-prediction-using-sarimax-and-prophet-methods
4. https://365datascience.com/tutorials/python-tutorials/xgboost-lgbm/
5. https://stackabuse.com/random-forest-algorithm-with-python-and-scikit-learn/
6. https://analyticsindiamag.com/complete-guide-to-sarimax-in-python-for-time-series-modeling/



