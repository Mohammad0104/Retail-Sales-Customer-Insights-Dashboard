🛒 Retail Sales & Customer Insights Dashboard
A four-page Power BI report exploring retail sales, product profitability, regional performance, and customer behaviour.

📌 Project Background
High sales do not always mean strong profits. This portfolio project explores retail transactions alongside customer information to understand where revenue comes from, where margins are weak, and which customer groups contribute the most sales.
The report moves from an overall business summary to product, regional, and customer analysis. Each page includes a short finding to help explain the numbers.
This is a practice project, not a commissioned business deployment. Recommendations are analytical suggestions, not measured business outcomes. The source and generation method of the additional customer attributes should be documented before treating those findings as real customer behaviour.
🗂️ Dashboard Pages
Page	Business question	Main visuals
1. Business Overview	How is the business performing overall?	KPI cards, monthly sales, category sales, segment sales
2. Product Profitability	Which product groups generate profit or losses?	Profit ranking, sales-versus-profit scatter chart, discount comparison, category/sub-category matrix
3. Regional Performance	Which regions perform well, and where are margins weaker?	Regional sales, state profit, monthly regional sales, region/segment matrix
4. Customer Insights	Which customer groups contribute sales, and how does satisfaction vary?	Loyalty-tier treemap, segment-profit waterfall, annual loyalty-tier ribbon chart, support/satisfaction chart, top-customer matrix


🖼️ Dashboard Preview
Save the four screenshots in an images folder using the filenames below so these previews display on GitHub.
Page 1 — Business Overview
<img width="1359" height="771" alt="image" src="https://github.com/user-attachments/assets/c137888c-558e-4368-a2d1-df535bbcd65e" />

 
Page 2 — Product Profitability

 <img width="1361" height="775" alt="image" src="https://github.com/user-attachments/assets/d7e3c921-5659-4405-b31b-48659c647bdd" />

Page 3 — Regional Performance
<img width="1373" height="776" alt="image" src="https://github.com/user-attachments/assets/062c4ed1-d9c1-49da-9a17-1d680d294f14" />

 
Page 4 — Customer Insights
<img width="1376" height="780" alt="image" src="https://github.com/user-attachments/assets/ad077161-ee63-4868-b7f0-8bafcbd31758" />

 
📂 Datasets
Dataset	Records	Level of detail	Example fields
Retail sales	9,994	One order line per row	Order ID, Order Date, Customer ID, Category, Sub-Category, Region, Sales, Profit, Quantity, Discount
Customer details	813	One customer per row	customer_id, loyalty_tier, acquisition_channel, customer_segment, satisfaction_score, support_ticket_count


The sales dataset contains 5,009 distinct orders and 793 purchasing customers. All purchasing customer IDs match the customer file. Another 20 customers have no matching purchase in the sales dataset.
The report displays sales for 2014–2017. Source date parsing should be validated against the original CSV before publication.
🔧 Analytical Approach
Connecting sales and customer information
The matching fields are Customer ID in the sales data and customer_id in the customer data. Customer IDs are unique in the customer file and repeat across sales rows.
The intended model is a one-to-many relationship from Customers to Sales, with single-direction filtering. This structure allows loyalty tier and acquisition channel to filter sales while preserving one record per customer for satisfaction and support analysis. Confirm the final relationship settings in the PBIX model view.
Metric definitions
Metric	Definition
Total Sales	Sum of sales amounts
Total Profit	Sum of profit amounts
Profit Margin	Total Profit / Total Sales
Total Orders	Distinct count of Order ID
Purchasing Customers	Distinct count of Customer ID in sales
Average Order Value	Total Sales / Total Orders
Average Customer Satisfaction	Average satisfaction score from the customer table


Orders can contain multiple lines, so order counts must use distinct IDs. Customer satisfaction should be averaged from the customer table to avoid giving more weight to customers with more sales rows.
Example DAX
These expressions show the calculation logic; replace Sales and Customers with the table names in the Power BI model.
Total Sales = SUM('Sales'[Sales])

