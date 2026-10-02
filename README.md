# 🛒 Retail Sales & Customer Insights Dashboard

> A four-page Power BI report exploring retail sales, product profitability, regional performance, and customer behaviour using two Excel datasets.

---

## 📌 Project Background

High sales do not always mean strong profits. I built this portfolio project to explore where retail revenue comes from, which product groups lose money, and how performance differs across regions and customer groups.

I brought two Excel datasets together, cleaned and prepared the data, and created a Power BI report covering four business areas. Each page includes key metrics, visual comparisons, and a short insight to explain the findings.

The goal was to turn sales and customer data into clear information that could support decisions about product performance, regional priorities, and customer experience.

> This is a portfolio project using practice data. The findings illustrate analytical opportunities; they do not represent measured improvements in a real business.

---

## 🗂️ Dashboard Pages

| Page | Business Question | Main Visuals |
| --- | --- | --- |
| **1. Business Overview** | How is the business performing overall? | KPI cards, monthly sales comparison, sales by category, sales by customer segment |
| **2. Product Profitability** | Which product groups generate profit or losses? | Profit by sub-category, sales-versus-profit scatter chart, discount comparison, category and sub-category matrix |
| **3. Regional Performance** | Which regions perform well, and where are margins weaker? | Sales by region, profit by state, monthly regional sales, region and segment matrix |
| **4. Customer Insights** | Which customer groups contribute sales, and how does satisfaction vary? | Loyalty-tier treemap, segment-profit waterfall, annual loyalty-tier ribbon chart, support and satisfaction chart, top-customer matrix |

---

## 🖼️ Dashboard Preview

### Page 1 — Business Overview

Provides an overview of sales, profit, profit margin, and orders. Category and customer-segment comparisons show the main sources of revenue.

<img width="1359" height="771" alt="Business Overview dashboard showing sales, profit, orders, and category and segment comparisons" src="https://github.com/user-attachments/assets/c137888c-558e-4368-a2d1-df535bbcd65e" />

### Page 2 — Product Profitability

Compares sales and profit across sub-categories to identify strong contributors and loss-making product groups.

<img width="1361" height="775" alt="Product Profitability dashboard with sub-category profit ranking, scatter chart, and detailed matrix" src="https://github.com/user-attachments/assets/d7e3c921-5659-4405-b31b-48659c647bdd" />

### Page 3 — Regional Performance

Compares regional sales, state-level profit, and profit margins across customer segments within each region.

<img width="1373" height="776" alt="Regional Performance dashboard comparing sales, profit, and margins across regions and states" src="https://github.com/user-attachments/assets/062c4ed1-d9c1-49da-9a17-1d680d294f14" />

### Page 4 — Customer Insights

Explores loyalty-tier sales, customer-segment profit, high-spending customers, and the relationship between support ticket counts and satisfaction.

<img width="1376" height="780" alt="Customer Insights dashboard with loyalty tiers, segment profit, support satisfaction, and top customers" src="https://github.com/user-attachments/assets/ad077161-ee63-4868-b7f0-8bafcbd31758" />

---

## 📂 Data Sources and File Formats

Two Excel workbooks provide the sales and customer information used in this project.

| File | Format | Description |
| --- | --- | --- |
| `Super_Market.xls` | Excel workbook | Retail transactions, products, locations, sales, profit, quantity, and discounts |
| `Super_Market2.xls` | Excel workbook | Customer details, loyalty tiers, acquisition channels, satisfaction scores, and support ticket counts |
| `Super_Market_Dashboard.pbix` | Power BI report | Report pages, data model, calculations, and visuals |
| `README.md` | Markdown | Project documentation and dashboard previews |

The filenames above follow the names shown in the project folder. Confirm the full extensions when uploading, since Windows can hide known file extensions.

### Dataset Structure

| Dataset | Source Records | Level of Detail | Key Fields |
| --- | ---: | --- | --- |
| Retail sales | 9,994 | One order line per row | Order ID, Order Date, Customer ID, Category, Sub-Category, Region, Sales, Profit, Quantity, Discount |
| Customer details | 813 | One customer per row | customer_id, customer_segment, loyalty_tier, acquisition_channel, satisfaction_score, support_ticket_count |

The supplied source datasets contain **5,009 distinct orders** and **793 purchasing customers**. All purchasing customer IDs match the customer dataset. Another **20 customer records have no matching purchase** in the supplied sales data.

These counts describe the source files; retained records after combining depend on the join method used.

---

## 🔧 Data Preparation and Analytical Approach

### Combining and Cleaning the Data

I combined information from the two Excel files and cleaned the data before building the report. The shared customer identifier connects transaction information with customer attributes:

- **Sales file:** `Customer ID`
- **Customer file:** `customer_id`

The preparation stage made the sales and customer information usable together for reporting. The analysis then focused on sales totals, profitability, order activity, customer groups, and satisfaction.

### Handling Different Levels of Detail

Sales data contains multiple rows for customers and orders. Customer details contain one row per customer. This distinction matters when calculating metrics:

- Count **distinct Order IDs** to calculate total orders.
- Count **distinct Customer IDs in sales** to calculate purchasing customers.
- Calculate profit margin as **total profit divided by total sales**.
- Calculate average order value as **total sales divided by distinct orders**.
- Calculate satisfaction at **one record per customer**. Averaging a merged sales table can give frequent purchasers more weight because their satisfaction score repeats across order lines.

