# SC1015 Mini_Project
School of Computer Science and Engineering  
Introduction to Data Science and AI  
Lab A125  
Group: 7  

**Members:**
   1. Mildred
   2. Jace
   3. Janice
#
### Description:

This repository includes the necessary code and documents to run our Mini-Project, we have used the following softwares to program our project: Jupyter Notebook and Deepnote. 

This ReadMe would summarise what we have done 
#
### Table of Contents:
   1. Purpose of our Project
   2. Preparation of Dataset
   3. Exploration of Dataset
   4. Machine Learning
   5. Uses for the Project
   6. How users can get started on the Project
   7. Members Contribution
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

Preparation of Google Stocks from Yahoo Fiance:  

    1. Date Splitting: Data extracted from 01/06/2018 to 01/06/2019 
    2. Data Cleanup: Remove all NaN Values
                     Using Hodrick-Prescott filter to remove seasonality and trend
    3. Detrend: Added a new column with the detrended values of the original data
    DataFrame Name: SP
    
Preparation of Reuter Headlines:  

    1. Data Splitting: Data extracted from 01/06/2018 to 01/06/2019
    2. Data CLeanup: Remove the Description column
                     Remove all weekends and public holidays, and NaN values
                     Group any headlines that falls on the same day, removal of any symbols from the headlines
    DataFrame Name: sp_copy
    
### 3. Exploration of Dataset

                     
                     
                     
                     
    
    





