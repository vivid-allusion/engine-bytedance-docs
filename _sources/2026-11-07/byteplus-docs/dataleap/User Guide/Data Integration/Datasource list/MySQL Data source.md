---
title: "MySQL Data source"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/mysql_data_source"
---

The MySQL data source provides bidirectional channel data integration capabilities for reading from and writing to MySQL, enabling data transfer between different data sources and MySQL.

This article introduces how DataSail supports MySQL data synchronization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Volcengine VeDB\-MySQL database has a configuration that is largely consistent with that of the MySQL data source. You can refer to this article to perform configuration operations for VeDB data source tasks.</div>


<span id="_1-支持的-mysql-版本"></span>
## 1 Supported versions


* MySQL offline reading and writing:

   * Supports the MySQL edition of Volcengine Cloud Database;

   * Supports self\-hosted MySQL 5.6.x, 5.7.x, and 8.0.x.

* VeDB MySQL offline read/write

   * Supports Volcengine Cloud Database VeDB MySQL edition.


<span id="_2-使用前提"></span>
## 2 Usage prerequisites


1. A sub\-account must have the project administrator role to perform the **create data source** operation. Note: For details on the permissions assigned to each role, see [Manage Member Information](https://docs.byteplus.com/docs/dataleap/manage_project_member)

2. Ensure that the dedicated data integration resource group used for integration synchronization tasks has network access to MySQL database nodes. For details about the network interoperability solution, see [Network connectivity solution](https://docs.byteplus.com/docs/dataleap/network_connectivity_solution).

   * When the data source is an RDS MySQL cloud database instance, you need to add the IPv4 CIDR address of the VPC where the integration resource group is located to the MySQL access whitelist:

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the VPC where the MySQL data source instance is located is the same as the VPC where the dedicated integration resource group is located, you only need to add the IPv4 CIDR address of the VPC to the MySQL access whitelist.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the VPC where the MySQL data source instance is located is different from the VPC where the dedicated integration resource group is located, you need to first connect the two VPC networks through <a href="https://docs.byteplus.com/en/docs/cen/Product-Overview-01">Cloud Enterprise Network (CEN)</a>. Then, add the IPv4 CIDR addresses of both the integration resource group VPC and the MySQL VPC to the MySQL access whitelist.      </div>
      

      1. Confirm the VPC where the integration resource group is located:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5f176e563ea4869a85e00f95344be78~tplv-goo7wpa0wc-image.image) </span>

      2. View the IPv4 CIDR address of the VPC:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c278c5b390184bf88f739d3e56a03a9c~tplv-goo7wpa0wc-image.image) </span>

      3. Add the obtained IPv4 CIDR addresses to the MySQL database whitelist. For details on how to add them, see [Create a whitelist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist).

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5805d6c27a204c099bbfe994307b6683~tplv-goo7wpa0wc-image.image) </span>

   * The data source is a self\-built public network data source and must be accessed via the public network.

      * Enable public network access for the integration resource group. For detailed instructions, see [Enable public network for Resource Group VPC](https://docs.byteplus.com/docs/dataleap/enable_public_network_for_resource_group).

      * Then add the public IP address to the MySQL database whitelist.


<span id="_3-支持的字段类型"></span>
## 3 Supported field types

The support status for main field types is as follows:


|Field types |Offline reading (MySQL Reader) |Offline write (MySQL Writer) |
|---|---|---|
|TINYINT |Support |Support |
|SMALLINT |Support |Support |
|INTEGER |Support |Support |
|BIGINT |Support |Support |
|FLOAT |Support |Support |
|DOUBLE |Support |Support |
|DECIMAL |Support |Support |
|REAL |Support |Support |
|VARCHAR |Support |Support |
|JSON |Support |Support |
|TEXT |Support |Support |
|MEDIUMTEXT |Support |Support |
|LONGTEXT |Support |Support |
|VARBINARY |Support |Support |
|BINARY |Support |Support |
|TINYBLOB |Support |Support |
|MEDIUMBLOB |Support |Support |
|LONGBLOB |Support |Support |
|ENUM |Support |Support |
|Blob |Support |Support |
|SET |Support |Support |
|BOOLEAN |Support |Support |
|BIT |Support |Support |
|DATE |Support |Support |
|DATETIME |Support |Support |
|TIMESTAMP |Support |Support |
|TIME |Support |Support |
|YEAR |Support |Support |
|MULTIPOLYGON |Support |Not supported |
|LINESTRING |Not supported |Not supported |
|POLYGON |Not supported |Not supported |
|MULTIPOINT |Not supported |Not supported |
|MULTILINESTRING |Not supported |Not supported |
|GEOMETRYCOLLECTION |Not supported |Not supported |


<span id="_4-数据同步任务开发"></span>
## 4 Data synchronization task development

<span id="_4-1-数据源注册"></span>
### Data source registration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In projects using <strong>Multi\-environment mode</strong>, the datasource can achieve registration isolation between the development environment and the production environment. When performing batch integration task configuration, data source information for all environments must be registered. See details about the New Data Source Action in <a href="https://docs.byteplus.com/docs/dataleap/configure_datasource#_2-%E6%96%B0%E5%BB%BA%E6%95%B0%E6%8D%AE%E6%BA%90">2 New Data Source</a>.</div>


The following provides configuration information for MySQL data sources for different access methods:


1. **Volcengine MySQL data source**

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When reading MySQL data offline, the configured account must have read (SELECT) permission for the table to be synchronized.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When performing offline writes to MySQL data, the configured account must have write permissions (INSERT, DELETE, and UPDATE) on the synchronization table.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To use this MySQL data source in the data synchronization solution and configure the real\-time solution to read the binlog, you must first execute the following authorization SQL command for the configured account: <code>GRANT SELECT, SHOW DATABASES, REPLICATION SLAVE, REPLICATION CLIENT ON</code><strong><code>*</code></strong><strong><code><em>.*</em></code></strong><code>TO 'user' IDENTIFIED BY 'password';</code>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When configuring a VeDB data source for the data synchronization solution, you must execute the following authorization SQL command for the user configured in the data source:<code>GRANT SELECT, REPLICATION SLAVE, REPLICATION CLIENT ON</code><strong><code>*</code></strong><strong><code><em>.*</em></code></strong><code>TO 'user' ;</code>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For details on network\-related configuration, see the above <a href="https://docs.byteplus.com/docs/dataleap/69127#_2-%E4%BD%BF%E7%94%A8%E5%89%8D%E6%8F%90">2 Usage prerequisites</a>explanation.   </div>
   

   
   |Parameters |Note |
   |---|---|
   |Basic configuration ||
   |Data source types |MySQL |
   |Access methods |Volcengine MySQL |
   |Data source name |The data source name can be set as needed. Only Chinese characters, English letters, numbers, and underscores are supported, and the name must be no more than 100 characters in length. |
   |Parameter configuration ||
   |RDS instance ID |Select the Volcengine Cloud Database MySQL instance ID from the dropdown. |
   |Database name |In the dropdown menu under the instance, select the name of an existing MySQL database. |
   |Username |Information about usernames authorized to access the database. |
   |Password |Enter the password information for the username. |
   

2. **MySQL data source in connection string form**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Connection string mode supports accessing MySQL data source instances across accounts and regions. You can establish network connectivity between the dedicated integration resource group and the data source instance via the public network or <a href="https://docs.byteplus.com/en/docs/cen/Product-Overview-01">CEN Cloud Enterprise Network</a>, ensuring network interoperability. For details on network interoperability operations, see <a href="https://docs.byteplus.com/docs/dataleap/network_connectivity_solution">Network connectivity solution</a>.   </div>
   

   
   |Parameters |Note |
   |---|---|
   |Basic configuration ||
   |Data source types |MySQL |
   |Access methods |Connection string |
   |Data source name |The name of the data source can be set by the user. Only Chinese characters, English letters, numbers, and the "_" character are supported, with a maximum length of 100 characters. |
   |Parameter configuration ||
   |Hostname or IP address |Enter the host name or IP address of the MySQL database.<br><br>You can also enter custom domain names mapped through **Volcengine Private Zone**. For details, see the **Private Network Resolution** documentation. |
   |Port |The port number of the host. |
   |Database name |Enter the name of the existing MySQL database. |
   |Username |Username information for users with permission to access the database. |
   |Password |Enter the password corresponding to the username. |
   


<span id="_4-2-新建任务"></span>
### Create tasks

After successfully testing the connectivity of the MySQL data source, enter the data development interface and begin creating new MySQL\-related channel tasks.

For details about methods for creating a new task, see [Batch data synchronization](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization) and [Streaming data synchronization](https://docs.byteplus.com/docs/dataleap/streaming_data_synchronization).

<span id="_4-3-可视化配置说明"></span>
### 4.3 Visual configuration instructions

After the task is created successfully, you can configure channel tasks such as **MySQL batch read, MySQL batch write** or **MySQL streaming write**, depending on your needs.

<span id="_4-3-1-mysql-批式读"></span>
#### 4.3.1 MySQL batch read

Select MySQL as the data source and complete the configuration of the following related parameters:

Parameters with an asterisk (\*) before the name are required, while those without an asterisk are optional.


|Parameters |Note |
|---|---|
|\*Data source type |Select the MySQL data source type from the dropdown. |
|\*Data source name |MySQL data sources that have been successfully registered in data source management are available for selection from the dropdown menu. If you have not yet created the corresponding data source, click the **Data Source Management** button to go to the page for creating a MySQL data source. |
|\*Data table |Select the data tables to be collected. You can select multiple tables with the same schema for data synchronization. Range expressions such as “**table_[0\-99]** ” and date expressions such as “**table_${date}** ” are supported, allowing you to quickly configure and select multiple tables. |
|Database and table sharding |MySQL supports reading data from sharded databases and tables. Click the **Add Sharded Database/Table** button to add sharded databases and tables. In the dropdown menu, select the sharded database data source and the specific table name. You can add multiple sharded databases and tables.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configuring database and table sharding, the schema information for all tables must be consistent; otherwise, the task will not execute properly.</div><br> |
|Data filtering |You can set filter conditions for the data to be synchronized, so that only data meeting the specified criteria will be synchronized. Enter the filter SQL statement that would follow the where keyword, for example: create_time \> '${date}'. Do not include the where keyword itself.<br><br>After completing the statement, you can click the **Validate** button on the right to validate the filter statement.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This filter statement is typically used for incremental synchronization. Filtering using the limit keyword is not currently supported, and its SQL syntax must match the selected data source type.</div><br> |
|Split and build workflows |Shard data based on the configured fields. It is recommended to use the primary key or an indexed column as the shard key:<br><br><br>* If the table does not have a primary key or index column, you can leave this field unconfigured. The synchronization task will not perform sharding and will synchronize all data using a single concurrent process.<br><br>* It is recommended to use a primary key or an indexed column as the split key. If a non\-indexed column is configured as the split key, the synchronization task will be relatively slow.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only fields of type integer or string are supported as split keys.</div><br> |


<span id="_4-3-2-mysql-批式写"></span>
#### 4.3.2 MySQL batch writing

Select MySQL as the data destination and configure the following relevant parameters:

Parameters with an asterisk (\*) before their name are required parameters; parameters without an asterisk are optional parameters.


|Parameters |Note |
|---|---|
|Target types |Select MySQL as the data destination type. |
|\*Data source name |MySQL data sources registered in the data source management interface can be selected from the dropdown menu. If you have not yet created the corresponding data source, you can click the **Data Source Management** button to go to the page for creating a MySQL data source. |
|Data tables |The name of the table in the data source into which data will be written, selectable from a dropdown menu. |
|Statements to prepare before writing |SQL statements that must be executed first, prior to running this data integration task, typically to ensure idempotency when the task is rerun.<br><br>For example, you can clear certain old data from the table by writing a statement. After the clearing is complete, you then execute the integration task to write new data. To delete data where date='${date}': `delete from table_name where date='${date}'`<br><br>You can simply configure multiple statements to be executed before writing, separated by a semicolon (";"). After you have finished entering the statement, you can click the **Validate** button on the right to check whether the statement is logically correct. |
|Prepared statements after a write operation |SQL statements executed after performing a data synchronization task. For example, after the write operation is completed, insert a special data item to indicate that the import task has been completed.<br><br>You can configure multiple post\-write preparation statements; separate them with an English semicolon (“;”). After completing the statement, you can click the **Validate** button on the right to check whether the statement is logically valid. |
|Data writing methods |Methods for writing data to MySQL (dropdown):<br><br><br>* insert into: When a primary key or unique index conflict occurs, the conflicting row cannot be inserted, and the task will fail to run.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure that the task continues to execute normally when there is a primary key or unique index conflict, you can add the advanced parameter <code>job.writer.is_insert_ignore</code> and set it to <code>true</code>.   </div><br>   <br><br>* on duplicate key update:<br><br>   * When there is no conflict with the primary key or unique key index, it behaves the same as `insert into`.<br><br>   * When a conflict occurs, the new row data will be used to update the existing data in the table.<br><br>* replace into:<br><br>   * When there is no conflict with the primary key or unique key index, the behavior is the same as that of `insert into`.<br><br>   * When a primary key or unique key conflict occurs, delete the existing row first, then insert the new row. This means that the new row will replace all field data of the original row. This approach is not recommended, as it may cause issues with data identification during writing and result in dirty data. |
|Update column settings |When the data write method is set to **on duplicate key update** and a primary key or unique key conflict occurs, you can choose to **update all columns** or **update only some columns** as needed:<br><br><br>* Update all columns: When a conflict occurs, all columns in the current row will be updated.<br><br>* Partial column update: You must select the columns. Only the selected columns will be updated in the event of a primary key or unique key conflict. Columns that are not selected will retain the original data in the table and will not be updated. |


<span id="_4-3-3-mysql-流式写"></span>
#### 4.3.3 MySQL streaming write

Supports configuring streaming write to a single MySQL table using a visual interface. MySQL Writer connects to the MySQL database remotely through JDBC, executes the corresponding SQL statements, and writes data to MySQL. The configuration for streaming writes to MySQL is as follows:

Select MySQL as the data target and configure the following parameters:

Parameters with an asterisk (\*) before their names are required, while those without an asterisk are optional.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data is streamed into MySQL, with the default write method being Upsert.</div>



|Parameters |Note |
|---|---|
|\*Target types |Select MySQL as the data destination target type |
|\*Data source name |MySQL data sources registered in the data source management interface can be selected from the dropdown. If the corresponding data source has not yet been created, you can click the **Data Source Management** button to create a MySQL data source. |
|\*Data tables |The name of the table under the data source into which data will be written can be selected from the dropdown menu. |


<span id="_4-3-4-字段映射"></span>
#### Field mapping

After configuring the data source and target, you need to specify the field mapping between the source and target. Based on this mapping, the data integration task writes data from the source fields to the corresponding fields in the target.

You can choose **basic mode** or **transition mode** when configuring field mapping:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Switching between basic mode and transition mode is not supported. After switching modes, all configuration information in the current field mapping will be cleared. This operation cannot be undone, so proceed with caution.</div>



* Transition mode:

   Field mapping supports data conversion. You can configure data transformation according to your actual business needs, so that data collected from the source is first converted and then entered into the target database in the specified format.

   For detailed operating instructions for convert mode, see details [4.1 The Transition mode](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization#9180ba09)

   In Convert Mode, you can configure the following in order: Source Node, data conversion, and Target Node Information.

   
   |Configuration node |Description |
   |---|---|
   |Source node |Configuration: Node information for the Source data source:<br><br><br>* Enter the node name for a custom input source. Only numbers, letters, underscores, hyphens, and periods are allowed; the length must not exceed 10 characters.<br><br>* Data fields: Add data source field information by **Add Automatically, Add Manually** and other methods.<br><br><br>After the configuration is complete, click the **OK** button to complete the Source Node configuration. |
   |Data conversion |Click the **Add** button to the right of Data Conversion, choose the **SQL transform** method, and configure the conversion information and rules:<br><br><br>* Node name: Enter a custom node name for the input source. Only numbers, letters, underscores, hyphens, and periods are allowed, and the length must not exceed 10 characters.<br><br>* SQL script: Enter the SQL script conversion rule. Currently, only one converted SQL statement can be added, and it cannot include ";".<br><br><br>After the configuration is complete, click the **OK** button to complete the data conversion node configuration. For SQL script examples, see [4.1.2 Add a Transition node](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization#59a6e8f0). |
   |Target node |Configure target node Sink information:<br><br><br>* Node name: Information about the custom input source node name. Only numbers, letters, underscores, hyphens, and periods are allowed, and the length must not exceed 10 characters.<br><br>* Data field: Add data destination field information using **add automatically, add manually**, and other methods.<br><br><br>After the configuration is complete, click the **OK** button to complete the target node configuration. |
   

* Basic mode:

   You can manage field mapping relationships in the following three ways:

   * Auto add: Click the **Auto add** button. Based on the information from the source and target data tables, the source and target field information can be automatically populated.

   * Manual addition: Click the **Manual Add** button to manually edit the field information for the source and target, and add fields one at a time.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The source field information supports entering database functions and constants. Click the <strong>Add Manually</strong> button, enter the value to be added in the source table field, and select either the function or constant type, for example:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Functions: You can enter now(), current_timestamp(), unix_timestamp(), and many other functions supported by the MySQL database.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Constants:      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can define custom input constant values, such as '123', '${DATE}', '${hour}', and more. Each input value must be enclosed in single quotation marks. You can also use them in combination with <a href="https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252">Description of platform time variables and constants</a>.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When configuring database and table sharding, you can also manually add constant fields in the form of ${database}_${table} or ${database}.${table} to write the source database and table information for each shard into the corresponding fields of the target table.      </div>
      

   * Move or delete fields: You can also change the order of field mappings or delete fields as needed.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the source uses database and table sharding, the metadata for the first configured table will be retrieved.      </div>
      

<span id="_4-4-dsl-配置说明"></span>
### 4.4 DSL configuration instructions

MySQL data sources can be configured using script mode (DSL).

In certain complex scenarios, you can run data integration tasks by using task scripts to write parameter scripts for MySQL Reader and MySQL Writer in a unified JSON format.

<span id="_4-4-1-进入-dsl-模式"></span>
#### Enter DSL mode


1. In the visual task editing interface, click the **Switch to script mode** button in the top toolbar to enter the editing interface.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Switching to script mode will clear the current visual interface configuration. Once you switch, this action cannot be undone.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a948b4e4d65a4672bd4dfec89d726b2a~tplv-goo7wpa0wc-image.image) </span>

2. When configuring DSL mode for the first time, you can click the **Import Script Template** button on the interface. Based on the template, make the necessary configuration changes to improve task configuration efficiency.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40ca81c40f144b9780ba479ee4853d41~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Importing a new script template will clear existing content; once imported, this action cannot be undone.   </div>
   

   Below are example scripts that respectively introduce batch reading and batch writing with a MySQL data source. You can replace the relevant parameters as needed.


<span id="_4-4-1-mysql-批式读"></span>
#### 4.4.1 MySQL batch read

Example of a MySQL batch read script:

```json
// The rules for using variables are as follows:
// 1. Custom parameter variable: {{}}, for example, {{number}}
// 2. System time variables ${}, for example, ${date} and ${hour}
// **************************************
{
    // [required] dsl version, suggest to use latest version
    "version": "0.2",
    // [required] execution mode, supoort streaming / batch now
    "type": "batch",
    // reader config
    "reader": {
        // [required] datasource type
        "type": "mysql",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": 12345,
        // [required] user parameter
        "parameter": {
            // ********** please write here **********
            // "key" : value
            "columns": [
                {
                    "name": "name_sample",
                    "type": "type_sample"
                }
            ],
            "filter": "id > 10",
            "split_pk": "split_pk_sample",
            "table_name": "table_name_sample"
        }
    },
    // writer config
    "writer": {
    },
    // common config
    "common": {
        // [required] user parameter
        "parameter": {
            // ********** please write here **********
            // "key" : value
        }
    }
}
```


Note: In the Reader parameter description, parameters with an asterisk (\*) before the name are required, while those without an asterisk are optional:


|Parameter name |Description |Default value |
|---|---|---|
|\*type |Data source type: For MySQL, enter "MySQL". |None |
|\*datasource_id |The ID of the registered MySQL data source. You can find it in the **Project Console \> Data Source Management** interface. |None |
|\*table_name |Name of the data table to be synchronized. Each data integration task can only synchronize data to one target table. The MySQL source supports configuring multiple tables or range reads.<br><br><br>* Configure multiple tables. Tables are separated by `,`, for example, `table0,table1`.<br><br>* Instructions for range reading configuration:<br><br>   * "table_[0\-99]" indicates that data will be exported from a total of 100 tables: table_0, table_1, ..., up to table_99.<br><br>   * table_[00\-99] represents exporting the data from 100 tables: table_00, table_01, through table_99. |None |
|filter |Filter criteria for data synchronization: only data that meets the filter conditions will be synchronized. Enter the SQL filter statement directly after the keyword 'where'.<br><br><br>* If the filter condition is set to: `date>=${date}`, this means that only records where date is greater than or equal to ${date} will be synchronized.<br><br>* Filter conditions can be used to effectively perform incremental synchronization of business data. If no configuration is set, all data will be synchronized by default. |None |
|split_pk |Data is sharded based on the configured fields. It is recommended to use the primary key or an indexed column as the sharding key. The synchronization task will launch concurrent tasks to synchronize data and improve the synchronization rate:<br><br><br>* If the table does not have a primary key or index column, you can leave this field unconfigured. The synchronization task will not perform sharding and will synchronize all data in single concurrency mode.<br><br>* It is recommended to use a primary key or an indexed column as the split key. If a non\-indexed column is configured as the split key, synchronization tasks will be slower.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only fields of integer or string type are supported as partition keys.</div><br> |None |
|\*columns |In the configured table, the set of column names that need to be synchronized is described using a JSON array.<br><br><br>* Support column pruning: You can export only selected columns.<br><br>* Supports column reordering: columns can be exported in an order different from the order defined in the table schema.<br><br>* The column must display the specified set of columns for synchronization and cannot be empty.<br><br>* Supports adding columns using functions or constants:<br><br>   * Function<br><br><br>MySQL Reader supports input of functions such as now(), current_timestamp(), unix_timestamp(), and other functions supported by the MySQL database.<br><br><br>* Constant: MySQL Reader allows you to define custom constant values, such as '123', '${DATE}', and '${hour}'. Each value must be enclosed in single quotes, and you can use this in combination with [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |None |


<span id="_4-4-2-mysql-批式写"></span>
#### 4.4.2 MySQL batch write

MySQL batch write script example:

```json
// **************************************
// Variable usage rules are as follows:
// 1. Custom parameter variable: {{}}, for example {{number}}
// 2. System time variables ${}, for example, ${date}, ${hour}
// **************************************
{
    // [required] dsl version, suggest to use latest version
    "version": "0.2",
    // [required] execution mode, supoort streaming / batch now
    "type": "batch",
    // reader config
    "reader": {
        // [required] datasource type
        "type": "xx",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": null,
        // [required] user parameter
        "parameter": {
            // ********** please write here **********
            // "key" : value
          
        }
    },
    // writer config
    "writer": {
        // [required] datasource type
        "type": "mysql",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": 12345,
        // [required] user parameter
        "parameter": {
            // ********** please write here **********
            // "key" : value
            "table_name":"table_1",
            "pre_sql_list":[""],
            "post_sql_list":[""],
            "write_mode":"overwrite",
            "columns": [
                {
                    "name": "name_sample",
                    "type": "type_sample"
                }
            ]
        }
    },
    // common config
    "common": {
        // [required] user parameter
        "parameter": {
            // ********** please write here **********
            // "key" : value
        }
    }
}
```


Description of Writer parameters: Parameters with an asterisk (\*) before the name are required; those without an asterisk are optional.


|Parameter name |Description |Default value |
|---|---|---|
|\*type |Data source type: For MySQL, enter 'MySQL'. |None |
|\*datasource_id |Registered MySQL data source ID. You can find it in the **Project Console \> Data Source Management** interface. |None |
|\*table_name |Enter the name of the table under the data source to which data will be written. |None |
|pre_sql_list |Pre\-write preparation statement: An SQL statement executed prior to performing a data integration task. This statement is typically used to ensure idempotency when rerunning a task. You can configure multiple preparation statements before writing, separated by English semicolons (“;”).<br><br>For example, clear certain old data from the table before execution. After clearing is complete, execute the integration task to write new data. For example, to delete data where date='${date}': `["delete from table_name where date='${date}'";"xxx"]` |None |
|post_sql_list |Post\-write preparation statements: SQL statements executed after a data synchronization task is performed. For example, after data writing is complete, you can insert a special data entry to indicate that the import task has finished. You can configure multiple post\-write preparation statements, which should be separated by semicolons (';').<br><br>Example: `["insert into table_name (col1,col2..) values(values1,values2)";"xxx"]` |None |
|\*write_mode |The data import mode supports three modes: insert into, on duplicate key update, and replace into.<br><br><br>* insert into: If a primary key or unique index conflict occurs, the conflicting rows cannot be inserted, and the task will fail.<br><br>   * When using this mode, please set `write_mode` to `directlyInsert`.<br><br>   * If you want the task to continue executing normally when a primary key or unique index conflict occurs, you can add the advanced parameter `job.writer.is_insert_ignore: true` under the `writer.parameter` parameter.<br><br>* on duplicate key update: When there is no primary key or unique index conflict, the behavior is the same as that of `insert into`. When a conflict occurs, the statement replaces the specified fields with values from the new row and writes the data to MySQL.<br><br>   * When using this mode, set `write_mode` to `overwrite`.<br><br>* replace into: When there is no primary key or unique index conflict, its behavior is consistent with `insert into`. When a conflict occurs, the existing row is deleted first, and then a new row is inserted. That is, the new row will replace all fields of the original row.<br><br>   * When using this mode, please set `writer_mode` to `replace`. |None |
|\*columns |Use a JSON array to describe the set of column names to be synchronized in the configured table.<br><br><br>* Column selection: You can select specific columns to export.<br><br>* Support column reordering: Columns can be exported in an order different from the table schema.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The column must display the set of columns specified for synchronization and cannot be empty.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Columns must be aligned with the set of source columns being imported; having more or fewer columns is not allowed.</div><br> |None |


<span id="_4-5-高级参数说明"></span>
### Description of advanced parameters


* For channel tasks, when configuring under **custom parameter settings**, the read parameters must be prefixed with `job.reader.`. Prefix: When specifying parameters, you must add `job.writer.` Prefix: as shown in the following figure:

* For DSL tasks, configure read parameters under `reader.parameter` and write parameters under `writer.parameter`. Enter the parameter names and values directly. As shown in the figure below:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1c6993ed4580ae571983fd10a446797.png) </span>


<span id="_4-5-1-mysql-批式读"></span>
#### 4.5.1 MySQL batch read

Batch read supports the following advanced parameters, which you can configure as appropriate for your situation:


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.init_sql |SQL statements executed before reading data. Queries on views may require using an init SQL statement to initialize the environment. |None |
|job.reader.reader_fetch_size |The number of records fetched each time is only applicable in accurate sharding mode. |10000 |
|job.reader.query_timeout_seconds |Read data using the JDBC method and set the read timeout in seconds. |300 |
|job.reader.shard_split_mode |JDBC connection sharding supports three modes: accurate sharding, concurrent sharding, and no sharding.<br><br><br>* Accurate sharding (default): Data is divided into different ranges based on the configured sharding key. Except for the last range, each range contains exactly reader_fetch_size records. This mode is slower, but it ensures that downstream file sizes are generally consistent.<br><br>   * When pulling tables that contain a large amount of data, or when the sharding key is not a primary key or index key, the sharding time for this mode will be relatively long.<br><br>   * This sharding mode supports shard keys of integer and string data types.<br><br>   * Configuration method: Set this parameter to `accurate`.<br><br>* Non\-precise sharding: This mode is faster, but it cannot guarantee that downstream file sizes will be consistent.<br><br>   * This sharding mode only supports sharding keys of the integer data type.<br><br>   * When the parameter is set to `parallelism`: Based on the table's maximum and minimum values, all data is partitioned into intervals according to the number of concurrent executions.<br><br>   * When the parameter is set to `quick`, fuzzy partitioning is performed based on reader_fetch_size.<br><br>* No sharding: Sharding is not performed. This option is suitable for tables with a small amount of data, or for tables that do not have a primary key or index key.<br><br>   * Configuration method: Set this parameter to `nosplit` or do not configure the parameter `split_pk`. |Accurate partitioning |
|job.reader.customized_sql |Read SQL statements for custom queries. The filter configuration option is not sufficient to describe the selection criteria. You can use this configuration option to customize and execute more complex SQL queries.<br><br>For example, if you need to synchronize data after performing a multi\-table join, use `select a, b from table_a join table_b on table_a.id = table_b.id`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After configuring this advanced parameter, you still need to configure required configuration items for the data synchronization task, such as table_name, column, split_pk, and shard_split_mode. However, when synchronization is performed, the system ignores this configuration item information and directly uses the content configured in the advanced parameter item to query and filter data.</div><br> |None |


<span id="_4-5-2-mysql-批式写"></span>
#### 4.5.2 MySQL batch write

Batch writing supports the following advanced parameters, which you can configure as needed:


|Parameter name |Description |Default value |
|---|---|---|
|job.writer.is_insert_ignore |In insert into mode, when a primary key or unique key conflict occurs, the task either fails or ignores the conflict depending on the setting: if set to false, the task fails; if set to true, conflicts are ignored and the task continues as normal. |false |
|job.writer.write_batch_interval |The number of data records submitted in a single batch. This value can reduce the number of network interactions with MySQL and improve overall throughput. If this value is set too high, it may cause the data synchronization process to run out of memory (OOM). |100 |
|job.writer.write_retry_times |Number of retries when MySQL write fails. |3 |
|job.writer.retry_interval_seconds |The interval between retry attempts after a write failure, in seconds. |write_batch_interval / 10 |
|job.writer.connection_parameters |All JDBC connection parameters. Additional parameters can be appended after the default values:<br><br><br>* tcpRcvBuf is used when reading a large amount of data in a single line:<br><br>   tcpRcvBuf=1024000 （1MB）<br><br>* allowMultiQueries enables support for multiple SQL statements separated by semicolons:<br><br>   allowMultiQueries=true<br><br>* connectTimeout Connection timeout period, in milliseconds:<br><br>   connectTimeout=60000 |autoReconnect=true&useUnicode=true&characterEncoding=utf\-8&useSSL=false&zeroDateTimeBehavior=convertToNull |


<span id="_5-最佳实践"></span>
## 5 best practices

<span id="_5-1-mysql-离线写实现-ttl"></span>
### 5.1 The MySQL offline write implementation for TTL

Offline task write to MySQL method: Only the most recent day's data is stored in the MySQL data table


1. Configure pre\-write statements:

   Assume the table name is table_name and the TTL field is date. To retain only the most recent day's data, enter the following statement: `delete from table_name where`date`<= "${date-1}"`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">date is a database keyword, so it needs to be escaped using backticks (`).   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d7b399a669b4f4d81e1b84a7c6034ba~tplv-goo7wpa0wc-image.image) </span>

2. The data writing method is configured as `insert into`.


<span id="_5-2-mysql-离线写实现幂等"></span>
### 5.2 Implement idempotency for MySQL offline writes

For offline writes to MySQL, when using the `insert into` write method, rerunning the task may result in two possible outcomes:


1. Rerun failed: The task failed to write to fields that are configured as a primary key or unique key due to a duplicate key error.

2. Data duplication: No primary key is configured in the write fields, resulting in duplicate data being written.


Therefore, to ensure idempotency when rerunning tasks, the following solutions can be considered:


1. Change the data writing method to `on duplicate key update` or `replace into`.

2. Use `insert into`, and set the advanced parameter `job.writer.is_insert_ignore` to `true`.


<span id="5aff6e49"></span>
### 5.3 Write data to multiple MySQL partitioned tables

One of the paths in TOS

Data from a source table or a file can be written to multiple MySQL sharded tables by configuring the relevant advanced parameters.

**Prerequisites:** 

Before executing a task, you must create a Schema Table that matches the data structure of the source table, file, and other data sources, based on their data. In the visual configuration interface on the target side, select this Schema Table as the target table. When mapping fields, you must include a complete mapping for all fields from the source table.

Caution: The target table selected in the visual configuration is only a nominal target table; data will not actually be written to this table. The name of the actual target table where data is written must be defined using the advanced parameter `job.writer.table_pattern` below.

**Advanced parameter configuration:** 


|Parameter name |Description |Default value |
|---|---|---|
|job.writer.table_pattern |Required.<br><br>This parameter allows you to reference a field name from the source table as part of the target table name. For example, if the source table or source TOS file contains a field named table_name, then "${table_name}" indicates that, at runtime, the value of this field from each data record will be automatically used to construct the target table name string.<br><br>Configuration example: job.writer.table_pattern=${table_name}_copy |None |
|job.writer.internal_columns |Optional.<br><br>This parameter allows you to specify that certain field data from the source table will not be written to the target table. For example, the table_name field, which has already been selected as the target table name, does not need to appear in the data fields actually written to the target table. You can configure this parameter as: job.writer.internal_columns=[ "table_name" ] |None |
