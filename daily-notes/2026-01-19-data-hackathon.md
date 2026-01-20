# Data Hackathon Project: Aadhar Data Anomaly Detection

## Project Overview

### Initial Understanding and Approach

So now after gaining some basic knowledge regarding AI/ML and dataset, I am thinking of seeing the dataset provided by DataHackathon of Aadhar data of some years with only numerical data like new enrollment, demographic update and biometric update type stuff log and using that type of data we have to identify technique to find anomality and fraud happening in some place or locality using the dataset of past years.

### The Problem Statement

So basically the problem statement stated that:

> Identify meaningful patterns, trends, anomalies, or predictive indicators and translate them into clear insights or solution frameworks that can support informed decision-making and system improvements.

Well in simple words basically they wanted us to use data analytics skill and find anomalous behavior in aadhar dataset provided by them using different technique we can find to improve both the accuracy and flag or try to stop such anomaly in future and also if possible explain them regarding the anomaly found using critical thinking and idea.

## Dataset Overview

Well the dataset is too large - it is around 30 lakh rows (4.93 million records to be exact) and 8 columns of data.

Well last time I didn't have any idea what exactly is the use of these dataset can be but now atleast I know a little. I know there is possibility of finding stuff using these dataset.

### Dataset Types Provided

Well based upon the dataset they provided they didn't gave us any full dataset about people information or anything they just gave us around 4.93 million UIDAI records of three different types:

- **Biometric authentication update**
- **Demographic authentication update**
- **Aadhaar enrolment data**

These are the three type of dataset they gave to us. Basically the problem was the dataset had a lot of noise and some dataset was not cleaned and even some contain duplicate dataset.

Also the data was only the age group divided and total provided for several months regarding how much people updated or changed or enrolled aadhaar data for different district and state.

So now the problem was to detect these anomalies based only and only upon number that too even raw and not very informative.

## Our Approach and Solution

### Team Structure

Well so we divided the work and my teammates are Aryan and Suri.

#### Team Members

**Aryan** is expert in analytics but he is more like follow rules and expect every other to do the same in case of project working.

**Suri** is like he got great real world experience and is actually great at making AI do the work for him.

#### Work Division Strategy

So we all three built and trained our own individual model and try different thing on our own and later we will add all our ideas in one that is just perfect and just like that we build our model and our date of submission is tomorrow so have to complete it before tomorrow and create report.

### Data Cleaning and Preprocessing

So for the problem we followed certain path to clean all the data and created specific pipeline and everything that now I will explain in order.

So as the data was loaded using the dataloader script we wrote that is basically cleaning all the data merging them consolidates all data of biometric demographic and enrollment dataset.

So basically its work was to perform data loading and making it ready to perform further analysis.

But before that we observed that dataset contains a lot of problem still.

#### Problems Identified in the Dataset

Like data had these problems:

##### 1. ✅ State Name Standardization

**Before:** 65 "states" due to variations like "West Bengal", "WEST BENGAL", "Westbengal"

**After:** Standardized to canonical names using master mapping table

**Fix Applied:**
- Created `DataValidator` class with state name mappings
- All state names converted to title case and trimmed
- Variations automatically merged (e.g., all West Bengal variants → "West Bengal")

##### 2. ✅ Date Continuity Validation

**Before:** Missing dates created gaps in time series, trends were broken

**After:** All date gaps identified and reported

**Fix Applied:**
- Validates complete date range from min to max
- Reports missing dates for investigation
- Enables proper time series filling if needed

##### 3. ✅ Geographic Hierarchy Consistency

**Before:** Districts and pincodes potentially in multiple states/districts

**After:** Full validation of state→district→pincode hierarchy

**Fix Applied:**
- Checks for districts appearing in multiple states
- Validates pincodes belong to single district
- Reports all hierarchy violations

##### 4. ✅ Robust Baseline Computation

**Before:** Mean corrupted 20-30x by outliers (5.3M spikes), making baselines useless

**After:** Separate baselines excluding top 1% for anomaly detection

**Fix Applied:**
- Full statistics (with outliers) for reporting
- Robust statistics (excluding top 1%) for baselines
- Corruption factor calculated (how much outliers skew data)
- Baselines used for anomaly detection, full data retained

