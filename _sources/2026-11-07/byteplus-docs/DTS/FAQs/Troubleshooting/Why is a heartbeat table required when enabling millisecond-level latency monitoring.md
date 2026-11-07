---
title: "Why is a heartbeat table required when enabling millisecond-level latency monitoring"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring"
---

After creating a data synchronization or data subscription task and enabling the millisecond\-level latency monitoring feature, the pre\-check may fail—and thus prevent task creation—due to issues such as the source database account not existing, the heartbeat database not existing, or the heartbeat table not existing. This article describes solutions for cases where the pre\-check fails when enabling millisecond\-level latency monitoring.

<span id="TSOLNtUQ"></span>
## Background

Since Database Transmission Service (DTS) cannot directly measure end\-to\-end latency across the entire data transmission pipeline, it must rely on precise time anchors to quantify delay. The heartbeat table serves as the only reliable source of these accurate time anchors; therefore, a heartbeat table is required when enabling millisecond\-level latency monitoring for database transmission.

<span id="O21OKwRV"></span>
### Precautions

Millisecond\-level latency monitoring is currently supported only when creating the following types of data transmission tasks:


* Synchronization: MySQL synchronization to MySQL, MongoDB synchronization to MongoDB

* Subscription: PostgreSQL subscription to Kafka, PostgreSQL subscription to RocketMQ, AIDAP subscription to RocketMQ


<span id="vjkyZEZP"></span>
## Solutions

<span id="bvAQZnQF"></span>
### Error type one: Insufficient privileges


<Tabs>
<Tab zoneid="ovbYtapHZ6" title="MySQL database type">
<TabTitle>MySQL database type</TabTitle>

1. Grant the Source database account permission to create databases and tables (recommended SELECT, INSERT, and UPDATE privileges). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql?lang=en). Confirm whether the heartbeat database _volc_dts and the heartbeat table exist in the source end instance.

3. Execute the following command to check if the heartbeat database _volc_dts exists.

   ```SQL
   SHOW DATABASES LIKE '_volc_dts';
   ```
   

   * If the heartbeat database exists, verify whether the heartbeat table exists.

      1. Execute the following command to query whether the heartbeat table exists.

      ```SQL
      USE _volc_dts;
      SHOW TABLES LIKE 'heartbeat';
      ```
      

      2. If the heartbeat table does not exist, execute the following command to create it.

      ```SQL
      CREATE TABLE IF NOT EXISTS heartbeat (
          id VARCHAR(64) NOT NULL COMMENT '固定心跳标识，主键',
          ts DATETIME(3) NOT NULL COMMENT '毫秒级时间戳（DATETIME(3)保留3位毫秒）',
          status TINYINT NOT NULL DEFAULT 1 COMMENT '心跳状态：1=正常，0=异常',
          PRIMARY KEY (id) USING BTREE
      ) ENGINE=InnoDB 
      COMMENT='E2E毫秒级延迟监控心跳表（Volc DTS专用）';
      ```
      

      3. Execute the following command to insert a fixed\-identifier heartbeat record and initialize the heartbeat table for the first time.

&nbsp;

      ```SQL
      REPLACE INTO heartbeat (id, ts) VALUES ('heartbeat', NOW(3));
      ```
      

   * If the heartbeat database does not exist, create the heartbeat database and heartbeat table.

      1. Execute the following command to create the heartbeat database.

      ```SQL
      CREATE DATABASE IF NOT EXISTS _volc_dts  
      COMMENT 'E2E毫秒级延迟监控心跳库';
      ```
      

      2. Execute the following command to switch to the heartbeat database.

      ```SQL
      USE _volc_dts;
      ```
      

      3. Execute the following command to create the heartbeat table.

      ```SQL
      CREATE TABLE IF NOT EXISTS heartbeat (
          id VARCHAR(64) NOT NULL COMMENT '固定心跳标识，主键',
          ts DATETIME(3) NOT NULL COMMENT '毫秒级时间戳（DATETIME(3)保留3位毫秒）',
          status TINYINT NOT NULL DEFAULT 1 COMMENT '心跳状态：1=正常，0=异常',
          PRIMARY KEY (id) USING BTREE
      ) ENGINE=InnoDB 
      COMMENT='E2E毫秒级延迟监控心跳表（Volc DTS专用）';
      ```
      

      4. Execute the following command to insert a fixed\-identifier heartbeat record and initialize the heartbeat table for the first time.

      ```SQL
      REPLACE INTO heartbeat (id, ts) VALUES ('heartbeat', NOW(3));
      ```
      




</Tab>
<Tab zoneid="zJOdIISdD5" title="PostgreSQL database type">
<TabTitle>PostgreSQL database type</TabTitle>

1. Grant the Source database account permission to create databases and tables (recommended SELECT, INSERT, and UPDATE privileges). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_account_permissions?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG?lang=en). Confirm whether the heartbeat schema _volc_dts and the heartbeat table heartbeat exist in the source end instance.

