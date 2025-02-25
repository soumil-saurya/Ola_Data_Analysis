
# Ola Data Analysis
## Overview
Have you ever wondered how ride-hailing companies like Ola manage massive amounts of booking data? This project delves into Bengaluru's ride-hailing landscape by analyzing an extensive dataset of **103,025** Ola bookings.

We delve into key aspects such as booking statuses, cancellations, ride distances, payment methods, and ratings. Utilizing SQL for data preparation and Power BI for visualization, we uncover intriguing trends like high demand on weekends, popular vehicle types, and common reasons for cancellations.

These insights showcase how data-driven decisions can boost customer satisfaction by optimizing operations and enhancing service quality.

## The Dataset
The Ola dataset contains 103,025 rows of ride-booking data for Bengaluru over one month. This dataset encompasses various data points related to ride bookings, customer and driver interactions, cancellations, and more. An overview of the columns is as follows:

**Date**: The date of booking.

**Time**: The time at which the booking was made.

**Booking ID**: A unique 10-digit identifier, prefixed by "CNR" (e.g., CNR1234567890).

**Booking Status**: The status of the booking (Successful/Cancelled).

**Customer ID**: Unique identifier for each customer.

**Vehicle Type**: Different types of vehicles used for the ride (e.g., Auto, Prime Plus, etc.).

**Pickup Location**: Dummy locations from 50 different areas in Bengaluru.

**Drop Location**: Another set of locations, chosen from the list of pickup locations.

**Avg VTAT (Vehicle Time Arrival Time)**: The average time taken for the vehicle to arrive at the pickup location.

**Avg CTAT (Customer Time Arrival Time)**: The average time taken for the customer to arrive at the pickup location.

**Cancelled Rides by Customer**: If the ride was cancelled by the customer.

**Reason for Cancelling by Customer**: Various reasons for cancellation (e.g., AC not working, change of plans).

**Cancelled Rides by Driver**: Cancellations by the driver, often due to personal or vehicle-related issues.

**Incomplete Rides**: Cases where the ride was incomplete for some reason.

**Incomplete Rides Reason**: Reasons for incomplete rides, such as vehicle breakdown or customer demand.

**Booking Value**: The fare for the ride.

**Payment Method**: The method used to pay (Cash/UPI/Card/Wallet).

**Ride Distance**: Distance of the ride in kilometres.

**Driver Ratings**: Ratings given to the driver by the customer.

**Customer Rating**: Ratings given by the driver to the customer.

## Project Goals
The primary goals of this project are as follows:

- **Analyze Customer Behavior**: Understand patterns in customer behavior, including ride preferences, peak booking times, and reasons for cancellations.
- **Identify Trends**: Detect trends in ride demand, vehicle type preferences, and payment methods.
- **Optimize Operations**: Provide insights to help Ola optimize its operations, reduce cancellations, and improve ride completion rates.
- **Enhance Customer Satisfaction**: Use data-driven insights to enhance customer satisfaction by offering better service quality and addressing common issues faced by customers and drivers.
- **Support Decision-Making**: Enable data-driven decision-making for strategic planning and policy formulation to improve overall service efficiency.

## Tech Stack
The technologies used in this project include:

- **Excel**: For data cleaning and exploration.
- **SQL**: For data analysis.
- **Power BI**: For data visualization.

## Why Use SQL Views?

- Views in SQL were used in this project for the following reasons:

- Simplifies Complex Queries: Instead of writing long and repetitive SQL queries, views allow us to save commonly used queries for easy access.

- Enhances Data Security: By restricting direct access to the raw database, views help expose only necessary data to users.

- Improves Performance: Views can improve query performance by precomputing and storing results, reducing the need for repeated calculations.

- Encapsulates Business Logic: Views serve as an abstraction layer, making it easier to modify queries without affecting application logic.

## Exploratory Data Analysis (EDA)
Let's perform an Exploratory Data Analysis (EDA) to find insights that can help inform decision-making.

### Database Creation and SQL Queries
Below are the SQL queries used for data analysis along with their explanations:

```sql
# DATABASE CREATION
CREATE DATABASE ola;                       
USE ola;
```
This creates and selects the database `ola` for storing booking records.

**Query 1**. Retrieve all successful bookings:
```sql
#1 RETRIEVE ALL SUCCESSFUL BOOKINGS
CREATE VIEW SUCCESSFUL_BOOKINGS AS
SELECT * FROM BOOKINGS WHERE BOOKING_STATUS = 'SUCCESS';

# Retrive Query Using
SELECT * FROM SUCCESSFUL_BOOKINGS;
```
Explanation: This view retrieves all successful bookings, filtering out canceled or incomplete rides.

**Query 2**. Find the average ride distance for each vehicle type:
```sql
#2 FIND THE AVERAGE RIDE DISTANCE FOR EACH VEHICLE TYPE
CREATE VIEW AVG_RIDE_DISTANCE_FOR_EACH_VEHICLE_TYPE AS
SELECT VEHICLE_TYPE, AVG(RIDE_DISTANCE) FROM BOOKINGS GROUP BY VEHICLE_TYPE;

# Retrive Query Using
SELECT * FROM AVG_RIDE_DISTANCE_FOR_EACH_VEHICLE_TYPE;
```
This calculates the average ride distance for each type of vehicle used in the bookings.

