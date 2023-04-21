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
   1. Purpose of our Project
   2. Preparation of Dataset
   3. Exploration of Dataset
   4. Machine Learning
   5. Members Contribution
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
   2. **Data Cleanup:** Remove all NaN values. Used Hodrick-Prescott filter to remove Seasonality and Trend
   3. **Detrend:** Detrended values added to the DataFrame     
    
    
**Preparation of Reuter Headlines:**     
   DataFrame Name: sp_copy
   1. **Date Splitting:** Data extracted from 01/06/2018 to 01/06/2019
   2. **Data Cleanup:** Remove the Description Column and NaN values. Remove all weekends and Public Holidays. Remove all symbols from headlines
   3. **Individual headline:** Grouped any headlines that falls on the same day  
    
 
**Combination of both Google Stocks and Reuter Headlines:**    
   DataFrame Name: df_merge
   1. **Data Merge:** Combined the Google Stocks and Headlines according to their dates  
    
#
### 3. Exploration of Dataset
In this section, we will delve deeper into the dataset and find which and how some variables would affect the seasonality and trend.


**Exploration of the Google Stocks from Yahoo:**    
DataFrame Name: SP  
   1. 
    
**Exploration of Reuter Headlines:**  
DataFrame Name: sp_copy  
   1. Caculate Subjectivity, Polarity for each headline
   2. Using Sentiment Intensity Analyzer, we were able to get the Positive, Negative, Neutral, Compound values for each headline

**Exploration of both Google Stocks and Reuter Headlines:**  
DataFrame Name: df_merge  
   1. Analyzed the relationship between the Subjectivity, Positive, Negative, Compound, and Polarity with Adjective Close and Detrended Adjective Close:  
   a. Subjectivity has the strongest relationship with Detrended Adjective Close  
   b. Positive has the strongest relationship with Adjective Close  
   Therefore, we'll be using the variables: Compound for Machine Learning

### 4. Machine Learning
In this section, we have experimented with 7 machine learning algorithms to test which algorithm best fits our purposes.  
1. Sarimax     
   
     1. 

