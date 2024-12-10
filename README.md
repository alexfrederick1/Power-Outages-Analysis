# Power Outages Analysis
Analysis of power outages for DSC 80 at UCSD

By Alex Frederick and Sam Ouyang


# Introduction


In this project, we analyzed a dataset about power outages in the United States. The dataset includes information about the climate, electricity consumption, and economic characteristics of the locations of outages.

        Need to decide what one question we want to say it's centered around here. what specifically about severe weather? maybe come back to this after finishing the whole thing

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

# Assessment of Missingness

# Hypothesis Testing


