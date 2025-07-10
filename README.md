# Data Analysis: Factors Affecting Demand for Shared Electric Cycles in India

**To:** Bike\_sharing\_company Management
**From:** \[Your Name / Consulting Company]
**Date:** July 9, 2025
**Subject:** Analysis of Factors Affecting Demand for Shared Electric Cycles in India

---

## 1. Executive Summary

This report analyzes the factors influencing demand for Bike\_sharing\_company’s shared electric cycles in the Indian market. The primary objective was to identify significant variables that predict demand and to evaluate how effectively these variables describe rental behavior.

Key findings indicate that **season**, **weather conditions**, and **working day status** significantly influence demand. While the original dataset description referenced the U.S. market, the analysis is tailored to India, consistent with contextual clues and company information. Recommendations are provided to help optimize bike inventory management.

---

## 2. Problem Statement and Objectives

Bike\_sharing\_company, a leading micro-mobility service provider in India, has experienced a notable decline in revenues. To investigate this, the company engaged a consulting firm to explore demand-driving factors for its electric cycles.

**Objectives:**

* Identify significant predictors of demand for shared electric cycles in India.
* Assess how well these predictors explain fluctuations in demand.

---

## 3. Data Exploration and Preparation

The dataset includes **10,886 records across 12 columns**, capturing temporal, environmental, and user activity information.

### 3.1 Column Profiling

Key columns:

* `datetime`: Date and time of rental
* `season`: 1 - Spring, 2 - Summer, 3 - Fall, 4 - Winter
* `holiday`: 1 if the day is a holiday, else 0
* `workingday`: 1 if neither weekend nor holiday
* `weather`:

  * 1: Clear/Few clouds
  * 2: Mist/Cloudy
  * 3: Light snow/rain
  * 4: Heavy rain/snow
* `temp`, `atemp`: Actual and "feels like" temperature (°C)
* `humidity`, `windspeed`: Atmospheric conditions
* `casual`, `registered`, `count`: Usage metrics

### 3.2 Data Quality Checks

* **Null Values**: None found
* **Duplicates**: None found
* **Categorical Value Distribution**:

  * **Season**: Evenly distributed across four seasons
  * **Holiday**: \~97% non-holidays
  * **Workingday**: \~68% working days
  * **Weather**: Majority in clear or misty conditions

### 3.3 Correlation Analysis

* Strong correlation between `temp` and `atemp` (0.98)
* `count` highly correlates with both `casual` (0.69) and `registered` (0.97)
* To reduce redundancy and multicollinearity, `atemp`, `casual`, and `registered` were removed from further analysis.

### 3.4 Outlier Detection & Distribution

* **Outliers**: Present in `count`, especially during high-demand days
* **Skewness**: `count` is right-skewed
* **Transformation**: Log transformation reduced skewness and made data more symmetric

---

## 4. Detailed Analysis

### 4.1 Demand by Working Day and Holiday

| Category        | Average Count | Std. Deviation |
| --------------- | ------------- | -------------- |
| Working Day     | 193           | 184.5          |
| Non-working Day | 188.5         | 173.7          |
| Holiday         | 185.9         | 168.3          |
| Non-Holiday     | 191.7         | 181.5          |

### 4.2 Demand by Season

* **Spring (1)**: Lowest average (116)
* **Summer (2)**: 215
* **Fall (3)**: Highest average (234)
* **Winter (4)**: 199

### 4.3 Demand by Weather Condition

* **Clear (1)**: Highest demand (\~205)
* **Mist (2)**: \~179
* **Light Rain/Snow (3)**: \~119
* **Heavy Rain/Snow (4)**: Only one data point (excluded in statistical tests)

---

## 5. Hypothesis Testing

### 5.1 Weekday vs. Weekend Demand

* **Null Hypothesis (\$H\_0\$)**: Weekday demand ≥ Weekend demand
* **Test**: Independent t-test
* **P-value**: 0.4269
* **Conclusion**: Fail to reject \$H\_0\$ — No significant difference

### 5.2 Demand by Weather Conditions (ANOVA)

* **Normality Test (Shapiro-Wilk)**: p < 0.05 ⇒ Data not normally distributed
* **Levene’s Test**: p < 0.05 ⇒ Unequal variances
* **One-way ANOVA**: p = 0.0048
* **Conclusion**: Significant differences in bike demand across weather types

---

## 6. Insights and Recommendations

### 6.1 Key Insights

* Higher demand on **working days** and **non-holidays**
* Demand significantly varies with **season** and **weather**
* **Fall** and **clear weather** correlate with peak usage
* `count` variable is non-normally distributed with visible outliers

### 6.2 Strategic Recommendations

* **Weekday/Regular Day Inventory**: Allocate more bikes during weekdays and non-holidays
* **Seasonal Planning**: Prepare for higher demand in **Fall** (Season 3)
* **Weather-Aware Allocation**: Stock more bikes during **clear weather**
* **Dynamic Stock System**: Develop a real-time, demand-driven inventory strategy incorporating season, weather, and calendar inputs
