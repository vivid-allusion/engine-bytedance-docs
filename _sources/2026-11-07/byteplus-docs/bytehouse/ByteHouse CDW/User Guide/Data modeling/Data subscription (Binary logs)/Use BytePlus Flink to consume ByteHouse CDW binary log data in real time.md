---
title: "Use BytePlus Flink to consume ByteHouse CDW binary log data in real time"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/flink-consume-bytehouse-cdw-binary-logs-in-real-time"
---

This tutorial introduces how to use BytePlus Flink to consume ByteHouse Cloud Data Warehouse (CDW) binary logs (binlog) in real time.

<span id="a2d7d479"></span>
# Prerequisites


* Before use, please refer to [Subscribe to ByteHouse CDW binary logs](https://docs.byteplus.com/docs/bytehouse/subscribe-to-bytehouse-cdw-binary-logs) for an overview of ByteHouse CDW binlog feature. Then, enable and configure ByteHouse CDW binlog as needed.

* To consume ByteHouse CDW binlog with Flink, you need read permissions on the target table and system tables. Please ensure that you have the required permissions. Please refer to [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission) for ByteHouse CDW privilege configuration.

* Please ensure that the ByteHouse CDW engine version you are using is v2.3.1 or above. You can log in to the ByteHouse console, click the top **Tenant management** tab, and then in **Basic information**, check whether the engine version you are using meets the requirements. Enabling the binlog feature on engine versions earlier than this will result in an error. To upgrade, please submit a ticket.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dee99a81dd224aca9ce2f8afa5e601a8~tplv-goo7wpa0wc-image.image) </span>


<span id="c1b7b967"></span>
# Usage restrictions


* This feature is in Beta. Before using it, please submit a support ticket or contact the ByteHouse team to obtain whitelist access.

