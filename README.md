# 🚛 Logistics Fleet Efficiency Analysis (Power BI)

## 📊 About the Project
This project involves implementing Business Intelligence (Power BI) solutions for Grape Transport, a fictional logistics company operating in the USA. 
The main objective is to identify unprofitable transport routes and optimize client collaboration to maximize the Profit/Mile metric.

## 🛠 Technologies Used
* **Tools:** Power BI, Power Query, MySQL
* **Languages:** DAX
* **Modeling:** Galaxy Schema

## 📂 Data Sources
The data architecture is hybrid, combining:
* **CSV Files:** Transactional data (loads.csv, trips.csv, fuel_purchases.csv)[cite: 3].
* **SQL Database (MySQL):** Dimensional data imported via a local server (customers, drivers, routes, trucks).

*Base Source: Synthetic Logistics Operations Database, [https://www.kaggle.com/datasets/yogape/logistics-operations-database]*

## ⚙️ Data Preparation and Modeling
* **Data Cleaning:** Removed records with missing keys (driver_id, truck_id, trailer_id) for completed transactions.
* **Data Types:** Converted financial data to fixed decimal numbers.
* **Data Model:** Built a Galaxy Schema consisting of 3 fact tables, 4 dimension tables, and a dedicated Calendar Table.

## 💻 Key DAX Measures
To provide deep analytical insights without requiring access to the `.pbix` file, below are the core DAX measures driving the dashboard logic:

**1. Time Intelligence (Year-to-Date Revenue):**
```dax
revenue_YTD = 
CALCULATE(
    [total_revenue],
    DATESYTD('date'[date])
)
```
**2. Route Efficiency Categorization:**
```dax
route_profit_rank = 
IF(
    HASONEVALUE(routes[route_id]),
    RANKX(
        ALL(routes),
        CALCULATE([total_profit]),
        , DESC, Dense
    ),
    BLANK()
)
```
**3. Dynamic Route Profitability Ranking:**
```dax
route_profit_rank = 
IF(
    HASONEVALUE(routes[route_id]),
    RANKX(
        ALL(routes),
        CALCULATE([total_profit]),
        , DESC, Dense
    ),
    BLANK()
)
```
## 💡 Key Business Insights
* Route profitability: Identified negative profits on short-haul routes.
* Client diversification: The client portfolio is highly diversifiedm ensuring financial stability and reducing reliance on key contracts.
