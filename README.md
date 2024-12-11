# Weathering the Storm
An in-depth analysis of power outages for DSC 80 at UCSD

By Alex Frederick and Sam Ouyang


# Introduction


In this project, we analyzed a dataset about power outages in the United States. The dataset includes information about the climate, electricity consumption, and economic characteristics of the locations of outages.

Our analyses are centered around the following question: **How do different types of severe weather impact the severity of power outages?** We defined "severe weather" as extreme weather events, mostly storms.



This data is extremely relevant to everyone, as power outages can happen everywhere. The data includes power outages in different states, regions, and climates. We hope that you will learn something from this about what you can do to minimize the risk of experiencing power outages. Everyone should take an interest in our question about severe weather. Every climate on Earth is at risk of destruction caused by extreme weather. Types of severe weather differ by climate, and it's important for people to understand the risks that their local weather may bring.


The dataset has 1534 rows and 57 columns. The dataset contains a lot of valuable information in all of these columns, but will only keep 11 columns that are relevant to our question about severe weather. Those columns are listed below with a description of each.  


**YEAR:** Indicates the year when the outage event occurred

**MONTH:** Indicates the month when the outage event occurred

**POSTAL.CODE:** Represents the postal code of the U.S. states

**CLIMATE.REGION:** U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)

**CLIMATE.CATEGORY:** This represents the climate episodes corresponding to the years. The categories—“Warm”, “Cold” or “Normal” episodes of the climate are based on a threshold of ± 0.5 °C for the Oceanic Niño Index (ONI)

**CAUSE.CATEGORY:** Categories of all the events causing the major power outages

**CAUSE.CATEGORY.DETAIL:** Detailed description of the event categories causing the major power outages

**OUTAGE.DURATION:** Duration of outage events (in minutes)

**CUSTOMERS.AFFECTED:** Number of customers affected by the power outage event

**POPULATION:** Population in the U.S. state in a year

**TOTAL.CUSTOMERS:** Annual number of total customers served in the U.S. state

&nbsp;&nbsp;&nbsp;

# Data Cleaning and Exploratory Data Analysis


&nbsp;&nbsp;&nbsp;

**Data Cleaning**

&nbsp;&nbsp;&nbsp;

Before beginning to analyze the data, there were several steps of cleaning that had to happen. The steps below are what we did to clean the dataset in order.

1. Removed all columns besides the 11 listed above that are applicable to our analysis. As mentioned previously, the original dataset contained 57 columns, so we dropped those that we did not plan to use. Removing this columns makes our analysis more narrow and focused on the question that we are trying to answer. 
   
2. Dropped all rows in which the value of the column CAUSE.CATEGORY was not "severe weather." This was done because our question is specifically about severe weather. We also dropped the column CAUSE.CATEGORY because it was no longer needed, as CAUSE.CATEGORY.DETAIL is more descriptive. This step makes our analyses more clear.

3. Classified similar values of the variable CAUSE.CATEGORY.DETAIL together as one under the new variable WEATHER.TYPE. Many unique values of CAUSE.CATEGORY.DETAIL are redundant, so we combined them to make that column easier to interpret. For example, if CAUSE.CATEGORY.DETAIL contained any of the terms "heavy wind," "wind/rain," or "wind," we reclassified that value of CAUSE.CATEGORY.DETAIL as "wind" under the new variable WEATHER.TYPE.

4. Labeled non-weather-related values of CAUSE.CATEGORY.DETAIL as NaN. We did this because those values are irrelevant to our analysis. Causes such as "fog," "earthquake," and "fire" do not fit our definiton of severe weather. This steps narrows the scope of our analyses by excluding values that are not revelant.

5. Dropped rows in which the value of WEATHER.TYPE is NaN. These rows have an NaN value because  WEATHER.TYPE is not a relevant, weather-related cause. Again, this step helps us eliminate unwanted data, making future analyses easier to conduct.

