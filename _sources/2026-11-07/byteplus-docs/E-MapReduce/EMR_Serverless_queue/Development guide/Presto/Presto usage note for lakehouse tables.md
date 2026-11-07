---
title: "Presto usage note for lakehouse tables"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Presto_usage_note_for_lakehouse_tables"
---

EMR Serverless Presto syntax is fully compatible with open source Presto syntax. For detailed syntax rules, refer to[ Presto syntax note](https://prestodb.io/docs/0.280/sql.html). This article mainly introduces and demonstrates some basic operations of Presto.

<span id="dc211a18"></span>
## Presto accesses Hive

<span id="8b631459"></span>
### Database operations

```SQL
-- If las catalog is not specified, hive catalog is used by default
CREATE SCHEMA IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA;

-- Specify a custom las catalog
CREATE SCHEMA IF NOT EXISTS las_catalog_test.SERVERLESS_PRESTO_SCHEMA;

-- Specify TOS path: The bucket has been created and has read and write permissions
CREATE SCHEMA IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA
WITH (
    LOCATION='tos://${your-presto-bucket}/serverless/presto'
    );
    
-- Delete database
DROP SCHEMA SERVERLESS_PRESTO_SCHEMA;
```


<span id="bb013ec1"></span>
### Table operations

```SQL
-- Create table
CREATE TABLE IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA.SP_TABLE (
    ID BIGINT,
    NAME VARCHAR,
    AGE INT
);

-- Create table and set storage path and storage format
-- FORMAT defaults to ORC. You can set it to Parquet, TEXTFILE, and other file formats as needed
CREATE TABLE IF NOT EXISTS SERVERLESS_PRESTO_SCHEMA.SP_TABLE (
    ID BIGINT,
    NAME VARCHAR,
    AGE INT
)
COMMENT 'EMR SERVERLESS TABLE'
WITH (
    EXTERNAL_LOCATION='tos://${your-presto-bucket}/serverless/presto/',
    FORMAT='ORC'
);

-- View table information
DESC SERVERLESS_PRESTO_SCHEMA.SP_TABLE;


-- Query data
SELECT * FROM SERVERLESS_PRESTO_SCHEMA.SP_TABLE;

-- Delete table
DROP TABLE SERVERLESS_PRESTO_SCHEMA.SP_TABLE;
```


<span id="327d7c4c"></span>
### UDF operations

```SQL
-- Presto uses UDF: catalog.db.udfname
select hive.dbname.udfname('aaabbB');
```


<span id="ddf1e862"></span>
## Presto accesses Iceberg

```SQL
-- Default Hive catalog
SELECT
  *
FROM
  test_iceberg_db.test_tb limit 10;

-- Custom catalog
SELECT
  *
FROM
  test_catalog.test_iceberg_db.test_tb limit 10;
```


<span id="0618ee62"></span>
## Presto accesses Paimon

```SQL
-- Default Hive catalog
SELECT
  *
FROM
  test_iceberg_db.test_tb limit 10;

-- Custom catalog
SELECT
  *
FROM
  test_catalog.test_iceberg_db.test_tb limit 10;
```


<span id="5c26d86a"></span>
## Presto accesses Hudi

```SQL
-- Default Hive catalog
SELECT
  *
FROM
  test_iceberg_db.test_tb limit 10;

-- Custom catalog
SELECT
  *
FROM
  test_catalog.test_iceberg_db.test_tb limit 10;
```


<span id="f7025439"></span>
## Presto accesses Delta

```SQL
-- Default Hive catalog
SELECT
  *
FROM
  test_iceberg_db.test_tb limit 10;

-- Custom catalog
SELECT
  *
FROM
  test_catalog.test_iceberg_db.test_tb limit 10;
```
