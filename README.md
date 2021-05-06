# Capstone_One
Springboard capstone one project on Apple app

## 1.0 Problem Summary
With millions of apps with similar functionalities around nowadays, mobile app analytics is a great way to understand the existing strategy to drive growth and retention of future users. Developers and investors can rely on users’ ratings to predict whether the overall rating for an app is more than 4 stars (which is assumed to be a good app) or not. The performance of an app based on user rating should inform decision-making on version update and functionality upgrade amongst other things. Hence, the goal of this project is to predict whether the overall rating for an app is more than 4 stars or not. This project set out to classify best performing iOS applications based on users’ ratings. On a general note, ratings serve as protection for both app users and investors to guard against time and financial investments in products/services that do not perform well in the market. Hence, the goal of this project is to predict whether the overall rating for an app is more than 4 stars (1=yes, 0=no). For this project, an app with 4 or more stars is assumed to be a very good app.
## 2.0 Approach Taken
 The project was addressed with data sourced from Kaggle and it was gotten from the iTunes search API at the Apple Inc website. The original data frame was made up of 5197 observations with 16 features (Table 1 lists all the 15 features excluding the rating column, which is the label’s column). The labeled column has Boolean variables of 1 and 0 that represented if the applications received ratings of more than 4 or not. Going by the nature of the label’s column, it could be seen that the project was a classification problem. 

The data obtained was cleaned up to prepare it for modeling. All the apps were priced in USD. As a result, the currency column was dropped as it will have little to no impact on the model. Features ‘track_name’ and ‘desc’ were recorded in different languages, and they were processed with Natural Language (NL) processing technique using sklearn’s TfidfVectorizer. New features were generated from these two variables and the data frame columns increased from 16 to 4897. ‘track_name’ and ‘desc’ were dropped from the data frame. 
The content rating column contained only 4 unique values and they were of string data type. These
It should be noted that none of the observations had missing values in the data frame. This could be because the data was partly cleaned from the source before it was obtained for this project.
## 2.1 Exploratory Data Analysis
The mean size of apps in the data frame was 197 MB. The biggest was 4gb and the smallest was 0.62mb. Other variables captured in descriptive statistics of the data frame can be seen in Table 2 below.