3. Execute the following command to confirm whether the heartbeat schema exists.

   ```SQL
   SELECT EXISTS (
     SELECT 1
     FROM pg_namespace
     WHERE nspname = '_volc_dts'
   ) AS schema_exists;
   ```
   

   * If the heartbeat database exists, verify whether the heartbeat table exists.

      1. Execute the following command to query whether the heartbeat table exists.

      ```SQL
      SELECT tablename  
      FROM pg_tables  WHERE schemaname = '_volc_dts' AND tablename = 'heartbeat';
      ```
      

      2. If the heartbeat table does not exist, execute the following command to create the heartbeat table.

      ```SQL
      CREATE TABLE IF NOT EXISTS _volc_dts.heartbeat (
          id int PRIMARY KEY,
          heartbeat_ts bigint NOT NULL
      );
      ```
      



&nbsp;

   * If the heartbeat schema does not exist, create the heartbeat schema and heartbeat table.

      1. If the heartbeat database does not exist in the source end instance, execute the following command to create the heartbeat schema.

         ```SQL
         CREATE SCHEMA IF NOT EXISTS _volc_dts;
         ```
         

      2. Execute the following command to create the heartbeat table.

         ```SQL
         CREATE TABLE IF NOT EXISTS _volc_dts.heartbeat (
             id int PRIMARY KEY,
             heartbeat_ts bigint NOT NULL
         );
         ```
         




</Tab>
<Tab zoneid="SZt4EqZSSx" title="MongoDB database type">
<TabTitle>MongoDB database type</TabTitle>

1. Grant the source database account permissions to create databases and tables (a superuser account or a role with readWriteAnyDatabase privileges is recommended). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb?lang=en). Verify whether the heartbeat database _volc_dts and the heartbeat collection heartbeat exist in the source instance.

3. Execute the following command to confirm whether the heartbeat database exists.

   ```SQL
   show dbs;  
   ```
   

   * If the heartbeat database exists, confirm whether the heartbeat collection exists.

      1. Execute the following command to check if the heartbeat collection exists.

      ```SQL
      use _volc_dts;
      show collections;
      show collections like "heartbeat";
      ```
      

      2. If the heartbeat collection does not exist, execute the following command to create it.

      ```JavaScript
      // create heartbeat collection
      db.createCollection("heartbeat")
      ```
      

   * If the heartbeat database does not exist, create both the heartbeat database and collection.

      1. If the heartbeat database does not exist in the source end instance, execute the following command to switch to it.

      ```SQL
      use _volc_dts; // 仅逻辑切换，写入数据后库才会实际创建
      ```
      

      2. Execute the following command to create the heartbeat collection.

      ```JavaScript
      // create heartbeat collection
      db.createCollection("heartbeat")
      ```
      




</Tab>
</Tabs>


<span id="BVEIAy7B"></span>
### Error type two: No heartbeat database


<Tabs>
<Tab zoneid="tM1WbAUJF6" title="MySQL database type">
<TabTitle>MySQL database type</TabTitle>

1. Grant the Source database account permission to create databases and tables (recommended SELECT, INSERT, and UPDATE privileges). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql?lang=en).

3. Execute the following command to create the heartbeat database.

   ```SQL
   CREATE DATABASE IF NOT EXISTS _volc_dts  
   COMMENT 'E2E毫秒级延迟监控心跳库';
   ```
   

4. Execute the following command to switch to the heartbeat database.

   ```SQL
   USE _volc_dts;
   ```
   

5. Execute the following command to create the heartbeat table.

   ```SQL
   CREATE TABLE IF NOT EXISTS heartbeat (
       id VARCHAR(64) NOT NULL COMMENT '固定心跳标识，主键',
       ts DATETIME(3) NOT NULL COMMENT '毫秒级时间戳（DATETIME(3)保留3位毫秒）',
       status TINYINT NOT NULL DEFAULT 1 COMMENT '心跳状态：1=正常，0=异常',
       PRIMARY KEY (id) USING BTREE
   ) ENGINE=InnoDB 
   COMMENT='E2E毫秒级延迟监控心跳表（Volc DTS专用）';
   ```
   

6. Execute the following command to insert a fixed\-identifier heartbeat record and initialize the heartbeat table for the first time.

   ```SQL
   REPLACE INTO heartbeat (id ts) VALUES ('heartbeat', NOW(3));
   ```
   




</Tab>
<Tab zoneid="HqF6ALjN9R" title="PostgreSQL database type">
<TabTitle>PostgreSQL database type</TabTitle>

1. Grant the Source database account permission to create databases and tables (recommended SELECT, INSERT, and UPDATE privileges). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_account_permissions?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG?lang=en).

3. Execute the following command to create the heartbeat schema.


```SQL
CREATE SCHEMA IF NOT EXISTS _volc_dts;
```



4. Execute the following command to switch to the heartbeat Schema.


```SQL
\c _volc_dts;
```



5. Execute the following command to create the heartbeat table.


```SQL
CREATE TABLE IF NOT EXISTS _volc_dts.heartbeat (
    id int PRIMARY KEY,
    heartbeat_ts bigint NOT NULL
);
```



</Tab>
<Tab zoneid="gvzzfXHagd" title="MongoDB database type">
<TabTitle>MongoDB database type</TabTitle>

