---
title: "FAQ"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/faq"
---

<span id="0a28dfc2"></span>
# FAQs on Product Capabilities

<span id="bbf4cc68"></span>
## What scenarios is ByteHouse suitable for?

ByteHouse is widely used in real\-time recommendation systems, advertising delivery, A/B testing, and other data analysis scenarios.

<span id="15a39ad8"></span>
## What are the performance differences between the Cloud Data Warehouse and Enterprise versions of ByteHouse?


* Enterprise version: Integrates storage and computation, with data locality and hot storage, direct node querying, and fewer network link hops.

* Cloud Data Warehouse version: Currently undergoing optimizations, including pre\-loading indexes and data, reducing some network overheads, and potentially handling thousands to tens of thousands of qps. It is theoretically capable of scaling up or down based on computing group specifications.


<span id="c586361d"></span>
## What regions does ByteHouse support?

Please refer to [Supported cloud providers and regions](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers). You can select the appropriate region and availability zone for deploying ByteHouse based on your business needs.

If you need services in other regions and availability zones, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact us.

<span id="395a2106"></span>
## What data sources does ByteHouse support for import?

The current cloud warehouse version of ByteHouse supports the import from the following data sources


|**Type** |**DataSource** |**Remark** |
|---|---|---|
|Offline Import |File Upload |Applicable when the file is smaller than 200 MB |
|Offline Import |BytePlus Object Storage TOS |Suitable for large file offline imports |
|Offline Import |Alibaba Cloud Object Storage OSS |Suitable for cross\-cloud large file offline imports |
|Offline Import |AWS Object Storage S3 |Suitable for cross\-cloud large file offline imports |
|Real\-time import |Apache Kafka |Suitable for real\-time stream data import |


<span id="7a0d2c63"></span>
## What data formats does ByteHouse support?


|**Datasource** |**Supported data formats** |**Remark** |
|---|---|---|
|File upload |Supports formats such as .csv, .json, .xls, .avro, .parquet, .csv.gz, and others |Uploaded files must be smaller than 200 MB |
|BytePlus TOS, AWS S3, Alibaba Cloud OSS, and others |Supports formats such as .csv, .json, .xls, .avro, .parquet, .csv.gz, etc. |Select up to 100 files for batch upload |
|Apache Kafka |Supports JSON and Parquet formats | |


<span id="7d4ec0f1"></span>
## Which BI tools can ByteHouse interface with?

ByteHouse currently supports interfacing with DataWind, Power BI, Superset, Tableau BI, and other tools. More BI tool integrations are under development.

<span id="cb953471"></span>
## What SQL semantics does ByteHouse support?

ByteHouse currently supports ANSI SQL 2011 and Clickhouse SQL. Users can specify this in the console or client.

<span id="e3061e55"></span>
## Does ByteHouse support ClickHouse syntax?

Currently, ByteHouse is compatible with the syntax of ClickHouse 23.3.

<span id="4e5a290c"></span>
## When there are many small queries (which use fewer resources and are faster), is it recommended to direct them to multiple small computing groups or one large computing group?

It is recommended to direct to one large computing group for higher efficiency.

<span id="aebd8f0f"></span>
## How to view the version of ByteHouse engine?

You can check your current engine version on the **Tenant management** \> **Basic information** page in the ByteHouse CDW console.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27db73f77de6457bae3441ded87e9f81~tplv-goo7wpa0wc-image.image) </span>

<span id="546e076c"></span>
## What is the default time zone of ByteHouse Cloud Data Warehouse?

The default time zone varies by region. You can check the default time zone of your region by executing the following SQL statement.

```SQL
SELECT timezone();
```


Query result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/195fc8b15c3c480c9003b3d804fc6f4b~tplv-goo7wpa0wc-image.image) </span>

<span id="8bdc6a87"></span>
## How many nodes does a virtual warehouse in ByteHouse have?

The number of nodes in a virtual warehouse is directly related to the specification you purchased and is not currently directly displayed in the console. The specific rules are as follows:


