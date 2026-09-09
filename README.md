# Online Retail Sales & Customer Performance Dashboard

An interactive Tableau dashboard that analyzes online retail revenue, customer purchasing behavior, repeat purchases, and geographic revenue concentration.

## Project Overview

This project uses online retail transactional data to answer the following business questions:

1. How did revenue change over time?
2. What share of identifiable customers made repeat purchases?
3. How much revenue came from repeat customers versus one-time customers?
4. Which countries generated the most revenue?
5. Which international markets lead when the United Kingdom is excluded?

The dashboard was built in Tableau using calculated fields, level-of-detail (LOD) expressions, filters, context filters, KPI cards, and bar charts.

## Dashboard Preview

_Add a screenshot of your final Tableau dashboard here after uploading it to GitHub._

```text
images/dashboard_overview.png
```

## Dashboard Components

The dashboard includes:

- Total Revenue KPI
- Total Orders KPI
- Unique Customers KPI
- Repeat Purchase Rate KPI
- Monthly Revenue Trend
- Revenue by Customer Type
- Repeat Customer Rate
- Top 10 Countries by Revenue
- Top Non-UK Countries by Revenue

## Data Preparation

The analysis uses a `Valid Sale` filter to exclude invalid or cancelled transactions from revenue and customer metrics.

Only valid transactions were included in the final revenue, order, customer, and country analyses.

### Important Data Note

The latest transaction date in the dataset is:

```text
09 December 2010, 20:01
```

Therefore, December is an incomplete month and should not be compared directly with complete calendar months in the monthly revenue trend.

## Key Tableau Calculations

### Revenue

```tableau
[Quantity] * [UnitPrice]
```

Revenue is aggregated as:

```tableau
SUM([Revenue])
```

### Orders per Customer

```tableau
{ FIXED [Customer ID] : COUNTD([Invoice]) }
```

This LOD expression counts the number of distinct invoices for each customer.

### Customer Type

```tableau
IF [Orders per Customer] >= 2 THEN "Repeat customer"
ELSE "One-time customer"
END
```

Customers who made two or more distinct orders are classified as repeat customers. Customers with one distinct order are classified as one-time customers.

### Repeat Purchase Rate

```tableau
COUNTD(
    IF [Customer Type] = "Repeat customer"
    THEN [Customer ID]
    END
)
/
COUNTD([Customer ID])
```

This field was formatted as a percentage with one decimal place.

### Context Filter Note

Because `Customer Type` uses a `FIXED` LOD expression, the `Valid Sale = True` filter was added as a context filter on customer-related worksheets.

This ensures that invalid or cancelled transactions are excluded before Tableau calculates the number of orders per customer.

## Key Findings

### Customer Behavior

| Metric | Result |
|---|---:|
| Identifiable customers included in segmentation | 4,312 |
| One-time customers | 1,419 |
| Repeat customers | 2,893 |
| Repeat purchase rate | 67.1% |

A total of 2,893 out of 4,312 identifiable customers made at least two distinct purchases.

This resulted in a repeat purchase rate of **67.1%**.

> Repeat purchase rate is not the same as retention rate. It measures whether a customer made two or more purchases during the available data period, while retention requires a defined time period after the first purchase, such as return within 30 days or return in the next month.

### Revenue by Customer Type

| Customer Type | Revenue | Revenue Share |
|---|---:|---:|
| One-time customers | Approximately £499K | Approximately 5.6% |
| Repeat customers | Approximately £8.333M | Approximately 94.4% |
| Total attributable revenue | Approximately £8.832M | 100.0% |

Repeat customers generated approximately **£8.33M**, representing **94.4%** of revenue attributable to customers with a known Customer ID.

Although repeat customers represented 67.1% of identifiable customers, they generated a disproportionately large share of revenue.

This suggests that customer retention, post-purchase communication, reactivation campaigns, and CRM initiatives may be high-leverage growth opportunities.

### Geographic Revenue Concentration

The United Kingdom was the dominant market, generating approximately:

```text
£7.415M in valid revenue
```

The top non-UK markets were:

| Rank | Country | Revenue |
|---:|---|---:|
| 1 | EIRE | Approximately £356.1K |
| 2 | Netherlands | Approximately £268.8K |
| 3 | Germany | Approximately £202.4K |
| 4 | France | Approximately £146.2K |
| 5 | Sweden | Approximately £53.2K |
| 6 | Denmark | Approximately £50.9K |
| 7 | Spain | Approximately £47.6K |
| 8 | Switzerland | Approximately £43.9K |
| 9 | Australia | Approximately £31.4K |
| 10 | Portugal | Approximately £23.8K |

The analysis shows strong geographic concentration in the United Kingdom.

EIRE, the Netherlands, Germany, and France are the strongest international markets and could be prioritized for further market-level analysis.

## Business Insights

- Revenue depends heavily on repeat customers.
- Repeat customers generated approximately 94.4% of attributable revenue.
- A high repeat purchase rate indicates that returning customers are an important source of business value.
- The United Kingdom is the company’s dominant market.
- International revenue is concentrated in a small group of European countries.
- EIRE, the Netherlands, Germany, and France represent the strongest non-UK growth opportunities.
- December should be interpreted carefully because the data only includes transactions through 09 December 2010.

## Repository Structure

```text
online-retail-tableau-dashboard/
│
├── README.md
│
├── tableau/
│   └── online_retail_dashboard.twbx
│
├── images/
│   ├── dashboard_overview.png
│   ├── monthly_revenue_trend.png
│   ├── revenue_by_customer_type.png
│   ├── repeat_customer_rate.png
│   ├── top_10_countries_revenue.png
│   └── top_non_uk_countries_revenue.png
│
├── data/
│   └── README.md
│
└── docs/
    └── project_notes.md
```

## How to Use

1. Download or clone this repository.
2. Open the Tableau packaged workbook from the `tableau` folder.
3. If Tableau requests a data connection, update it to point to the local dataset.
4. Explore the dashboard using the available filters.

## Dashboard Filters

The dashboard can include the following filters:

- `Country`
- `Invoice Date`

The `Country` filter can be applied to all worksheets using the same data source.

The date filter should be used carefully with customer-segment worksheets because customer type is based on total order history. Applying a date filter can change whether a customer is classified as one-time or repeat within the selected period.

`Valid Sale = True` remains a hidden technical filter and should not be exposed to dashboard users.

## Tools Used

- Tableau Desktop
- Tableau calculated fields
- Tableau LOD expressions
- Tableau filters and context filters
- Data cleaning and validation
- Exploratory data analysis
- Business data visualization

## Limitations

- The dataset ends during December, so the final month is incomplete.
- Customer segmentation includes only transactions with a known `Customer ID`.
- Repeat purchase rate is not equivalent to cohort retention.
- Revenue from repeat customers is cumulative across the observed period.
- The analysis describes observed patterns and does not prove causation.
- The high revenue contribution from repeat customers does not necessarily mean every repeat order is larger than every first order.

## Author

**Olha Sapon**

Data Analyst Portfolio Project
