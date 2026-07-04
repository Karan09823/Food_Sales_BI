# 🍔 Food Delivery Sales Dashboard | Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data%20Modeling-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## 📌 Project Overview

Developed a comprehensive Food Delivery Dashboard to analyze food sales, customer behavior, and delivery-partner performance for a food delivery platform. The dashboard consolidates user, restaurant, order, and delivery data into a single model with KPIs designed to monitor sales performance, customer engagement, and delivery efficiency.

---

## 🎯 Business Problem & Objective

A food delivery platform generates data across four disconnected areas — who's ordering, what restaurants are selling, how orders are placed, and how deliveries are executed — but without a unified view, it's difficult to answer basic operational questions:

- Which order types and customer segments actually drive revenue?
- Is delivery performance meeting customer expectations, and where is it falling short?
- Which delivery modes and partner conditions are being relied on most heavily?
- Where should the business focus to improve both sales and delivery efficiency?

The objective of this project is to merge user behavior, restaurant, order, and delivery-partner data into one model that surfaces where growth opportunities and operational risks actually sit — not just what total sales look like.

---

## 📊 Dataset Description

| Table | Description | Key Columns |
|---|---|---|
| `User_details` | Customers placing orders | Age, Age Group, City, Customer ID, Delivery Location (Lat/Long), Gender |
| `Restaurant_details` | Restaurants on the platform | Cuisine Type, Dine-in Available, Food Category, Name, Restaurant ID |
| `Order_details` | Orders placed by users | Order ID, Customer ID, Restaurant ID, Order Date, Time Ordered, Type of Order, Order Value, Order Value Category |
| `Delivery_details` | Delivery execution records | Order ID, Delivery Person ID, Time Picked, Weather Conditions, Road Traffic Density, Multiple Deliveries, Festival, Time Taken (Min), Delivery Person Ratings, Tip |
| `Delivery_person_details` | Delivery partner attributes | Delivery Person ID, Age, Vehicle Condition, Type of Vehicle |

---

## 🛠️ Methodology

### Data Cleaning & Preprocessing
- Removed unwanted and null columns across all five tables
- Corrected data types (dates, numerical fields)
- Removed duplicate Customer IDs from `User_details` and duplicate Order IDs from `Order_details`
- Filtered out null/NaN values to preserve accuracy

### Data Integration & Relationships

| Relationship | Type |
|---|---|
| `User_details` ↔ `Order_details` | One-to-Many |
| `Restaurant_details` ↔ `Order_details` | One-to-Many |
| `Order_details` ↔ `Delivery_details` | One-to-One |
| `Delivery_details` ↔ `Delivery_person_details` | Many-to-One |

This structure allows every order to be traced end-to-end — from the customer who placed it, to the restaurant that prepared it, to the partner who delivered it — inside a single Power BI model.

---

## 🧮 KPI Development (DAX Measures)

```DAX
Average Order Value = AVERAGE(Order_details[Order Value])

On-time Delivery % =
DIVIDE(
    COUNTROWS(FILTER(Delivery_details, Delivery_details[Time Taken (Min)] <= 30)),
    COUNTROWS(Delivery_details)
) * 100

Sales Percentage =
DIVIDE(
    SUM(Order_details[Order Value]),
    CALCULATE(SUM(Order_details[Order Value]), ALL(Order_details))
)

Total Deliveries = CALCULATE(DISTINCTCOUNT(Order_details[Order Id]))

Total Sales = CALCULATE(SUM(Order_details[Order Value]))

Total Sales for Drinks =
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Drinks")

Total Sales for Snacks =
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Snack")
```

---

## 📈 Dashboard Pages & Key Insights

### 1️⃣ KPIs
**Headline metrics:** Total Sales, Total Deliveries, Average Order Value, On-time Delivery %

- **Total Sales:** ₹22M | **Total Deliveries:** 25K | **Average Order Value:** ₹914
- **Total Sales – Drinks:** ₹5M | **Total Sales – Snacks:** ₹3M
- **On-time Delivery %:** 69% — meaning roughly **3 in 10 orders exceed a 30-minute delivery window**, a gap large enough to directly affect customer retention and ratings
- **Sales Percentage** (share of total across current filter context): 1% — a normalized measure useful for comparing any single slice (restaurant, city, order type) against total network sales

