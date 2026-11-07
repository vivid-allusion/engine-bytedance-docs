---
title: "Hive access to Hudi data"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_access_to_Hudi_data"
---

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. The cluster has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Ensure that the local server and the EMR cluster primary node can communicate over the network and that the cluster can be accessed directly. You need to bind a public IP address to the primary node, and add an allowlist rule for the local server's access in **Private Network \> Security Group**. For details, see: [Access Rules](https://www.volcengine.com/docs/6401/68895).


<span id="_2-创建-huid-的表"></span>
## 2 Create a Hudi table

Log in to the cluster primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).


1. Enter the Spark command line and execute the following command:


```sql
spark-sql --master local --conf 'spark.serializer=org.apache.spark.serializer.KryoSerializer' --conf 'spark.sql.catalog.spark\_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog' --conf 'spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension'
```



2. Create a Hudi table in Spark


```sql
CREATE TABLE hudi_mor_tbl (
  id INT,
  name STRING,
  price DOUBLE,
  ts BIGINT
) USING HUDI
TBLPROPERTIES (
  type = 'mor',
  primaryKey = 'id',
  preCombineField = 'ts'
);
```



3. Write data to the Hudi table


```sql
INSERT INTO hudi_mor_tbl SELECT 1, 'a1', 20, 1000;
```


<span id="_3-在-hive-中查看-hudi-数据"></span>
## 3 View Hudi data in Hive


1. Run the following command to enter the Hive command line


```shell
su hive
hive
```



2. Execute SQL


```sql
SELECT * FROM hudi_mor_tbl;
```


The following information is returned:

> OK

> 20220802214303953 20220802214303953_0_0 id:1 1bb25562\-0342\-4b99\-b7a6\-d2bf82fa0119\-0_0\-27\-1215_20220802214303953.parquet 1 a1 20.01000

> Time taken: 1.55 seconds, Fetched: 1 row(s)
