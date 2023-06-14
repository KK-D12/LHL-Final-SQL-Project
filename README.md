# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The aim of this project was to analyze and gain insights from an ecommerce dataset using SQL. The dataset consisted of all_sessions, analytics, 
products, sales_by_sku, and sales_report tables. The project involved extracting, transforming, and loading the data, as well as 
performing various analyses to answer specific questions and uncover meaningful patterns and trends.

## Process

### 1. Data Extraction and Pre-processing:
    * Extracted the dataset from CSV files and imported it into a PostgreSQL database.
    * Conducted initial data exploration to understand the structure and contents of each table.
    * Defined appropriate data types for columns based on their intended purpose.
    * Assessed and addressed missing or null values to ensure data integrity.
### 2. Data Transformation and Analysis:
    * Identified relationships between tables and utilized common attributes to establish meaningful connections.
    * Executed SQL queries to join tables, consolidate data, and perform analyses.
    * Utilized various SQL functions, aggregations, and filters to extract relevant information.
    * Addressed specific business questions by leveraging the dataset's columns and relationships.

## Results

Based on the data, I was able to obtain valuable insights  on various aspects of the business, including transaction revenues, product ordering
behaviour, product category preferences, top-selling products, top referring sites generating revenue, most frequently purchased products by
country, and the most viewed product categories. These insights drive data-driven decision-making and strategic planning to optimize business
performance, drive growth, maximize revenue potential, and enhance overall customer experience. The data was utilized as follows:

### 1. Which cities and countries have the highest level of transaction revenues on the site?
    * Extracted city, country, total transaction revenue, and currency code.
    * Filtered out null values and entries with 'not available in demo dataset' as the city.
    * Sorted the results in descending order of transaction revenue and limited to the top 5.
### 2. What is the average number of products ordered from visitors in each city and country?
    * Joined the "all_sessions" and "products" tables based on the product SKU.
    * Filtered out entries with '(not set)' as the country and 'not available in demo dataset' as the city.
    * Calculated the average ordered quantity of products for each city and country.
### 3. Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?
    * Aggregated the distinct product categories into an array for each city and country combination.
    * Filtered out entries with '(not set)' as the country and 'not available in demo dataset' as the city.
    * Identified patterns in the types of products ordered by examining the resulting arrays.
### 4. What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?
    * Joined the "all_sessions" and "products" tables based on the product SKU.
    * Filtered out entries with '(not set)' as the country and 'not available in demo dataset' as the city.
    * Calculated the total quantity sold for each product in each city/country.
    * Identified products with the highest sales in each city/country and analyzed any notable patterns. 
### 5. Can we summarize the impact of revenue generated from each city/country?
    * Calculated the total revenue and average revenue per transaction for each city and country.
    * Filtered out entries with '(not set)' as the country and 'not available in demo dataset' as the city.
    * Sorted the results in descending order of total revenue, summarizing the revenue impact.
### 6. What are the top 3 referring sites that generate the most revenue for the website?
    * Joined the "all_sessions" and "analytics" tables based on the visit ID.
    * Aggregated the total transaction revenue by channel grouping, along with the currency code.
    * Sorted the results in descending order of total revenue and limited to the top 3.
### 7. What are the most frequently purchased products by visitors from a specific country?
    * Joined the "all_sessions" and "analytics" tables based on the visit ID.
    * Filtered to include only entries where units sold were greater than 0.
    * Counted the number of purchases for each country and product name combination.
    * Sorted the results in descending order of purchase count.
### 8. What are the top 5 most viewed product categories?
    * Aggregated the number of views by product category from the "all_sessions" table.
    * Sorted the results in descending order of view count and limited to the top 5.
    
## Challenges 

Several challenges were encountered during the project:

### 1. Lack of Primary Keys:
    * Difficulty in identifying primary keys between the all_sessions and analytics tables.
    * Required alternative approaches to establish meaningful relationships between the tables.
### 2. Ambiguity in Data Representation:
    * Unclear column value representations and undefined meanings of certain variables.
    * Required additional research and interpretation to understand the data accurately.

## Future Goals

I performed two quality assurance (QA) processes to validate my findings:

### 1. Data Inconsistency:
    * Risk area: There might be inconsistencies or discrepancies in the data across tables, particularly with foreign key relationships between the all_sessions and products table.
    *  Identified issue: Rows with both v2productname and producsku as NULL in all_sessions indicate that the product is available, but the 
    productsku is missing.
    * Resolution: Deleting rows with NULL productsku would impact business requirements, so I replaced NULL values with 'N/A'.
### 2. Data Integrity Violations:
    * Risk area: Absence of primary keys and foreign keys between all_sessions and analytics table increases the risk of data integrity violations.
    * Analysis: Redundant rows in the tables contain different values across columns or variables, making it inappropriate to simply remove them.
    * Approach: Explore alternative methods for linking records and establishing meaningful relationships.
    * Solution: Utilize common attributes like visitid and fullvisitorid to link the analytics and all_sessions tables.

Given additional time, the following goals could be pursued:

### 1. Data Quality Assurance:
    * Perform further data profiling to identify and address data quality issues.
    * Validate data completeness, conformity, accuracy, consistency, and uniqueness.
### 2. Advanced Analysis and Visualization:
    * Utilize advanced statistical techniques to uncover deeper insights.
    * Develop visualizations and interactive dashboards for effective data presentation.
### 3. Expand Business Questions:
    * Explore additional business questions to gain a more comprehensive understanding.
    * Conduct deeper analysis on specific customer segments or product categories.
### 4. Enhancing Data Documentation:
    * Provide comprehensive descriptions of tables, relationships, and any transformations made during the integration process.

By pursuing these future goals, the project's insights can be enriched, data quality can be enhanced, and a more comprehensive understanding of
the dataset can be achieved. This will contribute to making informed business decisions and driving further improvements in performance and
revenue.

