Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
select s.country, s.city, sum(newrevenue) as sum_of_transactions
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.country, s.city, n.newrevenue
HAVING n.newrevenue > 0
ORDER BY sum_of_transactions desc

Answer:
United State is the country with the highest transactions on the site and Mountain View is the city with the higest transaction of 1,613,081,250,000.


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
select distinct(s.country), s.city, avg(n.units_sold) avg_products_ordered
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY distinct(s.country), s.city, n.units_sold
having n.units_sold is not null
order by avg_products_ordered desc


Answer:
Mountain View United States has the highest average number of products ordered at 825 units.



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
select country, city, v2productcategory, count(v2productname)
from all_sessions
GROUP BY 1, 2, 3
order by count(v2productname) desc



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







