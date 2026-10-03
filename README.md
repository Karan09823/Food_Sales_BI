# 🍔 Food Delivery Operations & Sales Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Data Modeling](https://img.shields.io/badge/Data%20Modeling-DAX-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## 📌 Executive Summary
This project delivers an end-to-end Power BI analytics solution designed to monitor sales performance, customer engagement, and delivery efficiency for a food delivery platform. By integrating user demographics, restaurant performance, and delivery-partner execution into a single relational model, this dashboard transitions the business from tracking basic revenue to understanding the operational bottlenecks impacting customer retention.

---

## 🎯 Business Problem & Objective
A food delivery platform generates vast amounts of data across disconnected nodes: customers, restaurants, and delivery drivers. Without a unified view, stakeholders struggle to answer critical operational questions:
* **Fulfillment Friction:** Is delivery performance meeting Service Level Agreements (SLAs), and what factors drive late deliveries?
* **Customer Value:** Which customer demographics and order types actually drive top-line revenue versus just order volume?
* **Fleet Dependency:** Are we over-reliant on specific delivery modes or partners?

**Objective:** Develop a comprehensive dashboard to isolate growth opportunities and operational risks, providing actionable insights into menu promotion, fleet optimization, and customer retention.

---

## 🏗️ Data Architecture & Methodology

### Data Engineering & Preprocessing
* **Data Cleansing:** Standardized data types, handled missing values, and removed duplicates across `User_details` and `Order_details` to preserve transactional accuracy.
* **Metric Engineering (DAX):** Developed dynamic KPIs including SLA breach rates (orders taking >30 mins), category-specific revenue pacing, Average Order Value (AOV), and customer retention metrics (Orders per Customer).

### Relational Data Modeling (Star Schema)
Built a unified model connecting five distinct tables to trace the end-to-end lifecycle of an order:
* `User_details` ↔ `Order_details` (1:Many)
* `Restaurant_details` ↔ `Order_details` (1:Many)
* `Order_details` ↔ `Delivery_details` (1:1)
* `Delivery_details` ↔ `Delivery_person_details` (Many:1)

---

## 📊 Key Performance Indicators (KPIs)

* **Financial Metrics:** Total Sales (₹22M) | Average Order Value (₹914) 
* **Operational Metrics:** Total Deliveries (25K) | On-time Delivery Rate (69%)
* **Customer Metrics:** Total Unique Customers | Average Orders per Customer

---

## 🔍 Key Insights & Findings

1. **The Fulfillment Bottleneck:** 
   Overall on-time delivery sits at 69%, meaning nearly **1 in 3 orders breaches the 30-minute window**. Given that the fleet is heavily reliant on motorcycles, this indicates structural routing or capacity issues that pose a direct risk to customer satisfaction and retention.
2. **High-Ticket vs. High-Volume:** 
   While Non-Vegetarian items drive high order volumes, "Buffet" and "Meal" categories drive the highest gross revenue. À la carte items (Snacks/Drinks) pull down the Average Order Value (AOV) due to inherently lower ticket sizes.
3. **Core Customer Profile & Loyalty:** 
   The highest lifetime value (LTV) segments are male customers in their 20s and 30s ordering at high frequencies. However, the data reveals a significant untapped market share among female demographics and alternative age brackets.
4. **Fleet Dependency:** 
   Motorcycles are overwhelmingly the dominant delivery vehicle. This heavy concentration in a single vehicle type creates operational vulnerability (e.g., susceptibility to fuel cost spikes or specific vehicle shortages).

---

## 💡 Strategic Recommendations

1. **Investigate the 31% Late Delivery Rate:** Segment the late deliveries by `Weather Conditions` and `Road Traffic Density` to determine if delays are conditional (weather spikes) or structural (route inefficiencies). Target interventions accordingly.
2. **Promote High-Value Bundling:** Since Buffet and Meal types financially outperform individual Snacks and Drinks, implement cross-selling features (e.g., "Add a drink for ₹X") at checkout to lift the basket size of low-ticket orders.
3. **Diversify the Delivery Fleet:** Incentivize the onboarding of scooter and e-scooter delivery partners to reduce single-mode dependency and improve unit economics on short-distance neighborhood deliveries.
4. **Targeted Demographic Marketing:** Continue catering to the core male (20s-30s) demographic, while deploying targeted promotional campaigns to acquire and retain underrepresented segments, expanding the overall active user base.

---

## 🔮 Future Improvements
* **Geospatial Delay Mapping:** Integrate the `Delivery Location (Lat/Long)` data into a heat map to visually identify specific neighborhoods or regional zones suffering from chronic >30-minute delivery delays.
* **Partner Rating Correlation:** Analyze `Delivery Person Ratings` against `Time Taken` to determine if slower deliveries are the primary driver of poor ratings, or if other variables (like food condition) carry more weight.

---

## 📈 Dashboard Pages & Key Insights

### 1️⃣ KPIs
**Headline metrics:** Total Sales, Total Deliveries, Average Order Value, On-time Delivery %

- **Total Sales:** ₹22M | **Total Deliveries:** 25K | **Average Order Value:** ₹914
- **Total Sales – Drinks:** ₹5M | **Total Sales – Snacks:** ₹3M
- **On-time Delivery %:** 69% — meaning roughly **3 in 10 orders exceed a 30-minute delivery window**, a gap large enough to directly affect customer retention and ratings
- **Sales Percentage** (share of total across current filter context): 1% — a normalized measure useful for comparing any single slice (restaurant, city, order type) against total network sales

<img width="1327" height="751" alt="image" src="https://github.com/user-attachments/assets/94e6c5d2-ee7f-4c62-afd4-08f4dd450fef" />


### 2️⃣ Charts — Sales & Customer Behavior
- **Food preference:** Non-vegetarian dishes are ordered more frequently than vegetarian options — relevant for restaurant onboarding and menu-promotion strategy
- **Customer demographics:** The majority of orders come from customers in their 20s and 30s, and within this group, **male customers order more frequently than female customers**
- **Sales by order type (highest to lowest):** Buffet → Meal → Drinks → Snacks — Buffet orders driving the most revenue suggests bundled/higher-ticket order types outperform à la carte items like snacks and drinks

<img width="1377" height="602" alt="image" src="https://github.com/user-attachments/assets/6a979e30-00ca-499c-9735-4507b5101935" />


### 3️⃣ Performance — Delivery Efficiency
- **Delivery mode usage:** Motorcycles are the dominant delivery vehicle, followed by scooters, then electric scooters — the platform's delivery capacity is heavily concentrated in a single vehicle type, which is a operational dependency worth monitoring (e.g., fuel cost sensitivity, single point of failure during motorcycle shortages)
- With On-time Delivery % sitting at 69%, cross-referencing this page against `Weather Conditions` and `Road Traffic Density` (available in the raw data but not yet surfaced as a dedicated visual) is a natural next step to isolate whether late deliveries cluster around specific conditions — flagged below under Future Improvements

<img width="1377" height="600" alt="image" src="https://github.com/user-attachments/assets/0efbf273-042c-44dc-9d78-58e2b4fcbbd3" />


### 4️⃣ Matrix — Restaurant & Order Breakdown
- Cross-tabulated view of order value and order type across restaurants/cuisine categories, allowing quick identification of which cuisine types or restaurants are consistently driving high-value orders versus high volume but low ticket size

<img width="1380" height="602" alt="image" src="https://github.com/user-attachments/assets/77a55182-f4c4-4533-adf1-b4ddd49bfe28" />


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
