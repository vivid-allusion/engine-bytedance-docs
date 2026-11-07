---
title: "Flink Connector Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Flink_Connector"
---

The Flink Connector Driver for ByteHouse Cloud Data Warehouse is specifically used to load data into ByteHouse Cloud Data Warehouse via Flink. This tutorial will introduce two ways to connect to ByteHouse and process data: using [Table API&SQL](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/overview/) and Flink's [DataStreamAPI](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/datastream/overview/).

<span id="cf070820"></span>
# Background information

ByteHouse supports connecting to the Flink Connector Driver using IAM users or database users. The differences between IAM users and database users are explained below. You can choose according to your needs.


* An **IAM user** is a user created in BytePlus access control (IAM), whose privileges are determined by IAM pprivilege policies as well as the ByteHouse resource and data privileges you grant. IAM users can access the ByteHouse console. ByteHouse also supports access through the CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resource, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through the CLI, connection drivers, ecosystem tools, API, and other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="51fb9361"></span>
# Preparation

Download the Flink SQL or Flink DataStream API driver that matches your installed Flink version.

<span id="c02c5832"></span>
## The Flink SQL driver


|**Flink version** |**Device driver** |**Release date** |
|---|---|---|
|1.18 |[v2.12-1.27.117-1.18](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.27.117-1.18/flink-sql-connector-bytehouse-cdw_2.12-1.27.117-1.18.jar) |2025\-01\-13 |
|1.17 |[v2.12-1.27.117-1.17](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.27.117-1.17/flink-sql-connector-bytehouse-cdw_2.12-1.27.117-1.17.jar) |2025\-01\-13 |
|1.16 |[v2.12-1.27.117-1.16](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.27.117-1.16/flink-sql-connector-bytehouse-cdw_2.12-1.27.117-1.16.jar) |2025\-01\-13 |
|1.15 |[v2.12-1.27.117-1.15](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/flink-sql-connector-bytehouse-cdw_2.12/1.27.117-1.15/flink-sql-connector-bytehouse-cdw_2.12-1.27.117-1.15.jar) |2025\-01\-13 |
|1.11<br><br>（scala 2.11） |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2be1b1b942c4355b017fbb86ab5b9b1~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-cdw_2.11-1.27.104-1.11.jar">flink-sql-connector-bytehouse-cdw_2.11-1.27.104-1.11.jar</Attachment><br> |2024\-10\-23 |


<span id="02b97236"></span>
## Local installation

Please run the following command to install the downloaded `flink-sql-connector-bytehouse-cdw-${flink-sql-connector-bytehouse-cdw.version}.jar` file into the local Maven repository:

```Bash
mvn install:install-file \
    -Dfile=${your_path}/flink-sql-connector-bytehouse-cdw-${flink-sql-connector-bytehouse-cdw.version}.jar \
    -DgroupId=com.bytedance.bytehouse \
    -DartifactId=flink-sql-connector-bytehouse-cdw \
    -Dversion=${flink-sql-connector-bytehouse-cdw.version} \
    -Dpackaging=jar
```


Then, you can use an IDE (for example, IntelliJ) to add it as a dependency in your project.

<span id="019c29b0"></span>
## Maven dependencies

For Maven projects that use the Flink connector, add the following dependencies to the project's pom.xml file. `scala.version` must be 2.11 or 2.12 to match the Scala version associated with the Flink distribution. `${flink-sql-connector-bytehouse-cdw.version}` can be set to the required Flink connector version.

```XML
<dependency>
    <groupId>com.bytedance.bytehouse</groupId>
    <artifactId>flink-sql-connector-bytehouse-cdw_${scala.version}</artifactId>
    <version>${flink-sql-connector-bytehouse-cdw.version}</version>
</dependency>

<dependency>
    <groupId>com.bytedance.bytehouse</groupId>
    <artifactId>flink-sql-connector-bytehouse-cdw_2.12</artifactId>
    <version>1.27.100_snapshot7</version>
</dependency>
```


Then, add the following repositories to the `pom.xml` file:

```XML
<repository>
    <id>bytedance</id>
    <name>ByteDance Public Repository</name>
    <url>https://artifact.bytedance.com/repository/releases</url>
</repository>
```


<span id="a3d45871"></span>
# Usage examples

<span id="889028e7"></span>
## Import data via Flink SQL

The following is an example of loading data tables into ByteHouse Cloud Data Warehouse tables using FlinkSQL.

