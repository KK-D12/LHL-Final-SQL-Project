Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

    SELECT country, city, totaltransactionrevenue, currencycode
    FROM all_sessions a
    where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)' and a.v2productcategory != '(not set)' 
    ORDER BY totaltransactionrevenue DESC
    LIMIT 5 

Answer:


<img width="1116" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/8b90cf81-46f1-4a47-866b-04c1f865b063">


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

       SELECT  a.country, a.city, AVG(p.orderedquantity) AS average_ordered_quantity
       FROM all_sessions AS a
       JOIN products AS p ON a.productsku = p.productsku
       where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)'
       GROUP BY a.city, a.country
       order by  average_ordered_quantity DESC

Answer:


Result : this will retrieve 268 rows of cities, countries, and the average ordered quantity of products for each unique combination of city and 
country. 


<img width="948" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/edd0ee45-2744-45ec-aa5a-46c31729ce15">


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries: 

    SELECT a.city, a.country, ARRAY_AGG(DISTINCT a.v2productcategory) AS product_categories
    FROM public.all_sessions AS a
    where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)'
    GROUP BY a.city, a.country
    ORDER BY  product_categories

Answer:

By using the ARRAY_AGG function to aggregate the distinct product categories into an array for each unique combination of city and country, I was
able to identify patterns in the types of products ordered by visitors. Specifically, I noticed that the categories "Home/Apparel" and
"Home/Apparel" appeared frequently across different countries and cities. This suggests that there is a consistent demand for apparel
products in the home category among visitors from various locations.


<img width="1140" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/63de13f7-1da5-4a61-9fb8-f387f263f4f5">


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

    SELECT a.city, a.country, a.productsku,  a.v2productname, SUM(p.orderedquantity) AS total_quantity_sold
    FROM all_sessions a
    join products p using (productsku)
    where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)' and a.v2productcategory != '(not set)' 
    GROUP BY city, country, productsku, v2productcategory, a.v2productname
    HAVING SUM(p.orderedquantity) = (
        SELECT MAX(quantity_sold)
        FROM (
        SELECT city, country, productsku, SUM(p.orderedquantity) AS quantity_sold
        FROM all_sessions a
        GROUP BY city, country, productsku
    ) AS subquery 
    WHERE subquery.city = a.city AND subquery.country = a.country
    )
    ORDER BY a.productsku

Answer:
 By examining the results, I can observe that there are products that have good customer preferences and market demand across cities/countries. 
 Total of 4055 rows are returned.   
 
 <img width="1124" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/91aef057-76be-4bb1-b41d-d89130309f26">


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

    SELECT a.city, a.country, SUM(a.totaltransactionrevenue) AS total_revenue, 
    AVG(a.totaltransactionrevenue) AS average_revenue_per_transaction
    FROM all_sessions a
    where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)' and a.v2productcategory != '(not set)' 
    GROUP BY city, country
    ORDER BY total_revenue DESC

Answer:

By examining the analysis results, I have identified the cities and countries that contribute the most to the overall revenue. The following are 
some rows from the generated 273 rows. 


<img width="1110" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/0a4452c5-c047-4801-82dd-e272f5f068a2">




















