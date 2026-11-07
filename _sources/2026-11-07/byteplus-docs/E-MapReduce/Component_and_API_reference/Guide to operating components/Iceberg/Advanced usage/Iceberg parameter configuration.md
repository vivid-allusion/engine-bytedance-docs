---
title: "Iceberg parameter configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Iceberg_parameter_configuration"
---

This article introduces the necessary configurations for Iceberg tables to use data lake metadata.

<span id="_1-spark-配置"></span>
## Spark configuration

Spark supports the catalog types Hive and Hadoop. For additional information about catalog parameter configuration, refer to [官网](https://docs.byteplus.com/docs/E-MapReduce/109285#catalog-properties).

<span id="_1-1-catalog-type-为-hive"></span>
### Catalog type: hive


|**Parameter** |**Parameter value** |**Description** |
|---|---|---|
|spark.sql.catalog..type |`iceberg` |Underlying Iceberg catalog implementation type, `HiveCatalog`, or `HadoopCatalog`. If not configured, a custom catalog is used. |
|spark.sql.extensions |`org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions` |Spark SQL extension module. Fixed value. |
|spark.sql.catalog. |`org.apache.iceberg.spark.SparkCatalog` |Catalog name. Fixed value.<br><br>Additionally, to view both non\-Iceberg tables and Iceberg tables under the same database, configure this parameter as: `org.apache.iceberg.spark.SparkSessionCatalog` |
|spark.sql.catalog..uri |thrift://master\-1\-1:9083 |Metastore address. Check the value of the `hive.metastore.uris` parameter in the Hive component configuration file hive\-site. |
|spark.sql.catalog..warehouse |hdfs://master\-1\-1:8020/warehouse/path |Warehouse address. Check the value of the `hive.metastore.warehouse.dir` parameter in the Hive component configuration file hive\-site, or customize the path. TOS paths are also supported. |


<span id="_1-1-1-示例："></span>
#### **Example:** 

```java
spark.sql.catalog.hive_prod = org.apache.iceberg.spark.SparkCatalog
spark.sql.catalog.hive_prod.type = hive
spark.sql.catalog.hive_prod.uri = thrift://master-1-1:9083
# omit uri to use the same URI as Spark: hive.metastore.uris in hive-site.xml
```


<span id="_1-2-catalog-type-为-hadoop"></span>
### Catalog type: hadoop


|**Parameter** |**Parameter value** |**Description** |
|---|---|---|
|spark.sql.catalog..type |`hadoop` |Underlying Iceberg catalog implementation type, `HiveCatalog`, or `HadoopCatalog`. If not configured, a custom catalog is used. |
|spark.sql.extensions |`org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions` |Spark SQL extension module. Fixed value. |
|spark.sql.catalog. |`org.apache.iceberg.spark.SparkCatalog` |Catalog name. Fixed value.<br><br>Additionally, to view both non\-Iceberg tables and Iceberg tables under the same database, configure this parameter as: `org.apache.iceberg.spark.SparkSessionCatalog` |
|spark.sql.catalog..warehouse |hdfs://master\-1\-1:8020/warehouse/path |Warehouse address. HDFS storage or TOS storage can be used. |


<span id="_1-2-1-示例："></span>
#### Example:

```java
spark.sql.catalog.hadoop_prod = org.apache.iceberg.spark.SparkCatalog
spark.sql.catalog.hadoop_prod.type = hadoop
spark.sql.catalog.hadoop_prod.warehouse = hdfs://master-1-1:8020/warehouse/path
```


<span id="_1-3-catalog-type-为空"></span>
### Catalog type: none


|**Parameter** |**Parameter value** |**Description** |
|---|---|---|
|spark.sql.catalog..catalog\-impl | |Underlying Iceberg catalog implementation type. When spark.sql.catalog..type is none, this parameter must be configured. |


<span id="_2-hive-配置"></span>
## Hive configuration

Hive supports the following Iceberg catalog types: Hive, Hadoop, or none. The configuration items vary depending on the type:

<span id="_2-1-catalog-type-为-hive"></span>
### Catalog type: Hive


|**Parameter** |**Note** |
|---|---|
|iceberg.catalog.<catalog_name\>.type |Set to Hive |
|iceberg.catalog.<catalog_name\>.uri |Metastore address. Check the value of the `hive.metastore.uris` parameter in the Hive component configuration file hive\-site. |
|iceberg.catalog.<catalog_name\>.clients |Number of client pool instances |


<span id="_2-1-1-示例："></span>
#### Example:

```java
SET iceberg.catalog.another_hive.type=hive;
SET iceberg.catalog.another_hive.uri=thrift://master-1-1:9083;
```


<span id="_2-2-catalog-type-为-hadoop"></span>
### Catalog type: hadoop


|**Parameter** |**Note** |
|---|---|
|iceberg.catalog.<catalog_name\>.type |Set to hadoop |
|iceberg.catalog.iceberg.clients |Number of client pool instances |
|iceberg.catalog.iceberg.warehouse |Warehouse address |


<span id="_2-2-1-示例："></span>
#### Example:

```java
SET iceberg.catalog.hadoop.type=hadoop;
SET iceberg.catalog.hadoop.warehouse=hdfs://master-1-1:8020/warehouse;
```


<span id="_2-3-catalog-type-为空"></span>
### Catalog type: none


|**Parameter** |**Note** |
|---|---|
|iceberg.catalog.<catalog_name\>.catalog\-impl |Catalog implementation. When catalog type is none, this must be configured. |