### Key Metrics

| Metric | Definition | Unfiltered Report Value |
| --- | --- | ---: |
| Total Sales | Sum of sales | $2.30M |
| Total Profit | Sum of profit | $286.4K |
| Profit Margin | Total Profit / Total Sales | 12.47% |
| Total Orders | Distinct Order IDs | 5,009 |
| Purchasing Customers | Distinct Customer IDs in sales | 793 |
| Average Order Value | Total Sales / Total Orders | $458.61 |
| Average Customer Satisfaction | Average satisfaction score at customer level | 3.13 displayed |

### Example DAX Calculations

These examples illustrate the metric definitions. Replace the table names with the names used in your model. The satisfaction example assumes a separate table containing one row per customer.

```dax
Total Sales =
SUM('Sales'[Sales])

Total Profit =
SUM('Sales'[Profit])

Profit Margin % =
DIVIDE([Total Profit], [Total Sales], 0)

Total Orders =
DISTINCTCOUNT('Sales'[Order ID])

Purchasing Customers =
DISTINCTCOUNT('Sales'[Customer ID])

Average Order Value =
DIVIDE([Total Sales], [Total Orders], 0)

Average Customer Satisfaction =
AVERAGE('Customers'[satisfaction_score])
```

---

## ⭐ Key Features

**Four-Page Business Story**  
The report moves from overall performance to product profitability, regional differences, and customer insights.

**Interactive Slicers**  
Year, region, and category slicers support sales analysis. Loyalty tier, acquisition channel, and customer segment slicers support customer comparisons.

**Product Profitability Analysis**  
Profit rankings and a sales-versus-profit scatter chart reveal product groups that generate substantial revenue but weak or negative profit.

**Detailed Matrices**  
Expandable tables provide category/sub-category, region/segment, and customer/loyalty-tier detail.

**Customer Experience Analysis**  
The support chart compares average satisfaction across ticket-count groups to highlight patterns for further investigation.

**Written Insights**  
Each page includes a short observation connecting the visuals to a business question or possible next step.

---

## 📊 Key Insights

The following findings refer to the unfiltered report.

- **Overall performance:** Sales reached approximately **$2.30M**, generating **$286.4K in profit** at a **12.47% margin**.
- **Category contribution:** Technology generated the highest category sales at approximately **$836.2K**.
- **Customer segments:** The Consumer segment contributed approximately **$1.16M in sales**, the largest share among the three segments.
- **Product profitability:** Copiers generated approximately **$55.6K in profit**, while Tables recorded a **$17.7K loss** despite approximately **$207K in sales**.
- **Regional differences:** The West generated **$725.5K in sales** at a **14.94% margin**. The Central region generated **$501.2K in sales** but achieved a lower **7.92% margin**.
- **Loyalty tiers:** Bronze customers contributed the most total sales at approximately **$892.4K**. Customer counts and sales per customer are needed to compare individual customer value across tiers.
- **Customer experience:** Average satisfaction generally declined across higher support-ticket-count groups, although the pattern fluctuated.

## 💡 Suggested Business Actions

| Area | Suggested Action |
| --- | --- |
| Loss-making products | Review pricing, costs, and discount patterns for Tables and other unprofitable sub-categories |
| Regional margins | Compare product mix and discount patterns in Central with stronger-margin regions |
| Customer value | Compare profit and sales per customer across loyalty tiers before setting retention priorities |
| Customer support | Investigate recurring issues and check how many customers are represented in each ticket-count group |

These are areas for investigation. The report does not establish that discounts caused losses or that support tickets caused lower satisfaction.

---

## 🛠️ Tools and Skills

- **Microsoft Excel:** source workbooks containing sales and customer data.
- **Power BI Desktop:** report development, KPI presentation, and visual analysis.
- **DAX:** calculations for totals, ratios, and distinct counts.
- **Data preparation:** combining and cleaning sales and customer information.
- **Data storytelling:** communicating findings through focused pages and short written insights.

---

## 🔍 Interpretation Notes and Future Improvements

- **Discount analysis:** The current screenshot shows summed discount rates formatted as currency. Replace this with average discount percentage by category or profit margin by discount level.
- **Time analysis:** The January–December charts combine months across selected years. They show seasonal comparisons; use Year-Month to show a continuous timeline.
- **Customer averages:** Validate satisfaction calculations at customer level after combining the files, so repeated transaction rows do not distort the average.
- **Loyalty history:** Annual sales are grouped by the customer's recorded loyalty tier. The data does not track historical tier changes.
- **Customer attributes:** Document the source of the additional customer fields and identify them as synthetic if they were generated for practice.
- **Report presentation:** Sort the top-customer table by sales descending, verify distinct order counts, and improve readability of smaller chart labels.
- **Static findings:** Written insights reflect the unfiltered report and do not automatically change with slicer selections.

---

## 🚀 How to Explore the Project

1. Download `Super_Market_Dashboard.pbix` and the two Excel source files.
2. Open the report in Power BI Desktop.
3. Update the source-file paths to the location of the Excel files on your computer.
4. Refresh the report.
5. Explore the four pages and use slicers to compare years, regions, categories, and customer groups.

---

## 👤 Author

**Mohammad**  
B.Sc. in Computer Science, Data Science concentration — Ontario Tech University

[GitHub](https://github.com/Mohammad0104)
