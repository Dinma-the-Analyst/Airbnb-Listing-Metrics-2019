# REAL ESTATE AND TOURISM TRENDS

## Project Overview
This project investigates real estate and tourism dynamics in New York City using publicly available Airbnb listings data. By analyzing pricing patterns, room types, and listing availability across different boroughs, we uncover insights that reflect broader urban, economic, and tourism trends.
The focus is on two key areas:
Real estate pricing, as inferred from Airbnb listing prices, and Tourism activity, observed through listing availability and accommodation types.

## Data Source
This project uses publicly available Airbnb listing data provided by Inside Airbnb.
Source: Inside Airbnb – Get the Data
Dataset: listings.csv (New York City, 2019 snapshot)
The dataset includes detailed information on Airbnb listings such as price, room type, availability, number of reviews, location (by borough and neighborhood), and more.

## Tools
- Excel - Data Cleaning
- SQL Server - Data Analysis
- BigQuery - Data Analysis and Visualization

- ## Data Cleaning and Preparation
The steps below outline how the data was cleaned and prepared using Microsoft Excel:
- Import the dataset
- Clean the dataset
- Remove duplicate listings
- Handle missing values
- Standardize text fields

## Exploratory Data Analysis
Exploratory Data Analysis was performed to uncover key patterns and insights from the Airbnb NYC 2019 dataset.
- What is the price analysis by neighborhood and room type?
- What are the availability patterns across boroughs?

## Data Analysis
Here are some interesting codes and features worked with
```BigQuery
SELECT
  DISTINCT HD.NEIGHBOURHOOD_GROUP,
  HD.NEIGHBOURHOOD,
  HD.ROOM_TYPE,
  AVG(TD.PRICE) AS AVG_PRICE
FROM
  `airbnb-listing-metrics-2019.2019_Airbnb_Listing_Metrics.HOUSE_DESCRIPTION` AS HD
JOIN
  `airbnb-listing-metrics-2019.2019_Airbnb_Listing_Metrics.TRANSACTION_DETAILS`AS TD
ON
  HD.ID = TD.ID
GROUP BY
  HD.NEIGHBOURHOOD_GROUP,
  HD.NEIGHBOURHOOD,
  HD.ROOM_TYPE
ORDER BY
  AVG_PRICE ASC; 
  
  /*QUESTION 2*/
SELECT
  DISTINCT HD.NEIGHBOURHOOD_GROUP,
  COUNT(TD.AVAILABILITY_365) AS AVAILABILITY_COUNT
FROM
  `airbnb-listing-metrics-2019.2019_Airbnb_Listing_Metrics.HOUSE_DESCRIPTION` HD
JOIN
  `airbnb-listing-metrics-2019.2019_Airbnb_Listing_Metrics.TRANSACTION_DETAILS` TD
ON
  HD.ID = TD.ID
GROUP BY
  HD.NEIGHBOURHOOD_GROUP
ORDER BY
  AVAILABILITY_COUNT DESC; 
  
  /*QUESTION 3*/
WITH HEAT_MAP AS(
SELECT
  NEIGHBOURHOOD_GROUP, 
  NEIGHBOURHOOD,
  'LATITUDE'
  LONGITUDE
FROM
  `airbnb-listing-metrics-2019.2019_Airbnb_Listing_Metrics.HOUSE_DESCRIPTION`
)
SELECT *
FROM HEAT_MAP
```
### Results/Key Finidings
1. Bronx has the highest average prices and Brooklyn offers a balance between affordability and proximity.
2. Manhattan have higher proportions of listings followed by Brooklyn. Also, Staten Island shows high listing volume, but relatively low availability.
3. Entire home/apartment is most common in Manhattan, while private rooms are more prevalent in Brooklyn and the Bronx.

### Recommendations
1. For Travelers: Consider Brooklyn for cost-effective stays. Brooklyn offers a balance of affordability, availability, and proximity to Manhattan.
2. For Hosts: Invest in full apartments over shared rooms. Entire homes consistently attract higher prices and longer stays, especially in Manhattan and Queens.

### Limitations
This analysis provides useful insights, but there are some limitations to keep in mind:
1. The data is from 2019 only. It doesn't show trends over time.
2. Some listings had wrong or extreme prices, which may affect the results, even after cleaning.

### Visualization using BigQuery

![1747169564888](https://github.com/user-attachments/assets/c3c6d222-158e-444a-9ba4-6b15a3d07504)
