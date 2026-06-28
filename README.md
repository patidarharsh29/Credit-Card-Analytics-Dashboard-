# Credit Card Analytics Dashboard

A full-stack analytics project that tracks credit card transactions, customer behavior, and revenue trends across all four quarters of 2023. The pipeline goes from raw CSV data loaded into PostgreSQL, through Power BI for interactive reporting.

---

## Project Overview

This dashboard gives a weekly view of credit card performance across 10,108 records spanning two relational tables. It covers everything from card utilization and transaction volumes to customer demographics and satisfaction scores, making it easy to spot patterns by card category, expense type, and geography.

---

## Tech Stack

| Layer | Tool |
|-------|------|
| Database | PostgreSQL |
| Visualization | Power BI |
| Data Format | CSV |
| Query Language | SQL |

---

## Database Schema

The project uses two tables under the `creditcard` schema, joined on `Client_Num`.

### `cc_detail` — Transaction Data

| Column | Type | Description |
|--------|------|-------------|
| Client_Num | INT | Unique client identifier |
| Card_Category | VARCHAR | Blue, Silver, Gold, or Platinum |
| Annual_Fees | INT | Annual fee charged |
| Activation_30_Days | INT | Activated within 30 days flag |
| Customer_Acq_Cost | INT | Cost to acquire the customer |
| Week_Start_Date | DATE | Week start date |
| Week_Num | VARCHAR | Week number |
| Qtr | VARCHAR | Quarter (Q1–Q4) |
| current_year | INT | Year of transaction |
| Credit_Limit | DECIMAL | Credit limit on the card |
| Total_Revolving_Bal | INT | Revolving balance |
| Total_Trans_Amt | INT | Total transaction amount |
| Total_Trans_Vol | INT | Total number of transactions |
| Avg_Utilization_Ratio | DECIMAL | Average credit utilization |
| Use_Chip | VARCHAR | Swipe, chip, or online |
| Exp_Type | VARCHAR | Expense category |
| Interest_Earned | DECIMAL | Interest earned |
| Delinquent_Acc | VARCHAR | Delinquency flag |

### `cust_detail` — Customer Data

| Column | Type | Description |
|--------|------|-------------|
| Client_Num | INT | Unique client identifier |
| Customer_Age | INT | Age of the customer |
| Gender | VARCHAR | Gender |
| Dependent_Count | INT | Number of dependents |
| Education_Level | VARCHAR | Highest education level |
| Marital_Status | VARCHAR | Marital status |
| state_cd | VARCHAR | State code |
| Zipcode | VARCHAR | ZIP code |
| Car_Owner | VARCHAR | Owns a car |
| House_Owner | VARCHAR | Owns a house |
| Personal_loan | VARCHAR | Has a personal loan |
| contact | VARCHAR | Contact type |
| Customer_Job | VARCHAR | Occupation |
| Income | INT | Annual income |
| Cust_Satisfaction_Score | INT | Satisfaction score (1–5) |

---

## Dataset Details

- **Total Records:** 10,108 customers
- **Time Period:** 2023 (Q1 to Q4), weekly granularity
- **Card Categories:** Blue, Silver, Gold, Platinum
- **Expense Types:** Travel, Entertainment, Bills, Grocery, Fuel, Food
- **Source Files:** `credit_card.csv`, `customer.csv`

---

## How to Set Up the Database

**1. Create the schema and tables**

Run the SQL script provided in `credit_card_database.sql`:

```sql
CREATE SCHEMA creditcard;

CREATE TABLE creditcard.cc_detail ( ... );
CREATE TABLE creditcard.cust_detail ( ... );
```

**2. Load the data**

```sql
COPY creditcard.cc_detail
FROM 'path/to/credit_card.csv'
DELIMITER ',' CSV HEADER;

COPY creditcard.cust_detail
FROM 'path/to/customer.csv'
DELIMITER ',' CSV HEADER;
```

> Update the file path to match your local directory before running COPY.

**3. Connect Power BI to PostgreSQL**

Go to `Home > Get Data > PostgreSQL database`, enter your server and database name, then select both tables. Power BI will load them through DirectQuery or Import mode depending on your preference.

---

## Dashboard Features

The Power BI report covers these key areas:

- **Revenue & Interest Tracking** — weekly and quarterly revenue with interest earned breakdowns
- **Transaction Analysis** — total transaction amount and volume by card category and expense type
- **Customer Segmentation** — income group, age group, and demographic filters
- **Utilization & Delinquency** — average utilization ratio and delinquency rate monitoring
- **Geographic View** — performance across states using `state_cd`
- **Satisfaction Scores** — customer satisfaction trends by segment

---

## Project Structure

```
credit-card-analytics/
│
├── credit_card.csv              # Raw transaction data
├── customer.csv                 # Raw customer data
├── credit_card_database.sql     # PostgreSQL setup script
├── credit_card_dashboard.pbix   # Power BI dashboard file
└── README.md
```

---

## Key DAX Measures (Power BI)

Custom columns and measures used in the report:

- `Revenue` — calculated from annual fees, transaction amounts, and interest earned
- `Age_Group` — bucketed from `Customer_Age`
- `Income_Group` — bucketed from `Income`
- `formed_date` — formatted date column for time intelligence

---

## Demo 
[!Credit Card Customer Dashboard](https://github.com/patidarharsh29/Credit-Card-Analytics-Dashboard-/blob/main/CC%20customer%20dashboard.png).
[!Credit Card Transaction Dashboard](https://github.com/patidarharsh29/Credit-Card-Analytics-Dashboard-/blob/main/CC%20transaction%20dashboard.png).

## Author

**Harsh Patidar**
B.Tech in Electronics & Communication Engineering
Samrat Ashok Technological Institute, Vidisha (2026)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](http://www.linkedin.com/in/harshpatidar1)
