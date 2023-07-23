What issues will you address by cleaning the data?

-dropped the sales_report tables as the records found there exists in both the product and the sales_by_colums.
-verified that all entries in the product table is unique. 
-linked products table (PK), sales_records (FK), sales_bu_sku (FK) and all_ sessions table using the ProductSKU column.
-deleted rows in the all_sessions table missing country and city.
-inserted the product of unit_price and units_sold into the new column creared called newrevenue on the analytics table.
-



Queries:
Below, provide the SQL queries you used to clean your data.

Dropped the sales_report tables as the records found there exists in both the product and the sales_by_colums:
        DROP TABLE sales_report

Verified that all entries in the product table is unique: 
        Count of all records in the products table - 1092.
        select count(*)
        from products
        
        Count of distincts records in the SKU column of the products table: 1092
        select distinct count(sku)
        from products

Deleted rows in the all_sessions table missing country and city:
        Count of all records in the all_sessions table - 15134.
        select count(*)
        from all_sessions

        Count of records missing either country or city value - 8656.
        select count(*)
        from all_sessions
        where country LIKE '%not%' or city LIKE '%not%'

        Deleting records missing either country or city value - 
        delete from all_sessions
        where country LIKE '%not%' or city LIKE '%not%'

        Verification: number of records in table - 6478
        select count(*)
        from all_sessions

Inserted the product of unit_price and units_sold into the new column creared called newrevenue on the analytics table.
        Creating new column newrevevnue.
        alter table analytics
        add newrevenue big int;

        Updating newrevenue column
        update analytics
        SET newrevenue = 
        (case 
	   		when revenue is not null then cast(revenue as bigint)
	   		ELSE (unit_price * units_sold)
        end)
        

        




        

Deleted rows in the analytics table missing units_sold values:
        Count of all records in the analytics table - 4301122.
        select count(*)
        from analytics

        Count of records missing missing units_sold values - 4205975.
        select *
        from analytics
        where units_sold is null

        Deleting records missing either units_sold values - 
        delete from all_sessions
        where country LIKE '%not%' or city LIKE '%not%'

        Verification: number of records in table - 6478
        select count(*)
        from all_sessions
        
