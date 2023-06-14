Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:


<img width="810" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/5bd18f33-82e0-4b8e-aba5-e9acc2c86945">


Answer:


<img width="604" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/e874453b-25c7-4cd7-a1b8-f21ab86df1e7">


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:


<img width="893" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/79824174-3e4a-4935-a3e7-fad757c0f27f">


Answer:


Result : this will retrieve 268 rows of cities, countries, and the average ordered quantity of products for each unique combination of city and 
country. 


<img width="1011" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/2ce4808a-a71b-43c1-a136-d6efdc23e6d8">


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries: 


<img width="920" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/64cbf365-ca5d-47ef-9446-1c4312350752">


Answer:

By using the ARRAY_AGG function to aggregate the distinct product categories into an array for each unique combination of city and country, I was
able to identify patterns in the types of products ordered by visitors. Specifically, I noticed that the categories "Home/Apparel" and
"Home/Apparel" appeared frequently across different countries and cities. This suggests that there is a consistent demand for apparel
products in the home category among visitors from various locations.


<img width="1111" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/55a04a02-2c6b-4606-98f3-271ab1d553cd">


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:


<img width="959" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/54f94e65-22be-40c2-abf6-d291b1058c09">
    

Answer:
 By examining the results, I can observe that there are products that have good customer preferences and market demand across cities/countries. 
 Total of 3572 rows are returned.   
 
 <img width="1131" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/4fd0476d-1ecd-4c1a-b7d7-e26c40ff9a74">


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:


<img width="963" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/08db2f33-c2a3-49fe-8b8a-7bb3875d7f2f">


Answer:

By examining the analysis results, I have identified the cities and countries that contribute the most to the overall revenue. The following are 
rows from the generated 282 rows. 


<img width="1111" alt="image" src="https://github.com/KK-D12/LHL-Final-SQL-Project/assets/127278841/a6cb8643-5bd9-4e01-b340-fc129d8b50a6">




















