# Sales-Performance-Dashboard

An interactive sales dashboard built in Tableau, covering sales, profit, and quantity performance across a four-year period (2020-2023). This project focuses on the full workflow from raw, messy data to a clean, decision-ready dashboard, rather than jumping straight into visualization.

## Overview

The goal of this project was to turn a raw transactional dataset into a dashboard that helps sales managers and executives track performance, spot trends, and compare product subcategories year over year. The dashboard answers four core questions:

- How are we performing on key metrics this year compared to last year
- Which months had the highest and lowest sales
- How do individual product subcategories compare on sales versus profit
- Which weeks performed above or below the average

## Dataset

The dataset consists of four related tables: Orders, Customers, Products, and Location, totaling 9,994 order records. Two versions of the dataset were provided, an EU version and a non-EU version. This project intentionally uses the EU version, which came in a raw, unprocessed format, to demonstrate a full data cleaning workflow rather than working with pre-cleaned data.

## Tools

- Python (Pandas) for data cleaning and preprocessing
- Tableau Public for data modeling and dashboard design

## Data Cleaning Process

The raw EU dataset had several issues that needed to be resolved before it was usable:

- **Delimiter**: the CSV files used semicolons instead of commas
- **Decimal format**: numeric columns (Sales, Discount, Profit) used commas as the decimal separator instead of periods, common in European number formatting
- **Encoding**: the files were encoded in cp437 rather than UTF-8, which caused accented characters in customer names to break silently if read with the wrong encoding
- **Date format**: Order Date and Ship Date were written in day-first format (DD/MM/YYYY), which caused date parsing errors when read with default settings

Each issue was resolved using Pandas: correcting the separator, converting decimal formatting, reading files with the correct encoding, and parsing dates with day-first logic. The cleaning process also included duplicate removal, missing value checks, and referential integrity validation to confirm that every Customer ID, Product ID, and Postal Code in the Orders table matched a corresponding record in the other tables.

## Data Model

Orders serves as the central table, connected to the other three tables through shared key fields:

- Orders to Customers via Customer ID
- Orders to Products via Product ID
- Orders to Location via Postal Code

There is no direct relationship between Customers, Products, and Location; all connections are established through Orders.

## Dashboard Features

**KPI Overview**
Total Sales, Total Profit, and Total Quantity for the selected year, each shown with year-over-year percentage change and a monthly trend line highlighting the highest and lowest performing months.

**Sales and Profit by Subcategory**
A side-by-side comparison of current year versus prior year sales across product subcategories, paired with profit contribution to identify categories that perform well on sales but underperform on profit.

**Sales and Profit Trends Over Time**
Weekly sales and profit trends for the current year, with an average benchmark line and color coding to flag weeks that fall above or below the average.

## Key Results (2023)

- Total Sales: 733 thousand dollars, up 20.4 percent year over year
- Total Profit: 93 thousand dollars, up 14.2 percent year over year
- Total Quantity: 12 thousand units, up 26.8 percent year over year

## Repository Structure

```
sales-dashboard-project/
├── datasets/
│   └── eu/
│       ├── Customers.csv
│       ├── Location.csv
│       ├── Orders.csv
│       └── Products.csv
├── cleaning/
│   ├── 1_clean_customers.py
│   ├── 2_clean_location.py
│   ├── 3_clean_products.py
│   └── 4_clean_orders.py
├── output/
│   ├── Customers_clean.csv
│   ├── Location_clean.csv
│   ├── Orders_clean.csv
│   └── Products_clean.csv
├── visualization.twb
└── README.md
```

## Author

Nadira Khumaira Putri
