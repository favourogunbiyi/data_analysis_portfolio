# Favour Ogunbiyi 
## Data Analyst

**Data Analyst** with project experience spanning **SQL business analysis, retail banking data modelling, Python-based feature engineering, and e-commerce data cleaning**. My work focuses on cleaning messy transactional data, building analysis-ready structures, and generating insights from business datasets through SQL analysis, exploratory analysis, and technical reporting. I’m particularly interested in data roles that combine analytics, data modelling, and pipeline-oriented thinking.

<p align="center">
  <a href="https://www.linkedin.com/in/favour-ogunbiyi-b64928162/"><img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin"></a>
  <a href="https://github.com/favourogunbiyi"><img src="https://img.shields.io/badge/Github-Connect-black?style=for-the-badge&logo=github"></a>
  <a href="mailto:ogunbiyifavour28@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-green?style=for-the-badge&logo=gmail"></a>
</p>

## Featured Projects
## 1) TradeZone E-Commerce Analytics
**Project Type:** SQL Business Analysis  
**Repo:** [TradeZone-E-Commerce-Analytics-SQL-Business-Analysis](https://github.com/favourogunbiyi/TradeZone-E-Commerce-Analytics-SQL-Business-Analysis)

### Business Context
TradeZone, a growing e-commerce marketplace, had customer, order, payment, review, seller, and product data but no structured way to answer recurring commercial questions around conversion, seller performance, revenue concentration, and transaction quality. Reporting directly from raw marketplace tables made it difficult to identify which customers, products, and sellers were driving business performance.

### The Problem
The project focused on turning raw multi-table marketplace data into a structured SQL analysis that could answer practical business questions such as:
- which states were generating strong customer acquisition but weak conversion
- which product categories and items were carrying revenue
- whether fulfilment speed was affecting seller quality and review outcomes
- how customer spending was distributed across the business
- which sellers qualified for quality-adjusted performance rewards

### What I Built
I developed a SQL analysis workflow that cleaned and validated the source tables before answering the business questions in a structured way. The work included:
- cleaning and validating **7 related SQL tables**
- checking for duplicates, missing values, and category inconsistencies
- standardising city/category fields and documenting unresolved data-quality issues
- answering **8 business questions** covering conversion, revenue, seller performance, customer spending, payment behaviour, and seller bonus qualification
- translating the findings into an **analyst memo** with business recommendations

### Analytical Focus
This project demonstrates my ability to work through the full analysis layer of a transactional business problem:
- clean marketplace data before analysis
- write SQL to answer commercial questions
- structure findings around business performance rather than only raw metrics
- communicate recommendations clearly in written form

**Tools:** PostgreSQL, SQL, Data Cleaning, Business Analysis

## 2) Palladium Bank Retail Data Modelling
**Project Type:** Dimensional Modelling / Analytics-Ready Data Design  
**Repo:** [Palladium-Bank-Retail-Data-Modelling-Project](https://github.com/favourogunbiyi/Palladium-Bank-Retail-Data-Modelling-Project)

### Business Context
Palladium Bank had 18 months of retail banking transaction data, but reporting directly from raw transaction logs made analysis slow, inconsistent, and difficult to scale. The bank needed a structure that could support recurring analysis across customers, branches, products, and transaction channels.

### The Problem
The challenge was to redesign raw banking transaction data into a model that could support questions such as:
- which customer segments generate the most fee income
- how transaction behaviour differs by branch and channel
- Which high-value customers are becoming inactive
- Which products drive deposits versus withdrawals
- How analysts can report consistently without querying raw logs every time

### What I Built
I designed a **star-schema retail banking model** centred on transaction-level analysis. The project included:
- defining the analytical grain of the model
- creating one fact table and multiple dimensions for customers, products, branches, channels, and dates
- deciding where Slowly Changing Dimension logic was needed for historical tracking
- documenting an ETL strategy for initial and incremental loads
- outlining indexing, partitioning, and pre-aggregation considerations for performance
- defining data-quality checks for duplicate transactions, invalid dates, null amounts, and unresolved customers

### Analytical Focus
This project demonstrates my ability to move beyond surface-level reporting and think about **how data should be structured before analysis happens**. It reflects:
- dimensional modelling skills
- star schema design thinking
- warehouse-oriented analytical planning
- ETL / ELT awareness
- performance-aware design for reporting use cases

**Tools:** SQL, MySQL, Star Schema Design, Dimensional Modelling, ETL Planning

## 3) MovieLens Feature Engineering & Exploratory Data Analysis
**Project Type:** Python Data Preparation & Exploratory Analysis  
**Repo:** [MovieLens-Engineering-and-EDA-Project](https://github.com/favourogunbiyi/MovieLens-Engineering-and-EDA-Project)

### Business Context
MovieLens contains user ratings, movie metadata, and tagging behaviour, but the raw tables do not directly explain the patterns behind rating behaviour. To make the data more useful for analysis, the project focused on transforming the raw files into a richer feature set for exploratory work and recommendation-oriented thinking.

### The Problem
A flat ratings table can show what users rated, but it does not provide enough context about:
- How movie age relates to rating patterns
- How genre complexity may influence user response
- Whether engagement signals like tags and rating frequency reveal useful behavioural patterns
- How raw timestamped ratings can be turned into more analysis-ready features

### What I Built
I created a Python workflow for cleaning, transforming, and engineering features from the MovieLens dataset. The work included:
- cleaning and merging multiple source files
- handling missing tag values and removing unrecoverable rows
- converting Unix timestamps into usable date fields
- engineering features such as release year, movie age, genre count, tag activity, and user rating frequency
- exploring how ratings vary across decades, genres, and engagement levels
- documenting where the work stops short of a production recommendation system

### Analytical Focus
This project demonstrates my ability to use Python for:
- dataset preparation and feature engineering
- exploratory analysis of user and content behaviour
- turning raw relational data into a richer analytical layer
- communicating analytical findings and limitations clearly

**Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn

## Supporting Projects
### E-Commerce Product Data Cleaning & Title Optimisation
**Project Type:** Excel Data Cleaning / Catalogue Preparation  
**Repo:** [E-Commerce-Product-Data-Cleaning-Title-Optimization](https://github.com/favourogunbiyi/E-Commerce-Product-Data-Cleaning-Title-Optimization)

Excel-based data cleaning project focused on improving the quality and usability of a product catalogue through duplicate removal, title standardisation, missing-value handling, outlier treatment, and creation of a `short_title` field for cleaner downstream analysis and reporting.

This project supports the portfolio by showing practical **Excel-first cleaning work** on text-heavy e-commerce data.

**Tools:** Excel, Data Cleaning, Text Standardisation

## Current Projects
### TradeZone Marketplace Performance Dashboard *(In Progress)*
**Project Type:** Power BI Dashboard / KPI Reporting

A Power BI dashboard project being built as a **follow-up reporting layer** to the TradeZone e-commerce analysis domain. Unlike the original TradeZone SQL project, this dashboard is not positioned as part of the original business problem. Instead, it is a separate BI project focused on translating marketplace analysis into a clearer reporting experience for KPI monitoring and performance review.

### Current Focus
The dashboard is being designed to support interactive monitoring of:
- revenue and order performance
- customer conversion patterns
- seller performance and review quality
- payment behaviour and category-level trends

### Goal
The goal of this project is to move from **SQL analysis outputs** to a more decision-friendly **Power BI reporting layer**, turning marketplace insights into a dashboard that can support recurring business monitoring.

**Tools:** Power BI, SQL, Data Modelling, KPI Reporting

## Portfolio Snapshot by Skill Area
| Skill Area | Evidence in Portfolio |
|---|---|
| SQL Business Analysis | TradeZone E-Commerce Analytics |
| Data Cleaning & Validation | TradeZone, MovieLens, Product Cleaning |
| Dimensional Modelling | Palladium Bank Retail Data Modelling |
| Feature Engineering | MovieLens |
| Excel-Based Data Preparation | Product Cleaning |
| Technical Documentation | TradeZone, Palladium, MovieLens |
| Reporting / Dashboard Direction | TradeZone Marketplace Performance Dashboard *(in progress)* |

## What This Portfolio Shows
Across these projects, my work demonstrates the ability to:
- clean and validate messy transactional, customer, and catalogue datasets
- write SQL to answer business questions and support commercial analysis
- design analytics-ready structures that make downstream reporting easier
- engineer useful features and explore behavioural patterns in Python
- communicate findings, assumptions, and limitations through structured technical documentation
  
## Current Focus
I’m continuing to strengthen this portfolio through work in:
- Power BI dashboard reporting
- KPI and performance analysis
- analytics-ready data modelling
- projects that connect SQL analysis, data cleaning, modelling, and reporting into a single workflow