<span id="7e2267d2"></span>
### Use IAM users to connect and import

You can refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to get the information required for connecting using an IAM user, and replace the corresponding placeholders below.


* `'bytehouse.gateway.host'`: Configure as ByteHouse's public or private domain name. You can view and copy the network information in the ByteHouse console under **Tenant Management** \> **Basic Information** \> **Network Information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* `'bytehouse.gateway.api-token'`: Set this to the ByteHouse API Key. You can create and copy an API Key in the ByteHouse console under **Tenant management** \> **Connection information** . For more details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).

* `'bytehouse.gateway.virtual-warehouse'`: Set to the ByteHouse virtual warehouse ID, which you can obtain from the **Virtual warehouse** page in the ByteHouse console.

* `'database'`: The name of the database you need to connect to.

* `'table-name'`: The name of the table you need to connect to.


For more information about parameters, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/Flink_Connector#55b41614).

```SQL
CREATE TABLE `bh_de_source` ( -- The source table
 `id` BIGINT NOT NULL,
 `time` TIMESTAMP(0),
 `content` ARRAY<DECIMAL(20, 0)>
) WITH (
 'connector' = 'datagen'
);
CREATE TABLE `bh_de_sink` ( -- The target table
 `id` STRING NOT NULL,
 `event_time` STRING,
 `content` ARRAY<DECIMAL(20, 0)>,
 PRIMARY KEY (`id`) NOT ENFORCED
) WITH (
 'connector' = 'bytehouse-cdw',
 'jdbc.enable-gateway-connection' = 'true',
 'bytehouse.gateway.region' = 'VOLCANO_PRIVATE',
 'bytehouse.gateway.host' = 'tenant-{TENANT-ID}-{REGION}.bytehouse.ibytepluses.com',
 'bytehouse.gateway.port' = '19000',
 'bytehouse.gateway.api-token' = '<API_KEY>',
 'bytehouse.gateway.virtual-warehouse' = '<VIRTUAL_WAREHOUSE>',
 'database' = '<BYTEHOUSE_DB>',
 'table-name' = '<BYTEHOUSE_TABLE>'
);
INSERT INTO `bh_de_sink` ( Load data
 `id`,
 `event_time`,
 `content`
)
SELECT
 CAST(`id` AS STRING), Type conversion with default values
 CAST(`time` AS STRING), Type conversion
 `content` -- Default values
FROM `bh_de_source`;
```


<span id="504c1b6b"></span>
### Use a database user connection and import

You can refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to get the information required for connecting with a database user, and replace the corresponding placeholders below. For more information about parameters, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/Flink_Connector#55b41614).


* `'bytehouse.gateway.host'`: Set this to ByteHouse's public or private domain name. You can view and copy the network information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For more information, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

* `'bytehouse.gateway.virtual-warehouse'`: Set this to the ByteHouse virtual warehouse ID. You can obtain it from the ByteHouse console's **Virtual warehouse** page.

* `'bytehouse.gateway.account'`: Set this to the BytePlus user account ID or name. You can log in to the ByteHouse console, click the Personal Center in the upper right corner, and view and copy your account ID or name.

* `'bytehouse.gateway.username'`: Set this to the ByteHouse database account username. You can log in to the ByteHouse console and view and copy the database username on the **Access control** \> **User** page.

* `'bytehouse.gateway.paasword'`: This parameter is set as the password for the ByteHouse database user. The password is custom\-configured by the administrator when creating the database account. You may contact the administrator to obtain the password.

* `'database'`: The name of the database you need to connect to.

* `'table-name'`: Name of the table to connect to.


