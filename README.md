# Ride-Sharing Demand Hotspot Detection Using Clustering

## 🔎 Overview

Ride-hailing platforms like Uber operate as two-sided marketplaces, matching riders who demand transportation with drivers who supply it. A key operational challenge is maintaining balance between supply and demand across both time and location.

When drivers are not located near high-demand areas, rider wait times increase significantly. Research from Uber indicates that most riders are willing to wait only 5–7 minutes before canceling a ride request.

This project analyzes 4.5 million Uber pickup records in New York City (April–September 2014) to identify spatial and temporal demand patterns. Using **clustering techniques and time-based analysis**, the study identifies **dynamic hotspot zones** where driver supply should be concentrated to improve rider-driver matching efficiency.

The resulting framework can help ride-hailing platforms reduce rider wait times, decrease cancellations, and optimize driver allocation.

## 🔐 Business Problem

Ride-hailing platforms face a real-time matching problem:

* Riders request trips from specific locations
* Drivers may not be located nearby
* Long pickup times cause ride cancellations

Even when drivers are geographically close, inefficient distribution across the city can create temporary supply shortages in high-demand areas.

Without understanding spatial demand patterns, platforms struggle to:

* position drivers effectively
* anticipate peak demand hours
* optimize matching algorithms

The key challenge is therefore: _How can Uber dynamically identify demand hotspots and recommend optimal zones for drivers to increase matching efficiency and reduce wait times?_

## 📊 Dataset

The dataset contains 4.5+ million Uber pickup records in New York City from April to September 2014.

Each observation represents an individual ride request and includes:

| Variable  | Description                          |
| --------- | ------------------------------------ |
| Date/Time | Timestamp of the ride request        |
| Latitude  | Pickup location latitude             |
| Longitude | Pickup location longitude            |
| Base      | Uber base associated with the driver |

During preprocessing, additional features were engineered:

* month
* week
* day of week
* hour of day
* weekday vs. weekend classification

These temporal features enable analysis of demand patterns across hours, days, and months. 

## 📍 Methodology

The analysis combines exploratory data analysis, regression modeling, and clustering algorithms.

### 1. Data Preprocessing

Key preprocessing steps included:

* converting timestamp fields to datetime format
* extracting temporal features (month, day, hour)
* categorizing trips as weekday or weekend
* aggregating trip counts across time intervals

These transformations enabled time-series analysis of demand patterns. 

### 2. Exploratory Data Analysis

EDA examined how ride demand changes across months, days of week, hours of day, and Uber driver base.

The analysis revealed:

* Steady growth in trips from April to September

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/c0cdbe6f-3403-4b4c-87ec-ea86426ef993" />

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/7ee5b0bb-29ac-42c3-bae1-f825018a7b46" />

* Higher demand during weekdays compared to weekends

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/7460589d-c653-4c1d-9e1e-685674500fb2" />

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/fe0383bb-d030-4d0a-a2c5-3ab2a5ae8ade" />

* Clear daily peaks during commuting and evening hours

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/dddd088e-3377-4814-bafd-ba7fa8bf8db6" />

<img width="923" height="590" alt="image" src="https://github.com/user-attachments/assets/198b9268-c238-448a-8dcc-08be59868168" />

For example, hourly trip analysis shows demand rising sharply from 6 AM, peaking during late afternoon hours, and declining overnight. 

### 3. Trend Analysis with Regression

A regression model was used to quantify the impact of day of week and month on ride demand.

The model achieved R² = 0.765, indicating that temporal variables explain a significant portion of demand variation.

Key findings include:

* weekends show significantly lower demand
* demand increases progressively from spring to late summer
* September exhibits the highest ride volumes

Regression analysis validates patterns observed during EDA and quantifies their statistical significance. 

### 4. Spatial Clustering for Hotspot Detection

To identify high-demand zones, K-Means clustering was applied to pickup coordinates.

Steps:

1. Extract latitude and longitude
2. Standardize geographic coordinates
3. Run clustering models with multiple K values
4. Use the Elbow Method to determine the optimal cluster number

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/97c8a5aa-debc-4841-b8b6-cbb8b2661fbc" />

The elbow analysis indicates K = 5 as the optimal number of clusters. 

Each cluster represents a demand hotspot zone where driver supply should be concentrated.

Monthly clustering was also performed to capture seasonal shifts in hotspot locations.

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/384dccf3-679f-4cb7-a27d-27be63a27129" />

## 🔑 Key Insights

### 1. Ride demand shows strong temporal patterns

Demand increases steadily from morning hours and peaks during late afternoon and evening, reflecting commuting and nightlife patterns.

### 2. Weekday demand is higher than weekend demand

Trip volumes are significantly higher on weekdays, suggesting that ride-hailing demand is strongly linked to work-related travel.

### 3. Demand increases during summer months

Trip counts rise from April through September, reflecting seasonal mobility increases.

### 4. Five key spatial hotspots drive most ride demand

Clustering analysis reveals that ride demand concentrates in a limited number of urban zones, including Manhattan business districts, airport travel hubs, and dense residential areas.

These zones represent optimal driver positioning areas.

## ✍️ Business Recommendations

### 1. Implement dynamic driver positioning

Ride-hailing platforms should recommend hotspot zones to drivers in real time using clustering outputs.

This can reduce idle time and improve ride matching speed.

### 2. Use time-aware supply allocation

Driver availability should be adjusted based on historical demand patterns such as weekday commuting hours, weekend nightlife demand, and seasonal demand shifts.

### 3. Integrate clustering with dispatch algorithms

Hotspot clusters can improve dispatch systems by assigning requests to nearby drivers within the same demand zone.

This increases the probability of quick driver assignment.

### 4. Incorporate predictive demand models

Combining clustering with forecasting models can help anticipate demand surges before they occur.

This allows platforms to proactively reposition drivers.

## ⚙ Tools & Technologies

* Python
* Data preprocessing (Pandas, NumPy)
* Data visualization (Matplotlib, Seaborn)
* Scikit-learn (K-Means clustering)
* Statsmodels (OLS regression)
* Folium (Interactive cluster maps)