1. Grant the source database account permissions to create databases and tables (a superuser account or a role with readWriteAnyDatabase privileges is recommended). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb?lang=en).

3. Execute the following command to switch to the heartbeat database.


```SQL
use _volc_dts;  // 仅逻辑切换，创建表才会实际创建
```



4. Execute the following command to create the heartbeat collection.


```JavaScript
// create heartbeat collection
db.createCollection("heartbeat")
```



</Tab>
</Tabs>


<span id="puhZAri3"></span>
### Error type three: No heartbeat collection


<Tabs>
<Tab zoneid="m6qtLr7jqf" title="MySQL database type">
<TabTitle>MySQL database type</TabTitle>

1. Grant the source database account permission to create databases and tables (SELECT, INSERT, and UPDATE permissions are recommended). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql?lang=en).

3. Execute the following command to switch to the heartbeat database.


```SQL
USE _volc_dts;
```



4. Execute the following command to create the heartbeat table.


```SQL
CREATE TABLE IF NOT EXISTS heartbeat (
    id VARCHAR(64) NOT NULL COMMENT '固定心跳标识，主键',
    ts DATETIME(3) NOT NULL COMMENT '毫秒级时间戳（DATETIME(3)保留3位毫秒）',
    status TINYINT NOT NULL DEFAULT 1 COMMENT '心跳状态：1=正常，0=异常',
    PRIMARY KEY (id) USING BTREE
) ENGINE=InnoDB 
COMMENT='E2E毫秒级延迟监控心跳表（Volc DTS专用）';
```



5. Execute the following command to insert a fixed\-identifier heartbeat record and initialize the heartbeat table for the first time.


```SQL
REPLACE INTO heartbeat (id, ts) VALUES ('heartbeat', NOW(3));
```



</Tab>
<Tab zoneid="LnDlr4lLnk" title="PostgreSQL database type">
<TabTitle>PostgreSQL database type</TabTitle>

1. Grant the Source database account permission to create tables (recommended SELECT, INSERT, and UPDATE privileges). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_account_permissions?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG?lang=en).

3. Execute the following command to switch to the heartbeat Schema.


```SQL
\c _volc_dts;
```



4. Execute the following command to create the heartbeat table.


```SQL
CREATE TABLE IF NOT EXISTS _volc_dts.heartbeat (
    id int PRIMARY KEY,
    heartbeat_ts bigint NOT NULL
);
```





</Tab>
<Tab zoneid="g2cDE4jori" title="MongoDB database type">
<TabTitle>MongoDB database type</TabTitle>

1. Grant the source database account permission to create tables (super administrator account or readWriteAnyDatabase role is recommended). For authorization of the Source end account, refer to [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges?lang=en).

2. Connect to the source instance. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb?lang=en).

3. Execute the following command to switch to the heartbeat database.


```SQL
use _volc_dts;  
```



4. Execute the following command to create the heartbeat collection.


```JavaScript
// create heartbeat collection
db.createCollection("heartbeat")
```



</Tab>
</Tabs>


<span id="XGRck8Vr"></span>
### Error type four: Read only related errors


<Tabs>
<Tab zoneid="oJ9Vu2reGe" title="MySQL database type">
<TabTitle>MySQL database type</TabTitle>

You may encounter the following two types of Ready only related error prompts as shown below:


* Error type one: `read_only = ON` and the account lacks high privileges

   * Error prompt: The system variable `read_only = ON` in the [source/target] database, and the user lacks the `SUPER` and `CONNECTION_ADMIN` privileges, so it cannot be updated.

   * Cause: The instance has enabled global read\-only mode, and the ordinary account does not have permission to modify data.

   * Solution: Connect to the source end instance using an advanced super account or disable the instance's global read\-only mode. For detailed operations, refer to [Disable global read-only](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_global_read-only?lang=en).

* Error type two: Other read\-only variables are ON

   * Error prompt: The system variable  `[super_read_only/innodb_read_only/transaction_read_only/tx_read_only] = ON` in the [source/target] database and cannot be updated.

   * Reason: The instance enters read\-only mode due to operation and maintenance protection, storage abnormalities, or session settings.

   * Solution:

      * If it is `super_read_only` or `read_only`: Use a super account to close read\-only mode. For detailed operations, refer to [Disable global read-only](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_global_read-only?lang=en).

      * If it is `innodb_read_only`: Check disk permissions or instance state; usually, instance restart is required. For more details, refer to [Restarting instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance?lang=en).

      * If it is a session\-level variable (such as `transaction_read_only`): Rebuild the connection instance.


</Tab>
<Tab zoneid="QYC4klO8Q6" title="PostgreSQL database type">
<TabTitle>PostgreSQL database type</TabTitle>

* Error prompt: The system variable`default_transaction_read_only = ON` in the [source/target] database and cannot be updated.

* Cause: The instance has enabled global read\-only mode.

* Solution: Disable the instance's global read\-only mode. For detailed operation, refer to [Disable global read-only](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_global_read-only?lang=en).


</Tab>
</Tabs>
