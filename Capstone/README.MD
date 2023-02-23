
# **Capstone Project: Cashflow** 
## **DSIR 1010 General Assembly - October 2022 Cohort**
## **Preet Sekhon**
---


#
## **Repo Folder Organization**
|Folder|Type|Description|
|---|---|---|
|Data|folder|contains raw and cleaned datasets|
|Plots|folder|exported graphs from VS Code as png files|
|1.0_Realty_Mole_Rent_API|VS Code notebook|contains VS Code notebook with API used to gather rental listing data |
|1.1_PDF_Scrape|Google Colab notebook|contains Google Colab notebook with coded used to scrape voter datasets that were in pdf format |
|2.0_Cleaning|VS Code notebook|contains VS Code notebook bringing in raw data for removing of nulls and making it ready for merging to the main dataset |
|3.0_Pre-Processing|VS Code notebook|contains VS Code notebook with joining of datasets, feature engineering, and removing of outliers |
|4.0_EDA-and-Data-Visualization|VS Code notebook|contains VS Code notebook with EDA and data visualization|
|4.1_EDA_Target_CFP|VS Code notebook|contains VS Code notebook with EDA for Target CFP|
|5.0_Models_Regression|VS Code notebook|contains VS Code notebook Linear Regression Modeling|
|5.1_Models_Classification|VS Code notebook|contains VS Code notebook Classification Modeling with SMOTEENN|
|6.0_Data_Dictionary_Creation|VS Code notebook|contains VS Code notebook for code on streamlining Data Dictionary Creation process|
|README.md|README|README file for Capstone Projec: Cashflow|
|Capstone.pptx|Presentation|Presentation PowerPoint file for Capstone Projec: Cashflow|
|Capstone.pdf|Presentation|Presentation PDF file for Capstone Projec: Cashflow|
|Data_Dictionary.pdf|pdf|pdf of data dictionary for dataset|


#
## **Data**
The largest challenge of this project was the data. I will detail the specifics obstacles faced below. It was important to me have relevant information. The rental and listing data had to be from the same timeline. Otherwise the Cashflow would've been inaccurate.
### **Real Estate Listings: Propstream.com**
A popular website amongst real estate investors. The only option that we found on how to extract large amounts of real estate listing data. The website wouldn't allow for a search at a state level. The biggest a search radius would go was county. Each of our 41 counties had to be searched for individually.
### **Rental Listings: Realty Mole Property API**
Subscription and API key acquired from RapidAPI.com. This API delivered all listings per zip code queried. From there we were able to establish a minimum, average, and maximum rent estimate per zip code and bedroom amount.
### **Voting Data: SOS.CA.Gov**
The Secretary of State of California's website housed the voter data I was looking for. I was able to download it in PDF format and scrape it to a CSV file.
### **Income/Population Data: Census.GOV**
Massive database housed at Census.gov. I sifted through to find what we needed. 
### **Metrics**
- Cashflow Positivity: Does this property generate income? After PITI(Principal, Interest, Taxes(property), Insurance) and Maintenance are paid, is there any money left over? 
- Cash on Cash Return: What is your annual return on your initial investment. So your down payment, closings costs, and any initial repair are your intial Cash investment. The Cash you have from your Cashflow is your annual return. You take your annual Cashflow and divide by your Cash investment to get your Cash on Cash Return. 
- Target Cashflow Posititivy: Cash on Cash Return of 4% or higher.


#
## **Software**
VS Code was used to house and run our Python notebooks. In addition, the following libraries were imported for use:
|Libraries|||
|---|---|---|
|NumPy|Scikit-Learn|Math|
|Pickle|Skopt|Scipy|
|Imblearn|Xgboost|Matplotlib|
|Seaborn|Tabulate|Google Colab|


#
## **Problem Statement**
A group of large investors are pooling their money together to add real estate to their portfolio. Are you able to design a strategy on how best to allocate capital?


