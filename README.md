# Retail-sales-prediction-regression-project

**About the Data**

Rossmann operates over 1000 stores in 7 European countries. Currently, Rossmann store managers are tasked with predicting their daily sales for up to six weeks in advance. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality, and locality. With thousands of individual managers predicting sales based on their unique circumstances, the accuracy of results can be quite varied. You are provided with historical sales data for 1,115 Rossmann stores. The task is to forecast the "Sales" column for the test set. Note that some stores in the dataset were temporarily closed for refurbishment.

The Retail Sales Prediction Project aims to develop a machine learning model to forecast sales for the retail company. The project leverages historical sales data and external factors to improve inventory management and optimize revenue. Expected outcomes include increased sales accuracy, reduced inventory costs, and improved customer satisfaction.

We have two datasets namely stores_df and rossmann_df .

stores_df has 1115 rows containing information about different Rossmann Stores and there are 10 columns

rossmann_df is a bigger dataset which contain sales information of the stores , the transaction date and multiple other information like number of customers visited on the store.


**Data Preprocessing :**

Getting the dataset: There were two datasets having the associated information of the Rossmann stores namely "Stores.csv" and "Rossmann Stores Data.csv".The Stores.csv contained the information about the 1115 Rossmann Stores like the storeType , assortmenttype , providing promo or not , competition available or not and promoInterval . Whereas the Rossmann Stores Data.csv was having the information of each day transaction in these stores from 2009 to 2015

Importing libraries: The necessary libraries to clean and preprocess the data were imported : Numpy and Pandas .
For Visualization the libraries used were Matplotlib and seaborn 
For Ml Model creation , the libraries used were Scikit-learn .

Importing datasets:The data was imported using pd.read_csv() method.

**Data Wrangling:** 

There are missing values in some columns . I initially thought of some inferences out of it and it is as follows: 

Missing data in CompetitionOpenSinceMonth and CompetitionOpenSinceYear indicates the stores without the presence of Competition stores . Such Stores are 354.However on further inspection , we found that there were only three such stores who do not have any competition store . So , remaining 351 stores were having missing values about the CompetitionOpenSinceMonth and CompetitionOpenSinceYear. 

Later, during cleaning the data for model feeding , I filled the missing values of these two columns with the existing non null values of the two columns respectively and the filling was based on the frequency of the non null values in the column.

Missing data in Promo2SinceWeek , Promo2SinceYear , PromoInterval indicates the stores that did not give promos recurringly. Such stores are 544 in number.

Later, during cleaning the data for model feeding , I decided to drop the Promo2SinceWeek column because it would be more accurate to consider the weeks as categorical value though the values appeared to be numerical . And considering those categorical , using them in the model data feed , it was needed to be one hot encoded . OHE could have been done , but the number of categories would be too high and dimensionality would be the problem then. So rather I dropped it.

Promo2SinceYear represented the Year when the store entered the recurring promotions activity.Later during the model data preparation , I first filled the missing values in the column using frequency based approach of filling non null values of the column.Then for model , I also scaled the column . OHE could also have been implemented here but I did not used it.

PromoInterval : For filling the missing values , I used the same above strategy 
of frequency base approach of filling non null missing values of the column.
After filling the missing values , I used One hot encoding on the column as it was a categorical column.


CompetitionDistance also has 3 missing values.These three missing values were associated to those 3 store who do not have any competition store. During the cleaning , when I dropped the outliers in the numerical columns namely CompetitonDistance , Customers , Sales , these missing values also got dropped . 


PromoInterval Jan,Apr,Jul,Oct is most popular PromoInterval.335 stores are giving recurring promos in this interval.

StoreType 'a' is most prevalent StoreType. During the model data preparation , I did OHE of the categorical column. The column represented the product type sold in the store

The Basic Assortment 'a' is most prevalent. The Basic assortment has limited variety of products available. Assortment 'c' contains the most varied products collection. Later , I did Ordinal encoding for this column because here assortment 'c' has bigger collection than 'b' and 'b' has bigger collection that 'a'. 




Feature Engineering : Converted the Date column in date datatype using pd.todatetime() .Then Extracted multiple column from it namely year , month , day.

**EDA :**

Checked the unique value counts of each column

Checked for missing values in the column and replaced them

Checked the best performing stores based on sales

Checked the best performing stores based on Customer footfall

Converted the data type of Date column

Created new columns from the Date column

Checked for the number of closed store observation

Checked for sales in each DayofWeek and concluded that Sundays have lowest sales and also that most often stores are closed on Sundays

Checked the distribution of each column and also looked for the presence of outliers and skewness in the features . Later did transformation and outlier removal for better performance of the models.

**Supervised ML algorithms implemented** :

1 ) Linear Regression

2 ) Lasso Regression

3 ) Ridge Regression

4 ) Decision Tree Regressor

The best performance was given by DT regressor though the tree was too deep and hence too complex and interpolation was also the issue . Hence the next best performing model , the ridge regression was choosen as the final model.The final model was giving the **R2 Score of 96%** .

**Conclusion**

In conclusion, this machine learning project aimed to predict sales based on various features, employing a combination of exploratory data analysis and regression modeling. The key findings and takeaways from this project are summarized below:

**Model Performance:**

Our regression models, including the Linear Regression,the Lasso Regression ,the Ridge regression and Decision Tree Regressor, demonstrated promising performance. The Ridge model, with its regularization capabilities, exhibited robust generalization to unseen data, achieving a mean absolute error of 801 on the test set.

**Feature Importance:**

Feature importance analysis revealed that the Cutomers , Promo , StoreType_d significantly positively influenced Sales value and StoreType_b , Assortment_b significantly negatively influenced the Sales value. The Ridge model, with its regularization penalty, effectively identified and assigned appropriate weights to these crucial features.

**Challenges and Limitations:**

Challenges in the project included dealing with missing data in certain features and the need for careful feature engineering. Despite these challenges, the models provided valuable insights into the factors influencing sales value.

In summary, this project successfully addressed the task of sales prediction, providing actionable insights and a reliable model for estimating sales value. The lessons learned and methodologies applied pave the way for future endeavors in predictive modeling within the Sales prediction domain.