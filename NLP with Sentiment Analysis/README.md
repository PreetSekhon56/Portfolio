General Assembly
DSIR 1010

Preet Sekhon
12/07/22

# Executive Summary

This NLP Project will classify Subreddits between to types, Dad Jokes and Poker.

# Problem Statement
Are the Dads Among us Playing Poker?

# Notebooks
    - Scrape.ipynb
    - DadJokesCleaning.ipynb
    - PokerCleaning.ipynb
    - FeatureEngineeringandPreprocessing.ipynb
    - Modeling - Logistic Regression.ipynb
    - Modeling - RandomForest.ipynb
    - Modeling - MultinomialNB.ipynb
    
    
# Data Science Workflow
___
## Web-Scraping

Scraping tool graciously provided by our instructors. 

Dad Jokes Raw Scraped Data: 
    - 3,697 days worth of data collected
    - 50,102 rows and 90 columns
    
Poker Raw Scraped Data:
    - 5,395 days worth of data collected
    - 50,234 rows and 99 columns in our Raw Data Frame

    
## Data Cleaning

Dad Jokes Cleaned Data: 
    - 9,713 rows and 2 columns
    
Poker Cleaned Data:
    - 6,778 rows and 2 columns
   
   
## Feature Engineering
    - Tokenization
    - Sentiment Analysis
    - Lemmatization
    - Count Vectorization


## Cleaning and Pre-Processing
    EDA through Histograms and Top 10 Word Bar Charts


## Modeling
    Used 3 models: Logistic Regression, Random Forest Classifier, and Multinomial Naive Bayes. All had high accuracy scores ranging from 97.3%, MNB, to 97.6%, LogReg. Random Forest was most likely overfit.


## Conclusions and Next Steps
    It would appear that we aren't in any danger of having poker players among our innocent Dads.
