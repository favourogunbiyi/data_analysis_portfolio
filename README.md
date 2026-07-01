# Favour Ogunbiyi 
## Data Analyst → Data Engineer (in progress)

**Data Analyst** with project experience spanning **SQL business analysis, retail banking data modelling, Python-based feature engineering, and e-commerce data cleaning**. I turn messy transactional and customer data into analysis-ready structures and business-facing insight — cleaning, modelling, and querying data so teams can answer their real business questions with confidence. I’m particularly interested in data roles that combine analytics, data modelling, and pipeline-oriented thinking.

**Recent proof:** Identified that 597 high-spending customers drove ₦866.5M of a multi-vendor marketplace's 2024 revenue — nearly 314x more than the platform's remaining 72 medium/low spenders combined — and turned that into a targeted retention recommendation. [see the analyst memo](https://github.com/favourogunbiyi/TradeZone-E-Commerce-Analytics-SQL-Business-Analysis/blob/main/Analyst_Memo(1).pdf) →

**Currently building:** Python ETL pipelines, dimensional data modelling (star schema, fact/dimension design), and SQL-based market basket analysis — as I move from analytics reporting toward data engineering.
<p align="center">
  <a href="https://www.linkedin.com/in/favour-ogunbiyi-b64928162/"><img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin"></a>
  <a href="https://github.com/favourogunbiyi"><img src="https://img.shields.io/badge/Github-Connect-black?style=for-the-badge&logo=github"></a>
  <a href="mailto:ogunbiyifavour28@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-green?style=for-the-badge&logo=gmail"></a>
</p>

## Core Tools & Skills
**Languages & Querying**    `SQL` `Python`

**Analytics & Reporting**   `Excel` `Power BI` `KPI reporting` `Exploratory Data Analysis (EDA)`

**Data Preparation**        `Data cleaning` `Data validation` `Transformation` `Missing-value analysis` `Duplicate detection` `Feature engineering`

**Data Modelling**          `Star schema design` `Fact and dimension modelling` `Slowly changing dimensions (SCD)` `Analytics-ready warehouse design` `ETL / ELT planning`

**Workflow & Communication** `Git/GitHub` `Technical documentation` `Analytical problem framing` `Business insight communication`

## Featured Projects
## 1. TradeZone E-Commerce Analytics
**Project Type:** SQL Business Analysis  

**Tools:** PostgreSQL, SQL, Data Cleaning, Business Analysis  

**Project Link:** [TradeZone-E-Commerce-Analytics-SQL-Business-Analysis](https://github.com/favourogunbiyi/TradeZone-E-Commerce-Analytics-SQL-Business-Analysis)

**Business Problem**
TradeZone, a multi-vendor marketplace, had customer, order, payment, review, seller, and product data spread across 7 raw tables with no analytical layer connecting them. Leadership couldn't see whether growth was healthy or fragile — until Q4 2024 revenue hit ₦364.7 million, a 392% jump year-on-year, and the obvious next question was: is this sustainable?

**Data & How Messy It Was**
I cleaned and validated 7 tables covering 850 customers, 3,015 orders, 6,426 order line items, 2,262 payments, 817 reviews, 280 products, and 90 sellers. Along the way, I found 150 orders with a NULL `total_amount` — 131 were recoverable from `order_items`, but 19 had no valid line items at all and had to be excluded from every revenue query. I also flagged 97 order_items rows where both unit price and line total were NULL, excluding them from product-revenue and rating-group calculations rather than guessing at the values.

**Tools & Methods**
PostgreSQL for cleaning and multi-table joins; SQL logic for 30-day cohort conversion tracking, revenue concentration by category, customer value segmentation, and a seller-bonus qualification model combining revenue contribution with review quality.

**Findings**
    Conversion is broken everywhere, not just in weak states. Even the best-performing state, Lagos, converts only 49.3% of new sign-ups within 30 days — meaning roughly half of all new customers never make a first purchase. Kano (31.6%) and Oyo (33.9%) are far worse, out of 418 combined new sign-ups across the top 5 states in 2024.
    Revenue is dangerously concentrated in one category. All 10 top-selling products by revenue in 2024 are Electronics — the top earner, an HP Pavilion 15 Laptop, alone generated ₦26.7 million from just 25 orders. Fashion, Food, and Home don't appear in the top 10 at all.
    A tiny customer segment carries almost the entire platform. 597 High Spenders (₦100,000+) generated ₦866.5 million in 2024 — averaging ₦1.45 million each — while the remaining 72 Medium/Low Spenders contributed only ₦2.76 million combined.

**Recommendation & Impact**
I recommended a time-limited first-purchase incentive targeted at Kano and Oyo within 7 days of sign-up, projecting a 10–15 percentage point lift in 30-day conversion, measurable by rerunning the same query at 60–90 days. I also proposed a fulfilment-speed benchmark (100 hours) with a "Fast Delivery" badge for sellers like SportsCentral NG (98.4 hrs, 4.08 rating) to protect customer experience as order volume scales. Full details and SQL queries are in the  [repo](https://github.com/favourogunbiyi/TradeZone-E-Commerce-Analytics-SQL-Business-Analysis).

**What the data couldn't answer** 
Repeat-purchase rate by cohort — I can identify first purchases, but not whether the 597 High Spenders are loyal repeat buyers or one-time spenders, which matters given how much revenue rides on that segment. I documented this gap rather than papering over it.

**Why this project matters:** This is raw marketplace data, cleaned by hand, turned into board-level decisions — not a demo dataset with the mess already removed.

**This SQL query describes how I solved my first business question**
````
-- Q1: Customer Acquisition & 30-Day Conversion
-- a. Find the top 5 states by new sign-ups in 2024 
-- b. 30-day purchase conversion rate

-- ALIASES USED IN THIS QUERY:
-- nc = new_customers (customers who signed up in 2024)
-- o  = orders (the orders table)
-- c  = converted (customers who bought within 30 days)

-- STEP 1: Every customer who signed up in 2024
SELECT 
    customer_id,
    state,
    signup_date
FROM customers
WHERE EXTRACT(YEAR FROM signup_date) = 2024;

-- STEP 2: Find which new customers purchased within 30 days of signing up
    SELECT DISTINCT nc.customer_id,
    nc.state,
    nc.signup_date,
    o.order_date
FROM customers nc
JOIN orders o ON nc.customer_id = o.customer_id
WHERE EXTRACT(YEAR FROM nc.signup_date) = 2024
AND o.order_date >= nc.signup_date
AND o.order_date <= nc.signup_date + INTERVAL '30 days';

---STEP 3: percentage of customers who bought in their first 30 days
SELECT 
    nc.state,
    COUNT(DISTINCT nc.customer_id) AS new_customers,
    COUNT(DISTINCT o.customer_id) AS converted_customers,
    ROUND(
        COUNT(DISTINCT o.customer_id) * 100.0 / 
        COUNT(DISTINCT nc.customer_id), 2
    ) AS conversion_percentage
FROM customers nc
LEFT JOIN orders o ON nc.customer_id = o.customer_id
AND o.order_date >= nc.signup_date
AND o.order_date <= nc.signup_date + INTERVAL '30 days'
WHERE EXTRACT(YEAR FROM nc.signup_date) = 2024
GROUP BY nc.state
ORDER BY new_customers DESC
LIMIT 5;
````

## 2. Palladium Bank Retail Data Modelling
**Project Type**: Dimensional Modelling / Analytics-Ready Data Design

**Tools**: SQL, MySQL, Star Schema Design, Dimensional Modelling, ETL Planning

**Project Link:** [Palladium-Bank-Retail-Data-Modelling-Project](https://github.com/favourogunbiyi/Palladium-Bank-Retail-Data-Modelling-Project)

**Business Problem**
Palladium Bank had 18 months of retail transaction history sitting in 15 raw columns, but analysts were still querying transaction logs directly for every report. Recurring questions — which customer segments drive fee income, which branches and channels see the most activity, which high-value customers are going quiet — had no reusable answer path.

**Data & How Messy It Was**
Transaction-level banking data at 18 months of volume, with no existing reporting layer — every report was being built from scratch against operational tables never designed for analysis. 

**Tools & Methods**
I designed a star schema at per-transaction grain — the most detailed level Kimball's methodology defines — because the business objectives centred on churn signals and recency/frequency behaviour, which only transaction-level detail can support. The model has one fact table (`Fact_Transactions`) surrounded by five dimensions: `Dim_Date`, `Dim_Customer`, `Dim_Branch`, `Dim_Product`, and `Dim_Channel`, plus a pre-aggregated `Agg_Monthly_Branch_Revenue` table. `Txn_ID` is handled as a degenerate dimension, stored directly in the fact table since it carries no attributes of its own.
I applied Type 2 SCD (full history preserved) to `State` and `Tier`, since branch reorganisation and customer tier upgrades both need historical accuracy for regional and loyalty analysis — and Type 1 SCD (overwrite) to `Branch_Name` and `Product_Name`, since rebrands carry no analytical value once they've happened. For scale, I planned monthly range partitioning on `Txn_Date` and composite indexes on the four foreign keys, so a query for "March transactions in Lagos" hits one partition instead of scanning 18 months of data.

**Findings**
The real bottleneck wasn't analyst skill — it was the absence of a reporting layer. Every recurring question (segment value, channel performance, inactivity risk) needed a join across entities that had never been formally modelled. Structuring the data at the transaction grain, with SCD logic where history matters, answers all of them directly instead of requiring a new ad-hoc query each time.

**Recommendation & Impact**
This schema replaces one-off SQL against raw logs with a queryable reporting layer — the `Agg_Monthly_Branch_Revenue` table alone removes the need to re-sum millions of transaction rows every time a branch performance report is requested. 

![Palladium Bank Star Schema](https://github.com/favourogunbiyi/Palladium-Bank-Retail-Data-Modelling-Project/blob/main/Retail%20bank%20dimensional%20visual%20design.png)

**Why this project matters**
It shows I can design how data should be structured before analysis happens, including the SCD and partitioning decisions that keep a model usable as data volume grows — not just query whatever structure I'm handed.

## 3. MovieLens Feature Engineering & Exploratory Data Analysis
**Project Type**: Python Data Preparation & Exploratory Analysis

**Tools**: Python, Pandas, NumPy, Matplotlib, Seaborn

**Project Link:** [MovieLens-Engineering-and-EDA-Project](https://github.com/favourogunbiyi/MovieLens-Engineering-and-EDA-Project)

**Business Problem**
The MovieLens dataset ships as flat rating records — user, movie, rating, timestamp — with no feature layer connecting content characteristics to user behaviour. On its own, it can't explain why engagement patterns look the way they do.

**Data & How Messy It Was**
Missing tags had to be replaced with a placeholder to avoid null-related errors downstream, duplicate records needed detection and removal, a small number of rows missing the `tmdbId` identifier were dropped to avoid mismatches, and raw Unix timestamps needed conversion into usable year/month fields before any temporal analysis was possible.

**Tools & Methods**
Pandas and NumPy for merging and cleaning; engineered 8 features including `release_year`, `num_genres`, `avg_rating`, `num_ratings`, `user_rating_freq`, `movie_age`, `num_tags`, and time-based fields extracted from rating timestamps; Matplotlib/Seaborn for exploring how ratings vary by decade, genre, and engagement level.

**Findings**
- Ratings peak for films from the **1940s**, and classics aged **61–100 years** score highest overall — recency doesn't correlate with quality in this dataset.
- Movies tagged with **more genres score higher on average** than single-genre films, suggesting genre diversity signals broader appeal.
- **Film-Noir, War, and Documentary** are the top-rated genres by average score, while Comedy and Horror show the widest spread in audience opinion.
- Cult titles like Pulp Fiction and Fight Club lead the most-tagged list — tag volume tracks cultural staying power, not just release-year popularity.

**Recommendation & Impact**
These engineered features — particularly `movie_age`, `num_genres`, and `num_tags` — form a usable foundation for a hybrid recommendation system that balances nostalgia against recency bias and surfaces genre-diverse, high-engagement titles. I documented the boundary explicitly: this stage is feature engineering and EDA, not a deployed model, and a production recommender would need additional work beyond this feature layer.

**Why this project matters:** It shows Python used for building an analytical structure on top of raw data, not just cleaning it.

## Supporting Project
## E-Commerce Product Data Cleaning & Title Optimisation

**Project Type:** Excel Data Cleaning / Catalogue Standardisation  
**Tools:** Excel, Data Cleaning, Text Standardisation  
**Project Link:** [E-Commerce-Product-Data-Cleaning-Title-Optimization](https://github.com/favourogunbiyi/E-Commerce-Product-Data-Cleaning-Title-Optimization)

**Business Problem**
A 3,847-record e-commerce product catalogue had titles averaging 86.4 characters — some running past 400 — which breaks search indexing, catalogue display, and mobile listing pages.

**Data & How Messy It Was**
3,847 raw records, reduced to 3,541 unique after deduplication. Titles carried HTML tags, stray punctuation, and embedded SKU/variant codes. 231 records (6.5%) had product-length values that were statistical outliers — likely data-entry errors or unit mismatches — and needed capping rather than deletion to preserve the rest of the dataset.

**Tools & Methods**
A three-stage Excel pipeline: base cleaning (TRIM + SUBSTITUTE to strip punctuation and HTML), variant/SKU code suppression via pattern matching, then 50-character capping at natural word boundaries. Outliers were capped at 4× the dataset median (638) rather than removed, preserving the raw values for auditability.

**Findings**
The cleaning pipeline cut mean title length from 86.4 to 40.8 characters, with all 3,541 titles now fitting the 50-character limit (up from an estimated ~60% before cleaning). Of those, 873 (24.7%) needed no further work, while 2,668 (75.3%) required the full variant-suppression and capping pipeline — meaning three in four listings had real title noise, not just a handful of edge cases.

**Recommendation & Impact**
The dataset is now ready for catalogue management and search indexing, with the original raw fields preserved alongside the cleaned versions so every change is auditable and reversible.

**Why this project matters:** Smaller in scope than the SQL and Python work above, but it's proof I do the unglamorous data-quality work — including deciding when to cap vs. delete — before analysis starts.


### Current Projects

### TradeZone Marketplace Performance Dashboard (In Progress)

**Project Type**: Power BI Dashboard / KPI Reporting
**Tools**: Power BI, SQL, Data Modelling, KPI Reporting

Built as a follow-up to the TradeZone SQL analysis above — turning the same marketplace domain into an interactive reporting layer covering revenue and order performance, customer conversion, seller quality and review trends, and payment behaviour by category. This is a live reporting build, not a finished case study, so it's listed separately from the completed TradeZone analysis.


### Portfolio Snapshot by Skill Area

| Skill Area | Evidence in Portfolio |
|---|---|
| SQL Business Analysis | TradeZone E-Commerce Analytics |
| Data Cleaning & Validation | TradeZone, MovieLens, Product Cleaning |
| Dimensional Modelling | Palladium Bank Retail Data Modelling |
| Feature Engineering | MovieLens |
| Excel-Based Data Preparation |Ecommerce Product Cleaning |
| Technical Documentation | TradeZone, Palladium, MovieLens, Ecommerce Title Optimisation |
| Reporting / Dashboard Direction | TradeZone Marketplace Performance Dashboard *(in progress)* |
|Data Engineering (in progress) |ETL pipeline design, star schema rebuilds — see Currently Building above|

### What This Portfolio Shows
Across these projects, I:
clean and validate messy transactional, customer, and catalogue datasets — and document exactly what was excluded and why
write SQL to answer business questions and support commercial decisions, including where the data falls short
design analytics-ready structures (star schemas, SCD strategy, partitioning) that make downstream reporting easier and faster
engineer features and explore behavioural patterns in Python
communicate findings, assumptions, and limitations honestly, not just the results that make a project look finished
