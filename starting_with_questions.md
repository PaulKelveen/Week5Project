Answer the following questions and provide the SQL queries used to find the answer.
    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SQL Queries:
Country with the highest revenue
```sql
SELECT distinct(country), sum(sum_of_transactions) 
FROM (select s.country, s.city, sum(newrevenue) as sum_of_transactions
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.country, s.city, n.newrevenue
HAVING n.newrevenue > 0
ORDER BY sum_of_transactions desc) as temp1
GROUP BY country
ORDER BY sum(sum_of_transactions) desc
```

City with the highest revenue
```sql
SELECT distinct(city), sum(sum_of_transactions) 
FROM (select s.country, s.city, sum(newrevenue) as sum_of_transactions
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.country, s.city, n.newrevenue
HAVING n.newrevenue > 0
ORDER BY sum_of_transactions desc) as temp1
GROUP BY city
ORDER BY sum(sum_of_transactions) desc
```
Answer:
United State, Canada and Hong Kong are the top three countries with the highest revenue. 
Mountain View, San Bruno and New York are the top three cities with the highest transaction revenues on the website.


**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
Average products ordered by country
```sql
SELECT distinct(country), sum(avg_products_ordered)
FROM (
select s.country, s.city, avg(n.units_sold) avg_products_ordered
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY (s.country), s.city, n.units_sold
having n.units_sold is not null
order by avg_products_ordered desc) as temp2
GROUP BY country
ORDER BY sum(avg_products_ordered) desc
```

Average products ordered by city
```sql
SELECT distinct(city), sum(avg_products_ordered)
FROM (
select s.country, s.city, avg(n.units_sold) avg_products_ordered
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY (s.country), s.city, n.units_sold
having n.units_sold is not null
order by avg_products_ordered desc) as temp2
GROUP BY city
ORDER BY sum(avg_products_ordered) desc
```
Answer:
United States, Canada and Hong Kong have the highest average products ordered with 3698, 11 and 11 units respectively. 
Mountain View, San Bruno and Sunnyvale have the highest average products ordered with 1143, 707 and 522 units respectively.


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

SQL Queries:

Product categories ordered by visitors from different countries
```sql
SELECT distinct(country), productcategory, sum(product)
FROM(
	select s.country, s.city, s.productcategory, count(s.productcategory) product
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.productcategory, s.country, s.city
order by product desc) as temp3
GROUP BY country, productcategory
order by sum(product) desc
```

Product categories ordered by visitors from different cities
```sql
SELECT distinct(city), productcategory, sum(product)
FROM(
	select s.country, s.city, s.productcategory, count(s.productcategory) product
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.productcategory, s.country, s.city
order by product desc) as temp3
GROUP BY city, productcategory
order by sum(product) desc
```
Answer:
It is evident that visitors from most countries order apparel on the website as that is the most ordered product category from the top 3 countries with the highest order by productcategories (US, India and Japan).
Apparel is also the most ordered product category from 4 out of the top 5 cities with the highest orders grouped by productcategories.

**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**

SQL Queries:

Top selling product based on Countries
```sql
SELECT distinct(country), v2productname, sum(product)
FROM(
	select s.country, s.city, s.v2productname, count(s.v2productname) product
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.v2productname, s.country, s.city
order by product desc) as temp3
GROUP BY country, v2productname
HAVING country not like '%not%'
order by sum(product) desc
```

Top selling product based on Cities
```sql
SELECT distinct(city), v2productname, sum(product)
FROM(
	select s.country, s.city, s.v2productname, count(s.v2productname) product
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
GROUP BY s.v2productname, s.country, s.city
order by product desc) as temp3
GROUP BY city, v2productname
HAVING city not like '%not%'
order by sum(product) desc
```
Answer:
Because the majority of the visitors came in from the United States, the top products ordered are also from visitors in the United States. There also isnèt any visible trends as the top three products ordered are Google's cotton short sleeve shirt, Google Power bank and Youtube Custom Decals.
There is no observable trend in the product ordered by visitors from various cities. Visitors from charlotte ordered 1582 units of the google lunch bags while visitors from chicago ordered the youtube custom decals. Coming in at third is visitorss from Hong Kong who ordered Google Device stands mostly. 

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```sql
SELECT
    city,
    country,
    SUM(product_revenue) AS total_revenue
FROM (
    SELECT
        s.city,
        s.country,
        s.productSKU,
        s.v2ProductName,
        SUM(a.newrevenue) AS product_revenue
    FROM
        all_sessions AS s
    INNER JOIN
        analytics AS a 
	ON s.fullVisitorId = a.fullVisitorId
    WHERE
        a.newrevenue IS NOT NULL
    GROUP BY
        s.city,
        s.country,
        s.productSKU,
        s.v2ProductName
) AS product_revenue_cte
GROUP BY
    city,
    country
ORDER BY
    total_revenue DESC;
```
Answer:
This query highlîghts the impact of revenue generated from each city and country, sorted by the total revenue.
As earlier called out, the company makes majority of its revenue from cities from United States.






