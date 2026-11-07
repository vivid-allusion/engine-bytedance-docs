---
title: "Operate Iceberg tables in TOS (applicable to EMR 2.x versions)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/operate_iceberg_tables_in_tos_emr_2x"
---

The data of Iceberg tables can be stored in Volcano Engine Object Storage Service (TOS). This section provides examples of creating Iceberg tables in TOS using different engine components.

<span id="_1-spark-组件操作示例"></span>
## 1 Spark component operation example

<span id="_1-1-使用前提"></span>
### 1.1 Prerequisites


1. An E\-MapReduce (EMR) cluster containing the Iceberg and Spark components has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).


<span id="_1-2-操作步骤"></span>
### 1.2 Procedure

The procedure is similar to [Basic usage of Iceberg (applicable to EMR 2.x versions)](https://docs.byteplus.com/docs/E-MapReduce/109274). When creating the table with CreateTable, specify the location information:

```sql
import org.apache.iceberg.hive.HiveCatalog;
val catalog = new HiveCatalog()
catalog.setConf(spark.sparkContext.hadoopConfiguration)
val properties = new util.HashMap[String, String]
properties.put("warehouse", "/user/hive/warehouse/iceberg/hive")
properties.put("uri", "thrift://emr-master-1-1:9083")
catalog.initialize("hive", properties)
catalog.createTable(name, schema, spec, ${tos地址}, properties); --Create Iceberg table
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the example, <code>{TOS address}</code> needs to be modified according to the actual situation. You can refer to the following example: tos://ceshi/autotest/iceberg/hive</div>


<span id="_2-trino-presto-组件操作示例"></span>
## 2 Trino/Presto component operation example

In EMR 2.X cluster versions, the steps for operating Iceberg tables with Presto/Trino are the same as those in EMR 3.X cluster versions. For operation examples, see [Operate Iceberg tables in TOS](https://docs.byteplus.com/docs/E-MapReduce/109283).
