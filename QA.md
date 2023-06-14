What are your risk areas? Identify and describe them.

# Risk area one: Data Inconsistency

In my analysis, I identified a risk area related to data inconsistency. Specifically, there might be inconsistencies or discrepancies in the data
across the tables, particularly in the foreign key relationships between the all_sessions and products tables. To validate this, I executed the
following query:

    SELECT *
    FROM all_sessions a
    LEFT JOIN products p ON a.productsku = p.productsku
    WHERE p.productsku IS NULL

By running this query, I discovered NULL values in the productsku column of the all_sessions table. This finding raised concerns about missing or
mismatched referenced values. To address this risk, I examined the business requirements, specifically focusing on question four in the initial
question section. I realized that I had joined the products and all_sessions tables on productsku to identify the top-selling products. This
analysis highlighted the importance of addressing the risk. To determine the affected rows, I used the following query:

    SELECT *
    FROM all_sessions
    WHERE v2productname IS NULL AND productsku IS NULL

By observing that no rows had both v2productname and productsku as NULL in the all_sessions table, I gained insight that the product itself was
available, but the productsku was not provided. Deleting the productsku column with NULL values would impact the business requirements. Therefore,
I decided to replace the NULL values with 'N/A' using the following query:

    UPDATE all_sessions
    SET productsku = 'N/A'
    WHERE productsku IS NULL

To ensure the success of this update, I re-ran the initial query, confirming the absence of NULL values in the productsku column and the
resolution of inconsistencies in the foreign key relationship between the all_sessions and products tables.

# Risk area two: Data Integrity Violations

Another risk area I identified is related to data integrity violations. The absence of primary keys and foreign keys between the all_sessions and
analytics tables increases the risk of integrity issues. To test this, I executed the following query:

    SELECT a.visitid, a.fullvisitorid
    FROM analytics a
    LEFT JOIN all_sessions s ON a.visitid = s.visitid
    WHERE s.visitid IS NULL

This query returned rows, indicating data integrity violations, specifically missing visitid values in the all_sessions table that are referenced
in the analytics table. To ensure data integrity and establish valid relationships between the tables, it is crucial to address these violations.
However, in this case, the redundant rows in the tables contain different values across columns or variables.

Simply removing these redundant rows or cleaning the data would not be appropriate as each row represents unique information. Instead, I needed to
find an alternative approach to integrate the data despite the lack of primary keys or foreign keys. To establish meaningful relationships, I
utilized common attributes such as visitid and fullvisitorid to link the analytics and all_sessions tables.

By performing joins on the visitid columns, I successfully brought together related records from both tables. This allowed me to analyze and
explore the combined data, overcoming the lack of primary keys or foreign keys. This approach validated the result of question two in the
'starting_with_data' section, which aimed to identify the most frequently purchased products by visitors from a specific country. By linking the
analytics and all_sessions tables using visitid as a common attribute, I could analyze visitor behavior, transactions, and product information
together, gaining comprehensive insights into purchasing patterns in relation to the visitor's country.

# QA Process:
Describe your QA process and include the SQL queries used to execute it.

During the quality assurance (QA) process, I employed various SQL queries to validate the findings. These queries included selecting data from
different tables, performing joins, and applying conditional filters. The purpose of these queries was to ensure data accuracy, completeness, and
conformity.

For data inconsistency, I used the query mentioned earlier to identify missing values in the foreign key relationship between the all_sessions and
products tables.

To address data integrity violations, I executed the query that identified missing visitid values in the all_sessions table that were referenced
in the analytics table.

By running these queries, I examined the data and verified the relationships established between tables. The QA process played a vital role in
ensuring the accuracy and validity of the findings obtained from the data analysis.

