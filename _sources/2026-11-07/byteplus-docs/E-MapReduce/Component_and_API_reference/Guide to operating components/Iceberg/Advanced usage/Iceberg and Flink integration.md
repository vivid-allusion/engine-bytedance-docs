---
title: "Iceberg and Flink integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Iceberg_and_Flink_integration"
---

[Apache Flink](https://flink.apache.org/) is a distributed open\-source computing framework that supports both stream processing and batch processing application types. This document describes how to operate Iceberg tables in Flink.

<span id="_1-前提条件"></span>
# 1 Prerequisites


1. Versions of E\-MapReduce (EMR) after 1.4.0 (including 1.4.0) support operating Iceberg tables in Flink.

2. Versions of EMR after 2.1.0 (including 2.1.0) support operating Iceberg tables in Flink.

3. An EMR cluster has been created with the Iceberg component and Flink component installed. There are two ways to install the Iceberg and Flink components:

   1. When creating an EMR cluster, select Iceberg and Flink as optional components. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an existing EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg and Flink services.


<span id="_2-操作步骤"></span>
# 2 Procedure

This document describes how to operate Iceberg tables using Flink SQL. To access Apache Iceberg tables using the Flink DataStream API, refer to the [Iceberg official website](https://iceberg.apache.org/docs/latest/flink/) for instructions.

<span id="_2-1-准备工作"></span>
### 2.1 Preparation


1. Configure Flink's checkpoint

   Currently, Flink submits Iceberg information at each checkpoint, so you need to configure Flink's checkpoint.

   1. On the **Cluster Management \> Cluster List \> Specific Cluster Name** page, go to the cluster details.

   2. In the navigation bar, click **Service List**, then click the **Iceberg** service to access it.

   3. Click the ECS ID of the EMR cluster node to go to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.

   4. Under the checkpoint parameter in the /usr/lib/emr/current/flink/conf/flink\-conf.yaml file, add the following configuration:

   ```yaml
   execution.checkpointing.interval: 10s   # Checkpoint interval
   execution.checkpointing.tolerable-failed-checkpoints: 10  # Checkpoint failure tolerance count
   ```
   

2. After completing the YAML file configuration, use the following command to start the Flink SQL Client:


```bash
export HADOOP_CLASSPATH=`hadoop classpath`


cd /usr/lib/emr/current/flink

# Copy dependencies required by Iceberg
cp /usr/lib/emr/current/iceberg/lib/iceberg-flink-runtime-*.jar  lib
cp /usr/lib/emr/current/flink/connectors/flink-sql-connector-hive-*.jar lib

# Use Flink on YARN mode to start the YARN session
./bin/yarn-session.sh --detached


# Start the flink SQL client
./bin/sql-client.sh embedded shell
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The version numbers of Flink and Iceberg may differ across different EMR versions. It is recommended to use the following commands to locate the paths of your iceberg\-flink\-runtime\-xx.xx.xx.jar and flink\-sql\-connector\-hive\-xx.xx.xx.jar files.</div>


<div data-tips="true" data-tips-type="tip">For EMR 3.x versions, use the following commands:</div>


<div data-tips="true" data-tips-type="tip">$ ls /usr/lib/emr/current/iceberg/lib/iceberg\-flink\-runtime\-<em>.jar</em></div>


<div data-tips="true" data-tips-type="tip"><em>/usr/lib/emr/current/flink/connectors/flink\-sql\-connector\-hive\-3</em>.jar</div>


<div data-tips="true" data-tips-type="tip">For EMR 2.x versions, use the following commands:</div>


<div data-tips="true" data-tips-type="tip">$ ls /usr/lib/emr/current/iceberg/lib/iceberg\-flink\-runtime\-<em>.jar</em></div>


<div data-tips="true" data-tips-type="tip"><em>/usr/lib/emr/current/flink/connectors/flink\-sql\-connector\-hive\-2.3.6</em>.jar</div>



3. Create a catalog

   ```plain
   CREATE CATALOG <catalog_name> WITH (
     'type'='iceberg',
     '<config_key>'='<config_value>'
    );
   ```
   

   Currently, Iceberg mainly supports HiveCatalog and HadoopCatalog.

   * HiveCatalog stores the metadata file path of the current table in Hive Metastore, so each time you read or write an Iceberg table, you must first retrieve the corresponding table metadata file path from Hive Metastore.

   * HadoopCatalog records the metadata file path of the current table in a file directory, so there is no need to connect to Hive Metastore.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The domain naming conventions for nodes may differ across EMR versions, so the "emr\-master\-1" in the example below can be adjusted according to your EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.   </div>
   

   **Example**: Create HiveCatalog

   ```sql
   CREATE CATALOG iceberg WITH (
     'type'='iceberg',
     'catalog-type'='hive',
     'uri'='thrift://emr-master-1:9083',
     'clients'='5',
     'property-version'='1',
     'warehouse'='hdfs://emr-cluster/warehouse/tablespace/managed/hive'
     );
   ```
   

   **Example**: Create HadoopCatalog

   ```sql
   CREATE CATALOG hadoop_catalog WITH (
     'type'='iceberg',
     'catalog-type'='hadoop',
     'warehouse'='hdfs://emr-cluster/warehouse/tablespace/managed/hive',
     'property-version'='1'
   );
   ```
   

   Check the result using Flink SQL Client:

   ```sql
   Flink SQL> SHOW CATALOGS;
   +-----------------+
   |    catalog name |
   +-----------------+
   | default_catalog |
   |  hadoop_catalog |
   |         iceberg |
   +-----------------+
   3 rows in set
   ```
   


<span id="_2-2-sql命令"></span>
### 2.2 SQL commands

For more SQL commands, see the [Iceberg and Flink integration](https://docs.byteplus.com/docs/E-MapReduce/109281) official documentation.


1. Create a database

   ```sql
   USE CATALOG iceberg;
   CREATE DATABASE iceberg_db;
   USE iceberg_db;
   ```
   

2. Create a table

   ```sql
   CREATE TABLE iceberg.iceberg_db.iceberg_001 (
       id BIGINT COMMENT 'unique id',
       data STRING
   ) WITH (
       'write.format.default'='ORC'
    );
   ```
   

3. Query

   You can execute the following commands to set the execution type to stream processing mode or batch processing mode.

   ```Plain
   --提交 flink批处理作业来获取iceberg表中的所有行
   SET execution.runtime-mode = batch;
   SELECT * FROM iceberg.iceberg_db.iceberg_001 limit 10;
   ```
   

   ```Plain
   --从flink流作业中增量获取数据
   SET execution.runtime-mode = streaming;
   SELECT * FROM iceberg.iceberg_db.iceberg_001 limit 10;
   ```
   

4. Write

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">INSERT OVERWRITE is only suitable for batch jobs. Set the batch job execution mode using the following command:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SET execution.runtime\-mode = batch;   </div>
   

   ```sql
   INSERT INTO iceberg.iceberg_db.iceberg_001 VALUES (1, 'a');
   ```
   

   You can also use INSERT OVERWRITE to replace the data in the table with the query results:

   ```sql
   INSERT OVERWRITE iceberg.iceberg_db.iceberg_001 VALUES (1, 'a');
   ```
   

5. Delete a table

   ```sql
   DROP TABLE iceberg.iceberg_db.iceberg_001;
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deleting a table will also delete the table's data. However, the empty directory information of the table will be retained, for example:<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1af8535a483c3f04b72fb551145e8e5.png" width="2149px" />   </div>