1. Node quantity rules: For virtual warehouses with XS/S/M/L specifications, the default number of nodes is 1. For those with XL and above specifications, the number of nodes is multiple.

2. The number of pods in a virtual warehouse is equal to the number of nodes.


<span id="2cb8533f"></span>
# Connecting to ByteHouse \- Network Access

<span id="29f11f35"></span>
## How to establish connectivity between ByteHouse and your VPC network?

For details, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings). Through binding a customer’s private network VPC, a private network domain name is generated. The customer can then connect to ByteHouse CDW from any resource within the bound VPC via the private network domain name.

<span id="c48023f4"></span>
## Why are some VPC options missing or absent when binding a private network VPC?

The reason is that there should be no conflicts between the customer's VPC network segments and ByteHouse's own service VPC network segments. ByteHouse service will filter out the conflicting segments. Below are the segments filtered by different regions:


* Beijing: ['[192.168.0.0/18','172.16.0.0/20](http://192.168.0.0/18','172.16.0.0/20)']

* Shanghai: ['[192.168.0.0/17','10.104.0.0/19](http://192.168.0.0/17','10.104.0.0/19)']


If there are no available VPC options at this time, the solution is to create a VPC that does not conflict with the above segments, such as: [192.168.128.0/24](http://192.168.128.0/24).

<span id="af5dc71e"></span>
## After establishing a dedicated line to the customer's private network, unable to access ByteHouse CDW?


* Common Questions:

   * Unable to resolve "CDW private network domain name" within the "Customer IDC/Private Network Environment", leading to connectivity issues.

   * When connecting via JDBC\-URL using the "private network domain name", encounters `unknown host`; IP and port can be telnet through, but cannot connect when configured in jdbc url.

* Resolution:

   It is recommended to add the mapping of "Private Network IP to CDW Private Network Domain Name" to the containers/environment/host/DNS server in the "private network environment" on the client's side, to ensure the client can resolve the CDW private network domain name to the established "Tenant's connected private network IP". Obtaining "Tenant's connected private network IP" can be done by:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf4d54da9c59455caccebedb90c57e3e~tplv-goo7wpa0wc-image.image) </span>

   Step 1. Obtaining "private network domain name": Go to the ByteHouse Cloud Data Warehouse Console \- Basic Information \- Network Information, and find the private network domain name.

   Step 2. Obtaining "private network connection IP": Enter any ECS instance in the VPC bound with CDW, execute nslookup/dig/ping on the private network domain name, to obtain it.


<span id="8c56c7a9"></span>
## Connection reset


1. First, ensure the protocol port is correct:

   * The port for the TCP protocol is: 19000

   * The port for the HTTP protocol is: 8123

   * The port for the MySQL protocol is: 3306

2. If the HTTP protocol is used, the HTTPS protocol must be used, such as: `https://tenant-{TENANE-ID}-{REGION}-public.bytehouse.bytepluses.com:8123`

3. If the TCP protocol is used, SSL must be used, such as JDBC: `jdbc:bytehouse://tenant-{TENANT-ID}-{REGION}-public.bytehouse.bytepluses.com:19000/${your_database}?secure=true`, ensure **`secure=true`** has been configured.


<span id="f41dc2fc"></span>
## How should the subnet be configured when creating ByteHouse?


* Background

   How should the subnet configuration be set when creating ByteHouse? There are now three subnets, but none of them can be selected.

* Cause of the problem

   When ByteHouse creates a private connection, a Load Balancer is created, and a network interface card (NIC) is generated in the VPC you specify, occupying one internal IP address in the VPC. This NIC is attached to the Load Balancer and serves as the entry point for ByteHouse.

   The core reason why the subnet cannot be selected is that the subnet CIDR block conflicts with the built\-in `bytehouse-vpc` CIDR block in ByteHouse. If network segments overlap, the routing rules within the VPC may become inconsistent, preventing normal connections from being established. Therefore, the system will disable conflicting subnets, making them unavailable for selection.

* Solutions:

   Create a subnet that does not conflict with the `bytehouse-vpc` network segment.


<span id="40d6987e"></span>
# Connect to ByteHouse \- Authentication and Authorization

<span id="eafbd8c9"></span>
## Can only two API_KEYS be generated? Can more be supported?

Currently, only two API_KEYS can be supported. Each sub\-account has its own two API_KEYS. If more API_KEYS are needed, they can be generated through different sub\-accounts.

<span id="79acd46c"></span>
## When calling the API, does it support obtaining the STS temporary credentials via AK/SK, and then using AK and STS temporary credentials to connect to the ByteHouse database?

No, ByteHouse CDW does not support this method. Currently, ByteHouse CDW only supports connecting to the ByteHouse database using the API token method.

Please refer to the specific operational standards [Calling method](https://docs.byteplus.com/docs/bytehouse/calling-method).

<span id="f75103fb"></span>
## What are the authorization scope and operations for the AccountAdmin / SystemAdmin roles?

AccountAdmin / SystemAdmin are special admin roles, whose permissions are equivalent to the policies in BytePlus IAM as follows:


* AccountAdmin equals BytePlus AdministratorAccess policy.

* SystemAdmin equals BytePlus ByteHouseFullAccess policy.


To configure the above roles for a user, you can assign the corresponding permission policies in BytePlus's Access Control (IAM) or add the user to a user group with the respective policies and wait for 3 to 5 minutes.

<span id="5852c6b7"></span>
## Why can't I grant Account Admin / System Admin permissions on the ByteHouse page?

The system admin is mapped to the BytePlus's ByteHouse Full Access policy. If a BytePlus sub\-account is configured with this policy, ByteHouse will automatically inherit and map these permissions. Sub\-accounts cannot be granted Account Admin / System Admin roles within ByteHouse. In the BytePlus IAM, assign the corresponding policies to the user or add the user to a group with the relevant policies. Changes will take effect in 3~5 minutes.

<span id="666ab295"></span>
## How can I extend the validity period of an API Key?

Log in to the ByteHouse Cloud Data Warehouse console. Click the **Tenant management** at the top. Then, click **Connection information**. In the **API Key** module, click the **Refresh** button in the row where the API Key is located. In the popup edit window, modify the expiry days of the API Key and click **Confirm**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9348fd49a6a4fedb5ff2987d59d19ac~tplv-goo7wpa0wc-image.image) </span>

<span id="4bf980ed"></span>
# Connect to ByteHouse\-JDBC

<span id="a7120074"></span>
## How to connect to ByteHouse Cloud Data Warehouse using JDBC, and what are the username and password?

To connect to bytehouse using JDBC, refer to [ByteHouse JDBC Driver](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-jdbc-driver), where the username is uniformly "bytehouse" and the password is "API_KEY," which can be generated and retrieved from the tenant management's connection information.

<span id="ad0f71d3"></span>
## Is JDBC supported if compiled with Java 1.7?

No support, only JDBC compiled with Java 1.8 is supported currently.

<span id="cc319019"></span>
## How to customize the query id after connecting to ByteHouse using JDBC?

After connecting to ByteHouse using JDBC, you can customize the query id with `((ByteHouseConnection) connection).setQueryId(queryId)`. The following is an example of customizing a query id:

```Java
try {
 statement.execute(String.format("CREATE DATABASE IF NOT EXISTS %s", databaseName));
 statement.execute(String.format("CREATE TABLE IF NOT EXISTS %s (id INT) "
 + "ENGINE=CnchMergeTree() order by tuple()", tableName));
 for (String queryId: queryIds) {
 // While constructing the prepared statement object, JDBC already sends the query to server. So we
 // need to set the queryId before constructing the prepared statement object.
 // While sending query, JDBC driver will use the queryId set in the connection object, or random UUID number if not set.
 // After sending the query, JDBC driver will reset the queryId.
 ((ByteHouseConnection) connection).setQueryId(queryId);
 ByteHousePreparedInsertStatement pstmt = (ByteHousePreparedInsertStatement) statement.
 getConnection().prepareStatement(String.format("INSERT INTO %s VALUES(?)", tableName));
 pstmt.setObject(1, 1);
 pstmt.addBatch();
 pstmt.executeBatch();
 }
} finally {
 statement.execute(String.format("DROP DATABASE IF EXISTS %s", databaseName));
}
```


<span id="73c94e6a"></span>
## Does MySQL JDBC support specifying a compute group (vm) when connecting to ByteHouse?

Currently, you cannot configure vm through the connection method. You can only add `SETTINGS virtual_warehouse = 'vw-name'` after the SQL command, or set it globally first `set virtual_warehouse = 'vw-name'`, then execute the SQL command.

<span id="55bd8971"></span>
# Connecting ByteHouse\-Python

<span id="bd867849"></span>
## How to output query_id in Python code after connecting to ByteHouse using Python?

```Python
from bytehouse_driver import Client
import uuid
def BH_driver_client(host, port, api_key):
    client = Client.from_url('bytehouse://bytehouse:{}@{}:{}/?secure=true&connect_timeout=20&send_timeout=3600&receive_timeout=3600'.format(api_key, host, port))
    return client
if __name__ == '__main__':
    PORT = 19000
    HOST_AWS_AP = 'gateway.aws-{REGION}.bytehouse.cloud'
    API_KEY = "xxxxxxxxxx"
    client = BH_driver_client(HOST_AWS_AP, PORT, API_KEY)
    query_id = str(uuid.uuid4())
    print("query_id:"+query_id)
    result_set = client.execute("select version()", query_id=query_id)
    for result in result_set:
        print(result)
```


<span id="74ecace8"></span>
## Error when using Python to connect to the ByteHouse cluster: no virtual warehouse was selected


* Error message: `no virtual warehouse was selected`

* Possible reason: No available compute group when executing the command.

* Solution: You need to provide the compute group information for command execution. Refer to the following two solutions and choose the appropriate one.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using the following two solutions, ensure that the computing group is <strong>launched</strong>, or is in a <strong>suspend</strong> state but has <strong>allow automatic start</strong> settings, otherwise even after the setup is complete, the SQL execution of the computing group will still throw an error.   </div>
   

   * Solution 1: Configure a default compute group in the tenant management.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08cecc77ab9548e28825e4cfe6444c9c~tplv-goo7wpa0wc-image.image) </span>

   * Solution 2: Specify the compute group when executing SQL, like: `SELECT column FROM database.table WHERE your_condition SETTINGS virtual_warehouse='vw-uuid'`


