# 🏠 Housing Market Analysis – Power BI + BigQuery  

## 📌 Project Overview  
This project is an **end-to-end housing market analytics solution** built using **Google BigQuery** (data warehouse) and **Power BI** (visualization + DAX).  

The dataset (`Housing`) contains property sales information such as **price, house type, sales type, SQM, region, interest rate, inflation, and mortgage yield**.  

The project delivers **3 interactive dashboards** providing business-ready insights for **real estate decision-making**.  

---

## 🧹 Data Cleaning & Transformation (Power Query in Power BI)  
Before building dashboards, the dataset was cleaned and transformed:  

- 🔹 **Handled Missing Values** – replaced null values in `sqm_price`, `interest_rate`, and `inflation` with average or median values.  
- 🔹 **Removed Duplicates** – dropped duplicate `house_id` rows to avoid double counting.  
- 🔹 **Date Column Formatting** – converted `date` into proper **Date hierarchy** (Year, Quarter, Month, Day) for time intelligence.  
- 🔹 **Data Type Corrections** – ensured numeric fields (`purchase_price`, `sqm`, `% change`, `interest_rate`) were correctly formatted as decimals.  
- 🔹 **Calculated Columns** –  
  - Created **Offer Price** from `%_change_between_offer_and_purchase`.  
  - Extracted **Year** and **Quarter** from `date`.  
- 🔹 **Outlier Treatment** – filtered extreme outliers in `sqm_price` and `purchase_price` using IQR method for cleaner visuals.  
- 🔹 **Standardized Categories** – cleaned inconsistent text fields (e.g., `house_type`, `region`, `sales_type`).  

---

## ⚡ Key Dashboards  

### **1. House Market Overview**  
📊 KPIs:  
- Median Sales Price Change by Region  
- Units Sold (Latest Year & Quarter)  
- Last 12-Month Sales  
- YoY Sales Growth (by Sales Type)  
- Offer Price vs Purchase Price  

---

### **2. Sales Performance**  
📊 KPIs:  
- Average SQM Price by Region  
- Sales by Region  
- Offer-to-SQM Ratio by Sales Type  
- Dynamic Table Charts  
- Key Influencers (AI-powered visual in Power BI)  

---

### **3. House Type Analysis**  
📊 KPIs:  
- Interactive Filters: `Area`, `City`, `Sales Type`, `Region`  
- Avg Offer Price & Purchase Price by House Type  
- Avg Inflation, Interest Rate, and Mortgage Yield by House Type  
- Avg SQM & SQM Price by House Type  

---

## 🛠️ Tech Stack  
- **Data Source:** Google BigQuery (SQL for pre-aggregation)  
- **Visualization:** Power BI (DAX measures, interactive dashboards)  
- **Language:** DAX & SQL  
- **Data Model:** Star schema with measures & calculated tables  

              YEAR(Housing[date]) = YEAR(MAX(Housing[date])) - 1)
RETURN
    IF(prevYear <> 0, (currYear - prevYear) / prevYear, BLANK())
