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

The following six columns in our dataset have at least one missing value: MONTH, CLIMATE.REGION, CLIMATE.CATEGORY, OUTAGE.DURATION, CUSTOMERS.AFFECTED WEATHER.TYPE. Of these, the missigness in the column CUSTOMERS.AFFECTED may be NMAR. Missing values in CUSTOMERS.AFFECTED could be influenced by the potential values themselves. For example, smaller outages that affect fewer customers might not have recorded customer impact data, while larger outages might be more thoroughly documented and reported. This could lead to missingness that depends on the magnitude of the outage, tying back to the value of the missing data itself. 

&nbsp;&nbsp;&nbsp;

**Missingness Dependency**

&nbsp;&nbsp;&nbsp;

# Hypothesis Testing

# Framing a Prediction Model

# Baseline Model

# Final Model

# Fairness Analysis

