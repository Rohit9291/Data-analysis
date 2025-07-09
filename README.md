# Data-analysis
To: Yulu Management
From: [Your Name/Consulting Company]
Date: July 9, 2025
Subject: Analysis of Factors Affecting Demand for Shared Electric Cycles in India

## 1. Executive Summary

This report presents an analysis of factors influencing the demand for Yulu's shared electric cycles in the Indian market. The objective was to identify significant variables predicting demand and assess how well these variables describe electric cycle demand. Key findings indicate that season, weather conditions, and working day status significantly impact demand. [cite_start]While the initial problem statement mentioned the American market [cite: 8][cite_start], the objective clearly specifies the Indian market [cite: 10, 11][cite_start], and the analysis was performed on the provided dataset which aligns with the Indian context based on company information[cite: 4, 5]. Recommendations are provided to optimize bike stock management based on these insights.

## 2. Problem Statement and Objectives

[cite_start]Yulu, a leading micro-mobility service provider in India, has experienced a considerable decline in revenues[cite: 4, 7]. To address this, Yulu contracted a consulting company to understand the factors affecting the demand for their shared electric cycles. The specific objectives were:
* [cite_start]To identify significant variables in predicting the demand for shared electric cycles in the Indian market[cite: 10].
* [cite_start]To evaluate how well these variables describe electric cycle demands[cite: 11].

## 3. Data Exploration and Preparation

[cite_start]The analysis utilized a dataset containing 10,886 entries across 12 columns[cite: 98].

### 3.1. Column Profiling

[cite_start]The dataset includes the following columns[cite: 75, 76, 77, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91]:
* `datetime`: Date and time of the rental.
* [cite_start]`season`: Season (1: spring, 2: summer, 3: fall, 4: winter)[cite: 76].
* [cite_start]`holiday`: Indicates if the day is a holiday (1) or not (0)[cite: 77].
* [cite_start]`workingday`: Indicates if the day is neither a weekend nor a holiday (1), otherwise (0)[cite: 79].
* `weather`:
    * [cite_start]1: Clear, Few clouds, partly cloudy [cite: 80]
    * [cite_start]2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist [cite: 81]
    * [cite_start]3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds [cite: 82, 83]
    * [cite_start]4: Heavy Rain + Ice Pellets + Thunderstorm + Mist, Snow + Fog [cite: 84]
* [cite_start]`temp`: Temperature in Celsius[cite: 85].
* [cite_start]`atemp`: Feeling temperature in Celsius[cite: 86].
* [cite_start]`humidity`: Humidity[cite: 87].
* [cite_start]`windspeed`: Wind speed[cite: 88].
* [cite_start]`casual`: Count of casual users[cite: 89].
* [cite_start]`registered`: Count of registered users[cite: 90].
* [cite_start]`count`: Total count of rental bikes, including both casual and registered users[cite: 91].

### 3.2. Data Quality Checks

* [cite_start]**Null Values**: No null values were found in any of the columns[cite: 153, 154, 155, 156, 157, 158, 159, 160, 161, 162, 163, 164].
* [cite_start]**Duplicate Values**: No duplicate rows were identified in the dataset[cite: 170].
* **Unique Values and Value Counts for Categorical Variables**:
    * [cite_start]**Season**: Has four unique values (1, 2, 3, 4) with counts of 2686 (spring), 2733 (summer), 2733 (fall), and 2734 (winter) respectively[cite: 184, 185, 186, 187, 188, 189, 190, 191, 192, 193].
    * [cite_start]**Holiday**: Has two unique values (0, 1) with 10,575 non-holidays and 311 holidays[cite: 196, 197, 198, 199, 200, 201].
    * [cite_start]**Workingday**: Has two unique values (0, 1) with 7,412 working days and 3,474 non-working days[cite: 204, 205, 206, 207, 208, 209].
    * [cite_start]**Weather**: Has four unique values (1, 2, 3, 4) with counts of 7,192 (Clear), 2,834 (Mist), 859 (Light Snow/Rain), and 1 (Heavy Rain/Snow)[cite: 212, 213, 214, 215, 216, 217, 218, 219, 220, 221].

### 3.3. Correlation Analysis

[cite_start]A correlation matrix was generated for numerical columns[cite: 225, 235].
* [cite_start]`atemp` and `temp` are highly correlated (0.98), indicating multicollinearity[cite: 235].
* [cite_start]`casual` and `registered` users are highly correlated with `count` (0.69 and 0.97 respectively)[cite: 235]. Since `count` is the sum of `casual` and `registered`, these columns represent redundant information for predicting `count`.
* [cite_start]Based on the high correlation, `atemp`, `casual`, and `registered` columns were dropped from the dataset to avoid multicollinearity and redundancy[cite: 310].

### 3.4. Outlier Detection and Distribution of 'count'

* [cite_start]Box plots were used to visualize outliers in `count` against categorical variables (`season`, `holiday`, `workingday`, `weather`)[cite: 325].
* [cite_start]The distribution of the `count` column was found to be right-skewed, indicating a non-normal distribution with many outliers at higher values[cite: 368, 371, 547].
* [cite_start]Applying a log transformation to the `count` column made its distribution more symmetrical and reduced the visual impact of outliers, suggesting it could be a useful transformation for modeling[cite: 415, 418].

## 4. Detailed Analysis

### 4.1. Demand by Workingday and Holiday

* **Workingday**:
    * [cite_start]On working days (`workingday` = 1), the average bike count is approximately 193, with a standard deviation of 184.5[cite: 456].
    * [cite_start]On non-working days (`workingday` = 0), the average bike count is approximately 188.5, with a standard deviation of 173.7[cite: 455].
