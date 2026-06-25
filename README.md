# Favour Ogunbiyi 
## Data Analyst

**Data Analyst** with project experience spanning **SQL business analysis, retail banking data modelling, Python-based feature engineering, and e-commerce data cleaning**. My work focuses on cleaning messy transactional data, building analysis-ready structures, and generating insights from business datasets through SQL analysis, exploratory analysis, and technical reporting. I’m particularly interested in data roles that combine analytics, data modelling, and pipeline-oriented thinking.

<p align="center">
  <a href="https://www.linkedin.com/in/favour-ogunbiyi-b64928162/"><img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin"></a>
  <a href="https://github.com/favourogunbiyi"><img src="https://img.shields.io/badge/Github-Connect-black?style=for-the-badge&logo=github"></a>
  <a href="mailto:ogunbiyifavour28@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-green?style=for-the-badge&logo=gmail"></a>
</p>

## Core Tools & Skills
**Languages & Querying**  `SQL` `Python`

**Analytics & Reporting** `Excel` `Power BI` `KPI reporting` `Exploratory Data Analysis (EDA)`

**Data Preparation**      `Data cleaning` `Data validation` `Transformation` `Missing-value analysis` `Duplicate detection` `Feature engineering`

**Data Modelling**        `Star schema design` `Fact and dimension modelling` `Slowly changing dimensions (SCD)` `Analytics-ready warehouse design` `ETL / ELT planning`

**Workflow & Communication** `Git/GitHub` `Technical documentation` `Analytical problem framing` `Business insight communication`