**Query 3**. Get the total number of cancelled rides by customers:
```sql
#3 GET THE TOTAL NUMBER OF CANCELED RIDES BY CUSTOMER
CREATE VIEW CANCELED_RIDES_BY_CUSTOMER AS
SELECT COUNT(*) FROM BOOKINGS WHERE BOOKING_STATUS = 'CANCELED BY CUSTOMER';

# Retrive Query Using
SELECT * FROM CANCELED_RIDES_BY_CUSTOMER;
```
This counts the total number of rides that were canceled by customers.

**Query 4**. List the top 5 customers who booked the highest number of rides:
```sql
#4 LIST THE TOP 5 CUSTOMERS WHO BOOKED THE HIGHEST NUMBER OF RIDES
CREATE VIEW TOP_5_CUSTOMERS AS
SELECT CUSTOMER_ID, COUNT(BOOKING_ID) 
FROM BOOKINGS 
GROUP BY CUSTOMER_ID 
ORDER BY COUNT(BOOKING_ID) DESC LIMIT 5;

# Retrive Query Using
SELECT * FROM TOP_5_CUSTOMERS;
```
This lists the top 5 customers who booked the highest number of rides.

**Query 5**. Get the number of rides cancelled by drivers due to personal and car-related issues:
```sql
#5 GET THE NUMBER OF RIDES CANCELED BY DRIVERS DUE TO PERSONAL AND CAR-RELATED ISSUES
CREATE VIEW CANCELED_BY_DRIVERS_P_C_ISSUES AS
SELECT COUNT(*) FROM BOOKINGS WHERE CANCELED_RIDES_BY_DRIVER = 'PERSONAL & CAR RELATED ISSUE';

# Retrive Query Using
SELECT * FROM CANCELED_BY_DRIVERS_P_C_ISSUES;
```
This counts the number of rides canceled by drivers due to personal or car-related reasons.

**Query 6**. Find the maximum and minimum driver ratings for Prime Sedan bookings:
```sql
#6 FIND THE MAXIMUM AND MINIMUM DRIVER RATINGS FOR PRIME SEDAN BOOKINGS
CREATE VIEW MAX_MIN_DRIVER_RATING_PRIME_SEDAN AS
SELECT MAX(DRIVER_RATINGS), MIN(DRIVER_RATINGS) FROM BOOKINGS WHERE VEHICLE_TYPE = 'PRIME SEDAN';

# Retrive Query Using
SELECT * FROM MAX_MIN_DRIVER_RATING_PRIME_SEDAN;
```
This finds the highest and lowest driver ratings for Prime Sedan rides.

**Query 7**. Retrieve all rides where payment was made using UPI:
```sql
#7 RETRIEVE ALL RIDES WHERE PAYMENT WAS MADE USING UPI
CREATE VIEW PAYMENT_USING_UPI AS
SELECT * FROM BOOKINGS WHERE PAYMENT_METHOD = 'UPI';

# Retrive Query Using
SELECT * FROM PAYMENT_USING_UPI;       
```
This retrieves all bookings where UPI was used for payment.

**Query 8**. Find the average customer rating per vehicle type:
```sql
#8 FIND THE AVERAGE CUSTOMER RATING PER VEHICLE TYPE
CREATE VIEW AVG_CUSTOMER_RATING_BY_VEHICLE_TYPE AS
SELECT VEHICLE_TYPE, AVG(CUSTOMER_RATING) FROM BOOKINGS GROUP BY VEHICLE_TYPE;

# Retrive Query Using
SELECT * FROM AVG_CUSTOMER_RATING_BY_VEHICLE_TYPE;
```
This query calculates the average customer rating for each vehicle type, helping evaluate customer satisfaction across different categories.

**Query 9**. Calculate the total booking value of rides completed successfully:
```sql
CREATE VIEW TOTAL_SUCCESSFUL_RIDE_VALUE AS
SELECT SUM(BOOKING_VALUE) AS TOTAL_SUCCESSFUL_RIDE_VALUE FROM BOOKINGS WHERE BOOKING_STATUS = 'SUCCESS';

# Retrive Query Using
SELECT * FROM TOTAL_SUCCESSFUL_RIDE_VALUE;
```
This query computes the total revenue generated from successfully completed rides, providing key financial metrics.

**Query 10**. List all incomplete rides along with the reason:
```sql
#10 LIST ALL INCOMPLETE RIDES ALONG WITH THE REASON
CREATE VIEW INCOMPLETE_RIDES AS
SELECT BOOKING_ID, INCOMPLETE_RIDES_REASON FROM BOOKINGS WHERE INCOMPLETE_RIDES = 'YES';

# Retrive Query Using
SELECT * FROM INCOMPLETE_RIDES;
```
This query lists all incomplete rides along with the reasons, helping identify and address the root causes of incomplete rides.

