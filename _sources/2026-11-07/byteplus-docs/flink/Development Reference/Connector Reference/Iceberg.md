---
title: "Iceberg"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Iceberg"
---

In the Flink console, you can create Iceberg tables under metadata management. After completing the creation and configuration of Iceberg metadata tables, you can directly read and write data in SQL code without needing additional DDL statements.

<span id="dfad942e"></span>
## Prerequisites

You have completed the creation and configuration of the Iceberg metadata table.

<span id="40964187"></span>
## Reading Data

After the configuration of the metadata table is complete, you can directly retrieve data from the metadata table in the SQL task code editing area, without needing to declare it.

```SQL
INSERT INTO ${other_sink_table}
SELECT ...
FROM iceberg.${DBname}.${Tablename}
```



* iceberg: In Flink, the naming of tables follows a three\-part format: Catalog.Database.Table. When using Iceberg tables, you need to add the `iceberg` prefix.

* DBname: Database name.

* Tablename: Metadata table name.


<span id="a61a4ea9"></span>
## Write Data

After configuring the metadata table, you can directly write data into the table in the SQL task code editing area.

```SQL
INSERT INTO iceberg.${DBname}.${hive_Tablename}
SELECT ... 
FROM ${other_source_table}
```



* Iceberg: In Flink, table naming follows a three\-part format: Catalog.Database.Table. When using Iceberg tables, you need to add an `iceberg` prefix.

* DBname: Database name.

* Tablename: Metadata table name.
