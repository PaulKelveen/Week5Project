What issues will you address by cleaning the data?

-dropped the sales_report table as the records found there exists in both the product and the sales_by_sku tables.
-verified that all entries in the product table is unique. 
-linked products table (SKU; PK), sales_records (productSKU; FK), sales_bu_sku (productSKU; FK) and all_ sessions (productSKU; FK) table.
-deleted rows in the all_sessions table missing country and city.
-inserted the product of unit_price and units_sold into the new column creared called newrevenue on the analytics table.
-inserted a new column in all_sessions table with a split of the product category



Queries:
Below, provide the SQL queries you used to clean your data.

Dropped the sales_report tables as the records found there exists in both the product and the sales_by_colums:
```sql
        DROP TABLE sales_report
```

Verified that all entries in the product table is unique: 

Count of all records in the products table - 1092.
```sql
        select count(*)
        from products
```
        
Count of distincts records in the SKU column of the products table: 1092
```sql
        select distinct count(sku)
        from products
```

Deleted rows in the all_sessions table missing country and city:

Count of all records in the all_sessions table - 15134.
```sql
        select count(*)
        from all_sessions
```

Count of records missing either country or city value - 8656.
```sql
        select count(*)
        from all_sessions
        where country LIKE '%not%' or city LIKE '%not%'
```

Deleting records missing either country or city value - 
```sql
        delete from all_sessions
        where country LIKE '%not%' or city LIKE '%not%'
```

Verification: number of records in table - 6478
```sql
        select count(*)
        from all_sessions
```

Inserted the product of unit_price and units_sold into the new column creared called newrevenue on the analytics table.

Creating new column newrevevnue.
```sql
        alter table analytics
	add newrevenue big int;
```

Updating newrevenue column
```sql
        update analytics
        SET newrevenue = 
        (case 
	   		when revenue is not null then cast(revenue as bigint)
	   		ELSE (unit_price * units_sold)
        end)
```
        
Inserted a new column in all_sessions table with a split of the product category
 
 Creating new column productcategory.
 ```sql
        alter table all_sessions
	add productcategory text;
```

Updating productcategory column
```sql
    	update all_sessions
	SET productcategory = split_part(v2productcategory,'/', 2);
```



        Verification: number of records in table - 6478
        select count(*)
        from all_sessions
        
