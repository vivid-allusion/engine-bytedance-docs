---
title: "Paimon Aggregation Table"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Paimon_Aggregation_Table"
---

<span id="504b1ff4"></span>
## 1. Overview

Flink Paimon's **Aggregation Table** supports real\-time aggregation computations. It allows users to perform aggregation operations on data while writing and directly store the results in the table. This table is particularly suited for scenarios requiring real\-time calculation and querying of aggregated results, such as user behavior analysis, real\-time monitoring, and real\-time reporting. The aggregation table includes the following features:


* **Real\-time Aggregation**: Automatically performs aggregation calculations (such as sum, maximum, minimum, etc.) on data during writing and stores the results in the table.

* **Enhanced Query Performance**: Since the aggregation results are precomputed and stored, queries can directly access these results, avoiding the performance overhead of real\-time computation.

* **Support for Retract**: Certain aggregation functions support the Retract operation (such as `sum`, `count`), accurately handling updates and deletions.


<span id="e4a03572"></span>
## 2. Applicable Scenarios


* **User Behavior Analysis**: By analyzing the traffic of a website or an app, total user visit duration and the number of visits are measured.

* **Advertising Effectiveness Analysis**: Ad vendors provide total advertisement clicks, impressions, and consumption statistics for advertisers.

* **E\-commerce Real\-time Reports**: By analyzing annual e\-commerce transaction data, it identifies popular products among various consumer groups for specified quarters or months.


<span id="5fe0f22f"></span>
## 3. Usage Examples

Before use, note the requirements for the Flink version:


* The version of Flink must be \>= 1.16, with the following features supported:

   * Flink 1.16 incorporates Paimon 0.6 version, which does not support `collect`, `merge_map`, and other Aggregation functions. If needed, it is recommended to upload a higher version of Paimon community Connector.

   * Flink 1.17 is recommended for use. Features Paimon version 0.8.2 byte\-enhanced function and also supports syntax like stored procedures.


<span id="0cbf6716"></span>
### Business Description

We have two tables: **Order Table** and **Suborder Table**. The Order Table stores the basic order information of the system, while the Suborder Table is associated with the Order Table through **Order ID**. Each order may contain multiple suborders, so it is necessary to aggregate the suborder information according to the Order ID and collect multiple rows of suborder data into a nested array (`ARRAY<ROW>`). Implementation logic is as follows:


1. **Configuration of the Primary Key for the Nested Table**


Specifies the primary key of the nested table through `fields.<field-name>.nested-key=pk0,pk1,...` Designating the primary key as the suborder's id (if not specified, it will be automatically added to the suborder array and will not be deduplicated).


2. **Price Aggregation**


The total price of the order equals the sum of all suborder prices. We can automatically cumulate prices when sub\-orders are stored by configuring `'fields.sum_price.aggregate-function' = 'sum'`.

<span id="bf092b5d"></span>
### 3.2 Business Modeling

Before creating the Paimon data table, we set up a Catalog, simplifying the test scheme using a FileSystem\-based Catalog. Also consider the following solution [Paimon with LAS Catalog](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog) using LAS as the metadata Catalog management strategy:

```SQL
CREATE CATALOG paimon_agg
WITH
  (
    'type' = 'paimon',
    'warehouse' = 'tos://<bucket-name>/paimon_agg'
  );
CREATE DATABASE IF NOT EXISTS paimon_agg.paimon_agg;
```


Creating the Paimon aggregation table is done as follows, noting that we use date as a partition field, and perform `sum` and `last_non_null_value` aggregation on pv and last_login_time.

```SQL
-- Orders table
CREATE TABLE IF NOT EXISTS paimon_agg.paimon_agg.orders (
  order_id BIGINT PRIMARY KEY NOT ENFORCED,
  user_name STRING,
  address STRING
);

-- Sub-orders with the same order_id belong to the same order
CREATE TABLE IF NOT EXISTS paimon_agg.paimon_agg.sub_orders (
  order_id BIGINT,
  sub_order_id INT,
  product_name STRING,
  price BIGINT,
  PRIMARY KEY (order_id, sub_order_id) NOT ENFORCED
);
```


The SQL statement for creating the aggregation table specifies the aggregation merge engine, and furthermore, it specifies.


1. Aggregating the `sub_orders` field with `nested_update`, simulating nested tables within orders, and deduplicated updates based on sub_order id `sub_order_id`.

2. Additionally, aggregating sub\-order prices with `sum` to calculate the total price of the orders.


```SQL
-- Wide table: aggregates sub-orders into a nested array and calculates the total price of all sub-orders
CREATE TABLE IF NOT EXISTS paimon_agg.paimon_agg.order_wide (
  order_id BIGINT PRIMARY KEY NOT ENFORCED,
  user_name STRING,
  address STRING,
  sub_orders ARRAY<ROW<sub_order_id BIGINT, product_name STRING, price BIGINT>>,
  sum_price BIGINT
) WITH (
  'merge-engine' = 'aggregation',
  'fields.sub_orders.aggregate-function' = 'nested_update',
  'fields.sub_orders.nested-key' = 'sub_order_id',
  'fields.sum_price.aggregate-function' = 'sum'
);
```


