---
title: "Dataset and catalog FAQ"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Dataset_and_catalog_FAQ"
---

<span id="0a30044f"></span>
# Create a dataset

<span id="_1-创建database时提示illegalargumentexception报错"></span>
## IllegalArgumentException error when creating a database

```java
代码：
create database test_db;
报错信息：
org.apache.kyuubi.KyuubiSQLException: org.apache.kyuubi.KyuubiSQLException: Error operating ExecuteStatement: java.lang.IllegalArgumentException: java.net.URISyntaxException: Relative path in absolute URI: tos://serverless-sparktest_lf.db
```


Cause:

The direct cause is that the user did not specify the database location. By default, the Database path is completed based on the LasFormation default data directory path, but the user did not set the default data directory path.

Solution:

Set the storage location in the LAS console under Data Directory.

If the bucket or directory does not exist, first go to the TOS console to create the bucket and directory.

<span id="_2-创建database时提示lfsecurityexception"></span>
## LfSecurityException error when creating a database

```java
代码：create database test_db location 'tos://testos/test_db.db';
报错信息：
代码：create database test_db location 'tos://testos/test_db.db';
报错信息：
org.apache.kyuubi.KyuubiSQLException: org.apache.kyuubi.KyuubiSQLException: Error operating ExecuteStatement: org.apache.spark.sql.AnalysisException: org.apache.hadoop.hive.ql.metadata.HiveException: MetaException(message:Caught exception: class bytedance.olap.las.gemini.exception.LfSecurityException, message:java.net.SocketException: Broken pipe (Write failed))at org.apache.spark.sql.hive.HiveExternalCatalog.withClient(HiveExternalCatalog.scala:119)
```


Cause: The user has not enabled LasFormation.

Solution: Enable LasFormation.

<span id="93917cb3"></span>
# Data query

<span id="ba3f9639"></span>
## How to query data from other catalogs

To query other catalogs created on LasFormation with Spark (for example, the catalog name is other_catalog), there are two methods


* Method 1: set spark.hive.metastore.catalog.default=other_catalog;


After setting this parameter, all ways to access db/table are the same as accessing the default catalog.

```Plain
select * from db.table1; # 实际上会访问other_catalog.db.table1
```



* Method 2: Access directly using the three\-part format


```SQL
select * from other_catalog.db.table1;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The three\-part format is currently only supported in select statements and not supported in insert/create database statements.</div>


<span id="2d3db2b3"></span>
## How to query data from other tenants

For example, if tenant A wants to access tenant B's db1.table1, tenant A can use the following method to access

```Plain
select * from `B@db1`.table1; # 其中B是租户B的租户id，比如210002323
```


<span id="302b5f88"></span>
# Data permissions

<span id="93cdbce1"></span>
## Failed to grant write permission to a user who already has read permission

Issue description: After the user is granted read permission for a table, attempting to write data results in a prompt indicating no write permission. When granting write permission to the user, it prompts that the user is already authorized and cannot be authorized again.

Cause of the issue: Only a single role can be granted to the same user.

Solution: Find the authorization record and edit the user's role.