* Currently, only [BytePlus Flink](https://www.byteplus.com/en/product/flink) supports consuming ByteHouse CDW binlog.

* Currently, only table\-level incremental binlog consumption is supported.


<span id="077367de"></span>
# Use Flink to consume binlog in real\-time

BytePlus Flink supports consuming binlogs in real time through the Flink Connector Driver for ByteHouse CDW. The specific usage is as follows.

<span id="cbe01c14"></span>
## Preparations


1. The current version of the ByteHouse connector built into BytePlus Flink does not support Binlog. Please use the provided connector by adding the dependency file. For detailed operations, please refer to [Maven dependencies](https://docs.byteplus.com/docs/bytehouse/Flink_Connector#019c29b0).

   
   |**Flink Version** |**Connector** |
   |---|---|
   |1.16 |[flink-sql-connector-bytehouse-cdw_2.12-1.28.17-1.16.jar](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.28.17-1.16/flink-sql-connector-bytehouse-cdw_2.12-1.28.17-1.16.jar) |
   |1.17 |[flink-sql-connector-bytehouse-cdw_2.12-1.28.17-1.17.jar](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.28.17-1.17/flink-sql-connector-bytehouse-cdw_2.12-1.28.17-1.17.jar) |
   

2. To consume ByteHouse CDW binlog with Flink, you need to connect to ByteHouse CDW. Currently, connections are supported through either IAM users or database users. You can obtain connection information in advance, such as the network domain name, port, API Key, database user, and password. For more information, see [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity). The differences between IAM users and database users are explained as follows. You can choose as needed.

   * **IAM user** is a user created in BytePlus Identity and Access Management (IAM), whose privileges are determined by IAM policies and the ByteHouse resource and data permissions you grant. IAM users can access ByteHouse through the console, CLI, connection drivers, ecosystem tools, APIs, and other methods.

   * **Database user** is a user created at the database level in ByteHouse, and can be granted permissions for environment, resources, and data. Database users cannot access the ByteHouse console, but can access ByteHouse through the CLI, connection drivers, ecosystem tools, API, and other methods.

      For more information about IAM users and database users, see the following documents:

   * [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

   * [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

   * [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="054fef0f"></span>
## Consume via Flink SQL

The source side automatically assigns the correct Flink RowKind type to each row of data based on the operation type, including INSERT, DELETE, UPDATE_BEFORE, and UPDATE_AFTER, to achieve data mirroring in synchronized tables, similar to the Change Data Capture (CDC) functionality in MySQL and Postgres.

After binlog is enabled for ByteHouse CDW tables, you can use the following DDL in Flink to configure the source table and consume binlog in real time. When connecting, you can use either a ByteHouse IAM user or a database user.


<Tabs>
<Tab zoneid="bLp7anmnjx" title="Use IAM users">
<TabTitle>Use IAM users</TabTitle>

```SQL
CREATE TABLE bh_binlog_source (
  `id` INT,
  `a` BIGINT,
  `b` STRING,
  PRIMARY KEY (`id`) NOT ENFORCED
) WITH (
  'connector' = 'bytehouse-cdw',
  'binlog' = 'true',
  'jdbc.enable-gateway-connection' = 'true',
  'bytehouse.gateway.region' = 'VOLCANO_PRIVATE',
  'bytehouse.gateway.host' = '<your_bytehouse_cdw_host>',
  'bytehouse.gateway.api-token' = '<your_bytehouse_cdw_api_key>',
  'bytehouse.gateway.virtual-warehouse' = '<your_bytehouse_cdw_vw_id>',
  'database' = '<your_database_name>',
  'table-name' = '<your_table_name>',
  'scan.startup.mode' = 'earliest',
  'scan.max-split-size' = '5000',
  'scan.cdc.shard.split' = 'true'
); 
CREATE TEMPORARY TABLE print_sink WITH (
  'connector' = 'print'
) LIKE bh_binlog_source (EXCLUDING OPTIONS);
INSERT INTO print_sink SELECT * FROM bh_binlog_source;
```



</Tab>
<Tab zoneid="TMFjwMgiMC" title="Use database users">
<TabTitle>Use database users</TabTitle>

```SQL
CREATE TABLE bh_binlog_source (
  `id` INT,
  `a` BIGINT,
  `b` STRING,
  PRIMARY KEY (`id`) NOT ENFORCED
) WITH (
  'connector' = 'bytehouse-cdw',
  'binlog' = 'true',
  'jdbc.enable-gateway-connection' = 'true',
  'bytehouse.gateway.region' = 'VOLCANO_PRIVATE',
  'bytehouse.gateway.host' = '<your_bytehouse_cdw_host>',
  'bytehouse.gateway.account' = '<your_volcano_engine_ID>',
  'bytehouse.gateway.username' = '<your_bytehouse_cdw_database_user>',
  'bytehouse.gateway.paasword' = '<your_bytehouse_cdw_database_user_password>',
  'bytehouse.gateway.virtual-warehouse' = '<your_bytehouse_cdw_vw_id>',
  'database' = '<your_database_name>',
  'table-name' = '<your_table_name>',
  'scan.startup.mode' = 'earliest',
  'scan.max-split-size' = '5000',
  'scan.cdc.shard.split' = 'true'
); 
CREATE TEMPORARY TABLE print_sink WITH (
  'connector' = 'print'
) LIKE bh_binlog_source (EXCLUDING OPTIONS);
INSERT INTO print_sink SELECT * FROM bh_binlog_source;
```



</Tab>
</Tabs>


<span id="7180958d"></span>
### **Parameter descriptions**


|**Parameters** |**Required** |**Default value** |**Note** |
|---|---|---|---|
|`CREATE TABLE ...` |Yes |None |Create a source table for binlog writing. You can customize the table name and define the column names and types. |
|`connector` |Yes |None |The connector to use must be configured as `bytehouse-cdw`. |
|`jdbc.enable-gateway-connection` |Yes |false |Specify whether the JDBC connection needs to go through the ByteHouse gateway. |
|`bytehouse.gateway.region` |Yes |None |Set the ByteHouse gateway region to `VOLCANO_PRIVATE`. |
|`bytehouse.gateway.host` |Yes |None |ByteHouse CDW network domain name. Before configuring, set `bytehouse.gateway.region` to `VOLCANO_PRIVATE`.<br><br>The format is `tenant-{TENANT-ID}-{REGION}.bytehouse.[i]bytepluess.com`. You can log in to the ByteHouse CDW console, go to the **Tenant management** tab, click **Basic Information**, and in the **Network information** section, view and copy the public or private domain name. |
|`bytehouse.gateway.virtual-warehouse` |No |The default compute group configured in the console |Name or ID of the compute group that processes queries via ByteHouse Gateway. By default, the default compute group configured through the ByteHouse Console is used.<br><br>You can also specify other compute groups. You can log in to the ByteHouse CDW console and, under the **Virtual warehouse** tab, view and copy the Compute Group ID. |
|`bytehouse.gateway.api-token` |Required when connecting with an IAM user |None |The ByteHouse gateway API key. You can log in to the ByteHouse CDW console, go to the **Tenant management** tab, click **Connection info**, then create and copy a new API Key. |
|`bytehouse.gateway.account` |Required when connecting with a database user |None |Refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click Personal Center in the upper right corner, and view or copy your account ID or name. |
|`bytehouse.gateway.username` |Required when connecting with a database user |None |ByteHouse database account username. You can view and copy the **database username** via the **ByteHouse Console** \> **Access control** \> **User** path. |
|`bytehouse.gateway.paasword` |Required when connecting using a database user |None |Refers to the password for a ByteHouse database user. The password is set by the administrator when creating the database account. You can contact the administrator to obtain the password. If your password is lost or forgotten, you can contact the administrator to reset your password. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|`database` |Yes |None |The name of the ByteHouse CDW database to connect to. |
|`table-name` |Yes |None |Name of the ByteHouse CDW table to be connected. |
|`binlog` |No |false |Whether to enable reading of binlog information. When set to true, real\-time binlog consumption is enabled. Currently, only setting it to true is supported. |
|`scan.startup.mode` |No |LATEST |Set the starting position for consumption. Currently, only incremental mode is supported. Available options:<br><br>• earliest: It starts from the earliest available BSN.<br><br>• latest: It starts from the latest BSN.<br><br>• specific: It starts from the BSN specified by `scan.startup.specific-offset.pos`. |
|`scan.max-split-size` |No |10000 |It sets the number of data rows to read in each batch from binlog. |
|`scan.cdc.shard.split` |No |true |It configures whether to enable shard\-based reading: set to true to enable, false to disable. The default is true. |
|`scan.cdc.max-retries` |No |3 |It sets the number of retry attempts for errors that occur during binlog data consumption. |
|`scan.startup.specific-offset.pos` |No |None |When `scan.startup.mode` is set to SPECIFIC, you can specify the BSN (Binary Log Sequence Number) to consume from. |
|`CREATE TEMPORARY TABLE ...` |Yes |None |Create a temporary table whose structure matches that of the write source `bh_binlog_source`, but with the connector set to print, meaning that data will be directly printed to the Stdout (standard output) log.<br><br><br>* `connector`: Specify the connector to use; it must be set to `print`. The Print connector is a built\-in result table specifically for debugging, which outputs job results and prints them to the Stdout log.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please do not use the Print debug connector in tasks running in the production environment, as this may affect task performance and carries the risk of filling up the disk.   </div><br>   <br><br>* `LIKE`: Specifies the name for the new table to be created and adopts the structure of the source table.<br><br>* `EXCLUDING OPTIONS`: Indicates that the connection parameters of the source table are not inherited. |
|`INSERT INTO ... SELECT * FROM ...` |Yes |None |Create a data synchronization task to synchronize all data read from the source `bh_binlog_source` to the `print_sink` table, and finally output it to the Stdout log via the print connector. |


<span id="ede23688"></span>
## Consume using Flink DataStream API

The following is an example of consuming ByteHouse CDW binlog using the Flink DataStream API. When using, you can connect using either a ByteHouse IAM user or a database user.


<Tabs>
<Tab zoneid="Htq1NvOpCu" title="Use IAM users">
<TabTitle>Use IAM users</TabTitle>

```Java
import com.bytedance.bytehouse.flink.cdc.connector.cnch.source.CnchCdcSource;
import com.bytedance.bytehouse.flink.cdc.connector.cnch.source.deserialization.RowDataDeserializationSchema;
import com.bytedance.bytehouse.flink.cdc.connector.cnch.table.StartupOptions;
import com.bytedance.bytehouse.flink.connector.cnch.ByteHouseCdwClient;
import com.bytedance.bytehouse.flink.connector.cnch.api.java.CnchCdcSourceBuilder;
import java.util.Arrays;
import java.util.List;
import org.apache.flink.api.common.eventtime.WatermarkStrategy;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.api.DataTypes;
import org.apache.flink.table.catalog.Column;
import org.apache.flink.table.data.RowData;

/**
 * The following demonstrates how to use the ByteHouse CDW CDC connector to write data to ByteHouse CDW tables by reading binlog.
 */ 
 */
public class CnchCdcSourceExample {

  public static void main(String[] args) throws Exception {
    final String region = "VOLCANO_PRIVATE";
    final int port = 19000;
    final String host = args[0];
    final String apiToken = args[1];
    final String virtualWarehouse = args[2];
    final String database = args[3];
    final String tableName = args[4];
    final String tableNameSink = args[5];
    final String hostSink = args[6];
    final String apiTokenSink = args[7];

    // Create execution environment
    final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    List<Column> columns =
        Arrays.asList(
            Column.physical("id", DataTypes.BIGINT()), Column.physical("c", DataTypes.STRING()));
    // Build ByteHouse CDW CDC source
CnchCdcSource<RowData> cdcSource =
    // Set CnchCdcSourceBuilder
    new CnchCdcSourceBuilder.CdcSource<RowData>(database, tableName)
        .withGatewayConnection(region, host, port)
        .withBinlog(true)
        .withGatewayApiToken(apiToken)
        .withGatewayVirtualWarehouse(virtualWarehouse)
        .withSchema(columns)
        .withStartupModeOption(StartupOptions.earliest()) // Set the starting position to earliest
        .withDeserializationSchema(new RowDataDeserializationSchema())
        .withScanSplitSize(10000)    // Set the maximum batch size for each binlog fetch (in rows)
        .withShardSplit(true)        // Enable sharded reading
        .build();

    // Build a ByteHouse CDW CDC datastream 
    DataStream<RowData> dataStream =
    env.fromSource(cdcSource, WatermarkStrategy.noWatermarks(), "testSource");
    dataStream.print();
      // Trigger execution
      env.execute(CnchSinkDataStreamExample.class.getName());
    }
  }
}
```



</Tab>
<Tab zoneid="Z2C7gPJiic" title="Use a database user">
<TabTitle>Use a database user</TabTitle>

```Java
import com.bytedance.bytehouse.flink.cdc.connector.cnch.source.CnchCdcSource;
import com.bytedance.bytehouse.flink.cdc.connector.cnch.source.deserialization.RowDataDeserializationSchema;
import com.bytedance.bytehouse.flink.cdc.connector.cnch.table.StartupOptions;
import com.bytedance.bytehouse.flink.connector.cnch.ByteHouseCdwClient;
import com.bytedance.bytehouse.flink.connector.cnch.api.java.CnchCdcSourceBuilder;
import java.util.Arrays;
import java.util.List;
import org.apache.flink.api.common.eventtime.WatermarkStrategy;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.api.DataTypes;
import org.apache.flink.table.catalog.Column;
import org.apache.flink.table.data.RowData;

/**
 * The following demonstrates how to use the ByteHouse CDW CDC connector to write data to ByteHouse CDW tables by reading the binlog.
 */ 
 */
public class CnchCdcSourceExample {

  public static void main(String[] args) throws Exception {
    final String region = "VOLCANO_PRIVATE";
    final int port = 19000;
    final String host = args[0];
    final String apiToken = args[1];
    final String virtualWarehouse = args[2];
    final String database = args[3];
    final String tableName = args[4];
    final String tableNameSink = args[5];
    final String hostSink = args[6];
    final String apiTokenSink = args[7];

    // Create an execution environment
    final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    List<Column> columns =
        Arrays.asList(
            Column.physical("id", DataTypes.BIGINT()), Column.physical("c", DataTypes.STRING()));

// Build a ByteHouse CDW CDC source
CnchCdcSource<RowData> cdcSource =
     // Set CnchCdcSourceBuilder
    new CnchCdcSourceBuilder.cdcSource<RowData>(database, tableName) 
        .withGatewayConnection(region, host, port)
        .withBinlog(true)
        .withGatewayAccount(accountId, username, password)
        .withGatewayVirtualWarehouse(virtualWarehouse)
        .withSchema(columns)
        .withStartupModeOption(StartupOptions.earliest())
        .withDeserializationSchema(new RowDataDeserializationSchema())
        .withScanSplitSize(10000)
        .withShardSplit(true)
        .build();
        
    // Build a ByteHouse CDW CDC datastream
    DataStream<RowData> dataStream =
    env.fromSource(cdcSource, WatermarkStrategy.noWatermarks(), "testSource");
    dataStream.print();
      // Trigger execution
      env.execute(CnchSinkDataStreamExample.class.getName());
    }
  }
}   
```



</Tab>
</Tabs>


<span id="8911512e"></span>
### Interface description


|Interface |Required |Note |
|---|---|---|
|**Build a ByteHouse CDW CDC source** |||
|`CnchCdcSource<RowData> cdcSource` |Yes |It declares a `CnchCdcSource` data source with the generic type `RowData`, named `cdcSource`. The name can be customized.<br><br><br>* `<RowData>`: Java generic type used to specify the data type generated by `CnchCdcSource`. Settings can be configured to the following values:<br><br>   * RowData: It is recommended to use RowData, a binary\-optimized data structure used internally by Flink Table API and SQL, which is suitable for production environments.<br><br>   * ByteHouseRecord: A data structure defined internally in ByteHouse, used when access to ByteHouse\-specific metadata is required.<br><br>   * GenericRowData is a basic implementation of the RowData interface, but it is memory\-inefficient and intended only for development and testing environments.<br><br>* `cdcSource`: Object name. You can customize it. |
|`new CnchCdcSourceBuilder.CcdSource<RowData>(database, tableName)` |Yes |It sets the ByteHouse database and table name to connect to. `database` and `tableName` are required; all other parameters have default values and can be overridden as needed.<br><br><br>* `database`: Name of the ByteHouse cloud data warehouse database to connect to.<br><br>* `tableName`: The name of the ByteHouse Cloud Data Warehouse Edition table that needs to be connected to. |
|`.withGatewayConnection(region, host, port)` |Yes |The ByteHouse CDW gateway connection information.<br><br><br>* `region`: The ByteHouse CDW gateway region. This value is always set to `VOLCANO_PRIVATE`.<br><br>* `host`: The network domain name of the ByteHouse CDW gateway, in the format `tenant-{TENANT-ID}-{REGION}.bytehouse.[i]bytepluses.com`. You can log in to the ByteHouse CDW console, go to the **Tenant management** tab, click **Basic information**, and in the **Network information** section, view and copy the public or private network domain name.<br><br>* `port`: The port number for the ByteHouse CDW gateway, which is fixed at 19000. |
|`.withBinlog(true)` |No |Whether to read binlog information. When set to true, this activates the real\-time binlog consumption feature. Currently, only true is supported. |
|`.withGatewayApiToken(apiToken)` |Required when connecting using an IAM user |Set it as the ByteHouse CDW API key. You can log in to the ByteHouse CDW console, go to the **Tenant management** tab, click **Connection information**, then create and copy an API Key. |
|`.withGatewayAccount(accountId, username, password)` |This field is required when connecting as a database user. |Set the account and password for the ByteHouse CDW database user:<br><br><br>* `accountId`: This refers to the BytePlus user account ID or name. After logging in to the ByteHouse console, click the personal center in the upper right corner to view and copy the account ID or name.<br><br>* `username`: The database user name. You can navigate to **ByteHouse Console** \> Access control \> **User** to view and copy the database username.<br><br>* `password`: The password of a database user. This password is custom\-configured by the administrator when creating the database account. You can contact the administrator to obtain the password. If your password is lost or forgotten, you can contact the administrator to reset the password. For more information, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|`.withGatewayVirtualWarehouse(virtualWarehouse)` |No |Name or ID of the computing group for query processing via the ByteHouse gateway. By default, the default compute group configured through the ByteHouse Console is used. You can also specify other virtual warehouses. You can log in to the ByteHouse CDW console and, under the **Virtual warehouse** tab, view and copy the virtual warehouse ID. |
|.withSchema(columns) |No |Set the columns to read. |
|`.withStartupModeOption(StartupOptions.*earliest*())` |Yes |It configures consumption of binlog starting from a specified BSN. Currently, only incremental consumption is supported. You can set the earliest, latest, or a specific position. The corresponding parameter values are earliest, latest, and specific, respectively. |
|`.withDeserializationSchema(new RowDataDeserializationSchema())` |Yes |It defines how to parse binlog data into Flink internal objects. When configuring, ensure that the type matches the `<T>` type set in the `CnchCdcSourceBuilder.CdcSource<T>` parameter. The following three types are supported:<br><br><br>* This is the recommended value and corresponds to `<RowData>`.<br><br>* SimpleDeserializationSchema: corresponds to `<ByteHouseRecord>`<br><br>* GenericRowDataDeserializationSchema: Corresponds to `<GenericRowData>`. |
|`withScanSplitSize(10000)` |Yes |It sets the number of data rows to read in each batch from the binlog. |
|`.withShardSplit(true)` |Yes |It specifies whether to enable shard\-based reading. Set to true to enable, false to disable. The default value is true. |
|`withScanRetries(retrys: 1)` |No |It sets the number of retry attempts after an error occurs when consuming binlog data. |
|`.build()` |Yes |It returns a `CnchCdcSource` instance, which is constructed by the corresponding `CnchCdcSourceBuilder`. |
|**Build ByteHouse CDW CDC data stream** |||
|DataStreamdataStream |Yes |It is used to build a ByteHouse CDW CDC data flow. The generic type specified for DataStream must be the same as the type defined in the above data source. |
|`env.fromSource(cdcSource, WatermarkStrategy.noWatermarks(), "testSource")` |Yes |It converts the CDC source to a Flink data stream.<br><br><br>* `cdcSource`: The name of the data source constructed above.<br><br>* `WatermarkStrategy`: It is recommended to set it to `noWatermarks()`.<br><br>* `testSource`: The name of the data source as displayed in Flink. You can enter a value based on your actual requirements. |
