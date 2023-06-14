What issues will you address by cleaning the data?

By cleaning the data, I aim to address several issues such as inconsistent data types, missing values, duplicate records, and formatting 
inconsistencies. The specific data cleaning tasks and SQL queries used for each table are as follows:

### Table name: Sales_by_sku

    * Change the data type of the total_ordered column to 'integer'.
    * Remove any 'null' values from the productsku column.
    * Remove all '0' values from the total_ordered column.
    * Remove duplicates from the data.

SQL query:

     SELECT DISTINCT productsku, CAST(total_ordered AS integer) AS total_ordered
     FROM sales_by_sku
     WHERE productsku IS NOT NULL
        AND total_ordered != 0

### Table name: Sales_report

    * Change the data types of relevant columns to their accurate types.
    * Remove duplicate values.

SQL query:

    SELECT DISTINCT productsku, CAST(total_ordered AS integer), name, CAST(stocklevel AS integer),
    CAST(restockingleadtime AS integer), CAST(sentimentscore AS float),
    CAST(sentimentmagnitude AS float), CAST(ratio AS float)
    FROM sales_report

### Table name: Products

    * Change the data types of relevant columns to their accurate types.
    * Remove duplicate values.

SQL query 1:

    CREATE TABLE public.distinct_products AS
    SELECT DISTINCT ON (productsku)
      CAST(productsku AS varchar) AS productsku,
      CAST(name AS varchar),
      CAST(orderedquantity AS integer),
      CAST(stocklevel AS integer),
      CAST(restockingleadtime AS integer),
      CAST(sentimentscore AS float),
      CAST(sentimentmagnitude AS float)
    FROM public.products;

SQL query 2:

    -- Drop the original products table
    DROP TABLE IF EXISTS public.products;
 
 SQL query 3:

    -- Rename the distinct_products table to products
    ALTER TABLE public.distinct_products RENAME TO products;

### Table name: Analytics

    * Change the data types of relevant columns to their accurate types.
    * Remove duplicate values.
    * Format the time and year variables to the appropriate formatting.
    * Update the unit_price column values' to meaningful numbers. 

SQL query 1:

    SELECT
      DISTINCT visitid AS visitid,
      CAST(visitnumber AS integer) AS visitnumber,
      TO_CHAR(TO_TIMESTAMP(CAST(visitstarttime AS integer))::timestamp, 'HH24:MI:SS') AS visitstarttime,
      TO_DATE(date, 'YYYYMMDD') AS date,
      fullvisitorid AS fullvisitorid,
      channelgrouping AS channelgrouping,
      socialengagementtype AS socialengagementtype,
      CAST(units_sold AS integer) AS units_sold,
      CAST(pageviews AS integer) AS pageviews,
      TO_CHAR(TIME '00:00:00' + (CAST(timeonsite AS integer) * INTERVAL '1 second'), 'HH24:MI:SS') AS timeonsite,
      CAST(bounces AS integer) AS bounces,
      CAST(revenue AS float) AS revenue,
      CAST(unit_price AS float) AS unit_price
    FROM analytics;

SQL query 2:

    -- Drop analytics table and reimport with cleaned data with all varchar datatypes
    DROP TABLE IF EXISTS analytics_cleaned;
    CREATE TABLE analytics_cleaned AS SELECT * FROM analytics;

SQL query 3:

    -- Alter column data types
    ALTER TABLE analytics_cleaned
      ALTER COLUMN visitid TYPE varchar,
      ALTER COLUMN visitnumber TYPE integer USING visitnumber::integer,
      ALTER COLUMN visitstarttime TYPE time USING CASE WHEN visitstarttime = '0' THEN NULL ELSE visitstarttime::time without time zone AT TIME 
      ZONE 'EST' END,
      ALTER COLUMN date TYPE date USING CASE WHEN date = '' THEN NULL ELSE date::date END,
      ALTER COLUMN fullvisitorid TYPE varchar,
      ALTER COLUMN channelgrouping TYPE varchar,
      ALTER COLUMN socialengagementtype TYPE varchar,
      ALTER COLUMN units_sold TYPE integer USING units_sold::integer,
      ALTER COLUMN pageviews TYPE integer USING pageviews::integer,
      ALTER COLUMN timeonsite TYPE time USING CASE WHEN timeonsite = '0' THEN NULL ELSE timeonsite::time without time zone AT TIME ZONE 'EST' 
      END,
      ALTER COLUMN bounces TYPE integer USING bounces::integer,
      ALTER COLUMN revenue TYPE double precision USING revenue::double precision,
      ALTER COLUMN unit_price TYPE double precision USING unit_price::double precision;

SQL query 4:

    -- Update the unit_price column by dividing the values by 1,000,000
    UPDATE analytics_cleaned
    SET unit_price = unit_price / 1000000;

### Table name: All_sessions

    * Change the data types of relevant columns to their accurate types.
    * Remove duplicate values.
    * Format the date and time variables to the appropriate formatting.
    * Drop variables which contians only null values through the entire row.
    * Update totaltransactionrevenue, transactions, productprice, productrevenue, transactionrevenue columns' values to meaningful numbers.

