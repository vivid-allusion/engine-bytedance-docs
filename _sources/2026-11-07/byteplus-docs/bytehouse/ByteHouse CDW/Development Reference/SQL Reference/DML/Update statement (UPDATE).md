---
title: "Update statement (UPDATE)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/update-statement"
---

ByteHouse supports using update statements (UPDATE) to update single\-table data or multi\-table linked data.

<span id="62cc6484"></span>
# Caution


* The target table of UPDATE must contain a unique key. Normal CnchMergeTree currently does not support update operations.

* Updating unique key and partition key columns is not supported yet.

* Avoid full table updates when possible.


<span id="af59c6cf"></span>
# Single\-table update

<span id="9c134dd1"></span>
## Usage restrictions

Currently only unique key tables support using update statements (UPDATE). For other table types, refer to the "ALTER TABLE \- UPDATE" statement.

<span id="4ab4e6cc"></span>
## **Syntax**

```SQL
UPDATE [db.]table SET a=b WHERE expr;
```


Param description is as follows:


|Param |description |
|---|---|
|`[db.]table` |Specify the target database name and data table name to update. |
|`a=b` |Specify the columns to update and their new values. |
|`expr` |Filter the rows to update; only rows that satisfy the condition `expr` will be modified. |


<span id="d6c2e942"></span>
## **Example**

```SQL
-- The engine guarantees the uniqueness of the unique key within partitions by default
CREATE TABLE test.unique_table
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO test.unique_table VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Update using the UPDATE statement
UPDATE test.unique_table SET amount = 10, revenue = 1000 WHERE event_time = '2020-10-29 23:40:00' and product_id=10001;

-- 10001 data rows were updated in the query results
select * from test.unique_table order by toDate(event_time), product_id;
┌─────event_time─┬─product_id─┬─city──┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men wear   │     10 │    1000   │
│ 2020-10-29 23:40:00 │      10002 │ Beijing │ men wear   │      2 │     200   │
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear   │      1 │     100   │
└────────────┴────────┴─────┴───────┴─────┴───────┘
```


<span id="c4610208"></span>
# Multi\-table update

<span id="c6f7d11c"></span>
## Prerequisites

Confirm you are using ByteHouse cloud data warehouse version 2.2 or above. You can check the engine version by following the **ByteHouse Console** \> **Tenant management** \> **Basic information** path.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6872505f4e40465e8bc957b81b602e88~tplv-goo7wpa0wc-image.image) </span>

<span id="64cf2c1b"></span>
## Syntax

```SQL
UPDATE Table_name1
[INNER JOIN | LEFT JOIN] Table_name2 ON Table_name1.C1 = Table_name2.C1
SET assignment_list
[WHERE where_condition]
```


Param description is as follows:


|Param |description |
|---|---|
|`Table_name1` |Specify the target table to update. For multi\-table updates, list the tables to update first. For example, to update the `customer` table's `customer_id` to 1, use the following statement:<br><br>```SQL```<br>```UPDATE customer```<br>```    LEFT JOIN new_customer ON customer.customer_name = new_customer.customer_name```<br>```SET```<br>```    customer.customer_id = '1';```<br> |
|`Table_name2` |Specify the source table for update, linking the target table `Table_name1` to be updated with the source table `Table_name2`. |
|`Table_name1.C1 = Table_name2.C1` |Define the join condition for the two tables mentioned above. |
|`assignment_list` |Define the fields to update and their new values. |
|`where_condition` |Filter rows that need to be updated; only rows that satisfy the condition `expr` will be modified. |


<span id="1fdc9b7a"></span>
## Example

Using the following tables as an example of multi\-table update, demonstrate how to use the UPDATE JOIN statement. Example creates tables `customer` and `new_customer`, with partition key set as `customer_name` and unique key set as `customer_id`.

```SQL
CREATE TABLE customer(customer_id Int32, customer_name String, customer_age Int32, addr String)
ENGINE = CnchMergeTree()  
PARTITION BY hash(customer_name) % 10
ORDER BY customer_id
UNIQUE KEY customer_id;

CREATE TABLE new_customer(customer_id Int32, customer_name String, customer_age Int32, addr String) 
ENGINE = CnchMergeTree() 
PARTITION BY hash(customer_name) % 10
ORDER BY customer_id
UNIQUE KEY customer_id;
```



* Example 1: Use LEFT JOIN clause with UPDATE statement

   Update the age of the customer with `customer_id ='2369'` to 42.

   ```SQL
   UPDATE customer
       LEFT JOIN new_customer ON customer.customer_id = new_customer.customer_id
   SET
       customer.customer_age = 42
   WHERE
       new_customer.customer_id = '2369';
   ```
   

   You can also run the following command for the same effect as the above command.

   ```SQL
   INSERT INTO customer
   SELECT customer.customer_id, customer.customer_name, 42, addr
   FROM customer 
   LEFT JOIN new_customer
   ON customer_customer_id = new_customer.customer_id
   WHERE new_customer.customer_id = '2369';
   ```
   

* Example 2: Use INNER JOIN clause with UPDATE statement

   * Update `addr` in the customer table to `'beijing'`.

      ```SQL
      UPDATE customer
          INNER JOIN new_customer ON customer.customer_name = new_customer.customer_name 
      SET
          customer.addr = 'beijing';
      ```
      

      You can also run the following command for the same effect as the above command.

      ```SQL
      INSERT INTO customer
      SELECT customer.customer_id, customer.customer_name, customer.customer_age, 'beijing'
      FROM customer 
      INNER JOIN new_customer
      ON customer.customer_name = new_customer.customer_name;
      ```
      

   * Update `customer_name` in the customer table to the `customer_name` in the new_customer table.

      ```SQL
      UPDATE customer
          INNER JOIN new_customer ON customer.customer_id = new_customer.customer_id
      SET
          customer.customer_age = new_customer.customer_age;
      ```
      

      You can also run the following command for the same effect as the above command.

      ```SQL
      INSERT INTO customer
      SELECT customer.customer_id, customer.customer_name, new_customer.customer_age, customer.addr
      FROM customer 
      INNER JOIN new_customer
      ON customer.customer_id = new_customer.customer_id;
      ```
