What are your risk areas? Identify and describe them.

-Risk areas observed:
Identifying null values in the required columns.
Ensuring the table contained all the data required.
Identifying missing data. 
Checking for duplicates.
Ensuring the right data type.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

Sales_by_SKU Table:

Count of all records in the sales_by_sku table: 462
```sql
    select count(*)
    from sales_by_sku
```

Count of SKU records in the sales_by_sku table: 462; no duplicates.
```sql
    select distinct count(productsku)
    from sales_by_sku
```

Products Table:

Count of all records in the products table: 1092
```sql
    select *
    from products
```

Count of SKU records in the products table: 1092; no duplicates.
```sql
    select distinct count(sku)
    from products
```

All_Sessions Table:

Count of all records in the all_sessions table: 15134
```sql
    select count(*)
    from all_sessions
```

Distinct fullvisitorid records: 14223; duplicate fullvisitorid records exist.
```sql
    select distinct (fullvisitorid)
    from all_sessions
```

Distinct visitid records: 14556; duplicate visitid records exist.
```sql
    select distinct (visitid)
    from all_sessions
```

Exploring the Country column: 24 records missing country, 135 distinct countries 
```sql
    select (country)
    from all_sessions
    where country not LIKE '%not%'
```

Exploring the City Column: 8656 records missing city, 264 distinct cities
```sql
    select distinct(city)
    from all_sessions
    where city not LIKE '%not%'
```

Number of Rows missing either country or city value: 8656
```sql
    select count(*)
    from all_sessions
    where country LIKE '%not%' or city LIKE '%not%'
```

Finding columns with complete or missing no data: productprice, productSKU, v2product name and v2productcategory all have 15134 records
```sql
    select productprice
    from all_sessions
    where productprice is not NULL
    order by productprice desc
```

Highlighting columns containing some data:
totaltransactionrevenue column has 81 records.
productquantity column has 53 records.
transactionid column has 9 records.
productrevenue and transactionrevenue columns has 4 records.

Columns without any data:
productrefundamount, itemquantity and itemrevenue columns are all empty.

Analytics Table: 

Count of all records in the analytics table: 4301122
```sql
    select count(*)
    from analytics
```

Distinct fullvisitorid records: 120018; duplicate fullvisitorid records exist.
```sql
    select distinct (fullvisitorid)
    from analytics
```

Distinct visitid records: 148642; duplicate visitid records exist.
```sql
    select distinct (visitid)
    from analytics
```

Exploring the units_sold column: 95147 records exist; the rest are null.
```sql
    select units_sold
    from analytics
    where units_sold > 0
    order by units_sold desc
```

Exploring the unit_price column: 4112808 records exist with the rest of the data set to 0.
```sql
    select unit_price
    from analytics
    where unit_price > 0
    order by unit_price asc
```
 
Exploring the revenue column:15355 records exist; the rest are null.
```sql
    select revenue
    from analytics
    where revenue is not null
```

Columns without any data:
userid columns is empty.


    
