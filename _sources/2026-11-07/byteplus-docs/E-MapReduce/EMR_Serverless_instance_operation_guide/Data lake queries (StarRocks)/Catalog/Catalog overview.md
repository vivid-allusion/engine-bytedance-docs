---
title: "Catalog overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Catalog_overview"
---

This article introduces what a Catalog is and how to use Catalogs to manage and query internal and external data. Some images and content in this article are sourced from the open\-source StarRocks [overview](https://docs.starrocks.io/zh/docs/data_source/catalog/catalog_overview#catalog).

<span id="_1-基本概念"></span>
## 1 basic concepts


* Internal data: Refers to data saved in StarRocks.

* External data: Refers to data saved in external data sources (such as Apache Hive™, Apache Iceberg, Apache Hudi, Delta Lake, JDBC).


<span id="_2-catalog"></span>
## 2 Catalog

Currently, StarRocks provides two types of Catalog: internal catalog and external catalog.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9a72afaa8e64d60ae4bd0c5b3477d91.png) </span>


* Internal catalog: The internal data directory used to manage all internal data in StarRocks. For example, databases and tables created by executing `CREATE DATABASE` and `CREATE TABLE` statements are managed by the internal catalog. Each StarRocks cluster has one and only one internal catalog named [default_catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/default_catalog).

* External catalog: The external data directory used to connect to external metastore. In StarRocks, you can directly query external data through the external catalog without importing or migrating data.

   When querying data using the external catalog, StarRocks uses two components of the external data source:

   * Metadata service: Used to expose metadata for StarRocks FE to plan queries.

   * Storage system: Used to store data. Data files are stored in various formats in distributed file systems or object storage systems. After FE distributes the generated query plan to each BE, each BE scans the target data in the Hive storage system in parallel, performs computation, and returns the query results.


<span id="_3-访问-catalog"></span>
## 3 access catalog

You can use [SET CATALOG](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/SET_CATALOG) to switch the Catalog effective in the current session, and then query data through that Catalog.

<span id="_4-查询数据"></span>
## 4 query data

<span id="_4-1-查询内部数据"></span>
### 4.1 query internal data

To query data saved in StarRocks, see [Default catalog](https://docs.starrocks.io/zh/docs/data_source/catalog/default_catalog).

<span id="_4-2-查询外部数据"></span>
### 4.2 query external data

To query data saved in external data sources, see [Querying external data](https://docs.starrocks.io/zh/docs/data_source/catalog/query_external_data).

<span id="_4-3-跨-catalog-查询数据"></span>
### 4.3 query data across catalogs

To query data from another catalog within a catalog, reference the target data using the format `catalog_name.db_name` or `catalog_name.db_name.table_name`. Examples:


* Under `default_catalog.olap_db`, query `hive_table` in `hive_catalog`.

   ```plain
   SELECT * FROM hive_catalog.hive_db.hive_table;
   ```
   

* Under `hive_catalog.hive_db`, query `olap_table` in `default_catalog`.

   ```sql
   SELECT * FROM default_catalog.olap_db.olap_table;
   ```
   

* Under `hive_catalog.hive_db`, perform a federated query on `hive_table` and `olap_table` in `default_catalog`.

   ```sql
   SELECT * FROM hive_table h JOIN default_catalog.olap_db.olap_table o WHERE h.id = o.id;
   ```
   

* In other catalogs, perform a federated query on `hive_table` in `hive_catalog` and `olap_table` in `default_catalog`.

   ```sql
   SELECT * FROM hive_catalog.hive_db.hive_table h JOIN default_catalog.olap_db.olap_table o WHERE h.id = o.id;
   ```
