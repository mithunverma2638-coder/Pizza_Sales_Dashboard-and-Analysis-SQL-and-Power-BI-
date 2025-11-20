# 🍕🍕 Pizza Sales Dashboard & Analysis SQL & Power BI 🍕🍕



# 🍕 Pizza Sales Analysis Dashboard & SQL Insights

## 📌 Project Overview
This project focuses on analyzing pizza sales data to uncover **business insights** and create an **interactive Power BI dashboard**. It also includes **SQL queries** for answering critical business questions.

<img width="4000" height="2250" alt="Pizza Sales" src="https://github.com/user-attachments/assets/bc7bebd4-2ccc-4f32-9810-15f8f97faf71" />

---

## 🎯 Objectives
- Visualize **sales performance** using Power BI.
- Answer **business questions** with SQL.
- Identify **top-selling pizzas**, **revenue trends**, and **customer preferences**.

---

## 📂 Files Included
### ✅ **Pizza Sales.pptx**
- A **Power BI dashboard design** showcasing:
  - **Total Revenue KPI**
  - **Revenue by Category**
  - **Top Pizza Types by Revenue**
  - **Monthly Revenue Trend**
  - **Size Preference Analysis**
  - **Detailed Table for Drill-Down**

### ✅ **Questions.md**
- A collection of **SQL queries** categorized as:
  - **Basic**: Total orders, total revenue, highest-priced pizza, most common size.
  - **Intermediate**: Category-wise quantity, hourly distribution, top pizzas by quantity.
  - **Advanced**: Percentage contribution, cumulative revenue, top pizzas by category.

---

## 🖥️ Power BI Dashboard Features
- **KPI Cards**: Total Revenue, Total Orders
- **Bar Chart**: Top 10 Pizza Types by Revenue
- **Pie Chart**: Revenue by Category
- **Horizontal Bar**: Size Preferences
- **Line Chart**: Monthly Revenue Trend
- **Table**: Pizza Name, Category, Quantity, Revenue
- **Interactive Filters**: Category, Size, Month

### 🔑 DAX Measures
```DAX
Revenue = order_details[quantity] * RELATED(pizzas[price])