* **Holiday**:
    * [cite_start]On non-holidays (`holiday` = 0), the average bike count is approximately 191.7, with a standard deviation of 181.5[cite: 464].
    * [cite_start]On holidays (`holiday` = 1), the average bike count is approximately 185.9, with a standard deviation of 168.3[cite: 466].

### 4.2. Demand by Season

* [cite_start]**Season 1 (Spring)**: Lowest average demand at approximately 116 bikes, with a standard deviation of 125[cite: 469].
* [cite_start]**Season 2 (Summer)**: Average demand of approximately 215 bikes[cite: 469].
* [cite_start]**Season 3 (Fall)**: Highest average demand at approximately 234 bikes, with a standard deviation of 197[cite: 469, 551].
* [cite_start]**Season 4 (Winter)**: Average demand of approximately 199 bikes[cite: 469].

### 4.3. Demand by Weather

* [cite_start]**Weather 1 (Clear)**: Highest average demand at approximately 205 bikes[cite: 479].
* [cite_start]**Weather 2 (Mist)**: Average demand of approximately 179 bikes[cite: 479].
* [cite_start]**Weather 3 (Light Snow/Rain)**: Lowest average demand at approximately 119 bikes[cite: 479].
* [cite_start]**Weather 4 (Heavy Rain/Snow)**: Only one instance with a count of 164[cite: 479]. [cite_start]This extreme weather condition was removed for further ANOVA testing due to its minimal data points[cite: 510].

## 5. Hypothesis Testing

[cite_start]A significance level (alpha) of 0.05 was used for all hypothesis tests[cite: 493].

### 5.1. Weekday vs. Weekend Demand

* [cite_start]**Null Hypothesis ($H_0$)**: The demand for bikes on weekdays is greater than or similar to the demand on weekends ($\mu_1 \ge \mu_2$)[cite: 486, 490].
* [cite_start]**Alternative Hypothesis ($H_a$)**: The demand for bikes on weekdays is less than the demand on weekends ($\mu_1 < \mu_2$)[cite: 487, 491].
* [cite_start]**Test**: Independent t-test (due to two samples)[cite: 495, 500].
* [cite_start]**P-value**: 0.4269[cite: 502].
* [cite_start]**Conclusion**: Since the p-value (0.4269) is greater than the significance level (0.05), we fail to reject the null hypothesis[cite: 508]. This implies that the demand for bikes on weekdays is greater than or similar to the demand on weekends.

### 5.2. Demand Across Different Weather Conditions

* [cite_start]**Null Hypothesis ($H_0$)**: The average number of bike rides in different weather conditions are equal[cite: 511].
* [cite_start]**Alternative Hypothesis ($H_a$)**: The average number of bike rides in different weather conditions are not equal[cite: 512].
* **Assumptions for ANOVA**:
    * **Normality (Shapiro-Wilk's test)**:
        * [cite_start]$H_0$: Count follows normal distribution[cite: 532].
        * [cite_start]$H_a$: Count doesn't follow normal distribution[cite: 534].
        * [cite_start]P-value: $2.34 \times 10^{-53}$[cite: 538].
        * **Conclusion**: The p-value is less than alpha, so we reject the null hypothesis. [cite_start]The `count` data does not follow a normal distribution[cite: 538].
    * **Homogeneity of Variance (Levene's test)**:
        * [cite_start]$H_0$: All the count variances are equal[cite: 539].
        * [cite_start]$H_a$: At least one variance is different from the rest[cite: 539].
        * [cite_start]P-value: 0.0325[cite: 539].
        * **Conclusion**: The p-value is less than alpha, so we reject the null hypothesis. [cite_start]The variances are not equal across different weather conditions[cite: 539].
* **ANOVA Test (despite assumption violations)**:
    * [cite_start]Test: One-way ANOVA test[cite: 540].
    * [cite_start]P-value: 0.0048[cite: 540].
    * [cite_start]**Conclusion**: Since the p-value (0.0048) is less than the significance level (0.05), we reject the null hypothesis[cite: 540]. [cite_start]This indicates that the demand for bicycles on rent differs significantly under different weather conditions[cite: 543].

## 6. Insights and Recommendations

### 6.1. Key Insights from Analysis

* [cite_start]The number of bikes rented on **weekdays is comparatively higher than on weekends**[cite: 541].
* [cite_start]The number of bikes rented on **regular days is comparatively higher than on holidays**[cite: 542].
* [cite_start]The demand for bicycles on rent **differs significantly under different weather conditions**[cite: 543].
* [cite_start]The demand for bicycles on rent is **different during different seasons**[cite: 544].
* [cite_start]The distribution of the 'count' column is right-skewed and not normal[cite: 546, 547].

### 6.2. Generic Recommendations

Based on the analysis, Yulu should consider the following recommendations for managing bike stock:

* [cite_start]**Weekdays and Regular Days**: Maintain higher bike stocks during weekdays and regular days, as demand is typically higher during these periods[cite: 549, 550].
* [cite_start]**Season 3 (Fall)**: Plan for increased bike availability during Season 3 (Fall), as this season shows the highest average demand for rentals[cite: 551].
* [cite_start]**Weather Condition 1 (Clear)**: Ensure ample bike availability during clear weather conditions, as this weather type correlates with the highest demand[cite: 551].
* [cite_start]**Dynamic Stock Management**: Implement a dynamic stock management system that considers the day of the week, holiday status, season, and real-time weather conditions to optimize bike allocation and availability at Yulu zones[cite: 6, 551]. This will help maximize revenue by meeting user demand effectively.