```SQL
CREATE TABLE `bh_de_source` ( Source table
 `id` BIGINT NOT NULL,
 `time` TIMESTAMP(0),
 `content` ARRAY<DECIMAL(20, 0)>
) WITH (
 'connector' = 'datagen'
);
CREATE TABLE `bh_de_sink` ( -- Target table
 `id` STRING NOT NULL,
 `event_time` STRING,
 `content` ARRAY<DECIMAL(20, 0)>,
 PRIMARY KEY (`id`) NOT ENFORCED
) WITH (
 'connector' = 'bytehouse-cdw',
 'jdbc.enable-gateway-connection' = 'true',
 'bytehouse.gateway.region' = 'VOLCANO_PRIVATE',
 'bytehouse.gateway.host' = 'tenant-{TENANT-ID}-{REGION}.bytehouse.ibytepluses.com',
 'bytehouse.gateway.port' = '19000',
 'bytehouse.gateway.virtual-warehouse' = '<VIRTUAL_WAREHOUSE>',
 'bytehouse.gateway.account' = '<your_byteplus_ID>',
 'username' = '<your_bytehouse_cdw_database_user>',
 'paasword' = '<your_bytehouse_cdw_database_user_password>',
 'database' = '<BYTEHOUSE_DB>',
 'table-name' = '<BYTEHOUSE_TABLE>'
);
INSERT INTO `bh_de_sink` ( Loading data
 `id`,
 `event_time`,
 `content`
)
SELECT
 CAST(`id` AS STRING), -- Type conversion with default values
 CAST(`time` AS STRING), Type conversion
 `content` -- Default value
FROM `bh_de_source`;
```


<span id="21c36b92"></span>
## Import data through the Flink DataStream API

The DataStream API of the Flink connector restricts the source data type to `RowData`.

The use of the DataStream API primarily involves obtaining a `CnchSinkFunctionBuilder` to acquire a `CnchSinkFunction` instance, which helps facilitate various connector configurations.

Example: Write user data to a multi\-table database

<span id="4afb32fd"></span>
### Use IAM users to connect and import

You can refer to the information required to connect using an IAM user in [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889), and replace the corresponding placeholders below. For more explanation about parameters, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/Flink_Connector#55b41614).


* `.withGatewayConnection("VOLCANO_PRIVATE", "your_host", "your_port")`：

   * `"your_host"`: This is configured as the public or private domain name for ByteHouse. You can view and copy the network information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

   * `"your_port")`: Fixed at 19000.

* `.withGatewayApiToken("<< your API token >>")`: Set this to the ByteHouse API Key. You can obtain the API Key in the ByteHouse console under **Tenant management** \> **Connection information** . For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).

* `.withGatewayVirtualWarehouse("default_vw")`: Set this to the ByteHouse virtual warehouse ID, which you can obtain from the **Virtual warehouse** page in the ByteHouse console.


```Java
import bytehouse.shaded.com.google.common.collect.Lists;
import com.bytedance.bytehouse.flink.connector.cnch.ByteHouseCdwClient;
import com.bytedance.bytehouse.flink.connector.cnch.CnchMultiSinkFunction;
import com.bytedance.bytehouse.flink.connector.cnch.api.java.CnchMultiSinkFunctionBuilder;
import com.bytedance.bytehouse.flink.connector.cnch.sql.ByteHouseCdwCreateTableStatementBuilder;
import com.bytedance.bytehouse.table.ByteHouseColumn;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.data.RowData;
import org.apache.flink.types.RowKind;
import java.time.Duration;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
public final class MultiSinkCdwTableExample {
  public static void main(String[] args) throws Exception {
    final String region = "VOLCANO_PRIVATE";
    final String host = args[0]; // e.g., tenant-{accountId}-{region}-public.bytehouse.bytepluses.com
    final int port = 19000;
    final String token = args[1]; // e.g., 1HkKORvYGV:xxxxxxxx
    final String vwId = args[2]; // e.g., vw-{environment_id}{account_id}-{virtual_warehouse_name}
    final String dbName = args[3];
    final String tableName = args[4];
    List<RowData> collectedRowData = Lists.newArrayList();
    ByteHouseCdwClient bhCli = new ByteHouseCdwClient(region, host, port, token, vwId);
    // Drop and recreate tables
    final String tableName1 = tableName + "1";
    bhCli.dropTableIfExists(dbName, tableName1);
    bhCli.execute(
        new ByteHouseCdwCreateTableStatementBuilder()
            .createTable(dbName, tableName1)
            .schema("id Int64, event_time DateTime, content String")
            .partitionBy("toYYYYMMDD(`event_time`)")
            .orderBy("id")
            .uniqueKey("id")
            .build());
    final String tableName2 = tableName + "2";
    bhCli.dropTableIfExists(dbName, tableName2);
    bhCli.execute(
        new ByteHouseCdwCreateTableStatementBuilder()
            .createTable(dbName, tableName2)
            .schema("id Int64, properties Map(String, String)")
            .addColumn(ByteHouseColumn.of("login_time", "Nullable(Time(3))"))
            .build());
    // Construct data
    for (int i = 0; i < 10; i++) {
      Map<String, Object> record = new HashMap<>();
      record.put("id", i);
      record.put("event_time", LocalDateTime.now());
      record.put("login_time", LocalTime.now());
      record.put("content", String.format("Row %d @ %s", i, record.get("event_time")));
      Map<String, String> props = new HashMap<>();
      props.put("propId", record.get("id").toString());
      props.put("propEventTime", record.get("event_time").toString());
      props.put("propContent", record.get("content").toString());
      record.put("properties", props);
      RowData rowData1 = bhCli.constructRichRowData(RowKind.INSERT, dbName, tableName1, record);
      collectedRowData.add(rowData1);
      RowData rowData2 = bhCli.constructRichRowData(RowKind.INSERT, dbName, tableName2, record);
      collectedRowData.add(rowData2);
    }
    // Create the execution environment
    StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    env.setParallelism(1);
    // Add a source to the data stream
    DataStream<RowData> dataStream = env.fromCollection(collectedRowData);
    try (CnchMultiSinkFunction<RowData> sink =
        new CnchMultiSinkFunctionBuilder.MultiRowDataTable(Duration.ofMinutes(3))
            .withGatewayConnection(region, host, port)
            .withGatewayApiToken(token)
            .withGatewayVirtualWarehouse(vwId)
            .withFlushInterval(Duration.ofSeconds(10))
            .withFlushBatchSize(5000)
            .build()) {
      // Add a sink to the data stream
      dataStream.addSink(sink);
      // Trigger the execution
      env.execute(MultiSinkCdwTableExample.class.getSimpleName());
    }
    // Select and print out all rows in the table
    System.out.printf("\n==== %s ====\n", tableName1);
    bhCli.selectAll(dbName, tableName1).forEach(System.out::println);
    System.out.printf("\n==== %s ====\n", tableName2);
    bhCli.selectAll(dbName, tableName2).forEach(System.out::println);
    // Clean up
    bhCli.close();
  }
}
```