<span id="1e356a39"></span>
# Connect to ByteHouse \- ByteHouse client

<span id="aa5f64e7"></span>
## When using bytehouse cdw client to connect, the following error occurs: dial tcp http://xxxxx:19000: i/o timeout

Take the following command as an example:

`bytehouse-cli --host http://bytehouse-{REGION}.bytepluses.com --port 19000 --secure --token xxxxxx -q "INSERT INTO xxx.xxxx (xxxx) format CSVWithNames" < 'xxxx.csv'`

The solution is: It is recommended to add a parameter — connection timeout configuration. The default connection timeout is 3 seconds, and i/o timeout can be affected by network issues, or changes on the server side might cause occasional disconnections etc. It is advisable to slightly increase the connection timeout.

For instance, setting the connection timeout to 10 seconds `-ct 10`:

`bytehouse-cli --host http://bytehouse-{REGION}.bytepluses.com --port 19000 --secure --token xxxxxx -ct 10 -q "INSERT INTO xxx.xxxx (xxxx) format CSVWithNames" < 'xxxx.csv'`

<span id="65668175"></span>
# SQL\-SET Settings

<span id="636cb00e"></span>
## What are the supported methods for configuring settings via SET?


* Session level: First execute `set max_execution_time = 60`, then execute the SQL.