## Data Analysis and Visualization with Power BI
After the Exploratory Data Analysis now we will export our data into MS Power BI for detailed analysis and visualization. Power BI helped us to transform raw data into interactive dashboards and reports by providing deep insights into ride-booking patterns.

Based on the dataset we will find the insights as shown below:
### 1. Ride Volume Over Time and Booking Status Breakdown
A time-series chart showing the number of rides per day/week.

A doughnut chart displaying the proportion of different booking statuses (success, cancelled by the customer, cancelled by the driver, etc.)

![alt image](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Overall%20Dashboard%20Screenshot.png?raw=true)

### 2. Top Vehicle Types by Ride Distance
This visualization highlights which vehicle types are most utilized in terms of ride distance. For instance, longer bars for "Prime SUV" or "Bike" may indicate their popularity for longer commutes or quick, short-distance trips. Businesses can leverage this information to allocate resources effectively and optimise vehicle availability based on demand trends.

![alt image](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Vehicle%20Type%20Dashboard%20Screenshot.png?raw=true)

### 3. Revenue by Payment Method
-    Revenue by Payment Method (Stacked Bar Chart)
     A stacked bar chart categorizes total revenue by payment methods such as Cash, UPI and Credit Card. Each bar segment represents the contribution of a specific payment method to the overall revenue.

     This visualization highlights the most popular payment methods and their impact on revenue by helping assess customer preferences and streamline payment processes.

-    Customer Spending Leaderboard:
     A leaderboard visual ranks customers based on their total spending on bookings by listing the top contributors to revenue.

     This helps identify high-value customers who contribute significantly to revenue, enabling targeted promotions or loyalty rewards to retain them.

-    Ride Distance Distribution (Histogram or Scatter Plot)
     A histogram shows the frequency distribution of ride distances over different dates, while a scatter plot can depict individual ride distances against dates.

     This visualization provides insights into ride patterns, including peak travel days and the variability of ride distances by helping in demand forecasting and route optimization.

![alt image](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Revenue%20Dashboard%20Screenshot.png?raw=true)

### 4. Reason for Cancelling Ride Either by Customer or Driver
A pie chart is used to visually represent the most prominent reasons why customers and drivers cancel rides.

The chart segments the data into proportions by highlighting which reason has the highest occurrence.

For customers, the leading reason for cancellations is often "Driver is not moving towards pickup location" reflecting potential delays or miscommunication.

For drivers, "Personal & Car related issues" is typically the top reason, showcasing operational challenges.

![alt image](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Cancellation%20Dashboard%20Screenshot.png?raw=true)

### 5. Customer Rating and Driver Rating
Driver Ratings: These reflect customer satisfaction with the driver, including professionalism, driving skills, and overall service quality. High ratings indicate positive experiences, while low ratings highlight areas for improvement.

Customer Ratings: These are provided by drivers to evaluate the behavior and cooperation of customers during the ride. They help maintain service standards and identify problematic behaviors.

![alt image](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Rating%20Dashboard%20Screenshot.png?raw=true)
## Key Insights and Learnings

The below Power BI dashboard provides a quick overview of key performance metrics, including KPIs such as total bookings, total revenue, and total distance travelled, all of which are dynamically updated through a date slicer.
Users can easily filter data by date to make informed decisions based on the selected time period. The dashboard features card visualizations for each metric and a line chart to visualize trends over time, helping users track performance and spot patterns efficiently.

![Screenshot dashboard](https://github.com/soumil-saurya/Ola_Data_Analysis/blob/main/Ola%20Dashboard%20Screenshot.png?raw=true)

Through this project, we derived several key insights about Bengaluru’s ride-hailing data:

**Booking Status Trends**: Success rates were consistent but cancellations by customers peaked during certain times of the day, particularly during bad weather.

**High Demand on Weekends and Match Days**: The data confirmed higher booking volumes during weekends and on match days, which could influence ride-hailing strategies for these days.

**Popular Vehicle Types**: Autos and Prime Sedans saw the highest demand while eBikes were less frequent but growing in popularity.

**Cancellation Insights**: The most common reasons for cancellations were "Driver is not moving towards pickup location" and "Change of plans."

**Incomplete Rides**: Vehicle breakdowns were the leading cause of incomplete rides, followed by customer demands.


## Conclusion
Overall, This data analysis project provided a comprehensive look into Bengaluru’s ride-hailing patterns, using SQL, Power BI, and Excel to handle large datasets and derive actionable insights. By adhering to the given constraints and using the appropriate tools, I was able to analyze booking trends, cancellations, ratings, and other key metrics.

These insights can help ride-hailing companies like OLA better understand customer behaviour, optimize driver assignments, and improve customer satisfaction. The project was also an excellent opportunity to strengthen your skills in SQL data management, Power BI visualization and Excel data manipulation.

---
⭐ If you find my work useful, consider giving a star to the repository!



