# Weathering the Storm
An in-depth analysis of power outages for DSC 80 at UCSD

By Alex Frederick and Sam Ouyang


# Introduction


In this project, we analyzed a dataset about power outages in the United States. The dataset includes information about the climate, electricity consumption, and economic characteristics of the locations of outages.

        Need to decide what one question we want to say it's centered around here. what specifically about severe weather? maybe come back to this after finishing the whole thing. say we define severe weather as an extreme weather event that is a storm (because we dropped random stuff like earthquakes and fires).

This data is extremely relevant to everyone, as power outages can happen everywhere. The data includes power outages in different states, regions, and climates. We hope that you will learn something from this about what you can do to minimize the risk of experiencing power outages.

        add why they should care about our question specifically

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

         

# Data Cleaning and Exploratory Data Analysis

**Data Cleaning**

Before beginning to analyze the data, there were several steps of cleaning that had to happen. The steps below are what we did to clean the dataset in order.

1. Removed all columns besides the 11 that are applicable to our analysis. As mentioned previously, the original dataset contained 57 columns, so we dropped those that we did not plan to use.
   
2. Dropped all rows in which the value of the column CAUSE.CATEGORY was not "severe weather." This was done because our question is specifically about severe weather.

3. Classified similar values of the variable CAUSE.CATEGORY.DETAIL together as one under the new variable WEATHER.TYPE. Many unique values of CAUSE.CATEGORY.DETAIL are redundant, so we combined them to make that column easier to interpret. For example, if CAUSE.CATEGORY.DETAIL contained any of the terms "heavy wind," "wind/rain," or "wind," we reclassified that value of CAUSE.CATEGORY.DETAIL as "wind" under the new variable WEATHER.TYPE.

4. Labeled non-weather-related values of CAUSE.CATEGORY.DETAIL as NaN. We did this because those values are irrelevant to our analysis. Causes such as "fog," "earthquake," and "fire" do not fit our definiton of severe weather.

5. Dropped rows in which the value of WEATHER.TYPE is NaN. These rows have an NaN value because  WEATHER.TYPE is not a relevant, weather-related cause.

6. Converted all "unknown" values of WEATHER.TYPE back to NaN. We keep unknown values because there may be a reason they are unknown that our analysis could uncover. This is different from NaN values that are a result of non-weather-related causes. These should be excluded and dropped because they are outside the scope of our analysis.

               still need to do this: show the head of your cleaned DataFrame (see Part 2: Report for instructions).

**Univariate Analysis**

    
  
![image](https://github.com/user-attachments/assets/ba0081f1-2b62-4f67-a7d6-7c41ca0a6e47)


This pie chart shows the distriubtion of causes of power outages by severe weather type. We can see from it that the most common form of severe weather in causing power outages is thunderstorms, followed by winter storms, wind storms, and hurricanes, respectively. There are several fairly uncommon types that make up a small portion of the pie.


![image](https://github.com/user-attachments/assets/5f226bf3-54f1-4afc-8be3-3eb70f90ac75)

This histogram depicts the distribution of the number of customers affected by power outages. We can see in it that the most common bin is the one from 50,000-100,000, followed by the bin from 100,000-150,000, giving us a good sense of the number of people typically impacted by any given power outage. The histogram is skewed right, as most values are in the bins on the left, and very few are in the bins far on the right, showing that very rarely, power outages affect more than 1 million people.


**Bivariate Analysis**

![image](https://github.com/user-attachments/assets/b18e97ee-5fbf-4f09-b8ba-768fe26954f2)


This line chart visualizes the average outage duration in days by year. The general downward trend indicates that the average power outage duration has decreased over time. This is an interesting observation that we plan to explore further.


**Interesting Aggregates**

<img width="620" alt="Screenshot 2024-12-09 at 10 36 02 PM" src="https://github.com/user-attachments/assets/f7e96396-b0e2-4143-9dda-0bf6d7e66295">

This pivot table shows the mean and median of the counts of customers affected by weather type. The mean is greater than the median for all weather types, indicating that there are likely several high outliers in which a huge number of customers are affected.

<img width="545" alt="Screenshot 2024-12-09 at 10 42 12 PM" src="https://github.com/user-attachments/assets/3bb01995-a53b-49c2-a2ab-b3430aa0d1b0">

This pivot table highlights a comparison between the mean and median power outage duration by weather type. Like the previous pivot table, we see that the mean is greater than the median for all weather types, indicating that there are likely some very long durations skewing the dataset.

# Assessment of Missingness

# Hypothesis Testing

# Framing a Prediction Model

# Baseline Model

# Final Model

# Fairness Analysis

