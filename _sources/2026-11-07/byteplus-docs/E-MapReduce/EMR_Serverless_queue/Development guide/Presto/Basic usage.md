---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sq_presto_basic_usage"
---

EMR Serverless Presto syntax is fully compatible with open\-source Presto syntax. For detailed syntax rules, refer to[ Presto syntax Note](https://prestodb.io/docs/0.280/sql.html). This document mainly introduces and demonstrates some basic operations of Presto.

<span id="d257f6d5"></span>
## Database and table operations

<span id="b97fbb58"></span>
### Database operations


1. Create a database.


```SQL
CREATE SCHEMA IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA;
```



2. Create a database and set the corresponding TOS Bucket and path.


```SQL
CREATE SCHEMA IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA
WITH (
    LOCATION='tos://${your-presto-bucket}/serverless/presto'
    );
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When specifying a custom Bucket, ensure that the Bucket has already been created and has read and write permissions.</div>



3. Delete a database.


```SQL
DROP SCHEMA SERVERLESS_PRESTO_SCHEMA;
```


<span id="cbf688d6"></span>
### Table operations


1. Create a table.


```SQL
CREATE TABLE IF NOT EXISTS SP_TABLE (
    ID BIGINT,
    NAME VARCHAR,
    AGE INT
);
```



2. Create a table and set the storage path and storage format.


```SQL
CREATE TABLE IF NOT EXISTS SP_TABLE (
    ID BIGINT,
    NAME VARCHAR,
    AGE INT
)
COMMENT 'EMR SERVERLESS TABLE'
WITH (
    EXTERNAL_LOCATION='tos://${your-presto-bucket}/serverless/presto/',
    FORMAT='ORC'
);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">EXTERNAL_LOCATION must specify a directory.</div>


* <div data-tips="true" data-tips-type="warning">The default FORMAT is ORC. You can set it to Parquet, TEXTFILE, or other file formats as needed.</div>


3. View table information.


```SQL
DESC SP_TABLE;
```



4. Insert data.


```SQL
INSERT INTO SP_TABLE
VALUES (1, 'Serverless', 0),
       (2, 'Presto', 1);
```



5. Query data.


```SQL
SELECT * FROM SP_TABLE;
```



6. Delete a table.


```SQL
DROP TABLE SP_TABLE;
```


<span id="a37c6ea1"></span>
## Presto access to lake\-format data

Currently, EMR Serverless Presto supports querying three lake formats: Hudi, Iceberg, and Delta. Lake format databases and tables can be created using EMR Serverless Spark. Data can be written, and then queries can be executed using Presto.

<span id="ecf56a9f"></span>
### Operate Hudi data

The default Catalog for EMR Serverless Presto is Hive. Before operating Hudi data, update the Catalog to Hudi.

```SQL
-- Method 1
USE HUDI.PRESTO_HUDI_DB;

-- Method 2
SELECT
  *
FROM
  HUDI.PRESTO_HUDI_DB.HUDI_TBL;
```


<span id="90f723ac"></span>
### Operate Iceberg data

The default Catalog for EMR Serverless Presto is Hive. Before operating Iceberg data, update the Catalog to Iceberg.

```SQL
-- Method 1
USE ICEBERG.PRESTO_ICEBERG_DB;

-- Method 2
SELECT
  *
FROM
  ICEBERG.PRESTO_ICEBERG_DB.ICEBERG_TBL;
```


<span id="be7d847c"></span>
### Operate Delta data

The default Catalog for EMR Serverless Presto is Hive. Before operating Delta data, update the Catalog to Delta.

```SQL
-- Method 1
USE DELTA.PRESTO_DELTA_DB;

-- Method 2
SELECT
  *
FROM
  DELTA.PRESTO_DELTA_DB.DELTA_TBL;
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To ensure data security and cluster stability, UDFs are currently not supported. For UDF requirements, use EMR Serverless Spark.</div>


* <div data-tips="true" data-tips-type="warning">To ensure cluster stability, running large ETL jobs on the Presto cluster is not recommended. Use EMR Serverless Spark for large ETL jobs.</div>