<span id="c9cdf63c"></span>
### Use a database user to connect and import

You can refer to the information required for connecting with a database user in [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) and replace the corresponding placeholders below. For more information about parameters, see [Parameter description](https://docs.byteplus.com/docs/bytehouse/Flink_Connector#55b41614).


* `.withGatewayConnection("VOLCANO_PRIVATE", "your_host", "your_port")`：

   * Set `"your_host"` as the public or private domain name for ByteHouse. You can view and copy the network information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486).

   * `"your_port")`: Fixed at 19000.

* `.withGatewayAccount(accountId, username, password)`：

   * `accountId`: Set it to your BytePlus user account ID or account name. You can log in to the ByteHouse console, click the Personal Center in the upper right corner, and view and copy your user account ID or account name.

   * `username`: Set this to the ByteHouse database account username. You can log in to the ByteHouse console and view and copy the database username on the **Access control** \> **User** page.

   * `password`: The password set for the ByteHouse database user account. This password is custom configured by the administrator when creating the database account. You can contact the administrator to obtain the password.

* `.withGatewayVirtualWarehouse("default_vw")`: Set this to the ByteHouse virtual warehouse ID, which you can obtain from the Virtual warehouse page in the ByteHouse console.


```Java
import bytehouse.shaded.com.google.common.collect.Lists;
import com.bytedance.bytehouse.flink.connector.cnch.ByteHouseCdwClient;
import com.bytedance.bytehouse.flink.connector.cnch.CnchMultiSinkFunction;
import com.bytedance.bytehouse.flink.connector.cnch.api.java.CnchMultiSinkFunctionBuilder;
import com.bytedance.bytehouse.flink.connector.cnch.sql.ByteHouseCdwCreateTableStatementBuilder;
import com.bytedance.bytehouse.table.ByteHouseColumn;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.data.RowData;
import org.apache.flink.types.RowKind;
import java.time.Duration;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
public final class MultiSinkCdwTableExample {
  public static void main(String[] args) throws Exception {
    final String region = "VOLCANO_PRIVATE";
    final String host = args[0]; // e.g., tenant-2100000000-cn-guangzhou-public.bytehouse.bytepluses.com
    final int port = 19000;
    final String accountId = args[1];
    final String username = args[2];
    final String password = args[3];
    final String vwId = args[4]; // e.g., vw-2100000000-default-vw
    final String dbName = args[5];
    final String tableName = args[6];
    List<RowData> collectedRowData = Lists.newArrayList();
    ByteHouseCdwClient bhCli = new ByteHouseCdwClient(region, host, port, accountId, username, password, vwId);
    // Drop and recreate tables
    final String tableName1 = tableName + "1";
    bhCli.dropTableIfExists(dbName, tableName1);
    bhCli.execute(
        new ByteHouseCdwCreateTableStatementBuilder()
            .createTable(dbName, tableName1)
            .schema("id Int64, event_time DateTime, content String")
            .partitionBy("toYYYYMMDD(`event_time`)")
            .orderBy("id")
            .uniqueKey("id")
            .build());
    final String tableName2 = tableName + "2";
    bhCli.dropTableIfExists(dbName, tableName2);
    bhCli.execute(
        new ByteHouseCdwCreateTableStatementBuilder()
            .createTable(dbName, tableName2)
            .schema("id Int64, properties Map(String, String)")
            .addColumn(ByteHouseColumn.of("login_time", "Nullable(Time(3))"))
            .build());
    // Construct data
    for (int i = 0; i < 10; i++) {
      Map<String, Object> record = new HashMap<>();
      record.put("id", i);
      record.put("event_time", LocalDateTime.now());
      record.put("login_time", LocalTime.now());
      record.put("content", String.format("Row %d @ %s", i, record.get("event_time")));
      Map<String, String> props = new HashMap<>();
      props.put("propId", record.get("id").toString());
      props.put("propEventTime", record.get("event_time").toString());
      props.put("propContent", record.get("content").toString());
      record.put("properties", props);
      RowData rowData1 = bhCli.constructRichRowData(RowKind.INSERT, dbName, tableName1, record);
      collectedRowData.add(rowData1);
      RowData rowData2 = bhCli.constructRichRowData(RowKind.INSERT, dbName, tableName2, record);
      collectedRowData.add(rowData2);
    }
    // Create the execution environment
    StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    env.setParallelism(1);
    // Add a source to the data stream
    DataStream<RowData> dataStream = env.fromCollection(collectedRowData);
    try (CnchMultiSinkFunction<RowData> sink =
        new CnchMultiSinkFunctionBuilder.MultiRowDataTable(Duration.ofMinutes(3))
            .withGatewayConnection(region, host, port)
            .withGatewayAccount(accountId, username, password)
            .withGatewayVirtualWarehouse(vwId)
            .withFlushInterval(Duration.ofSeconds(10))
            .withFlushBatchSize(5000)
            .build()) {
      // Add a sink to the data stream
      dataStream.addSink(sink);
      // Trigger the execution
      env.execute(MultiSinkCdwTableExample.class.getSimpleName());
    }
    // Select and print out all rows in the table
    System.out.printf("\n==== %s ====\n", tableName1);
    bhCli.selectAll(dbName, tableName1).forEach(System.out::println);
    System.out.printf("\n==== %s ====\n", tableName2);
    bhCli.selectAll(dbName, tableName2).forEach(System.out::println);
    // Clean up
    bhCli.close();
  }
}
```