Total Profit = SUM('Sales'[Profit])

Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)

Total Orders = DISTINCTCOUNT('Sales'[Order ID])

Purchasing Customers = DISTINCTCOUNT('Sales'[Customer ID])

Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)

Average Customer Satisfaction = AVERAGE('Customers'[satisfaction_score])
⭐ Key Features
- Four connected business themes: overall performance, product profitability, regional differences, and customer insights.
- Slicers: year, region, and category on the sales pages; loyalty tier, acquisition channel, and segment on the customer page.
- Profitability analysis: compares sales with profit and highlights loss-making sub-categories.
- Expandable matrices: explore category/sub-category, region/segment, and customer/loyalty-tier detail.
- Customer analysis: compares sales by recorded loyalty tier and examines satisfaction across support-ticket counts.
- Page-level findings: short written observations connect the charts to possible next steps.
📊 Key Insights
Figures below refer to the unfiltered report.
Finding	Result	Possible next step
Overall performance	Approximately $2.30M in sales and $286.4K in profit, at a 12.47% margin	Use these totals as a baseline for further analysis
Category contribution	Technology generated approximately $836.2K in sales	Compare profitable product groups and their contribution over time
Product losses	Tables generated approximately $207K in sales but lost $17.7K	Review pricing, costs, and discount patterns
Profitable sub-category	Copiers generated approximately $55.6K in profit	Investigate which products and orders contribute most
Regional differences	West: $725.5K sales and 14.94% margin; Central: $501.2K sales and 7.92% margin	Compare product mix and discount patterns across regions
Loyalty-tier contribution	Bronze customers contributed approximately $892.4K in sales	Compare customer counts and sales per customer before judging tier value
Customer experience	Average satisfaction was 3.13; satisfaction generally declined across higher ticket-count groups, with fluctuations	Investigate recurring issues and check the number of customers in each group


These patterns show associations. They do not establish that discounts caused losses or that support tickets caused lower satisfaction.
🛠️ Tools and Skills
- Power BI Desktop: report design and visual analysis.
- DAX: KPI calculations, ratios, and distinct counts.
- Data modelling: linking transaction and customer information using customer IDs.
- Data storytelling: turning sales, profit, and customer comparisons into concise findings.
🔍 Current Limitations and Next Improvements
- Replace the summed discount-rate chart with Average Discount (%) by Category, or analyse profit margin by discount level. Summing percentage rates and displaying them as currency is not a meaningful discount metric.
- The January–December charts combine matching months across selected years. Label them as seasonal comparisons, or use Year-Month for a continuous trend.
- Validate date conversion against the original CSV; the displayed years must match the source dates.
- Confirm the top-customer matrix uses distinct order counts, applies a Top 10 filter by total sales, and sorts sales descending.
- Use straight lines and markers for the satisfaction chart so the visual does not imply measurements between integer ticket counts. Show customer counts in tooltips.
- Keep satisfaction and support calculations at customer level. Sales-date and region filters do not automatically filter the customer table in a single-direction model.
- Recorded loyalty tiers are not a history of tier changes. Annual comparisons group historical sales by each customer's recorded tier.
- Confirm the provenance of the customer attributes and label them synthetic if generated for practice.
- Static insight text reflects the unfiltered totals and should be updated or labelled when users filter the report.
📁 Suggested Repository Files
File or folder	Description
Retail_Sales_Customer_Insights.pbix	Power BI report; add the completed file
README.md	Project documentation
images/	Four dashboard screenshots using the preview filenames above
data/	Source CSV files, if their sharing terms permit redistribution


To explore the report, open the PBIX in Power BI Desktop, update source-file paths if necessary, refresh the data, and use the page slicers to compare groups.
👤 Author
Mohammad
GitHub