![KPIs](images/kpis.png)

### 2️⃣ Charts — Sales & Customer Behavior
- **Food preference:** Non-vegetarian dishes are ordered more frequently than vegetarian options — relevant for restaurant onboarding and menu-promotion strategy
- **Customer demographics:** The majority of orders come from customers in their 20s and 30s, and within this group, **male customers order more frequently than female customers**
- **Sales by order type (highest to lowest):** Buffet → Meal → Drinks → Snacks — Buffet orders driving the most revenue suggests bundled/higher-ticket order types outperform à la carte items like snacks and drinks

![Charts](images/charts.png)

### 3️⃣ Performance — Delivery Efficiency
- **Delivery mode usage:** Motorcycles are the dominant delivery vehicle, followed by scooters, then electric scooters — the platform's delivery capacity is heavily concentrated in a single vehicle type, which is a operational dependency worth monitoring (e.g., fuel cost sensitivity, single point of failure during motorcycle shortages)
- With On-time Delivery % sitting at 69%, cross-referencing this page against `Weather Conditions` and `Road Traffic Density` (available in the raw data but not yet surfaced as a dedicated visual) is a natural next step to isolate whether late deliveries cluster around specific conditions — flagged below under Future Improvements

![Performance](images/performance.png)

### 4️⃣ Matrix — Restaurant & Order Breakdown
- Cross-tabulated view of order value and order type across restaurants/cuisine categories, allowing quick identification of which cuisine types or restaurants are consistently driving high-value orders versus high volume but low ticket size

![Matrix](images/matrix.png)

---

## 💡 Business Recommendations

1. **Investigate the 31% of late deliveries** — segment by weather, traffic density, and multiple-deliveries flag to determine whether delays are structural (route/vehicle capacity) or conditional (weather/traffic spikes), then target the fix accordingly
2. **Promote Buffet and Meal order types** — these outperform Snacks and Drinks; bundling snacks/drinks into meal or buffet offers could lift their otherwise-low individual sales contribution
3. **Diversify delivery vehicle mix** — near-total reliance on motorcycles creates operational risk; incentivizing scooter/e-scooter adoption could reduce single-mode dependency
4. **Target menu and marketing toward the core demographic** (males in their 20s–30s) while testing campaigns to grow underrepresented segments (e.g., female customers, other age groups) to expand the customer base rather than only optimizing for the existing one

---

## 🧠 Skills Demonstrated

`Data Modeling` · `DAX` · `Power Query (ETL)` · `Relational Data Integration` · `KPI Design` · `Customer & Delivery Analytics` · `Dashboard/UX Design`

---

## 🛠️ Tools & Technologies

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query
- Excel Data Source

---

## 📁 Repository Structure

```
Food_Sales_BI/
│
├── Food_Delivery_Sales_BI.pbix   # Power BI report file
├── Food_Delivery_Data.xlsx       # Source data
├── README.md                     # Project documentation (this file)
└── images/
    ├── kpis.png
    ├── charts.png
    ├── performance.png
    └── matrix.png
```

> ⚠️ **Setup note:** Create an `images/` folder and add the four dashboard screenshots with the filenames above. The previous version of this README linked images through GitHub's temporary signed URLs, which expire within minutes — relative paths make them permanent.

---

## 🚀 How to Use

1. Clone this repository
2. Open `Food_Delivery_Sales_BI.pbix` in Power BI Desktop
3. Use the report's slicers to filter by order type, city, or time period and explore each of the four dashboard pages

---

## 🔮 Future Improvements

- Add a dedicated visual crossing `On-time Delivery %` against `Weather Conditions` and `Road Traffic Density` to test whether late deliveries are weather/traffic-driven or structural
- Analyze `Delivery Person Ratings` against `Time Taken` to see whether slower deliveries correlate with lower partner ratings, or whether ratings are driven by other factors
- Build a cohort view of repeat vs. one-time customers to measure retention, not just total order volume

---

## 👤 Author

**Karan Kumar Sahu**
Data Analyst | SQL · Python · Power BI
[LinkedIn](#) · [GitHub](https://github.com/Karan09823) · [Portfolio](#)