* SQL level: As in `sql setting max_execution_time = 60`


<span id="e1452d7d"></span>
## How to set a timeout configuration for long\-running SQL queries?

Before executing long\-running SQL statements, use a set statement to configure the timeout parameter at the session level, for example:

`set receive_timeout = 10800000, send_timeout = 10800000;`

<span id="39baeceb"></span>
# SQL Syntax

<span id="7eaaf123"></span>
## Key points for using UPDATE / DELETE syntax

The syntax for updating/deleting on Unique tables and non\-Unique tables is different.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The way to determine if it is a Unique table is whether the table creation statement includes the configuration: UNIQUE KEY.</div>



* Unique table syntax

   ```SQL
   UPDATE table_name SET field1=new-value1, field2=new-value2 [WHERE Clause]
   DELETE FROM <table_name> [WHERE Clause]
   ```
   

* Non\-Unique table syntax

   ```SQL
   ALTER TABLE [db.]table UPDATE column1 = expr1 [, ...] [IN PARTITION partition_expr] WHERE filter_expr
   ALTER TABLE [db.]table DELETE [IN PARTITION partition_expr] WHERE filter_expr
   ```
   


<span id="68ad756a"></span>
## When using left join, how to substitute values when the right table has no data?

In a left join, when data exists in the left table but not in the right table, the default behavior is to supplement the missing data in the right table with null. You can also configure to fill with empty values using `settings join_use_nulls=0`. Examples are as follows.

```SQL
SELECT
    a.id,
    a.name,
    b.address
FROM
    users AS a
LEFT JOIN
    user_details AS b
ON
    a.id = b.user_id settings join_use_nulls=0;
```


<span id="e1254448"></span>
## How to delete a partition?


* Unique table

   
   |Delete Partition Command |Function Description |
   |---|---|
   |alter drop partition statement (recommended) |Delete Partition, supports all tables, directly deletes directories at the underlying level, offers good performance, and is highly recommended for use.<br><br><br>* General Example<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION '2024-10-09'，DROP PARTITION '2024-10-08';```<br>```   ```<br>   <br><br>* Delete partition according to conditions<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION where `toDate(toStartOfDay(date1))` >'2024-10-06';```<br>```   ```<br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DROP PARTITION where the Expression must contain a complete PARTITION BY expression, and if it's a complex expression, use backticks (``) to enforce separation. <code>toDate(toStartOfDay(date1))</code> is used after PARTITION BY and can refer to the create table statement.   </div><br>    |
   |Delete statement (Not recommended) |Deleting data is a synchronous operation; the underlying method first searches then deletes, using an append\-file method for deletion, which consumes performance, and only supports unique tables.<br><br>Examples are as follows.<br><br>```SQL```<br>```DELETE FROM $database_name.$table_name WHERE date1 = '2024-10-10';```<br> |
   

* Non\-unique table

   
   |Delete Partition command |Function Description |
   |---|---|
   |alter drop partition statement (Recommended) |Delete Partition supports all tables. It directly deletes directories at the underlying level, providing excellent performance. It is recommended as the preferable method.<br><br><br>* General Example<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION '2024-10-09'，DROP PARTITION '2024-10-08';```<br>```   ```<br>   <br><br>* Delete partition based on conditions<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION where `toDate(toStartOfDay(date1))` >'2024-10-06';```<br>```   ```<br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">toDate(toStartOfDay(date1)) is used after PARTITION BY and can refer to the create table statement.   </div><br>    |
   |alter delete (Not recommended) |Deleting data is an asynchronous operation and does not support unique tables.<br><br>Examples are as follows.<br><br>```SQL```<br>```ALTER TABLE $database_name.$table_name DELETE WHERE k1 = 'a';```<br> |
   


<span id="09274f77"></span>
## In DML and DDL statements, which are synchronous operations and which are asynchronous operations?


* DML

   
   |Actions |Method |
   |---|---|
   |INSERT |Sync |
   |ALTER TABLE ... DELETE WHERE |Asynchronous |
   |ALTER TABLE ... UPDATE WHERE |Asynchronous |
   |OPTIMIZE TABLE |Asynchronous, mutaitons_sync = 1 will try to synchronize |
   |TRUNCATE TABLE |Sync |
   |delete where |Sync |
   

* DDL

   
   |DDL Statement Type |Example |Execution Method |
   |---|---|---|
   |CREATE |CREATE DATABASE，CREATE TABLE |Sync |
   |DROP |DROP DATABASE，DROP TABLE |Sync |
   |ALTER |ALTER TABLE ... ADD COLUMN (Sync) |Sync |
   |RENAME |RENAME TABLE |Sync |
   |TRUNCATE |TRUNCATE TABLE |Sync |
   |ATTACH / DETACH |ATTACH TABLE，DETACH TABLE |Sync |
   |SHOW / DESCRIBE |SHOW TABLES，DESCRIBE TABLE |Sync |
   |EXISTS |EXISTS TABLE，EXISTS DATABASE |Sync |
   |SYSTEM |System drop partition (asynchronous), reload tables (synchronous) |Mixed |
   


<span id="bcea8d23"></span>
## Can a table accidentally deleted using DROP TABLE be recovered?

If you accidentally delete a table using `DROP TABLE`, you can restore it using `UNDROP TABLE`. This method is limited to recovering deletions performed by `DROP TABLE`, and its validity period is restricted; currently, it supports recovery of tables deleted within the past two days, and can be used to temporarily stop losses caused by accidental operations. It is strongly recommended that you use the **backup and restore** feature. For details, please refer to [Backup and restore](https://docs.byteplus.com/docs/bytehouse/full-backup-restore).

Example:

```SQL
# Drop a table but then realize it was deleted by mistake
DROP TABLE db_name.table_name;

# Restore this table using UNDROP TABLE
UNDROP TABLW db_name.table_name;

# Query data to verify whether the restoration is successful
SELECT count() FROM db_name.table_name;
```


<span id="f3a7621d"></span>
# SQL error

<span id="f0c0170f"></span>
## SQL execution error: DB::Exception: Memory limit (for query) exceeded: would use xxx GiB

This error `(for query)` occurs when a single query exceeds the memory limit. Consider optimizing the SQL if possible, such as:


* Reducing the amount of data in joins, positioning the larger table on the left and the smaller on the right.

* Eliminating the group by action.


The relevant configuration parameter is `max_memory_usage`. If the actual memory used by the SQL operation is very large, you can submit a work order or contact ByteHouse officials to increase this value.

<span id="2ce86923"></span>
## SQL execution error: Exception: Memory limit (total) exceeded: would use xxx GiB (attempt to allocate chunk of xxx bytes), maximum: xxxxx GiB

This type of error `(total)` indicates that the node's overall memory limit has been exceeded. Consider checking the group memory monitor to confirm if it meets expectations (by default, this limit is set to 90% of the group's memory).

Solution:


* Reduce the overall SQL concurrency.

* For SQLs with high stability requirements, consider setting up a separate group.

* Expand the current computation group.


<span id="2debef1a"></span>
## SQL error: Too many simultaneous queries / Too many simultaneous tasks


* Description: There are too many queries being executed.

* Description: There are too many merges.


Solution:


1. Optimize the write mode, batch together, reduce concurrency, which means increasing the number of values in a single insert and reducing the frequency.

2. If your computing unit is always running and won't stop automatically, you can accelerate the backend data merge speed in the UI by executing `ALTER TABLE your_database.your_table MODIFY SETTING cnch_vw_write = 'vw_id'`.


<span id="9745310c"></span>
## SQL write error: Too many partitions for single INSERT block (more than 100)


* Complete error: `Too many partitions for single INSERT block (more than 100).` `The limit is controlled by 'max_partitions_per_insert_block' setting.` `Large number of partitions is a common misconception.` `It will lead to severe negative performance impact, including slow server startup, slow INSERT queries and slow SELECT queries.` `Recommended total number of partitions for a table is under 1000..10000. Please note, that partitioning is not intended to speed up SELECT queries (ORDER BY key is sufficient to make range queries fast).`

* Possible reasons: Description that the current batch INSERT has written to multiple partitions (default 100). Excessive partition files can severely affect import efficiency and query speed.

* Solution:

   1. Optimize the write mode within the task, and ensure values in each INSERT are as much as possible within the same partition.

   2. Adjust the target table DDL partition key to aggregate partitions by date, at daily or monthly granularity.

   ```SQL
   PARTITION BY (toDate(`event_time`))
   ```
   

   3. Add larger limits behind SQL, but it is not recommended to be too large, for example: `insert into tabela_name values('1') settings max_partitions_per_insert_block = xxx`

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Delete command does not support settings, temporary settings at the session level can be done as follows: <code>set max_partitions_per_insert_block = xxx;</code>, then execute SQL      </div>
      

<span id="48eaea93"></span>
## Query error: query fails 5 minutes later, reporting EOF or I/O timeout

To prevent query timeouts, add the following parameters to increase the timeout time (in seconds)


* max_execution_time

* send_timeout

* receive_timeout


At JDBC, for example:

```Plain
jdbc:bytehouse://<domain>:19000?api_key=xxx&send_timeout=10000&receive_timeout=10000&max_execution_time=10000
```


Or at the session level, run SQL first in

```SQL
set receive_timeout = 10800000, send_timeout = 10800000;  
```


<span id="27cd87ac"></span>
## SQL intermittent error: Code: 2010

Error message examples are as follows:

```SQL
Code: 2010, e.displayText() = DB::Exception: Query [6xxxxx-fxxx-4xxx-axxx-dxxxxxxxxxx3] failed with RootCause: SegmentId: 0, ErrorCode:2010, Message: Fail to call DB.Protos.RegistryService.registry, error code: 1011, msg: [E1011][192.168.
```


Answer:

The buffer in the socket queue for RPC communication has exceeded its limit; you can first increase the buffer size.

You need to configure the socket_max_unwritten_bytes Param at both the server and virtual warehouse levels simultaneously.

<span id="d1499ed7"></span>
# Function

<span id="6f1b247a"></span>
## How to use the finderGroupFunnel function?

With the function name changed from vvcfunnelOpt to finderGroupFunnel, this function does not support not configuring mode. If the mode value is not filled in and the chekc_envent parameter is directly filled, it will fail to pass the check, or pass but the result does not meet expectations, such as treating the first event field as the group field and the second event field as the first event field.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e1db9ac2fb14c9197e4d322cbd59f80~tplv-goo7wpa0wc-image.image" width="1710px" /></div>


<span id="b91d66d1"></span>
# External Table

<span id="825a333d"></span>
## When configuring an external MySQL table, does it support intranet access?

Internal network access is not supported yet. This function is still not open and is being scheduled for evaluation, expected to be scheduled for 2025.

<span id="fa0beaf1"></span>
## When configuring an external MySQL table, which IPs and ports need to be whitelisted?

Current internal network access is not supported. Public network access needs to be configured. You only need to open public network access to bytehouse cdw. For details on the public network, see [Supported cloud providers and regions](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers).


* Port: random, please open all ports.