SQL query 1:

    SELECT DISTINCT
       CAST(fullvisitorid AS varchar),
       CAST(channelgrouping AS varchar),
       CAST(country AS varchar),
       CAST(city AS varchar),
       CAST(totaltransactionrevenue AS float),
       CAST(transactions AS integer),
       CAST(pageviews AS integer),
       CAST(sessionqualitydim AS integer),
       CAST(visitid AS varchar),
       CAST(type AS varchar),
       CAST(productquantity AS integer),
       CAST(productprice AS float),
       CAST(productrevenue AS float),
       CAST(productsku AS varchar),
       CAST(v2productname AS varchar),
       CAST(v2productcategory AS varchar),
       CAST(productvariant AS varchar),
       CAST(currencycode AS varchar),
       CAST(transactionrevenue AS float),
       CAST(transactionid AS varchar),
       CAST(pagetitle AS varchar),
       CAST(pagepathlevel1 AS varchar),
       CAST(ecommerceaction_type AS integer),
       CAST(ecommerceaction_step AS integer),
       CAST(ecommerceaction_option AS varchar),
       CASE
          WHEN LENGTH("time") = 6 AND SUBSTRING("time", 1, 2)::integer BETWEEN 0 AND 23
            AND SUBSTRING("time", 3, 2)::integer BETWEEN 0 AND 59
            AND SUBSTRING("time", 5, 2)::integer BETWEEN 0 AND 59
            THEN CAST(SUBSTRING("time", 1, 2) || ':' || SUBSTRING("time", 3, 2) || ':' || SUBSTRING("time", 5, 2) AS time) AT TIME ZONE 'EST'
        ELSE NULL
      END AS "time",
      CASE
        WHEN LENGTH(timeonsite) = 6 AND SUBSTRING(timeonsite, 1, 2)::integer BETWEEN 0 AND 23
            AND SUBSTRING(timeonsite, 3, 2)::integer BETWEEN 0 AND 59
            AND SUBSTRING(timeonsite, 5, 2)::integer BETWEEN 0 AND 59
            THEN CAST(SUBSTRING(timeonsite, 1, 2) || ':' || SUBSTRING(timeonsite, 3, 2) || ':' || SUBSTRING(timeonsite, 5, 2) AS time) AT TIME
            ZONE 'EST'
        ELSE NULL
      END AS timeonsite,
      TO_DATE(date, 'YYYYMMDD') AS date
    FROM all_sessions;

SQL query 2:
   
    -- Drop all_sessions table and reimport with cleaned data with all varchar datatypes
    DROP TABLE IF EXISTS all_sessions_cleaned;
    CREATE TABLE all_sessions_cleaned AS SELECT * FROM all_sessions;

    -- Alter the table to modify column data types
    ALTER TABLE all_sessions_cleaned
      ALTER COLUMN fullvisitorid TYPE varchar,
      ALTER COLUMN channelgrouping TYPE varchar,
      ALTER COLUMN country TYPE varchar,
      ALTER COLUMN city TYPE varchar,
      ALTER COLUMN totaltransactionrevenue TYPE float USING NULLIF(totaltransactionrevenue, 'NULL')::float,
      ALTER COLUMN transactions TYPE integer USING NULLIF(transactions, 'NULL')::integer,
      ALTER COLUMN pageviews TYPE integer USING NULLIF(pageviews, 'NULL')::integer,
      ALTER COLUMN sessionqualitydim TYPE integer USING NULLIF(sessionqualitydim, 'NULL')::integer,
      ALTER COLUMN visitid TYPE varchar,
      ALTER COLUMN type TYPE varchar,
      ALTER COLUMN productquantity TYPE integer USING NULLIF(productquantity, 'NULL')::integer,
      ALTER COLUMN productprice TYPE float USING NULLIF(productprice, 'NULL')::float,
      ALTER COLUMN productrevenue TYPE float USING NULLIF(productrevenue, 'NULL')::float,
      ALTER COLUMN productsku TYPE varchar,
      ALTER COLUMN v2productname TYPE varchar,
      ALTER COLUMN v2productcategory TYPE varchar,
      ALTER COLUMN productvariant TYPE varchar,
      ALTER COLUMN currencycode TYPE varchar,
      ALTER COLUMN transactionrevenue TYPE float USING NULLIF(transactionrevenue, 'NULL')::float,
      ALTER COLUMN transactionid TYPE varchar,
      ALTER COLUMN pagetitle TYPE varchar,
      ALTER COLUMN pagepathlevel1 TYPE varchar,
      ALTER COLUMN ecommerceaction_type TYPE integer USING NULLIF(ecommerceaction_type, 'NULL')::integer,
      ALTER COLUMN ecommerceaction_step TYPE integer USING NULLIF(ecommerceaction_step, 'NULL')::integer,
      ALTER COLUMN ecommerceaction_option TYPE varchar,
      ALTER COLUMN "time" TYPE time USING TO_TIMESTAMP(NULLIF("time", 'NULL'), 'HH24:MI:SS') AT TIME ZONE 'EST',
      ALTER COLUMN timeonsite TYPE time USING TO_TIMESTAMP(NULLIF(timeonsite, 'NULL'), 'HH24:MI:SS') AT TIME ZONE 'EST';

SQL query 3:

    -- Update invalid dates to NULL
    UPDATE all_sessions_cleaned
    SET date = NULL
    WHERE date <> '' AND TO_DATE(date, 'YYYY-MM-DD') IS NULL;

SQL query 4:

    -- Alter the column to change data type to date
    ALTER TABLE all_sessions_cleaned
      ALTER COLUMN date TYPE date
      USING TO_DATE(date, 'YYYY-MM-DD');
      
SQL query 5:

    -- Update the columns by dividing by 1,000,000
    UPDATE all_sessions_cleaned
    SET 
        totaltransactionrevenue = totaltransactionrevenue / 1000000,
        transactions = transactions / 1000000,
        productprice = productprice / 1000000,
        productrevenue = productrevenue / 1000000,
        transactionrevenue = transactionrevenue / 1000000;


