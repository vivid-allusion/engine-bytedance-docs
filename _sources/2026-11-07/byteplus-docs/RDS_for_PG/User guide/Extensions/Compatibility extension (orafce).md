---
title: "Compatibility extension (orafce)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/compatibility_extension-orafce"
---

Orafce is a PostgreSQL extension designed to provide functionality compatible with Oracle databases, including some syntax, data types, functions, and dictionary tables. This allows applications using Oracle data to more conveniently migrate to PostgreSQL, thereby reducing the amount of application code changes and simplifying the migration process.

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   create extension orafce;
   ```
   

* Delete extension

   ```sql
   drop extension orafce;
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

```sql
-- String handling:
postgres=# SELECT oracle.INSTR('Hello World', 'World') AS position; -- return 7
 position 
----------
        7
(1 row)

postgres=# SELECT oracle.SUBSTR('Hello World', 1, 5) AS substring;    -- return 'Hello'
 subString
-----------
 Hello
(1 row)


-- Date handling:
postgres=# SELECT oracle.ADD_MONTHS(NOW(), 1) AS next_month;        -- return the same day next month
     next_month
---------------------
 2024-09-16 17:21:24
(1 row)

postgres=# SELECT oracle.LAST_DAY(NOW()) AS laslast_day_of_month;      -- Return the last day of the month
  last_day_of_month
---------------------
 2024-08-31 17:21:24
(1 row)

--Math function:
postgres=# SELECT oracle.ROUND(123.456, 2) ASrounded_value;        -- Return 123.46
 rounded_value
---------------
        123.46
(1 row)

postgres=# SELECT oracle.TRUNC(123.456, 2) AStruncated_value;      -- Return 123.45
 truncated_value
-----------------
          123.45
(1 row)

--Conditional expression: Use the NVL function to handle null values:
postgres=# SELECT oracle.NVL(NULL::text, '默认值') AS result;  -- Return 'Default value'
 result 
--------
 默认值
(1 row)

postgres=# select oracle.nvl(NULL::int, 2);
 nvl
-----
   2
(1 row)

--Regular expression:
postgres=# SELECT oracle.REGEXP_LIKE('abc123', '^[a-zA-Z]+[0-9]+$') ASis_match;  -- return true
 is_match
----------
 t
(1 row)

postgres=# SELECT oracle.REGEXP_INSTR('123 123456 1234567, 1234567 1234567 12', '[^ ]+', 1, 6) ;
 regexp_instr
--------------
           37
(1 row)


-- DBMS_UTILITY package
postgres=# DO $$
postgres$# DECLARE
postgres$#     start_time integer;
postgres$#     end_time integer;
postgres$# BEGIN
postgres$#     start_time := DBMS_UTILITY.GET_TIME();
postgres$#     PERFORM pg_sleep(2);
postgres$#     end_time := DBMS_UTILITY.GET_TIME();
postgres$#     -- clamp long runtime on slow build machines to the 2s the testsuite is expecting
postgres$#     IF end_time BETWEEN start_time + 300 AND start_time + 1000 THEN end_time := start_time + 250; END IF;
postgres$#     RAISE NOTICE 'Execution time: % seconds', trunc((end_time - start_time)::numeric/100);
postgres$# END
postgres$# $$;
NOTICE:  Execution time: 2 seconds
DO
postgres=#

-- dbms_random package
postgres=# SELECT dbms_random.initialize(8);
 initialize
------------
 
(1 row)

postgres=# SELECT dbms_random.normal()::numeric(10, 8);
   normal
-------------
 -0.37787769
(1 row)

postgres=# SELECT dbms_random.normal()::numeric(10, 8);
   normal
------------
 0.80499804
(1 row)

postgres=# SELECT dbms_random.seed(8);
 seed
------
 
(1 row)

postgres=# SELECT dbms_random.random();
   random
------------
 -632387854
(1 row)


--DBMS_OUTPUT package
postgres=# CREATE FUNCTION dbms_output_test() RETURNS VOID AS $$
postgres$# DECLARE
postgres$#   buff1  VARCHAR(20) := 'orafce';
postgres$# BEGIN
postgres$#   PERFORM DBMS_OUTPUT.DISABLE();
postgres$#   PERFORM DBMS_OUTPUT.ENABLE();
postgres$#   PERFORM DBMS_OUTPUT.SERVEROUTPUT ('t');
postgres$#   PERFORM DBMS_OUTPUT.PUT_LINE ('ORAFCE');
postgres$#   PERFORM DBMS_OUTPUT.PUT_LINE (buff1);
postgres$#   PERFORM DBMS_OUTPUT.PUT ('ABC');
postgres$#   PERFORM DBMS_OUTPUT.PUT_LINE ('');
postgres$# END;
postgres$# $$ LANGUAGE plpgsql;
CREATE FUNCTION
postgres=# SELECT dbms_output_test();
ORAFCE
orafce
ABC
 dbms_output_test
------------------
 
(1 row)
```


<span id=".5YW25LuW"></span>
## Others

For more information, please see the [orafce official documentation](https://github.com/orafce/orafce).