6. Converted all "unknown" values of WEATHER.TYPE back to NaN. We keep unknown values because there may be a reason they are unknown that our analysis could uncover. This is different from NaN values that are a result of non-weather-related causes. These should be excluded and dropped because they are outside the scope of our analysis.

&nbsp;&nbsp;&nbsp;

Here is the head of our cleaned DataFrame:

<img width="1142" alt="Screenshot 2024-12-10 at 7 59 16 PM" src="https://github.com/user-attachments/assets/977c5d46-a6b9-427e-aa2f-bc47cac4180d">

&nbsp;&nbsp;&nbsp;


**Univariate Analysis**

&nbsp;&nbsp;&nbsp;
  
![image](https://github.com/user-attachments/assets/ba0081f1-2b62-4f67-a7d6-7c41ca0a6e47)


This pie chart shows the distriubtion of causes of power outages by severe weather type. We can see from it that the most common form of severe weather in causing power outages is thunderstorms, followed by winter storms, wind storms, and hurricanes, respectively. There are several fairly uncommon types that make up a small portion of the pie.

&nbsp;&nbsp;&nbsp;


![image](https://github.com/user-attachments/assets/5f226bf3-54f1-4afc-8be3-3eb70f90ac75)

This histogram depicts the distribution of the number of customers affected by power outages. We can see in it that the most common bin is the one from 50,000-100,000, followed by the bin from 100,000-150,000, giving us a good sense of the number of people typically impacted by any given power outage. The histogram is skewed right, as most values are in the bins on the left, and very few are in the bins far on the right, showing that very rarely, power outages affect more than 1 million people.

&nbsp;&nbsp;&nbsp;


**Bivariate Analysis**

![image](https://github.com/user-attachments/assets/b18e97ee-5fbf-4f09-b8ba-768fe26954f2)


&nbsp;&nbsp;&nbsp;

This line chart visualizes the average outage duration in days by year. The general downward trend indicates that the average power outage duration has decreased over time. This is an interesting observation that we plan to explore further.


&nbsp;&nbsp;&nbsp;

**Interesting Aggregates**

<img width="620" alt="Screenshot 2024-12-09 at 10 36 02 PM" src="https://github.com/user-attachments/assets/f7e96396-b0e2-4143-9dda-0bf6d7e66295">

This pivot table shows the mean and median of the counts of customers affected by weather type. The mean is greater than the median for all weather types, indicating that there are likely several high outliers in which a huge number of customers are affected.

&nbsp;&nbsp;&nbsp;

<img width="545" alt="Screenshot 2024-12-09 at 10 42 12 PM" src="https://github.com/user-attachments/assets/3bb01995-a53b-49c2-a2ab-b3430aa0d1b0">

This pivot table highlights a comparison between the mean and median power outage duration by weather type. Like the previous pivot table, we see that the mean is greater than the median for all weather types, indicating that there are likely some very long durations skewing the dataset.

&nbsp;&nbsp;&nbsp;

# Assessment of Missingness

&nbsp;&nbsp;&nbsp;

**NMAR Analysis**

The following six columns in our dataset have at least one missing value: MONTH, CLIMATE.REGION, CLIMATE.CATEGORY, OUTAGE.DURATION, CUSTOMERS.AFFECTED WEATHER.TYPE. Of these, the missigness in the column CUSTOMERS.AFFECTED may be NMAR. Missing values in CUSTOMERS.AFFECTED could be influenced by the potential values themselves. For example, smaller outages that affect fewer customers might not have recorded customer impact data, while larger outages might be more thoroughly documented and reported. This could lead to missingness that depends on the values of the data themselves, the magnitude of the outage. That would be NMAR missingness, which is missingness that depends on the values of the missing data themselves.

To make this missingness MAR, we could find data that has the potential to explain the missingness. This could happen through analysis of other columns in our dataset and their relationships with CUSTOMERS.AFFECTED.

&nbsp;&nbsp;&nbsp;

**Missingness Dependency**

&nbsp;&nbsp;&nbsp;

To determine the missigness mechanism of the missing values in the column CUSTOMERS.AFFECTED, we ran permutation tests between CUSTOMERS.AFFECTED and several other columns. We found that the missingness of CUSTOMERS.AFFECTED does depend on OUTAGE.DURATION and does not depend on TOTAL.CUSTOMERS.

The permutation test we ran against OUTAGE.DURATION returned an observed test statistic of 0.1479, indicating a relatively high absolute correlation for missingness of CUSTOMERS.AFFECTED and OUTAGE.DURATION. The p-value for our permutation test was 0.001, so we reject the null hypothesis that CUSTOMERS.AFFECTED is not dependent on OUTAGE.DURATION at the 0.01 significance level.

&nbsp;&nbsp;&nbsp;

This plot depicts the distribution of OUTAGE.DURATION for when CUSTOMERS.AFFECTED is present and for when it is missing separately. We can clearly that the distributions are very different. The one with CUSTOMERS.AFFECTED missing has a much lower mean and less extremely high values. This leads us to believe that CUSTOMERS.AFFECTED's missingness is dependent on OUTAGE.DURATION, as when an outage has a long duration, it is more likely to be reported and therefore more likely to have a value in the CUSTOMERS.AFFECTED column.

&nbsp;&nbsp;&nbsp;

<img width="1244" alt="Screenshot 2024-12-10 at 10 20 16 PM" src="https://github.com/user-attachments/assets/d101e563-80f4-468b-9320-cd69e7865266">

&nbsp;&nbsp;&nbsp;

The permutation test that we ran against TOTAL.CUSTOMERS returned an observed test statistic of 0.0778, which is far lower than that ran against OUTAGE.DURATION. The p-value of this permutation test was 0.043, which is low, but at the 0.01 significance level, we still failed to reject the null hypothesis that CUSTOMERS.AFFECTED is not dependent on TOTAL.CUSTOMERS.

&nbsp;&nbsp;&nbsp;

This plot depicts the distribution of TOTAL.CUSTOMERS for when CUSTOMERS.AFFECTED is present and for when it is missing separately. The distributions appear fairly similar. The distribution when CUSTOMERS.AFFECTED is present appears to have slightly less spread, but overall, they appear very simialr. This, along with the p-value result, leads us to believe that CUSTOMERS.AFFECTED's missingness is not dependent on TOTAL.CUSTOMERS.

<img width="1247" alt="Screenshot 2024-12-10 at 10 17 37 PM" src="https://github.com/user-attachments/assets/eab38675-0688-45c8-99f6-ce26eee46125">

&nbsp;&nbsp;&nbsp;


# Hypothesis Testing

&nbsp;&nbsp;&nbsp;

The question that we would like to answer through a permutation test is the following: **Have power outage durations improved over time?**

&nbsp;&nbsp;&nbsp;

Null hypothesis: Power outage durations have not improved over time.
Alternative hypothesis: The distribution of power outage durations has improved over time. 

&nbsp;&nbsp;&nbsp;

To test these hypotheses, we split the data into four groups based on the YEAR variable. The four groups are of roughly equal sizes, as we calculated the interquartile range and assigned data to groups based on their placement in one of the four IQR groups. to create the groups. The first group is from before 2006, the second is from 2006-2010, the thirs is from 2010-2012, and the fourth is from after 2012.

&nbsp;&nbsp;&nbsp;

The columns from the dataset that this question requires are OUTAGE.DURATION and YEAR. Additionally, is uses a new column called 'Year Group.'

&nbsp;&nbsp;&nbsp;

The test statistic that we are using is the proportion of shorter durations, which falls under the umbrella of difference of proportions. When comparing two year groups, we are looking at what proportion of power outages have shorter durations in the more recent year group than the older year group. The significance level is 0.01. We chose this low significance level because we want to minimize risk of incorrectly rejecting the null hypothesis.

&nbsp;&nbsp;&nbsp;

Our permutation test runs 6 different permutation tests between all possible different year groups. Here are the results:

Before 2006 vs 2006-2010: Observed Stat = 0.4716, P-value = 0.1612

Before 2006 vs 2010-2012: Observed Stat = 0.4268, P-value = 0.0111

Before 2006 vs After 2012: Observed Stat = 0.3248, P-value = 0.0000

2006-2010 vs 2010-2012: Observed Stat = 0.4484, P-value = 0.0460

2006-2010 vs After 2012: Observed Stat = 0.3457, P-value = 0.0000

2010-2012 vs After 2012: Observed Stat = 0.3984, P-value = 0.0014


&nbsp;&nbsp;&nbsp;

These resulting p-values indicate that we reject the null hypothesis for the following three tests: Before 2006 vs After 2012, 2006-2010 vs After 2012, and 2010-2012 vs After 2012.
Meanwhile, we fail to reject the null hypothesis for the following three tests: Before 2006 vs 2006-2010, Before 2006 vs 2010-2012, 2006-2010 vs 2010-2012.

&nbsp;&nbsp;&nbsp;

From this, we can conclude that power outage durations have generally improved over time. The three groups in which we rejected the null hypothesis included the 'After 2012' group against an older group. This leads us to believe that power outage durations did not improve significantly in the year from 2006-2012, but they made major improvements after 2012. These conclusions are extremely valuable for answering our question about power outage durations improving over time, as they give us insight into specific time frames in the improvement of outage durations. 

&nbsp;&nbsp;&nbsp;

# Framing a Prediction Model

&nbsp;&nbsp;&nbsp;

Our prediction problem is to predict the type of severe weather that causes a power outage. We are building a classifier, as our goal is to predict a categorical variable based on the available data. Specifically, we are trying to determine which type of severe weather is occurring at the time of the power outage based on the features in our dataset.

&nbsp;&nbsp;&nbsp;

This is a multiclass classification problem, since there are multiple possible classes or types of severe weather that could cause a power outage. Each weather type, such as wind storm, thunderstorm, winter storm, is a distinct category that we want to predict.

&nbsp;&nbsp;&nbsp;

The response variable we are predicting is the 'WEATHER.TYPE' column, which indicates the type of severe weather associated with each power outage. We chose this variable because identifying the cause of power outages based on weather type can help people better prepare for and respond to different weather events. This can help minimize outages and increase safety in the event of outages.

&nbsp;&nbsp;&nbsp;

For evaluating our model, we will use the accuracy metric, which is the proportion of correct predictions made by the classifier. Accuracy may not always capture the full picture, especially if the classes are imbalanced (if some weather types are much more frequent than others). If we have issues with class imbalance, we could consider using other metrics such as F1-score or confusion matrices, which provide more insights into how the model is performing with respect to each class. 

&nbsp;&nbsp;&nbsp;

# Baseline Model

&nbsp;&nbsp;&nbsp;

This is a multiclass classifier model aimed at predicting the type of severe weather (WEATHER.TYPE) causing a power outage using a DecisionTreeClassifier. The model includes the following features, two of which are quantitative and one of which is nominal:

CLIMATE.CATEGORY (Nominal): A categorical feature that is encoded using OneHotEncoding.
OUTAGE.DURATION.IMPUTED (Quantitative): The imputed outage duration, used as-is.
TOTAL.CUSTOMERS (Quantitative): The total number of customers affected by the outage, used as-is.

The target variable is WEATHER.TYPE, which has seven possible categories.

**Encoding Approach**

OneHotEncoding is applied to the CLIMATE.CATEGORY feature.
OUTAGE.DURATION.IMPUTED and TOTAL.CUSTOMERS are numerical and don't require further encoding.
Model Performance

The model achieves an accuracy of 48.89% on the test set. Given that this is a multiclass classifier with seven options, an accuracy around 50% is not entirely unexpected, especially when predicting multiple categories. A random guess would likely achieve around 14% accuracy (1/7), so 48.89% shows that the model is learning meaningful patterns from the data.

**Is the Model "Good"?**

An accuracy of 48.89% is decent for a multiclass classification problem, but it suggests there's room for improvement.
This score indicates the model is significantly better than random guessing. Further improvements could come from additional feature engineering, hyperparameter tuning, or using a more complex model.
It's important to consider other metrics like precision, recall, or F1-score, especially if some weather types are more important to predict accurately.
In conclusion, while the model's performance is not ideal, it's a reasonable starting point, and there are clear opportunities for improvement.

&nbsp;&nbsp;&nbsp;

# Final Model

&nbsp;&nbsp;&nbsp;

In this final model, we included a set of features designed to capture various factors influencing power outages:

MONTH (Nominal): The month of the year is important for accounting for seasonal variations in weather patterns. We encoded this feature using OneHotEncoding to represent different seasons as separate categories.
POSTAL.CODE (Nominal): The postal code helps capture regional weather patterns that might affect power outages differently across locations. It is encoded using OneHotEncoding.
CUSTOMERS.AFFECTED (Quantitative): This feature reflects the scale of an outage. We binarized it using a Binarizer to distinguish between large and small outages, specifically focusing on outages that affect more than 1 million customers.
POPULATION (Quantitative): Population size gives context to the outage’s scale and potential impact. It is kept as a continuous feature.

The algorithm used is a DecisionTreeClassifier, which is well-suited for handling both categorical and numerical features. It works by splitting data into smaller homogeneous subsets based on feature values, which is useful for understanding how different factors affect the type of severe weather.

**Performed GridSearchCV to optimize hyperparameters:**

max_depth: Controls the maximum depth of the tree, helping prevent overfitting by limiting the number of splits.
min_samples_split: Determines the minimum number of samples required to split an internal node, which helps avoid overfitting by ensuring nodes are split only when there are enough samples.
criterion: The function to measure the quality of a split. We used both entropy (information gain) and gini (impurity) and selected the best one.

After performing grid search, the model achieved a best cross-validation score of 69.28% and a test set accuracy of 63.78%. These results are a significant improvement from the baseline model's 48.89% accuracy. The addition of more relevant features, like seasonality, regional factors, and customer impact, alongside hyperparameter tuning, helped the model better capture the factors influencing power outages, leading to a more accurate prediction.

**Conclusion**
The final model improved over the baseline by incorporating features that better represent the key factors affecting power outages. Hyperparameter tuning further enhanced the model's performance, resulting in a stronger prediction ability.

&nbsp;&nbsp;&nbsp;

# Fairness Analysis

&nbsp;&nbsp;&nbsp;

For this fairness analysis, the two groups we are comparing are the different types of severe weather predicted by our model. These groups are the following:

Group X: The weather categories in the dataset: thunderstorm, winter storm, wind storm, hurricanes, heatwave, tornadoes, and flooding.
Group Y: The accuracy of predictions made by the model for each weather category.

The evaluation metric we used is accuracy. Accuracy is appropriate in this context because it accounts for how well the model predicts each type of severe weather. Given that we are dealing with a multiclass classification problem, accuracy allows us to compare how the model performs across all weather types.

Null Hypothesis: The model is fair. Its accuracy in predicting each type of severe weather is roughly the same, and any observed differences are due to random chance.

Alternative Hypothesis: The model is unfair. Its accuracy in predicting each type of severe weather varies significantly between the different weather categories.

The test statistic we used is the accuracy per class for each weather category, and we performed a permutation test to compare the observed accuracy to the distribution of accuracies obtained by randomizing the labels.

We set the significance level at 0.05, a standard value for hypothesis testing that includes some risk of Type I errors.
These are the p-values for each weather category:

Flooding: p = 1.0

Hurricanes: p = 0.86

Thunderstorm: p = 0.384

Tornadoes: p = 1.0

Wind Storm: p = 0.977

Winter Storm: p = 0.175

Since all p-values are greater than 0.05, we fail to reject the null hypothesis for each weather type. This indicates that the accuracy of the model does not significantly vary between the different categories of severe weather.
