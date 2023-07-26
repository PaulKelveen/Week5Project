Question 1: 
Total sales records being analyzed.

SQL Queries:
```sql
select count(*)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
```
Answer: 
There are 113633 matching records between the analytics and the all_sessions table.

Question 2: 
Total number of unique visitors (fullVisitorID).

SQL Queries:
```sql
select distinct(s.fullvisitorid)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
```
Answer:
We have a total of 1657 unique visitors based on the fullvisitorid column.

Question 3: 
Total number of unique visitors (VisitID) 

SQL Queries:
```sql
select distinct(s.visitid)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid
```
Answer:
We have a total of 1700 unique visitors based on the visitid columns.

Question 4: 
Percentage of visitors to the site that actually makes a purchase

SQL Queries:
```sql
select ceiling((((select count(n.units_sold)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid) *100) / (select count(*)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid))) as percentage_of_customers_making_purchase 
From (select count(*)
from all_sessions s
join analytics n
on s.fullvisitorid = n.fullvisitorid) as temp6
```

Answer:
About 2% of all visitors to the website go on to make a purchase.



Question 5: 

SQL Queries:

Answer:
