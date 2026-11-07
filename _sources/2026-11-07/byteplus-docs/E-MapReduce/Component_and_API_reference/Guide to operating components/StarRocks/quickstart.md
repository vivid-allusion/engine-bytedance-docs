---
title: "quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/starrocks_quickstart"
---

This article describes how to create and manage E\-MapReduce (EMR) StarRocks clusters, as well as how to query and analyze data stored in StarRocks.

<span id="_1-创建集群"></span>
## Create a cluster

Creating a cluster consists of four steps: software settings \-\-\> hardware settings \-\-\> other settings \-\-\> preview and confirmation.


1. Log in to [EMR Console](https://console.volcengine.com/emr/).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario:

* Region: The created cluster and corresponding resources will be deployed in the selected region and cannot be changed.

* Project space: The system has automatically created a default project named **default**. You can create your own project space using the following path:

   * Go to the project page via the upper right corner **User \> Access Control \> Resource Management \> Project**.

   * Click the **Create Project** button, enter the project name, display name, remarks, and other information to complete the creation of a new project.

      For details, see [Project configuration](https://docs.byteplus.com/docs/E-MapReduce/105422).

3. In the EMR Console, click **Create Cluster**, select **Interactive Query** \> **StarRocks**, and choose the appropriate version according to your needs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7cfa788992f4042288dc0654e4bd522.png) </span>

   Note

   
   |Configuration items |Note |
   |---|---|
   |Product versions |It is recommended to use the latest version. You can click [EMR on ECS 功能发布记录（2026年前）](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b89) to view the release notes for each version. |
   |Service high availability |Enabled by default. When enabled, three FE nodes and at least three BE nodes are deployed to improve the cluster's service capability and fault tolerance, avoiding single points of failure. It is recommended to enable high availability for production clusters. |
   |Optional services |Currently, StarRocks 2.x and 3.x versions are available for selection. If you are starting a new business or do not have version migration requirements, it is recommended to use version 3.x. |
   |Custom configuration |Starting from StarRocks 3.x, deployment supports separation of storage and compute. |
   

4. In the **Hardware Settings** section, select the payment type, configure the availability zone, network, and ECS instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fa3fa5091df9c2afd28fdca9b04c9de.png) </span>

   Note

   
   |Configuration items |Note |
   |---|---|
   |Payment type |Both Pay\-As\-You\-Go and Subscription billing modes are supported:<br><br><br>* **Pay\-As\-You\-Go**: Charges are based on the actual activation duration, calculated in hours. This is a postpaid model, and nodes can be released at any time.<br><br>* **Subscription**: Purchase and renew on a monthly basis. This is a prepaid model, and nodes can only be released after expiration. |
   |Availability zone |A physically isolated area within the same region where power and network are independent. Within the same region, internal networks are interconnected between different availability zones, and fault isolation can be achieved between availability zones. |
   |Network configuration |Configure the cluster network for StarRocks:<br><br><br>* **Select project**: A VPC belongs to a specific project. If the desired VPC is not available in the VPC options list, try switching projects or select "All Projects."<br><br>* **VPC**: The cluster's private network. Internal network connectivity is ensured within the same VPC. It is recommended to deploy EMR upstream and downstream systems within the same private network. For example, downstream BI tools that need to access the StarRocks FE service must ensure that the cluster where the BI tool resides and the StarRocks cluster are in the same VPC.<br><br>* **Subnet**: A subnet is used to assign a private IP address to the primary network interface of an instance. Network management of the instance can be achieved through the network interface.<br><br>* **Security group**: Select the configured security group rules to control inbound and outbound traffic of ECS within the security group. |
   |Instance settings |Instance node groups are divided into Master and Core. Typically, StarRocks deploys FE nodes on the Master node group and BE nodes on the Core node group. You need to plan node specifications, the number of BE nodes, and disk space reasonably based on business requirements and data growth.<br><br>Although the Core node group can be disabled during instance settings, allowing both FE and BE to be deployed on the Master node group, it is strongly recommended for production clusters to deploy BE on the Core node group to achieve better performance and cluster stability, as well as to better support cluster scaling to accommodate future business growth. |
   

5. In the **Other Settings** section, set the cluster name, access credentials, and other information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c738b1760a7343a3f704a96b4ae7151.png) </span>

   Note

   
   |Configuration items |Note |
   |---|---|
   |Cluster name |The name of the cluster. The length is limited to 1–64 characters and can only contain Chinese characters, letters, numbers, hyphens (\-), and underscores (_). |
   |Access credentials |This credential is used for remote login to the ECS machine of the cluster master node. You can choose to log in using either a key pair or a password.<br><br><br>* **Key pair**: Select a successfully created key pair from the dropdown, or click [Create key pair](https://console.volcengine.com/ecs/region:ecs+cn-beijing/keyPair) to go to the console and create one.<br><br>* **Password**: Enter the login password for the cluster master node. For password format requirements, refer to [Other settings](https://docs.byteplus.com/docs/E-MapReduce/105456#_3-3-%E5%85%B6%E4%BB%96%E8%AE%BE%E7%BD%AE). |
   |Cluster script |Used to configure scripts that execute bootstrap operations when the cluster starts. Bootstrap operations can customize the cluster environment, such as deploying and installing third\-party components in an EMR cluster. |
   |Cluster role |Bind an IAM role to the cluster to provide ECS in the EMR cluster with resource permissions to access TOS. |
   |Tags |Tags consist of case\-sensitive key\-value pairs and are used to label all instances and cloud disks created in this cluster. |
   |Cluster project |Assign the newly created cluster to a project. You can select an existing project or create a new one. |
   

6. In the **Preview and Confirmation** section, the configuration sheet for this cluster will be displayed. After confirming that the cluster configuration information is correct and checking **EMR Service Terms**, you can click the **Create Now** button to start creating the StarRocks cluster. Cluster creation is an asynchronous process that typically takes several minutes. You can view the cluster creation progress in the EMR Console.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can further visit <a href="https://docs.byteplus.com/docs/E-MapReduce/105456">Create clusters (version 3.18.0 and earlier)</a> to learn detailed descriptions of each configuration item related to cluster creation.</div>


<span id="_2-连接-starrocks"></span>
## Connect to StarRocks

StarRocks is compatible with the MySQL protocol. You can connect to the StarRocks service directly using the MySQL client in the following format:

```bash
mysql -h {fe_node_ip} -P {fe_query_port} -u {username} -p;
```


Note


* `fe_node_ip`: Any FE node IP of StarRocks, which can be either a private IP or a public IP. You can obtain it from the cluster details page in the EMR Console by accessing "**Node Management \- MasterGroup**". Ensure connectivity with this IP.

* `fe_query_port`: StarRocks MySQL Server port. You can obtain it in the EMR console by accessing the cluster details page and navigating to "**Service List \- StarRocks \- Service Parameters**" to find the `query_port` configuration item. The default value is 9030.


You can log in for the first time using the root account without a password. Example:

```bash
# No password required for first connection
$ mysql -h 127.0.0.1 -P 9030 -u root -p;
```


After connecting successfully and entering the MySQL interactive terminal, it is strongly recommended to set a password for the root account using the [SET PASSWORD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SET_PASSWORD/) command. Example:

```sql
SET PASSWORD FOR 'root'@'%' = PASSWORD('******');
```


To ensure data security, it is strongly recommended to set a highly complex password for the `root` account and keep it safe. After the password is set successfully, you need to exit the terminal and reconnect to the StarRocks cluster.

In addition to using the MySQL client, you can also use any other GUI tool that supports the MySQL protocol to connect to and access the StarRocks service.

<span id="_3-用户和权限管理"></span>
## User and permission management

Users with `user_admin` administrator privileges (such as the `root` user) can perform more granular management of cluster users and permissions to ensure data security.

<span id="_3-1-用户管理"></span>
### User management

<span id="5f5fad36"></span>
#### **Create user**

You can create a user using the following SQL syntax:

```sql
CREATE USER 
-- User identifier, consisting of username and login IP, for example, zhangsan@'127.0.0.1'
{user_identity}
-- User authentication method. Supports native password, mysql_native_password, and LDAP authentication methods.
[auth_option]
-- Bind permission roles to users to grant corresponding operation permissions.
[DEFAULT ROLE {role_name}[, {role_name}, ...]]
```


Example:

```sql
mysql> CREATE USER username@'%' IDENTIFIED BY '***' DEFAULT ROLE db_admin, user_admin;
```


<span id="8d2531de"></span>
#### **View user**

You can use `SHOW USERS` to view all users in the current cluster. Example:

```sql
mysql> SHOW USERS;
+-------------------------+
| User                    |
+-------------------------+
| 'root'@'%'              |
| 'username'@'%'          |
| 'emr'@'127.0.0.1'       |
+-------------------------+
```


<span id="5a376cbb"></span>
#### **Modify user**

You can modify the information of a specified user, such as the user's password, authentication method, and permission roles, using the following SQL syntax:

```sql
ALTER USER 
-- User identifier, consisting of username and login IP, for example, zhangsan@'127.0.0.1'
user_identity 
-- User authentication method. Supports native password, mysql_native_password, and LDAP authentication methods.
[auth_option] 
-- Bind permission roles to users to grant corresponding operation permissions.
[default_role]
```


The following example demonstrates how to modify the password information of a specified user:

```sql
mysql> ALTER USER 'username'@'%' IDENTIFIED BY '***';
```


<span id="2bdc8ede"></span>
#### **Delete user**

You can delete a specified user using `DROP USER`. Example:

```sql
mysql> DROP USER 'username'@'%';
```


<span id="_3-2-权限管理"></span>
### Permission management

StarRocks provides a built\-in RBAC\-based permission management policy. You can view existing permission roles in the cluster by executing `SHOW ROLES`.

<span id="6de66cd9"></span>
#### **Permission granting**

By associating a user with a role using the [GRANT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/GRANT/) operation, you can grant the permissions corresponding to that role to the user. For example, associate a user with the `db_admin` role:

```sql
mysql> GRANT db_admin TO USER 'username'@'%';
```


You can also bypass roles and directly grant specific permissions to a user. The following example demonstrates how to directly grant SELECT permission on the tb_primary_key table to a user:

```sql
mysql> GRANT SELECT ON TABLE tb_primary_key TO USER 'username'@'%' WITH GRANT OPTION;
```


You can use `SHOW GRANTS` to view the permission granting status of the current user or a specified user:

```sql
mysql> SHOW GRANTS FOR 'username'@'%' \G;
*************************** 1. row ***************************
UserIdentity: 'username'@'%'
     Catalog: NULL
      Grants: GRANT 'db_admin' TO 'username'@'%'
*************************** 2. row ***************************
UserIdentity: 'username'@'%'
     Catalog: default_catalog
      Grants: GRANT SELECT ON TABLE examples.tb_primary_key TO USER 'username'@'%' WITH GRANT OPTION
```


<span id="bf0414cb"></span>
#### **Permission revocation**

You can revoke the permissions of a specified user or role by using the `REVOKE` operation. For example, to revoke a user's SELECT permission on the tb_primary_key table:

```sql
mysql> REVOKE SELECT ON TABLE tb_primary_key FROM USER 'username'@'%';
```


<span id="_4-库表管理"></span>
## Database and table management

After connecting to the StarRocks service via the MySQL protocol, you can use SQL statements to view and manage databases and tables.

<span id="_4-1-数据库管理"></span>
### Database management

<span id="698a1f55"></span>
#### **Create a database**

You can create a database using the following SQL syntax:

```sql
CREATE DATABASE [IF NOT EXISTS] {db_name}
```


The `db_name` parameter specifies the database name. For naming rules, refer to the [StarRocks official documentation](https://docs.starrocks.io/zh/docs/sql-reference/System_limit/). The following example demonstrates how to create a database named examples:

```sql
mysql> CREATE DATABASE IF NOT EXISTS examples;
```


<span id="85705730"></span>
#### **View databases**

You can use the following SQL syntax to view the databases created under a specified catalog:

```sql
SHOW DATABASES [FROM {catalog_name}]
```


The `catalog_name` parameter specifies the catalog name. If not specified, the default is `default_catalog`. The following example demonstrates how to view databases in `default_catalog`:

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| _statistics_       |
| examples           |
| information_schema |
| sys                |
+--------------------+
```


You can also use the following SQL syntax to view the creation statement of a specified database:

```sql
SHOW CREATE DATABASE {db_name}
```


Example:

```sql
mysql> SHOW CREATE DATABASE examples;
+----------+----------------------------+
| Database | Create Database            |
+----------+----------------------------+
| examples | CREATE DATABASE `examples` |
+----------+----------------------------+
```


<span id="172f322d"></span>
#### **Update a database**

You can use the following SQL syntax to rename a database or set its quota:

```sql
-- Rename database
ALTER DATABASE {db_name} RENAME {new_db_name}

-- Set database data quota. Unit: B/K/KB/M/MB/G/GB/T/TB/P/PB
ALTER DATABASE {db_name} SET DATA QUOTA {quota}

-- Set database replica quota
ALTER DATABASE {db_name} SET REPLICA QUOTA {quota}
```


The following example demonstrates renaming the examples database to demo:

```sql
mysql> ALTER DATABASE examples RENAME demo;
```


<span id="a31c2a44"></span>
#### **Delete a database**

You can use the following SQL syntax to delete a specified database:

```sql
DROP DATABASE [IF EXISTS] {db_name} [FORCE]
```


Example:

```sql
mysql> DROP DATABASE demo;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After executing DROP DATABASE, by default, the deleted database can be recovered within 1 day using the RECOVER statement. However, any Pipe import jobs deleted along with the database cannot be recovered.</div>


* <div data-tips="true" data-tips-type="tip">If DROP DATABASE FORCE is executed, the system will not check whether there are any unfinished transactions in the database. The database will be deleted directly and cannot be recovered. It is generally not recommended to perform this operation.</div>



<span id="_4-2-数据表管理"></span>
### Table management

<span id="ecf9210b"></span>
#### **Create a table**

You can use the `CREATE TABLE` statement to create a table in a specified database. The typical SQL syntax is as follows:

```sql
CREATE [EXTERNAL] TABLE [IF NOT EXISTS] [{database_name}.]{table_name}
(
    -- Column definition
    column_definition1[, column_definition2, ...]
    -- Index definition
    [index_definition1[, index_definition2, ...]]
)
-- Engine definition. The default is OLAP, which indicates an internal table. External tables are also supported, including mysql, elasticsearch, hive, jdbc, hudi, iceberg, and more.
[ENGINE = OLAP]
-- Define the data model and sort key. The default is the detail model.
[key_desc]
-- Define the table description
[COMMENT '这里是表的描述信息']
-- Define the table partitioning method. Expression partitioning, range partitioning, and list partitioning are supported.
[partition_desc]
-- Define the data bucketing method. Random bucketing and hash bucketing are supported.
[distribution_desc]
-- For the primary key model, the sort key can be set independently using ORDER BY.
[ORDER BY (column_definition1,...)]
-- Set table property configurations, such as the number of replicas
[PROPERTIES ("key"="value", ...)]
```


For detailed descriptions of each parameter, see the [StarRocks official documentation](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/CREATE_TABLE/). The following example demonstrates how to create a primary key table named tb_primary_key in the examples database:

```sql
mysql> USE examples;
Database changed

mysql> CREATE TABLE IF NOT EXISTS tb_primary_key
    -> (
    ->     user_id BIGINT       NOT NULL COMMENT 'user id',
    ->     name    VARCHAR(32)  NOT NULL COMMENT 'user name',
    ->     age     TINYINT      NOT NULL COMMENT 'user age',
    ->     sex     TINYINT      NOT NULL COMMENT 'user sex',
    ->     email   VARCHAR(256) NULL COMMENT 'email'
    -> ) ENGINE = OLAP PRIMARY KEY (user_id)
    -> DISTRIBUTED BY HASH(user_id)
    -> ORDER BY(`name`)
    -> PROPERTIES (
    ->     'replication_num' = '3'
    -> );
```


You can also use the [CREATE TABLE AS SELECT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/CREATE_TABLE_AS_SELECT/) syntax to query the original table and create a new table based on the query results, or use the [CREATE TABLE LIKE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/CREATE_TABLE_LIKE/) syntax to create a new table based on the structure of an existing table.

<span id="e1d288dc"></span>
#### **View tables**

You can use the following SQL syntax to view tables in a specified database:

```sql
SHOW TABLES [FROM {catalog_name}.{db_name}]
```


The `catalog_name` parameter specifies the catalog name. If not specified, the default is `default_catalog`. The `db_name` parameter specifies the database name. If not specified, the default is the current database. Example:

```sql
mysql> SHOW TABLES;
+--------------------+
| Tables_in_examples |
+--------------------+
| tb_primary_key     |
+--------------------+
```


You can also use the following SQL syntax to view the creation statement of a specified table:

```sql
SHOW CREATE TABLE [{db_name}.]{table_name}
```


Example:

```sql
mysql> SHOW CREATE TABLE tb_primary_key \G;
*************************** 1. row ***************************
       Table: tb_primary_key
Create Table: CREATE TABLE `tb_primary_key` (
  `user_id` bigint(20) NOT NULL COMMENT "user id",
  `name` varchar(32) NOT NULL COMMENT "user name",
  `age` tinyint(4) NOT NULL COMMENT "user age",
  `sex` tinyint(4) NOT NULL COMMENT "user sex",
  `email` varchar(256) NULL COMMENT "email"
) ENGINE=OLAP
PRIMARY KEY(`user_id`)
DISTRIBUTED BY HASH(`user_id`)
ORDER BY(`name`)
PROPERTIES (
"replication_num" = "3",
"in_memory" = "false",
"enable_persistent_index" = "true",
"replicated_storage" = "true",
"compression" = "LZ4"
);
```


<span id="0925063d"></span>
#### **Update a table**

You can modify a specified data table using the following SQL syntax:

```sql
ALTER TABLE [{db_name}.]{tbl_name}
alter_clause1[, alter_clause2, ...]
```


Here, alter_clause refers to the specific modification operation. The currently supported operations are listed in the following table:


|Operation type |Note |
|---|---|
|RENAME |Modify the table name, rollup index name, and partition name. Modifying column names is not supported. |
|COMMENT |Modify the table comment. |
|PARTITION |Modify the table partition properties, delete partitions, or add partitions. |
|BUCKET |Modify the table bucketing method and the number of buckets. |
|COLUMN |Add columns, delete columns, adjust column order, and modify column types. |
|ROLLUP INDEX |Create or delete a rollup index. |
|BITMAP INDEX |Modify the bitmap index. |
|SWAP |Atomically swap two tables. |
|COMPACTION |Manually perform data version compaction on the specified table or partition. |


The following example demonstrates how to modify the comment information of a data table:

```sql
mysql> ALTER TABLE tb_primary_key COMMENT='这里是新的描述信息';
```


You can use [SHOW ALTER TABLE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/SHOW_ALTER/) to view the execution status of ALTER tasks.

<span id="ec548125"></span>
#### **Delete data table**

You can delete a specified data table using the following SQL syntax:

```sql
DROP TABLE [IF EXISTS] [{db_name}.]{table_name} [FORCE]
```


Example:

```sql
mysql> DROP TABLE tb_primary_key;
```


Note:


* After executing DROP TABLE, by default, the deleted data table can be recovered within one day using the `RECOVER` statement.

* If you execute DROP TABLE **FORCE**, the system will not check whether there are unfinished transactions for the table. The data table will be deleted directly and cannot be recovered. It is generally not recommended to perform this operation.


<span id="_5-数据查询"></span>
## Data query

After connecting to the StarRocks service via the MySQL protocol, you can use SQL statements to query, update, and delete data in StarRocks.

<span id="0056253d"></span>
### **Insert data**

You can use the [INSERT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/loading_unloading/INSERT/) statement to insert data into a specified data table. The typical SQL syntax is as follows:

```sql
INSERT { INTO | OVERWRITE } [{db_name}.]{table_name}
-- Specify the partition to insert into
[ PARTITION ({partition_name} [, ...] ) ]
-- Values to be inserted
{ VALUES ( { {expression} | DEFAULT } [, ...] ) | {query} }
```


Example:

```sql
mysql> INSERT INTO tb_primary_key
    -> VALUES (10001, 'aaaa', 26, 1, 'aaaa@starrocks.com'),
    ->        (10002, 'bbbb', 17, 0, 'bbbb@starrocks.com'),
    ->        (10001, 'aaaa', 27, 1, 'aaaa@starrocks.com'),
    ->        (10001, 'aaaa', 28, 1, 'aaaa@starrocks.com');
{'label':'insert_42bd9455-dd1b-11ee-9417-00163e11548e', 'status':'VISIBLE', 'txnId':'2'}
```


<span id="3993f128"></span>
### **Query data**

You can use the [SELECT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/SELECT/) statement to query data in a specified data table. The typical SQL syntax is as follows:

```sql
SELECT ...
FROM ...
[ ... ]
GROUP BY [
    , ... |
    GROUPING SETS [, ...] (  groupSet [ , groupSet [ , ... ] ] ) |
    ROLLUP(expr  [ , expr [ , ... ] ]) |
    CUBE(expr  [ , expr [ , ... ] ])
    ]
[ ... ]
```


Example:

```sql
mysql> SELECT * FROM tb_primary_key;
+---------+------+------+------+--------------------+
| user_id | name | age  | sex  | email              |
+---------+------+------+------+--------------------+
|   10002 | bbbb |   17 |    0 | bbbb@starrocks.com |
|   10001 | aaaa |   28 |    1 | aaaa@starrocks.com |
+---------+------+------+------+--------------------+
```


<span id="e48e97d2"></span>
### **Delete data**

You can use the [DELETE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/table_bucket_part_index/DELETE/) statement to delete data that meets the conditions in a specified data table. The typical SQL syntax is as follows:

```sql
DELETE FROM [{db_name}.]{table_name} [PARTITION {partition_name}]
WHERE
-- Set delete filter conditions. One or more columns can be specified. The delete operation is performed when all conditions are met.
column_name1 op { value | value_list } [ AND column_name2 op { value | value_list } ...]
```


Example:

```sql
mysql> DELETE FROM tb_primary_key WHERE user_id = 10001;
{'label':'delete_3f0f15e5-dd1c-11ee-9417-00163e11548e', 'status':'VISIBLE', 'txnId':'4'}
```