## Featured Projects
## 1) TradeZone E-Commerce Analytics
**Project Type:** SQL Business Analysis  
**Tools:** PostgreSQL, SQL, Data Cleaning, Business Analysis  
**Project Link:** [TradeZone-E-Commerce-Analytics-SQL-Business-Analysis](https://github.com/favourogunbiyi/TradeZone-E-Commerce-Analytics-SQL-Business-Analysis)

### Business Problem
TradeZone, a multi-vendor e-commerce marketplace, had customer, order, payment, review, seller, and product data spread across multiple raw tables but no clear analytical layer for decision-making. Leadership needed answers to recurring business questions around **conversion, revenue concentration, seller quality, payment behaviour, and customer spending patterns**.

### Solution
I built a SQL-driven analysis workflow that cleaned the marketplace data, investigated performance across multiple business areas, and translated the findings into a structured **Executive Analyst Memo**.

### What This Project Solved
- **Conversion visibility:** Identified states generating strong customer acquisition but weak purchase conversion, helping highlight where customer growth was not translating into revenue.
- **Revenue concentration:** Surfaced the product categories and items driving the largest share of sales, giving the business a clearer view of revenue dependency.
- **Seller quality monitoring:** Connected fulfilment performance and review behaviour to evaluate which sellers were supporting or damaging customer experience.
- **Customer value segmentation:** Analysed spending patterns to separate low-, mid, and high-value customer groups for more targeted retention and marketing decisions.
- **Performance-based incentives:** Built the analytical logic for a seller bonus qualification view using both revenue contribution and review quality.

### What I Delivered
- **Cleaned and validated 7 SQL tables** before analysis
- **Answered 8 business questions** across conversion, product performance, seller quality, customer spend, payment behaviour, and reward qualification
- **Documented unresolved data-quality issues** and flagged risks that could affect interpretation
- **Produced an Executive Analyst Memo** that translated SQL outputs into business-facing findings and recommendations

### Analytical Highlights
- **SQL joins & aggregations:** combined multi-table marketplace data to answer business questions across customers, sellers, products, and payments
- **Data quality checks:** handled missing values, duplicates, inconsistent category labels, and city standardisation issues before analysis
- **Business framing:** structured the work around decisions and performance questions, not just raw metrics
- **Insight communication:** converted technical findings into written recommendations suitable for non-technical stakeholders

### Example SQL Logic
> Replace this block with one of your best real TradeZone queries — ideally a query that shows business thinking, not just basic cleaning.
-- Replace this with your actual TradeZone SQL query from the repo
````
WITH state_conversion AS (
    SELECT
        c.customer_state,
        COUNT(DISTINCT c.customer_id) AS total_customers,
        COUNT(DISTINCT o.order_id) AS total_orders,
        ROUND(
            COUNT(DISTINCT o.order_id)::numeric /
            NULLIF(COUNT(DISTINCT c.customer_id), 0), 4
        ) AS conversion_rate
    FROM customers c
    LEFT JOIN orders o
        ON c.customer_id = o.customer_id
    GROUP BY c.customer_state
)
SELECT
    customer_state,
    total_customers,
    total_orders,
    conversion_rate
FROM state_conversion
ORDER BY conversion_rate ASC, total_customers DESC;
````
### Why this project matters

This project shows my ability to take raw transactional marketplace data and turn it into business-facing analysis through cleaning, SQL investigation, and structured reporting. It reflects the kind of analyst work that sits between messy source data and decision-making.

## 2) Palladium Bank Retail Data Modelling

**Project Type**: Dimensional Modelling / Analytics-Ready Data Design
**Tools**: SQL, MySQL, Star Schema Design, Dimensional Modelling, ETL Planning
**Project Link**: Palladium-Bank-Retail-Data-Modelling-Project

## Business Problem

Palladium Bank had 18 months of retail banking transaction data, but analysts were still reporting directly from raw transaction logs. This made reporting slow, inconsistent, and difficult to scale across customer, branch, product, and transaction-channel analysis.

## The business needed a cleaner analytical structure that could support questions such as:
- Which customer segments generate the most fee income?
- Which branches and channels drive the highest transaction activity?
-Which high-value customers are becoming inactive?
-Which products contribute more to deposits vs withdrawals?
### Solution
I designed a retail banking star schema that transformed raw transaction-level data into an analytics-ready model for consistent reporting and downstream business analysis.

### What This Project Solved
- Reporting consistency: replaced raw-log analysis with a structured fact-and-dimension model designed for repeatable reporting
- Customer analysis readiness: created a model that supports segmentation, inactivity analysis, and customer-level value tracking
- Channel and branch performance reporting: made it easier to compare banking activity across service channels and locations
- Historical analysis support: introduced Slowly Changing Dimension logic where business reporting required history preservation
- Scalable analytics design: documented ETL, indexing, and partitioning considerations to make the warehouse usable beyond a one-off model sketch

### What I Delivered
- Defined the analytical grain at the transaction level
- Designed one fact table and multiple dimensions for customers, products, branches, channels, and dates
- Mapped SCD logic for dimensions where historical changes matter
- Documented ETL flow for initial loads and daily incremental updates
- Outlined data-quality checks for duplicates, null amounts, invalid dates, and unresolved customers
- Included performance planning through indexing, partitioning, and pre-aggregation considerations

## Star Schema Snapshot

Replace this placeholder with your actual star schema image path when you add the diagram to the repo.

![Palladium Bank Star Schema](images/palladium-star-schema.png)

````
If you want a temporary text version before adding the image, you can use this:

                    +------------------+
                    |   dim_customer   |
                    +------------------+
                             |
                             |
+-------------+     +------------------+     +--------------+
| dim_branch  |-----| fact_transaction |-----| dim_product  |
+-------------+     +------------------+     +--------------+
                             |
                             |
                    +------------------+
                    |   dim_channel    |
                    +------------------+
                             |
                             |
                    +------------------+
                    |    dim_date      |
                    +------------------+
````
### Analytical Highlights
- Dimensional modelling: structured raw banking data into a reusable reporting model
- Star schema design: built around transaction-level grain for downstream analytics
- SCD decision-making: considered where history tracking was necessary for accurate reporting
- ETL thinking: planned how raw operational data would be transformed into a reporting layer
- Performance awareness: included indexing and partitioning considerations rather than stopping at logical design

### Why This Project Matters
This project demonstrates that I can think beyond dashboards and SQL queries alone. It shows how I approach analytics-ready data design, which matters when the business problem is not only what should be analyzed but also how the data should be structured so analysis can happen efficiently and consistently.

### 3) MovieLens Feature Engineering & Exploratory Data Analysis
**Project Type**: Python Data Preparation & Exploratory Analysis
**Tools**: Python, Pandas, NumPy, Matplotlib, Seaborn
**Project Link**: MovieLens-Engineering-and-EDA-Project

## Business Problem
MovieLens contains user ratings, movie metadata, and tagging behaviour, but the raw files do not directly explain the patterns behind user engagement. To make the dataset more useful for analysis, I needed to transform flat rating records into a richer feature layer that could support deeper exploration of rating behaviour, genre patterns, and engagement signals.

## Solution
I built a Python-based data preparation and exploratory analysis workflow that merged the source files, cleaned inconsistencies, engineered new features, and explored how user ratings vary across movie attributes and engagement behaviour.

What This Project Solved
Made raw ratings more analysis-ready: transformed timestamps and movie metadata into usable behavioural features
Added context to user behaviour: engineered features such as movie age, genre count, tag activity, and rating frequency to move beyond a flat ratings table
Improved exploratory depth: created a stronger base for analyzing how content characteristics and user engagement relate to rating patterns
Clarified modelling boundaries: documented where exploratory analysis ends and where a production recommendation system would require additional work
What I Delivered
Merged and cleaned multiple MovieLens source tables
Handled missing tags and removed unrecoverable records
Converted Unix timestamps into usable time-based fields
Engineered analytical features including release year, movie age, genre count, tag activity, and user rating frequency
Explored rating behaviour across decades, genres, and engagement levels
Documented analytical limitations and next-step opportunities
Analytical Highlights
Feature engineering: created richer variables for content and user-behaviour analysis
Python data cleaning: prepared a multi-table dataset for exploratory work
EDA: explored relationships between ratings, movie characteristics, and engagement signals
Analytical communication: explained findings while clearly separating exploration from predictive modelling
Why This Project Matters

This project shows my ability to use Python not just for cleaning data, but for building a stronger analytical layer on top of raw source files. It reflects feature engineering, exploratory thinking, and the ability to turn a flat dataset into a more informative one.

Supporting Project
E-Commerce Product Data Cleaning & Title Optimization

Project Type: Excel Data Cleaning / Catalog Standardisation
Tools: Excel, Data Cleaning, Text Standardisation
Project Link: E-Commerce-Product-Data-Cleaning-Title-Optimization

Business Problem

Messy product catalogue data creates friction for both analysis and operations. Duplicate records, inconsistent naming, missing values, and overly long product titles reduce reporting quality and make product-level analysis harder to trust.

Solution

I built an Excel-based cleaning workflow to standardize product records, improve title consistency, and create cleaner fields for downstream analysis and reporting.

What This Project Solved
Catalog standardisation: reduced inconsistencies in text-heavy product records
Duplicate cleanup: improved confidence in product-level analysis by identifying repeated listings
Title usability: created a cleaner short_title field for easier downstream reporting and display
Data preparation support: strengthened the quality of the dataset before any analysis layer was built
What I Delivered
Removed duplicates and standardized text-heavy product fields
Handled missing values and documented cleaning decisions
Applied outlier checks where product records required additional review
Created a short_title feature to improve title consistency and reporting usability
Analytical Highlights
Excel-based cleaning workflow
Text standardisation for messy catalogue data
Preparation of analysis-ready product records
Practical data-quality improvement before reporting
Why This Project Matters

Although smaller than the SQL and Python projects in this portfolio, this work shows an important part of analytics: improving data quality before analysis begins. It adds evidence of hands-on cleaning work in Excel and strengthens the portfolio’s coverage of end-to-end data preparation.

Current Projects
TradeZone Marketplace Performance Dashboard (In Progress)

Project Type: Power BI Dashboard / KPI Reporting
Tools: Power BI, SQL, Data Modelling, KPI Reporting

Project Context

This is a follow-up reporting project built from the TradeZone e-commerce analysis domain. It is not positioned as part of the original SQL case study, but as a separate Power BI project designed to turn marketplace analysis into a more interactive reporting experience.

Current Goal

Build a Power BI dashboard that supports recurring monitoring of:

Revenue and order performance
Customer conversion patterns
Seller quality and review trends
Payment behaviour and category-level performance
Why It’s in Progress

The analytical direction is defined, but the dashboard build is still underway. It currently sits in the portfolio as an active reporting project rather than a completed case study.

Portfolio Snapshot by Skill Area
Skill Area	Evidence in Portfolio
SQL Business Analysis	TradeZone E-Commerce Analytics
Data Cleaning & Validation	TradeZone, MovieLens, Product Cleaning
Dimensional Modelling	Palladium Bank Retail Data Modelling
Feature Engineering	MovieLens
Excel-Based Data Preparation	Product Cleaning
Technical Documentation	TradeZone, Palladium, MovieLens
Reporting / Dashboard Direction	TradeZone Marketplace Performance Dashboard (In Progress)
What This Portfolio Shows

Across these projects, my work demonstrates the ability to:

clean and validate messy transactional, customer, and catalogue datasets
write SQL to answer business questions and support commercial analysis
design analytics-ready structures that make downstream reporting easier
engineer useful features and explore behavioural patterns in Python
communicate findings, assumptions, and limitations through structured technical documentation
Current Focus

I’m continuing to strengthen this portfolio through work in:

Power BI dashboard reporting
KPI and performance analysis
analytics-ready data modelling
projects that connect SQL analysis, data cleaning, modelling, and reporting into a single workflow
Contact
LinkedIn: [Add your LinkedIn link here]
GitHub: https://github.com/favourogunbiyi
Email: [Add your email here]