![Table1](https://user-images.githubusercontent.com/61480297/117222009-5157cf00-adbf-11eb-8d53-e76e2dd040b9.png)

The pricing of the applications in the data frame ranged from 0 to $299.99. The mean price of the application in the data frame was $1.74. Also, the least and maximum supporting devices for any app were 9 and 47 respectively, while the average was 37. Perhaps, when the data frame was cleaned, missing observations in the language column were replaced with 0. This is a possible explanation for the least number of languages supported to be 0. On average, 5 languages are supported by the apps. Values were converted to integers so that they could be used as part of features for the modeling.

![Heat Map](https://user-images.githubusercontent.com/61480297/117222036-63d20880-adbf-11eb-901f-c4b92a7b8c84.png)


Using Spearman's rank correlation coefficient, the heatmap above was generated. No strong relationship can be seen between any of the variables in the data frame. 
There were 23 genres the apps were associated with game-based applications were the highest in the data frame, followed by entertainment and education. The least genre of apps in the data frame was catalog.

![Heat Map](https://user-images.githubusercontent.com/61480297/117246603-c7752980-adf1-11eb-8519-3cb0d30b500d.png)
Based on the bar plot below, Health & Fitness, Medical, Photo & Video, and Games rank highest amongst genres with the total number of ratings greater than 4. The second plot further shows that of all the application genres present in the data frame, game applications are 2824. Using this value, roughly half of the users gave more than 4 stars rating for the application.

![Prime Genre](https://user-images.githubusercontent.com/61480297/117246864-32266500-adf2-11eb-88d0-aff726469b04.png)

The data frame was grouped by rating and price and the table below was generated. 56.5% of the apps received a rating of less than 4 or less by users. The mean price of apps that received ratings above 4 stars was $0.1 higher than those with a lesser rating. However, the prices of apps with lesser than 5 stars are more widespread based on their standard deviation. The most expensive application of the data frame had a rating of 0 (less than or equal to 4 stars). From the box plot below, based on price, more of the applications received favorable ratings of above 4. Also, applications with favorable ratings tend to be more expensive in general compared to those with lower ratings.

Due to the extreme prices of applications distorting the distribution of the data frame, extreme observations based on prices were dropped. As a result of this, the total number of observations was reduced to 4605. As a result of this, the box plot above was generated.
In terms of the supported number of languages per application, applications with a higher number of supporting languages had more favorable ratings higher than 4 stars. This is depicted in the image below.

![Box Plot](https://user-images.githubusercontent.com/61480297/117247275-d3adb680-adf2-11eb-9c3c-de3204dd7312.png)
![Box Plot](https://user-images.githubusercontent.com/61480297/117247380-fdff7400-adf2-11eb-912f-ad2fde3a0fcb.png)

The values of the prime_genre column were converted to dummy variables. This further increased the total number of features to 4918. 
Also, due to the magnitude of values of 'size_bytes', 'rating_count_tot', 'rating_count_ver', and 'sup_devices.num', the values of these features were standardized, and the new values were added to the data frame.
For the modeling purpose, the data frame was split into training and testing data set in the ratio of 75% to 25% respectively.

## 2.2 Modeling:
This is a classification problem, in supervised learning. Here we have used the following classification models:
•	Logistic Regression
•	K-Nearest Neighbor (KNN)
•	Support vector machine (SVM)
•	Random Forest
•	Naive Bayes
•	Gradient Boost
Evaluating the performance of a model by training and testing on the same dataset can lead to overfitting. Hence the model evaluation is based on splitting the dataset into train and validation set as done above. But the performance of the prediction result depends upon the random choice of the pair. To overcome that, the Cross-Validation procedure is used where under the k-fold CV approach, the training set is split into k smaller sets, where a model is trained using k-1 of the folds as training data and the model is validated on the remaining part.

## Classification/ Confusion Matrix:
This matrix summarizes the correct and incorrect classifications that a classifier produced for a certain dataset. Rows and columns of the classification matrix correspond to the true and predicted classes respectively. The two diagonal cells (upper left & lower right (TP & TN respectively)) give the number of correct classifications, where the predicted class coincides with the actual class of the observation. The off-diagonal cells give the count of the misclassification (upper right & lower left (FP & FN respectively)). The classification matrix gives estimates of the true classification and misclassification rates.

Logistic Regression's Confusion Matrix
![Logistic Regression](https://user-images.githubusercontent.com/61480297/117247990-115f0f00-adf4-11eb-8bd0-22a88e37d84d.png)

The accuracy score using a grid search was 59.98%
The precision rate of this classification is 66%

The recall rate of the classification is 62.9%

Using cross-validation score, the mean test and train scores are 57.24% and 64.48% respectively.

Random Forest: the accuracy score using a grid search was 69.97%
![Random Forest](https://user-images.githubusercontent.com/61480297/117248293-96e2bf00-adf4-11eb-990a-194a0cba9ba0.png)

The precision rate of this classification is 78.20%

The recall rate of the classification is 71.64%

Using the cross-validation score, the mean test and train scores are 73.17% and 79.81% respectively. 

Gradient Boosting: the accuracy score using a grid search was 69.97%
![Gradient Boost](https://user-images.githubusercontent.com/61480297/117248488-e9bc7680-adf4-11eb-8a17-aeffdbe61ea1.png)

The precision rate of this classification is 77.44%

The recall rate of the classification is 72.26%

Using the cross-validation score, the mean test and train scores are 73.25% and 79.52% respectively. 


![Model Comparisons](https://user-images.githubusercontent.com/61480297/117247600-69e1dc80-adf3-11eb-9e63-cf19eaa13bc0.png)


From the table above, it can be seen that Random Forest and Gradient Boost have the best scores from the 6 models used for classification. The Naive Bayes model is the worst performed of the models. The performances based on their accuracies are depicted in the graphs below.

![Model Performance](https://user-images.githubusercontent.com/61480297/117248745-559edf00-adf5-11eb-943d-ef50bdebe39c.png)

The hyperparameter tuning of the Random Forest algorithm improved its score from 69.97% to 71.00%.  On the other hand, the most important features of the data frame were the engineered features. The ROC-AUC score for the Random Forest Algorithm is 0.7797

![ROC RF](https://user-images.githubusercontent.com/61480297/117248981-aca4b400-adf5-11eb-920e-45709afc44aa.png)

The hyperparameter tuning of the Gradient Boost algorithm reduced its accuracy score from 70.23% to 69.97%.  On the other hand, the most important features of the data frame were the engineered features. The ROC-AUC score for the Gradient Boost algorithm is 0.7656. 

![ROC GB](https://user-images.githubusercontent.com/61480297/117249062-d067fa00-adf5-11eb-8a5a-78d542cb65cd.png)

A comparison of the two ROC-AUC scores of the two algorithms shows that Random Forest performs better than Gradient Boost in the classification of the test data set.

## 3.0 Important Features from Model:
The features that impacted the performance of the model most were those engineered from the original features in the dataset. The top features were interpreted from Chinese and Japanese languages to English to be able to make more sense of their relevance and for analysis purpose. The most important feature of the database from the Random Forest model (which was the best performing model) is volume control. As a result, for most application, the ability of users to be able to control volume of the sound output seamlessly can play a good role in improving ratings amongst users. It should also be noted that some applications do not need sound output and this feature might not really affect the likeability of such apps. 

![Important Features](https://user-images.githubusercontent.com/61480297/117249284-2e94dd00-adf6-11eb-8e1b-41f288533ab5.png)

![Important Feature Graph](https://user-images.githubusercontent.com/61480297/117249354-4704f780-adf6-11eb-8df8-32c19f2c51f6.png)

Features related to billing and subscription were also important to this classification problem as they were among the top 20 features. It is a norm that humans generally want commodities that are priced at low value. The pricing and billing structure of an app will also affect its likeability. As a result, to improve likeability amongst app users, developers and investors must price apps in ways that enable users to gain more for less (users must have value for money).
App genres that developers can look into based on the important features of the model relate to commuting, hospitality (hotel), gaming, messaging and sport streaming.
Description also came out as an important feature. Hence, it can be seen that good description of functionalities of apps will go a long way to improve the ratings of apps.

## 3.0 Ideas for Future Research:
•	An idea for further research on this topic is to investigate the impact of prices and prime genres on application retention among similar applications. 

## 4.0 Recommendations
1.	Based on the best performing model in the data set, investors can compare apps and predict the possibility of their apps gaining traction in the market and giving a good return on investment in the long run.
2.	Apps platforms can use the model to rank and suggest high performing apps to users. Time spent by consumers trying to reduce similar applications will be reduced through this rating ranking system.
3.	For apps’ owners and apps platforms (app store), revenue generation can be properly structured to mirror the performance of the apps based on customer ratings.