<span id="55b41614"></span>
# Parameter description


|**Parameters** |**Required** |**Default value** |**Data types** |**Description** |
|---|---|---|---|---|
|`connector` |Yes |(none) |String |Specify the driver to use; in this case, it should be `bytehouse-cdw`. |
|`database` |Yes |(none) |String |The name of the ByteHouse Cloud Data Warehouse Edition database to be connected. |
|`table-name` |Yes |(none) |String |Name of the ByteHouse Cloud Data Warehouse Edition table to be connected. |
|`jdbc.query.timeout` |No |`1 minute` |Duration |The timeout setting for executing queries via JDBC. |
|`jdbc.enable-gateway-connection` |No |`false` |Boolean |Specify whether JDBC connections need to go through the ByteHouse Gateway. |
|`bytehouse.gateway.region` |No |(none) |String |Set the ByteHouse gateway region to `VOLCANO_PRIVATE`. |
|`bytehouse.gateway.host` |No |(none) |String |The network domain name of the ByteHouse gateway. The format is `tenant-{TENANT-ID}-{REGION}.bytehouse.[i]bytepluses.com`. You can log in to the ByteHouse CDW console, go to the **Tenant management** tab, click **Basic information**, and in the **Network information** module, view and copy the public or private network domain name.<br><br>Before use, set bytehouse.gateway.region to `VOLCANO_PRIVATE`. |
|`bytehouse.gateway.port` |No |`19000` |Integer |The private port of the ByteHouse gateway. The prerequisite is to set bytehouse.gateway.region to `VOLCANO_PRIVATE`. |
|`bytehouse.gateway.virtual-warehouse` |No |(none) |String |Name or ID of the compute group that processes queries through ByteHouse Gateway. By default, the default compute group configured via the ByteHouse console is used. |
|`bytehouse.gateway.api-token` |No |(none) |String |The ByteHouse API key. Log in to the ByteHouse CDW console. Under the **Tenant management** tab, click **Connection information**, then create and copy an API Key. |
|`bytehouse.gateway.account` |No |(none) |String |This refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click Personal Center in the upper right corner, and view or copy your account ID or name. |
|`username` |No |(none) |String |The ByteHouse database user name. You can view and copy the database username by navigating to the **ByteHouse Console** \> **Access control** \> **Users** path. |
|`paasword` |No |(none) |String |The database user's password. The password is custom\-configured by the administrator when creating the database account. You may contact the administrator to obtain the password. If your password is lost or forgotten, you can contact the administrator to reset the password. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|`sink.group-by.key` |No |(none) |String |The key of the pre\-receiver group. A key can consist of multiple fields, separated by commas. |
|`sink.group-by.expression` |No |(none) |String |Expression for grouping pre\-receivers. If set, all involved field names must also be listed in sink.group\-by.key. |
|`sink.group-by.number-of-groups` |No |(none) |Integer |Record the number of pre\-receiver groups. If not specified, it will fall back to sink.parallelism, if provided. |
|`sink.buffer-flush.interval` |No |`1 second` |Duration |The maximum interval between two batch refreshes. Minimum: 200 milliseconds (ms). |
|`sink.buffer-flush.max-rows` |No |`50,000` |Integer |The maximum size of buffer records before a refresh. The minimum is 100. |
|`sink.buffer-flush.max-batches` |No |`6` |Integer |The threshold for the number of pending batches that triggers asynchronous refresh overload prevention. Minimum: 1. |
|`sink.max-retries` |No |`3` |Integer |Maximum number of retry attempts when data refresh fails. Setting it to \-1 means unlimited retries. |
|`sink.parallelism` |No |(none) |Integer |Maximum parallelism for data refresh. By default, the framework determines parallelism by using the same parallelism as the upstream chained operators. |
|`sink.mode` |No |`insert` |String |Select the data records to be received. Supported values:<br><br><br>* insert: Only INSERT records are accepted.<br><br>* upsert: (applies when the base table is a unique table) accepts INSERT, UPDATE_AFTER, and DELETE records<br><br>* upsert\-no\-delete: (Applicable when the base table is a unique table) Accepts INSERT and UPDATE_AFTER records.<br><br>* upsert\-all: (applicable when the base table is a unique table) accepts all types of records.<br><br>* upsert\-all\-no\-delete: (Applicable when the base table is a unique table) Accepts all types of records except DELETE.<br><br>* delete\-only: Only DELETE records are accepted. |
|`metrics.update-interval` |No |`5 seconds` |Duration |The fixed interval for refreshing metrics. The minimum time is `5` seconds. |
|`metrics.log-level` |No |`INFO` |String |The log level for recording metrics. This corresponds to [the built-in standard log levels of Log4J](https://logging.apache.org/log4j/2.x/manual/customloglevels.html). |
|`timestamp-offset` |No |(none) |Duration |Additional time offset for timestamp data. |
|`jdbc.connection.custom-settings` |No |`enable_point_lookup_profile = 1` |String |Custom settings at the query level are typically used to optimize lookup. |
|`lookup.async.scale-factor` |No |`1` |Integer |Scaling factor for asynchronous lookup. If set to less than 2, the search will run in synchronous (SYNC) mode. If set to n (where n ≥ 2), the lookup will run in asynchronous (ASYNC) mode, and the maximum concurrency for each lookup instance will be equal to n. |
|`lookup.cache.max-rows` |No |`0` |Long |Maximum number of rows in the data table lookup cache. If set to 0, caching is disabled. |
|`lookup.cache.ttl` |No |(none) |Duration |TTL for the lookup cache of the ByteHouse table. If not specified, TTL is not set for cache records. |
|`lookup.max-retries` |No |`3` |Integer |The maximum number of retries allowed when a lookup operation fails. |
