# Environmental_analysis


Statistical analysis and exploratory data analysis (EDA) of daily weather, pollutant, and Air Quality Index (AQI) data.

**Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn

---

## 1. Introduction

Air pollution is a major environmental and public-health concern. Air quality changes from day to day with weather conditions such as temperature, humidity, wind speed, and rainfall, and with pollutant levels such as PM2.5, PM10, and NO2.

This project uses a daily environmental dataset with weather variables, pollutant concentrations, the Air Quality Index (AQI), and a Green Environmental Index. Statistical techniques and EDA are used to identify the factors most strongly associated with AQI.

## 2. Problem Statement

AQI varies daily, but the factors behind these changes are not always obvious. This project aims to understand how weather conditions and pollutant concentrations relate to the daily AQI, using 500 days of recorded data. The analysis also prepares the data for a supervised regression model that predicts AQI.

## 3. Objectives

1. Study the structure and quality of the dataset.
2. Perform statistical analysis (mean, median, standard deviation, quartiles, correlation).
3. Examine the distribution of AQI and the other variables.
4. Explore how AQI relates to temperature, humidity, wind speed, rainfall, and pollutants.
5. Visualise AQI trends over time and the spread of air quality categories.
6. Identify the variables most strongly associated with AQI.
7. Build a Linear Regression model to predict AQI.

   
## 4. Dataset Description

| Detail | Value |
|---|---|
| File | environmental_dataset.xlsx (sheet: DATASET) |
| Observations | 500 |
| Variables | 12 |
| Time period | 2025-01-01 to 2026-05-15 |
| Target variable | Air_Quality_Index_AQI |
| Problem type | Regression (AQI value) |
| Missing values | None |

**Variables**

| Variable | Description | Type |
|---|---|---|
| Record_ID | Unique row identifier | Identifier |
| Date | Date of observation | Date |
| Temperature_C | Temperature in C | Numerical |
| Humidity_percent | Relative humidity (%) | Numerical |
| Rainfall_mm | Rainfall in mm | Numerical |
| Wind_Speed_kmh | Wind speed in km/h | Numerical |
| PM2_5_ug_m3 | Fine particulate matter (ug/m3) | Numerical |
| PM10_ug_m3 | Coarse particulate matter (ug/m3) | Numerical |
| NO2_ug_m3 | Nitrogen dioxide (ug/m3) | Numerical |
| Air_Quality_Index_AQI | Air Quality Index value | Numerical |
| Green_Environmental_Index | Composite environmental score | Numerical |
| Air_Quality_Category | Good, Moderate, Unhealthy for Sensitive Groups | Categorical |

**Target and predictors**

- **Target:** Air_Quality_Index_AQI
- **Predictors:** temperature, humidity, rainfall, wind speed, PM2.5, PM10, NO2, Green Environmental Index
- **Excluded:** Air_Quality_Category, Record_ID, and Date

## 5. Data Pre-processing

The data was already clean, so pre-processing focused on validation and light preparation.

| Step | Finding / Action |
|---|---|
| Dimensions | 500 rows x 12 columns |
| Missing values | None, so no imputation needed |
| Duplicates | No duplicate rows or Record_IDs |
| Date continuity | 500 consecutive days, no gaps |
| Data types |Date:Datetime|

## 6. Exploratory Data Analysis

### 6.1 Descriptive Statistics

| Variable | Mean | Median | Std | Min | Max |
|---|---|---|---|---|---|
| Temperature (C) | 26.9 | 27.0 | 5.3 | 14.0 | 42.0 |
| Humidity (%) | 69.7 | 69.7 | 10.2 | 38.3 | 98.0 |
| Rainfall (mm) | 2.0 | 0.0 | 4.1 | 0.0 | 35.0 |
| Wind Speed (km/h) | 10.1 | 10.0 | 3.3 | 1.0 | 19.8 |
| PM2.5 (ug/m3) | 26.4 | 26.4 | 9.1 | 5.0 | 55.3 |
| PM10 (ug/m3) | 50.6 | 50.2 | 14.3 | 10.8 | 95.3 |
| NO2 (ug/m3) | 25.7 | 25.3 | 8.2 | 5.0 | 57.9 |
| **AQI** | **60.5** | **60.0** | **16.4** | **20** | **104** |
| Green Env. Index | 63.8 | 64.1 | 5.0 | 47.4 | 80.4 |

AQI quartiles: Q1 = 49, Q2 (median) = 60, Q3 = 72.

### 6.2 Distribution of AQI

AQI is roughly symmetric (skewness about -0.02) and centred near 60, with no outliers. 
The mean and median are almost equal. 
Among the predictors, rainfall is heavily right-skewed: about 65% of days have no rain, with occasional events up to 35 mm. The other variables are roughly symmetric.

### 6.3 AQI over Time and Air Quality Categories

The 30-day rolling mean of AQI stays between about 54 and 69, so there is no strong trend over time.

| Category | Days | Share |
|---|---|---|
| Good (AQI up to 50) | 140 | 28.0% |
| Moderate (51-100) | 358 | 71.6% |
| Unhealthy for Sensitive Groups (101+) | 2 | 0.4% |

The categories are highly imbalanced, which matters for any classification task.

### 6.4 AQI by Month and Rainfall

Average AQI stays within a narrow band across calendar months (55 in December to 65 in July), so seasonality is weak. Rainy days have a slightly lower average AQI (59.3) than dry days (61.1). 

### 6.5 AQI vs Temperature

AQI rises steadily as temperature increases.

| Temperature band | Up to 20 C | 20-25 C | 25-30 C | 30-35 C | Above 35 C |
|---|---|---|---|---|---|
| Average AQI | 43.8 | 52.8 | 62.1 | 70.0 | 77.3 |


### 6.6 Key Takeaways

1. PM2.5 is the main driver of AQI, with NO2, PM10, and temperature also contributing.
2. Hotter, drier, and calmer days tend to have poorer air quality.
3. AQI is stable across the period, mostly in the Moderate range, with no clear seasonality.
4. Only 2 records fall in "Unhealthy for Sensitive Groups", so the category is highly imbalanced.

## Conclusion

This project analysed 500 days of environmental data (January 2025 to May 2026) to understand what influences the Air Quality Index (AQI) and to predict it using Linear Regression.

**Data and EDA findings**
- The dataset was clean, with no missing values, no duplicates, and continuous daily records.
- AQI averages about 60 (Moderate) and is roughly symmetric. About 72% of days are Moderate, 28% are Good, and only 2 days are Unhealthy for Sensitive Groups.
- AQI shows no strong trend over time and only weak seasonality.
- PM2.5 has the strongest correlation with AQI (0.68), followed by NO2 (0.58), temperature (0.58), and PM10 (0.53). Humidity (-0.38) and wind speed (-0.20) are negatively correlated.
- Hotter, drier, and calmer days tend to have poorer air quality.


Overall, the project shows that AQI is mainly driven by particulate matter and NO2, and that Linear Regression captures a large part, though not all, of its variation.