<span id="5bc08830"></span>
### 3.3 Aggregation Writing

The SQL for aggregation writing merges multiple update streams with `UINON ALL` operation. In different data streams, ensure that fields not needing updates are set to NULL, and other fields will be updated or merged.

```SQL
-- 宽化
INSERT INTO paimon_agg.paimon_agg.order_wide
SELECT * FROM (
  SELECT 
    order_id, 
    user_name,
    address, 
    CAST (NULL AS ARRAY<ROW<sub_order_id BIGINT, product_name STRING, price BIGINT>>) ,
    CAST (NULL AS BIGINT) 
  FROM paimon_agg.paimon_agg.orders


  UNION ALL 
    
  SELECT 
    order_id, 
    CAST (NULL AS STRING), 
    CAST (NULL AS STRING), 
    ARRAY[ROW(sub_order_id, product_name, price)],
    price 
  FROM paimon_agg.paimon_agg.sub_orders
);
```


Once the data stream is successfully built, we can use the following SQL to test data insertion:

```SQL
-- Insert main order data
INSERT INTO paimon_agg.paimon_agg.orders VALUES
(1001, 'John Smith', 'No.123 Park Avenue, New York'),
(1002, 'Emma Davis', '456 Ocean Drive, Los Angeles'),
(1003, 'Michael Brown', '789 Lake Street, Chicago'),
(1004, 'Sarah Wilson', '321 Forest Road, Seattle');

-- Insert sub-order data
INSERT INTO paimon_agg.paimon_agg.sub_orders VALUES
-- Sub-orders for order 1001 (contains 3 items)
(1001, 1, 'iPhone 15', 6999),
(1001, 2, 'AirPods Pro', 1999),
(1001, 3, 'Power Adapter', 199),
-- Sub-orders for order 1002 (contains 2 items)
(1002, 1, 'MacBook Pro', 12999),
(1002, 2, 'Laptop Bag', 299),
-- Sub-orders for order 1003 (contains 4 items)
(1003, 1, 'iPad Air', 4799),
(1003, 2, 'Apple Pencil', 999),
(1003, 3, 'Protective Case', 299),
(1003, 4, 'Screen Protector', 99),
-- Sub-order for order 1004 (contains 1 item)
(1004, 1, 'Apple Watch', 3299);
```


<span id="220dcb2c"></span>
### 3.4 Data Validation

Data can be outputted downstream using print:

```SQL
-- Print the results following the nested schema of the table
CREATE TABLE IF NOT EXISTS print_result (
  order_id BIGINT PRIMARY KEY NOT ENFORCED,
  user_name STRING,
  address STRING,
  sub_orders ARRAY<ROW<sub_order_id BIGINT, product_name STRING, price BIGINT>>,
  sum_price BIGINT
) WITH (
    'connector' = 'print'
);

INSERT INTO `print_result`
SELECT * FROM `paimon_agg`.`paimon_agg`.`order_wide`;
```


The validation data is shown in the table below; it is evident that the sub\-orders and total order amounts have been correctly aggregated:

<span id="2e61bc2f"></span>
## 4. Aggregation Functions

The currently supported aggregation functions and data types are as follows:


* `sum`: The function aggregates values across multiple rows. It supports the data types DECIMAL, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, and DOUBLE.

* `product`: The function can calculate the product of values across multiple rows. It supports DECIMAL, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, and DOUBLE data types.

* `count`: The function counts values across multiple rows. It supports INTEGER and BIGINT data types.

* `max`: The function identifies and retains the maximum value. It supports CHAR, VARCHAR, DECIMAL, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, DOUBLE, DATE, TIME, TIMESTAMP, and TIMESTAMP_LTZ data types.

* `min`: The function identifies and retains the minimum value. It supports CHAR, VARCHAR, DECIMAL, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, DOUBLE, DATE, TIME, TIMESTAMP, and TIMESTAMP_LTZ data types.

* `last_value`: The function replaces previous values with the most recently imported value. It supports all data types.

* `last_non_null_value`: The function replaces previous values with the latest non\-null value. It supports all data types.

* `listagg`: The function concatenates multiple string values into one string. It supports STRING data type.

* `bool_and`: The function evaluates whether all values in a Boolean set are true. It supports BOOLEAN data type.

* `bool_or`: The function checks if there is at least one true value in a Boolean set. It supports BOOLEAN data type.

* `first_value`: The function retrieves the first null value from a dataset. It supports all data types.

* `first_non_null_value`: The function selects the first non\-null value in a dataset. It supports all data types.

* `nested_update`: The function collects multiple rows into an array(the so\-called "nested table"). It supports ARRAYdata types. Use `fields.<field-name>.nested-key=pk0,pk1,...` to specify the primary keys of the nested table. If there is no key, rows will be appended to the array.

* `collect`: The function collects elements into an array. You can set `fields.<field-name>.distinct=true` to deduplicate elements. It only supports ARRAY types.

* `merge_map`: The function merges the input maps. It only supports MAP types.


For stream queries, `aggregation` merge engine must be used together with `lookup` or `full-compaction` (producers of `input` change logs are also supported, but only return input records).