#
## **Executive Summary**
Cashflow is they key to real estate investment. An investment property shouldn't become an 'alligator', a investment that requires you to add more funds to cover your monthly costs. Cashflow is having money leftover after you haved paid your mortgage(principal and interest), property taxes, insurance, and maintenance. If one evaluates a property based on Cashflow, then one can buy and hold as long as they like. Real estate values will rise and fall, and if your property's value is now worth less than before, you can rest assured. You invested for Cashflow, and the property will cover it's costs. When the time is right, you can sell. Cashflow allows for the luxury of time. Finally, Cashflow isn't the end of the returns on the property. Each month you are paying down the principal of the property. You can also use your Cashflow at the end of the year for additional Principal pay down. The last piece of this is appreciation. Now that you have the luxury of time, you can exit the property when the time is right.

The data we collected on our listings was centered around Cashflow. 
 - **Revenue = Annual Rent**
 - **Costs = Principal, Interest, Property Taxes, Insurance, and Maintenance**
 - **Cashflow = Revenue - Costs**

**Revenue** is fairly simple to calculate, just take annual rent.
For **Costs** we had to make some decisions on some of the constants. First off, the MLS Amount is what we used for the Price, and a deposit of 25% was used. We assumed our closing costs were 4%, and we didn't add any make ready costs. Make ready costs, are any repairs that would be necessary to start to rent the property. The closing costs were added to the 75% of the Price. 

Other Constants:
- 6.5% interest rate
- .71% of MLS Amount for annual property tax
- .25% of MLS Amount for annual insurance
- .3% of MLS Amount for annual insurance 

For this project, we started off with a continuous target variable: Cash on Cash Return. Only 14.8% of the dataset returned a positive return on the investment. Even if that was .0001%. Still I chose to compare 4 Regression Models: Linear, Random Forest, Decision Tree, and Support Vector Machines. I was not happy with the results. Random Forest produced the best model score of .433 and an RMSE of .043. Each model used GridSearchCV.

I then pivoted to a Classification Problem. I switched my target variable to Target Cash Flow Positivity, which was an Average Cash on Cash return of 4% or higher. That is half of the minimum Cach on Cash return I accept as a real estate investor, but I felt it was a good number to use. This is a declining market and price reductions are common place. So a property giving a 4% return can easily become 8% or more based on a more attractive purchase price. This created a new problem though.

Now my target variable only made up 5.6% of the dataset. So to help balance out our data, SMOTEENN was used. I also utilized BayesSearchCV to fine tune the models for optimal parameters. The metric I chose to evaluate the models is the Brier score which is an accuracy metric of a model's predicted probability. A lower score is indicative of a better model. As a secondary metric, we evaluated the models on precision score to reduce false positives. The models used were: Logistic Regression, Random Forest Classifier, and XGBoost Classifer. XGBoost was a clear winner with the lowest Brier Score of .047 and a precision score of .955. Finally the Feature Importance from the XGBoost model had Single Family Residences and Child Dependency Ratio amongst it's top results. Further solidifying the strategy of targeting rental properties for families. Please see below for findings, conclusions, and next steps.


#
## **EDA Learnings**
The process revealed that most correlated features had to do with renters that have children. The 5 most correlated features were:
- Percent Male 5-9 years
- Percent 5-9 years
- Percent 5-14 years
- Percent under 18 years
- Child Dependency Ratio

I was able to then create bar charts of Zip Codes, Cities, and Counties that scored high on those features. These charts will be usefull in my strategy creation.


#
## **Conclusions and Recommendations**
Real estate investments have to be evaluated on an individual basis. Standardization and scalability are very hard tactics to execute due to the variability of the industry. What I've tried to accomplish in this project was to help focus our sites on property types and demographics that should produce more Cashflow. So my recommendations for next steps would be to follow this 3 pronged approach:

- Task 1A: Focus on the top 5 cities with a population percentage of 5-9 years old.
    - Yuba City, Live Oak, Visalia, Porterville, and Tulare. Evaluate listings and execute deals that deliver a minimum 8% Cash on Cash Return.
- Task 1B: Focus on the top 5 cities with a population percentage under 5 years old.
    - Smartsville, Marysville, Edwards, Visalia, California City. Keep tabs on listings and trends in these cities. Returns might not be there now, but the future might be greener based on the aging population.
- Task 2: Review the top 10 cities for Cash on Cash Return.
- Task 3: Review the top 10 cities by bedroom count for Cash on Cash Return.
- Overall Strategy: After further review of Tasks 1-3, look for opportunities to cluster investments. Clustering will provide a reduction of overhead and allow for a certain amount of scalability. 
