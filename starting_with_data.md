Question 1: What are the top 3 referring sites that generate the most revenue for the website?

SQL Queries:

    SELECT al.channelgrouping, SUM(al.totaltransactionrevenue) AS total_revenue, al.currencycode
    FROM all_sessions AS al
    JOIN analytics AS a ON a.visitid = al.visitid 
    GROUP BY al.channelgrouping, al.currencycode
    ORDER BY total_revenue DESC
    LIMIT 3


Answer: 


<img width="556" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/57becec6-f6a6-4418-a8fb-342baa151054">


Question 2: What are the most frequently purchased products by visitors from a specific country?


SQL Queries:

    SELECT al.country, al.v2productname, COUNT(*) AS purchase_count
    FROM all_sessions AS al
    JOIN analytics AS a ON al.visitid = a.visitid
    WHERE a.units_sold > 0
    GROUP BY al.country, al.v2productname
    ORDER BY purchase_count DESC;

Answer:

<img width="1105" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/3f8ab9d9-fc8c-4e4d-9c64-67ea5d8f1f51">


Question 3: What are the top 5 most viewed product categories?


SQL Queries:

    SELECT al.v2productcategory, COUNT(*) AS view_count
    FROM all_sessions AS al
    where country != '(not set)' and city != 'not available in demo dataset' and city != '(not set)' and v2productcategory != '(not set)'
    GROUP BY al.v2productcategory
    ORDER BY view_count DESC
    LIMIT 5

Answer:


<img width="1131" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/58c67e87-7b33-4368-bb62-b80e00f77148">