##### 5. ✅ Functional Duplicate Detection

**Before:** Same location+date with multiple records (double counting)

**After:** All functional duplicates identified

**Fix Applied:**
- Checks for duplicate keys (date, state, district, pincode)
- Reports duplicate count and percentage
- Enables proper deduplication strategy

### Exploratory Data Analysis (EDA)

Well the next part was performing EDA analysis on project understanding the dataset for future model training and stuff.

Before that we also created a merged CSV using all three dataset to make it better and easy to work upon.

And for EDA we used several technique and plots to summarise the dataset and stuff.

### Anomaly Detection Implementation

Well next step comes out performing anomaly detection.

#### Anomaly Detection Module for Aadhar Data

Implements multiple anomaly detection methods:

1. **Statistical (Z-score)**
2. **Machine Learning (Isolation Forest)**
3. **Cross-dataset ratio analysis**

Using these top technique and several other we used and find out that based on the dataset we have these 3 are the most effective and are providing better result for model training.

As using only one model might not be a good idea so we thought why not use multiple and setup a connection and perform feature engineering to improve detection and find better result.

#### Initial Results

Well this actually worked and we got amazing results from the dataset around **98,000 anomalies detected** and that was very good result starting from around 5 million records we have narrowed it down to 98k anomalies that was great.

### Risk Scoring and Final Refinement

But we thought who would be interested in seeing 98k anomalies and even that much anomaly is not the best we can do with the dataset so we analyzed and read other technique and we finally came out with a technique of creating a **risk_scoring script** that basically use the most accurate and high accuracy providing model and based upon the result of each technique we used to find anomaly why not setup a final solution of ranking.

#### Method Weights

Based upon these 3 technique:

```python
METHOD_WEIGHTS = {
    "isolation_forest": 3,
    "cross_dataset": 4,
    "zscore": 1
}
```

As these are giving the best result we thought of choosing these three but even using these without thinking critically might not be a good idea so we also set up a weight for each technique based upon how we connect it with the result.

And we found amazing result by performing trial and error on this weight value.

#### Why Cross-Dataset Technique Was Crucial

As isolation forest provided good result also zscore but they were missing the most important thing that u cant compare two states only upon the anomaly they are giving.

Cause some state are big with high population while some are small with low population so comparing them based upon just model without thinking critically about the place and its locality might not be a good idea so we used **cross_dataset technique**.

It helped a lot before using this specific weightage our result was very like turned toward large district with high population but after using this technique we were able to detect state and district with less population but even higher level of anomaly cause normal module missed or ignore such value cause it is low.

#### Final Results

But our model based upon these above 3 technique created a final scoring list of around **900 or u can say top 900**.

Out of those selected we also used these weighted value to calculate their total score and based upon those which have most value to be marked as **high risk** and **medium** and similarly **low**.

Using this we narrowed the most high risk value to around **100 top** and even in those we used **top 5** of those 100 to make a special case builder and case plots for those specific 5 to make people see their result and we will be using those specific top 5 plots to show our final summary. Well we also have output plots explain dataset but we wanted to show others about the anomalies based upon our top 5 findings and maybe explain them and create solutions.

## Review of Team Members' Work

### Suri's Project Review

So I checked Suri project out and it was just great - model was well trained, structure was perfect and everything was just nice even the plot and cleaned dataset was great but his model was just giving of around 80k anomalous stuff but we dont want that, we want accuracy with result.

#### Improvements Made to Suri's Model

So I improved his model and setup some custom engineering feature using dataset and also I narrowed down the result to top 10 and even I plotted top 5 of them in case study format which will help in analyze the result and everything.

### Aryan's Project Review

Now is the time to analyze Aryan project and see what I can update in it and will it be of any use for our project. Lets see what we can do.

## Current Progress and Next Steps

Well I did some part in it, later will be done in evening now as they will help me out after sometime cause based upon my code and my current knowledge I did what I could have done. Well I could have done better but what can I say, I need some help. I am no expert in such stuff, well they are and they can help if they want to help so I will build the project with them. That way I will get knowledge from them and will enhance my knowledge of AI/ML and been able to observe their workflow might even help me maybe.

## Submission Timeline

Our date of submission is tomorrow so have to complete it before tomorrow and create report.
