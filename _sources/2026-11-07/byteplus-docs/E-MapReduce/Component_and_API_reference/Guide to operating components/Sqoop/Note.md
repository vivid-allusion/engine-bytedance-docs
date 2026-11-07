---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sqoop_note"
---

<span id="sqoop-使用说明"></span>
# Sqoop Note

Apache Sqoop is a tool for efficient bulk data transfer between Hadoop ecosystem software and structured data storage, such as relational databases.

<span id="将-mysql-数据导入-hdfs"></span>
## Import MySQL data into HDFS

sqoop import \-\-connect/\-\-username\-\-password\-\-query\-\-target\-dir\-\-split\-by

Parameter explanation:


|Parameter |Description |
|---|---|
|dburi |Database access URI |
|dbname |Database name |
|username |Database username |
|password |Database password |
|query\-sql |SQL query |
|hdfs\-dir |HDFS output directory |


For more information, refer to [Sqoop User Guide](http://sqoop.apache.org/docs/1.4.7/SqoopUserGuide.html?spm=a2c4g.11186623.0.0.378961feAHtS3F#_syntax)

<span id="将-hdfs-数据导入-mysql"></span>
## Import HDFS data into MySQL

sqoop export \-\-connect/\-\-username\-\-password\-\-table\-\-export\-dir

Parameter explanation:


|Parameter |Description |
|---|---|
|dburi |Database access URI |
|dbname |Database name |
|username |Database username |
|password |Database password |
|tablename |Database table name |
|hdfs\-dir |HDFS directory |


For more information, refer to [Sqoop User Guide](http://sqoop.apache.org/docs/1.4.7/SqoopUserGuide.html?spm=a2c4g.11186623.0.0.378961feAHtS3F#_syntax)

<span id="将-mysql-数据导入-hive"></span>
## Import MySQL data into Hive

Please ensure that the Hive service is selected.

sqoop import \-\-connect/\-\-username\-\-password\-\-table\-\-hive\-import \-\-target\-dir\-\-hive\-table

Parameter explanation:


|Parameter |Description |
|---|---|
|dburi |Database access URI |
|dbname |Database name |
|username |Database username |
|password |Database password |
|tablename |Database table name |
|hdfs\-dir |HDFS directory |
|hive\-tablename |Hive table name |


For more information, refer to [Sqoop User Guide](http://sqoop.apache.org/docs/1.4.7/SqoopUserGuide.html?spm=a2c4g.11186623.0.0.378961feAHtS3F#_syntax)

<span id="将-hive数据导入-mysql"></span>
## Import Hive data into MySQL

sqoop export \-\-connect/\-\-username\-\-password\-\-table\-\-export\-dir

Parameter explanation:


|Parameter |Description |
|---|---|
|dburi |Database access URI |
|dbname |Database name |
|username |Database username |
|password |Database password |
|tablename |Database table name |
|hdfs\-dir |HDFS directory |


For more information, refer to [Sqoop User Guide](http://sqoop.apache.org/docs/1.4.7/SqoopUserGuide.html?spm=a2c4g.11186623.0.0.378961feAHtS3F#_syntax)
