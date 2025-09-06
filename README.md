# Food Sales Data Analysis
📌 Project Overview

This project focuses on analyzing food sales data to generate key performance indicators (KPIs) and business insights. The dataset includes information about:

Users

Orders placed from restaurants

Orders placed by users

Delivery details

Delivery partner details

The goal is to help a food delivery company:

Understand customer behavior

Track order and sales performance

Evaluate restaurant and delivery partner efficiency

Identify growth opportunities to expand and maximize profits

# 📊 Dataset Description

The dataset consists of the following tables:

User_details → Information about customers placing food orders (Age,Age Group,City,Customer ID,Delivery Location Latitude,Delivery Loaction Longitude,Gender).

Restaurant_details → Details of restaurants listed on the platform (Cuisine Type,Dine-in Available,Food Category,Name,Restaurant ID).

Order_details → Records of food orders placed by users (Order Id,Customer ID,Restaurant ID,Order Date,Time Ordered,Type of Order,Order Value,Order Value Category).

Delivery_details → Information about each delivery made (Order Id,Delivery Person Id,Time Order Picked,Weather Conditions,Road Traffic Density,Multiple Deliveries,Festival,Time Taken(Min),Delivery Person Ratings,Tip).

Delivery_person_details → Data about delivery partners (Delivery_person_ID,Delivery_person_Age,Vehicle_condition,Type_of_vehicle).

# 🛠️ Methodology
🔹 Data Cleaning & Preprocessing

Removed unwanted and null columns from all tables

Corrected data types according to column values (e.g., dates, numerical values)

Removed duplicate user IDs from User_details table

Removed duplicate order IDs from Order_details table

Filtered out null or NaN values to ensure accuracy

🔹 Data Integration & Relationships

Merged User_details, Restaurant_details, and Delivery_details with Order_details

Connected Delivery_details with Delivery_person_details

Established relationships between tables:

| Relationship                                   | Type        |
| ---------------------------------------------- | ----------- |
| `User_details` ↔ `Order_details`               | One-to-Many |
| `Restaurant_details` ↔ `Order_details`         | One-to-Many |
| `Order_details` ↔ `Delivery_details`           | One-to-One  |
| `Delivery_details` ↔ `Delivery_person_details` | Many-to-One |

# 🧑‍💻 Key Skills
🔹 Data Preparation

Data cleaning (handling null values, removing duplicates, correcting data types)

Merging and joining relational tables (User_details, Order_details, Restaurant_details, Delivery_details, Delivery_person_details)

Defining relationships between tables (one-to-many, one-to-one, many-to-one)

🔹 DAX Formulas for KPIs
Created several Key Performance Indicators (KPIs) using DAX formulas in Power BI:
#### Average Order Value
Average Order Value = AVERAGE(Order_details[Order Value])

On-time Delivery %
On-time Delivery % = 
DIVIDE(
    COUNTROWS(FILTER(Delivery_details, Delivery_details[Time Taken (Min)] <= 30)),
    COUNTROWS(Delivery_details)
) * 100

#### Sales Percentage
Sales Percentage = 
DIVIDE(
    SUM(Order_details[Order Value]),
    CALCULATE(SUM(Order_details[Order Value]), ALL(Order_details))
)

#### Total Deliveries
Total Deliveries = CALCULATE(DISTINCTCOUNT(Order_details[Order Id]))

#### Total Sales
Total Sales = CALCULATE(SUM(Order_details[Order Value]))

#### Total Sales for Drinks
Total Sales for Drinks = 
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Drinks")

#### Total Sales for Snacks
Total Sales for Snacks = 
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Snack")

# 📌 Key Insights

From the analysis of the food sales dataset, the following insights were derived:

🔹 KPI Highlights

Total Sales → ₹22 Million

Total Deliveries → 25K

Total Sales for Drinks → ₹5 Million

Total Sales for Snacks → ₹3 Million

Average Order Value → ₹914

On-time Delivery % → 69%

Sales Percentage → 1%

🔹 Business Insights

Food Preference → Non-vegetarian dishes are ordered more compared to vegetarian options.

Customer Demographics →

Majority of orders come from people in their 20s and 30s.

Among this age group, males place more orders than females.

Sales by Order Type →

Buffet (highest)

Meal

Drinks

Snacks (lowest)

Delivery Mode Usage →

Most deliveries are made using motorcycles, followed by scooters, and then electric scooters.

# Dashboard
#### Kpis
<img width="1304" height="731" alt="image" src="https://github.com/user-attachments/assets/e61260fb-dd8d-40d7-8169-180644064e99" />

#### Charts
<img width="1689" height="737" alt="image" src="https://github.com/user-attachments/assets/443f8096-4707-490a-88b7-c33406621e6b" />

#### Performance
<img width="1686" height="744" alt="image" src="https://github.com/user-attachments/assets/4f582082-4e22-4d00-8602-e2a0ce6c9b17" />

#### Matrix
<img width="1678" height="731" alt="image" src="https://github.com/user-attachments/assets/a5cb2100-0c24-49c0-b373-00ab0de90984" />



