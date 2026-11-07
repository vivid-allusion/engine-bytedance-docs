---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/doris_advanced_usage"
---

This article introduces advanced use cases related to Doris clusters.

<span id="_1-高可用设置"></span>
## 1 High availability configuration

Doris supports multiple FE deployments. When using a high availability cluster, you need to select **Service High Availability** during cluster creation. When creating a high availability cluster, three Master node types are created to deploy Doris FE.

For details on cluster creation operations, see: [Create a cluster (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to enable high availability for services in production environments.</div>


<span id="_2-节点扩容"></span>
## 2 Node scaling

E\-MapReduce (EMR) provides a convenient scaling experience. To scale the cluster, go to the **Cluster Management \> Cluster Details \> Node Management** page, click **Node Scaling**, select the number of nodes to scale, and confirm to start the scaling operation.

You can subsequently view the scaling progress and scaling logs in real time on the **Cluster Details \> Operation Log** page.

After scaling is complete, you can use the MySQL Client or refer to the Doris Web page below to view the scaled Backend nodes.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf89877ffab4a8f4a2a060dcaa7c8d64.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Cluster usage is not affected during scaling.</div>


<span id="_3-doris-web页面使用"></span>
## 3 Doris Web page usage

<span id="_3-1-前置条件"></span>
### 3.1 Prerequisites


1. Bind Elastic EIP to the FE node. For details, see: [Bind Public IP](https://www.volcengine.com/docs/6401/68687).

2. The security group of the FE node allows access to port 8030. For details, see: [Add Access Rule](https://www.volcengine.com/docs/6401/68895).

3. Executing SQL on the Doris Web page is supported in EMR\-3.0.0 and later versions.


<span id="_3-2-进入-doris-web-页面"></span>
### 3.2 Accessing the Doris Web page

Enter the following address in your browser to be randomly redirected to the login page of the native Doris WebUI. Enter the corresponding account to complete SQL editing and execution in the Playground tab.

```plain
http://{{EIP}}:8030
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13c9a904ecefaa6d6cefb62e232c28ba.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Versions of EMR below 3.0.0 do not support submitting queries via Playground due to MySQL license reasons.</div>


<span id="_4-hudi-数据湖分析"></span>
## 4 Hudi data lake analytics

<span id="_4-1-doris-中创建-hudi-的外表"></span>
### 4.1 Creating Hudi external tables in Doris

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from Doris 1.2.1, querying Hudi tables by creating Hudi external tables is no longer supported. To use Hudi tables, configure hive catalog using multi\-catalog. For more details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109214">Advanced usage</a>.</div>


You can create Hudi external tables in Doris using the following two table creation examples. When creating external tables, there is no need to declare the column definitions. Doris can obtain column information from HiveMetaStore during queries.

Create a separate external table to mount the Hudi table. Refer to [CREATE TABLE](https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Data-Definition-Statements/Create/CREATE-TABLE) for specific syntax.

```sql
CREATE [EXTERNAL] TABLE table_name
[(column_definition1[, column_definition2, ...])]
ENGINE = HUDI
[COMMENT "comment"]
PROPERTIES (
"hudi.database" = "hudi_db_in_hive_metastore",
"hudi.table" = "hudi_table_in_hive_metastore",
"hudi.hive.metastore.uris" = "thrift://127.0.0.1:9083"
);
```


```plain
-- 例子：挂载 HiveMetaStore 中 hudi_db_in_hive_metastore 下的 hudi_table_in_hive_metastore，挂载时不指定schema。
CREATE TABLE `t_hudi` 
ENGINE = HUDI
PROPERTIES (
"hudi.database" = "hudi_db_in_hive_metastore",
"hudi.table" = "hudi_table_in_hive_metastore",
"hudi.hive.metastore.uris" = "thrift://127.0.0.1:9083"
);

-- 例子：挂载时指定schema
CREATE TABLE `t_hudi` (
    `id` int NOT NULL COMMENT "id number",
    `name` varchar(10) NOT NULL COMMENT "user name"
) ENGINE = HUDI
PROPERTIES (
"hudi.database" = "hudi_db_in_hive_metastore",
"hudi.table" = "hudi_table_in_hive_metastore",
"hudi.hive.metastore.uris" = "thrift://127.0.0.1:9083"
);
```


**Parameter description:** 


|Parameters |Note |
|---|---|
|External table columns |* Column names do not need to be specified. In this case, column information will be retrieved from HiveMetaStore during queries. This table creation method is recommended.<br><br>* If column names are specified, the specified column names must exist in the Hudi table. |
|ENGINE |Must be specified as HUDI. |
|PROPERTIES attribute |* `hudi.hive.metastore.uris`: Hive Metastore service address<br><br>* `hudi.database`: Name of the database mounted for Hudi<br><br>* `hudi.table`: Name of the table mounted for Hudi |


<span id="_4-2-展示表结构"></span>
### 4.2 Displaying table structure

To display the table structure, see [SHOW CREATE TABLE](https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Show-Statements/SHOW-CREATE-TABLE).

<span id="_4-3-查询用法"></span>
### 4.3 Query usage

After creating the Hudi external table in Doris, except for being unable to use Doris data models (such as rollup, pre\-aggregation, materialized views, and many others), there is no difference from ordinary Doris OLAP tables.

```sql
select * from t_hudi where k1 > 1000 and k3 ='term' or k4 like '%doris';
```


<span id="_4-4-注意事项"></span>
### 4.4 Important notes

The vectorization engine is enabled by default in Doris 1.1.1. However, Operators for querying external tables related to HiveMetaStore do not yet have a vectorized implementation. Therefore, querying Hudi tables only supports non\-vectorized mode. To query, you must set vectorization to false using the following command.

```plain
set enable_vectorized_engine=false
```
