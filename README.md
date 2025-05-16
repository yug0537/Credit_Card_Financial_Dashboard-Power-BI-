# Credit_Card_Financial_Dashboard-Power-BI-
To analyze and visualize credit card transaction behavior and customer demographics by leveraging SQL for data preparation and Power BI for dynamic reporting. The dashboard enables data-driven insights into revenue generation, customer segmentation, and card category performance.

## Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends,enabling stakeholders to monitor and analyze credit card operations effectively.

## Tools & Technology Used
- SQL (MySQL) for structured data storage, table creation, and data transformation
- Power BI Desktop for data modeling and dashboard development
- Power Query Editor for data cleaning and transformation
- DAX (Data Analysis Expressions) for calculated measures and KPIs
- Data Source: credit_card and customer tables created from CSV imports


## Dataset Used
- <a href="https://github.com/yug0537/Credit_Card_Financial_Dashboard-Power-BI-/blob/main/credit_card.csv">Credit Card Raw<a/>
- <a href="https://github.com/yug0537/Credit_Card_Financial_Dashboard-Power-BI-/blob/main/customer.csv">Customer Raw<a/>

## KPIs
- Core Financial KPIs:
   - Total Revenue : Sum of all customer spending across all card types : ₹55M
   - Total Transaction Amount : Sum of Total_Trans_Amt from all transactions : Indicates customer purchasing volume
   - Total Transaction Count : Reflects activity level and usage frequency
   - Total Interest Earned : Useful for evaluating profitability beyond purchases
     
- Customer & Demographic KPIs:
   - Revenue by Age Group : Track which age brackets are the most profitable (e.g., 30–40, 60+)
   - Revenue by Gender : Gender-wise breakdown of total revenue
   - Revenue by Education Level : Helps target education-level-specific campaigns (e.g., Graduates contribute the most)
   - Revenue by Occupation (Customer_Job) : Identifies top segments like Businessmen, White-collar, etc.
   - Revenue by Marital Status : Understand if single or married customers spend more
         
- Card Category KPIs:
   - Revenue by Card Category : Track revenue for each: Blue, Silver, Gold, Platinum : Example: Blue card = ₹46M
   - Interest Earned by Card Category : Profitability measure per card type
   - Annual Fees by Card Category : Total revenue earned through card fees
   - Revenue by Card Usage Type : Swipe vs Chip vs Online
     
- Time-Based KPIs:
   - Quarterly Revenue Trend : Q1 to Q4 comparison for seasonality
 
## Dashboard Interaction
- <a href="https://github.com/yug0537/Credit_Card_Financial_Dashboard-Power-BI-/blob/main/Credit_Card_Report.pbix">Dashboard<a/>

## Project Workflow
- Data Ingestion via SQL:
   - 	Imported credit_card.csv and customer.csv into MySQL using LOAD DATA INFILE and created two tables: cc_detail and cust_detail.
   - 	Cleaned and formatted data (e.g., converting dates to YYYY-MM-DD, handling nulls).
- Data Modeling in SQL:
   - Created structured schemas for both tables.
- Connecting SQL to Power BI:
   - 	Established a direct connection from Power BI to MySQL database.
	-  Imported tables without merging in Power BI (relationships handled via SQL if needed).
- Dashboard Development in Power BI:
   - Dax Queries Performed:
       - Age_Group = SWITCH(
TRUE(),
'ccdb cust_detail'[customer_age] < 30, "20-30",
'ccdb cust_detail'[customer_age] >= 30 && 'ccdb cust_detail'[customer_age] < 40, "30-40",
'ccdb cust_detail'[customer_age] >= 40 && 'ccdb cust_detail'[customer_age] < 50, "40-50",
'ccdb cust_detail'[customer_age] >= 50 && 'ccdb cust_detail'[customer_age] < 60, "50-60",
'ccdb cust_detail'[customer_age] >= 60, "60+",
"unknown")
       - IncomeGroup = SWITCH(
TRUE(),
'ccdb cust_detail'[income] < 35000, "Low",
'ccdb cust_detail'[income] >= 35000 && 'ccdb cust_detail'[income] <70000, "Med",
'ccdb cust_detail'[income] >= 70000, "High",
"unknown")
     - week_num2 = WEEKNUM('ccdb cc_detail'[week_start_date])
     - Revenue = 'ccdb cc_detail'[annual_fees] + 'ccdb cc_detail'[total_trans_amt] + 'ccdb cc_detail'[interest_earned]
      
     - Current_week_Reveneue = CALCULATE(
SUM('ccdb cc_detail'[Revenue]),
FILTER(
ALL('ccdb cc_detail'),
'ccdb cc_detail'[week_num2] = MAX('ccdb cc_detail'[week_num2])))

     - Previous_week_Reveneue = CALCULATE(
SUM('ccdb cc_detail'[Revenue]),
FILTER(
ALL('public cc_detail'),
'ccdb cc_detail'[week_num2] = MAX('ccdb cc_detail'[week_num2])-1))
-  Built visuals using card KPIs, bar charts and line graphs.
- Used slicers for time, card category, region, and gender for dynamic filtering.
- Designed two key pages:
	- Customer Demographics View
	- Transaction & Revenue View

## View Dashboard
<img width="1071" alt="Screenshot 2025-05-16 at 20 18 47" src="https://github.com/user-attachments/assets/f574950a-5fe8-4941-af22-17a1598e4a9c" />
<img width="1071" alt="Screenshot 2025-05-16 at 20 19 13" src="https://github.com/user-attachments/assets/bc2d2bac-9e00-4c8d-88b5-a247bf535328" />

## Key Insights
- Total Revenue: ₹55M | Transaction Amount: ₹45M | Transaction Count: 656K
- Blue Card customers contributed over ₹46M in revenue—dominating the portfolio.
- Businessmen and white-collar workers generated the highest income and interest.
- Majority of customers fall under medium and low salary groups, with spending concentrated in fuel, groceries, and bills.
- Age groups 30–40 and 60+ are the most financially active.
- Revenue is distributed evenly across all four quarters, with Q3 slightly leading in transactions.
- States like CA, NY, and TX emerged as top revenue contributors.

## Conclusion
- This project successfully demonstrates how to build a scalable and professional BI solution by:
- Leveraging SQL for robust data handling and backend logic
- Using Power BI to deliver visually rich and insight-driven reports
- It showcases how organizations can use a SQL-to-Power BI pipeline to transform raw financial and customer data into powerful dashboards that guide    strategic business decisions, product targeting, and customer engagement.