* IP address: The public access addresses for different regions are as follows.

   
   |**Regions** |**Public Internet Exit IP** |
   |---|---|
   |Hong Kong |[150.5.146.60](https://console.byteplus.com/eip/region:eip+cn-hongkong/eips/detail?id=eip-3e1c8qn1jeups2h2n5oj5d89r), [150.5.168.25](http://150.5.168.25/) |
   |Southeast Asia (Johor) |[101.47.140.89](https://console.byteplus.com/eip/region:eip+ap-southeast-1/eips/detail?id=eip-14w1m7g264mps3tvs80iln5no), [101.47.11.124](http://101.47.11.124/) |
   


<span id="5da5ec10"></span>
# Data Import

<span id="80b0ad17"></span>
## Configuration instructions for Kafka Datasource?


|Kafka Scenarios |Configuration Key Points |
|---|---|
|**The Kafka cluster is configured with a public network access address**. |You can configure it on the ByteHouse Console. Use the Kafka public IP address.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94e94f0cac3646afad1b061855a7eea8~tplv-goo7wpa0wc-image.image) </span> |
|**Kafka does not have a public network access address and is in the same region as ByteHouse**.<br><br>Includes, under the same main account Kafka cloud products, Kafka clusters built under the same main account, Kafka cloud products under different main accounts, and Kafka clusters built under different main accounts. |Private network addresses can be used to connect to ByteHouse, refer to the document: [ByteHouse Kafka Import with Private IP address](https://bytedance.larkoffice.com/docx/BBgEdSz8YoL4bJxUjg0cOIWkn0e) |
|**Kafka has no public network access address and is not in the same region as ByteHouse**.<br><br>Includes BytePlus Kafka products under different regions, self\-built BytePlus Kafka clusters under different regions, and clusters from other cloud providers or self\-built ones. |It is recommended to use the Datasail link: Your Kafka \-\> Sail \-\> CDW |


<span id="632accd0"></span>
## When importing data from Kafka, how to extract one field from Kafka into multiple fields in the ByteHouse table multiple times?

The first column uses the same name, the rest use col01, col02. For example, in the middle of Kafka field data: `"ds_http_uri_query": "a=1&b=2"`, extract the values of fields a and b into two fields in ByteHouse.


* a field: `extractURLParameter(concat('http://?', ds_http_uri_query), 'a')`

* b field: `extractURLParameter(concat('http://?', ds_http_uri_query), 'b')`


For details on nested parsing, refer to [Streaming loading](https://docs.byteplus.com/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json).

<span id="ae91a828"></span>
## How to configure date parsing format?

The default date format supported for automatic parsing in ByteHouse data import is `yyyy-MM-dd'T'HH:mm:ss` (the default Java time format). Caution: The date and time parts are separated by the constant 'T'. If your data uses other formats, manual configuration is required. The configuration steps are as follows:


1. After uploading files, in source columns with the format set to Date, DateTime, and other date formats, click the **edit** button to open the format configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4738df552bbb40bebb7ba37de4b18b32~tplv-goo7wpa0wc-image.image) </span>

2. Select the corresponding time format in the format list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a42d438ac7044551a2a60d6018a2b57f~tplv-goo7wpa0wc-image.image) </span>

3. If you do not find the date format you need, scroll to the bottom of the format list, click **New Format**, and input the log format you need. The format is Joda.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/006430b128aa471fab0a2f5f8130f690~tplv-goo7wpa0wc-image.image) </span>


<span id="b08d5e59"></span>
## How to configure timezone?

When importing files using local small file import or other import methods, you may encounter timezone import anomalies, such as the timezone being offset by +8 or \-8. This section will introduce some best practices for import methods to avoid similar problems.

<span id="892d8d33"></span>
### Use the recommended data format

It is recommended to use the following two methods to store time in the file, which can avoid timezone problems when converting dates during import.

<span id="1f9532ab"></span>
#### Option 1: Use a date format with timezone

It is recommended to add timezone information when storing dates.


| |Information with timezone (recommended) |Date without timezone information (not recommended) |
|---|---|---|
|Sample value |2025\-01\-02 12:13:14+0800 |2025\-01\-02 12:13:14 |
|Corresponding format |yyyy\-MM\-dd HH:mm:ssZ<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47f802a7caea4012a82ecdf7a52ea898~tplv-goo7wpa0wc-image.image) </span> |yyyy\-MM\-dd HH:mm:ss<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc072f9a8ca5489cbd9d1e83435b8fcb~tplv-goo7wpa0wc-image.image) </span> |


<span id="375d9c4d"></span>
#### Option 2: Use Int type to store date

For dates with higher time precision, it is recommended to use the Int type to store dates.


| |Precision: seconds. |Precision: ms |
|---|---|---|
|Sample value |1735791194 |1735791194000 |
|Corresponding format |seconds<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/087ae772350641cbbca2ac88a73ed7f3~tplv-goo7wpa0wc-image.image) </span> |milliseconds<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc20946ffb8a472c921a991770a00895~tplv-goo7wpa0wc-image.image) </span> |


<span id="25d7e8d3"></span>
### Specify time partitions when creating a table

When creating a table, if a time type column is included in the partition, it is recommended to explicitly specify a time partition. Examples are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/550cd07182194d3fa846841ba37a8c40~tplv-goo7wpa0wc-image.image) </span>
