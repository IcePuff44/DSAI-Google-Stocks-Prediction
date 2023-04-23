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
   6. [Extra Things Learnt (Out of Course Syllabus)](#6-extra-things-learnt-out-of-course-syllabus)
   7. [Recommendations for Enhancements](#7-recommendations-for-enhancements)
   8. [Members Contribution](#8-members-contribution)
   9. [Reference List](#9-reference-list)
#
### 1. Project Purpose
As youths in Singapore, there are 3 economic factors that are of concern in 2023. 
1. Inflation
2. Recession
3. GST Increase to 9% 

We can get a side income through trading to help combat these economic concerns. 
However, there are many stocks available to trade in the market and thus we need to be able to roughly predict the closing prices for the stock.
As such, through this project we plan to use daily headlines from Reuters, a financial news site to see if it can predict future Google stock prices with relative accuracy.

With the use of Data Science and Machine Learning, we hope to: 
   1. Give a visualisation of the historical stock market prices
   2. Convert headlines of natural language to values we can use for prediction
   3. Know how predictable Google Stocks can be using subjectivity and positive sentiment of Reuters headlines.

#
### 2. Preparation of Dataset
For this Project, we have chosen to work with 2 Datasets: Historical Google Stocks from Yahoo Finance, and Reuter Headlines. In this section, we will analyse the dataset and prepare it to be used for Machine Learning.


**Preparation of Google Stocks from Yahoo Finance:**  
   DataFrame Name: SP
   1. **Set Dateframe:** Data extracted from 01/04/2018 to 01/12/2019 (DD/MM/YYYY)
   2. **Data Cleanup:** Remove all NaN values. 
   3. **Detrend:**  Used **Hodrick-Prescott** filter to remove Seasonality and Trend, and create new variable "ADJ_Close_Detrended"
    
    
**Preparation of Reuter Headlines:**     
   DataFrame Name: sp_copy
   1. **Set Dateframe:** Data extracted from 01/04/2018 to 01/12/2019 (DD/MM/YYYY)
   2. **Data Cleanup:** Remove the Description Column and NaN values. Remove all weekends and Public Holidays. Remove all symbols from headlines
   3. **Individual headline:** Grouped headlines that falls on the same day  
   4. Calculate **Subjectivity, Polarity** for each headline
   5. Using Sentiment Intensity Analyzer, we were able to get the Positive, Negative, Neutral, Compound values for each headline
    
 
**Combination of both Google Stocks and Reuter Headlines:**    
   DataFrame Name: df_merge
   1. **Data Merge:** Combined the Google Stocks and Headlines according to their dates  
   2. **Dataframe for ML** Created new .csv file "df_ML.csv" to be used for Machine Learning Models
    
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
Machine Learning can be used to predict stocks as long as we:
   1. Identify quality predictors to work with
   2. Conduct Feature Engineering
   3. Handle and process time series data appropriately

That being said, we should take note that while forecasting future stock prices is conducted accurately with Machine Learning, it does have its shortcomings, such as being unable to predict sudden events that may cause a spike or fall in stock prices overnight. Hence, predicting stocks is a complex process that requires a fair amount of effort for prior research.

Based on our observations and analysis, LSTM and Prophet are both excellent models for consideration to predict stocks. LSTM is designed to perform non-linear mapping for input and output variables; handle sequential and missing data; learn patterns and trends in the data over time for an accurate forecast. These features are all essential for stock predictions. Prophet greatly reduces overhead during data preprocessing by handling trends; breaks down time-based features into component plots; provides a built-in feature selection algorithm to get the most relevant features. Prophet is a new creation, and we see endless potential in the model for it to become one of the most oustanding Machine Learning models.

#
### 6. Extra Things Learnt (Out of Course Syllabus)
Our team decided to embark on a project that embodies practicality, where we can use it as a stepping stone to stretch our learning in more domains. Therefore, the selection of the application of data science in the finance industry.

The main categories that we employed out-of-syllabus methods are as follows:
   1. Datasets: Time Series and Natural Language (unstructured)
   
         a. New methods of data cleaning
         
         b. Requires techniques like checking for stationary data and trends; detrending; NLP encoding etc
         
         c. Data normalisation
   2. Visualisations: Different methods of visual representation that involves interactivity. i.e. Plot.ly
   3. Feature engineering: Preparation of useful data to assist our forecast goal. Technical indicators merged with sentiment analysis.
   4. 7 Machine Learning models.
   
         a. Varying natures and advantages. Each model has to be dealt with differently, which required tons of research and hours of implementation.
         
         b. 1 common characteristic of being able to work with time series data. 
   
The above is just a subset of the new knowledge we have put into play for our project. For in-depth details, please refer to our presentation video for our process to find out!

#
### 7. Recommendations for Enhancements
We note that every project, including ours, has limitations. Hence, we have identified some possible ways for improvement to acquire results with higher accuracy, for the best data-driven decisions.

1. Include other metrics for a more holistic approach towards stock prediction

   -Stationary, numeric data: Market Economic Indicators (GDP, Company Financial Reports)
   
   -Consider the global development (probably involves unstructured data) by incorporating aspects like political development for a wider range of considerations
 
2. Use a larger dataset
   A small dataset was in fact, one of the limitations of our project. We are unable to acquire stocks and headlines data that have aligned dates for a period longer than 2 years, as the datasets were retrieved from different sources. Besides, the stock market closes on holidays, weekends and some other special occasions, reducing the number of days we can analyse. Headlines may also not always be directly related to the chosen stock, which is a factor we cannot control but can reduce its impacts by using a larger dataset to factor in more relativity over time.
   
3. Hyperparameter tuning
   This is a type of configuration that is external to the model and whose value cannot be estimated from data. The process involves selecting optimal values for the model hyperparameters, such as learning rate, regularisation strength, and number of hidden layers. It involves techniques such as grid search or Bayesian optimisation.


#
### 8. Members Contribution

**Project:**  
Data Preparation: Mildred, Jace and Janice  
Data Exploration: Mildred, Jace and Janice  
Machine Learning: Mildred and Janice  


**Video Preparation:**  
Slides design and content: Jace  
Audio Recording: Mildred, Jace and Janice  

#
### 9. Reference List
1. https://towardsdatascience.com/predicting-stock-prices-using-a-keras-lstm-model-4225457f0233
2. https://stackabuse.com/k-nearest-neighbors-algorithm-in-python-and-scikit-learn/
3. https://www.kaggle.com/code/ramlalnaik/sales-prediction-using-sarimax-and-prophet-methods
4. https://365datascience.com/tutorials/python-tutorials/xgboost-lgbm/
5. https://stackabuse.com/random-forest-algorithm-with-python-and-scikit-learn/
6. https://analyticsindiamag.com/complete-guide-to-sarimax-in-python-for-time-series-modeling/



