---
title: "Hive Data Source"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/hive_data_source"
---

Hive is commonly used to store structured data, and it uses HDFS as its underlying storage system. DataSail provides data synchronization functionality in two ways: based on HDFS files and based on JDBC.


* Data synchronization based on HDFS files (supports reading and writing in Hive): The Hive reader obtains the underlying storage path of the specified Hive table from HMS (Hive Metastore Service), then directly reads and writes the underlying HDFS files, and finally synchronizes the metadata with HMS.

* JDBC\-based data synchronization (only supports Hive reading): The Hive reader connects to the HiveServer2 service using a JDBC client to read data.


<span id="_1-支持的版本"></span>
## 1 Supported versions


* Volcengine E\-MapReduce (EMR) Hive, EMR Serverless Hive data sources

* The connection string format supports Hive version 3.1.2.


<span id="_2-使用前提"></span>
## 2 Prerequisites for use


1. To create a new data source as a sub\-account, you must have the project administrator role in order to perform the **create data source** operation. Explanation of permissions for each role. For details, see [Manage Member Information](https://docs.byteplus.com/docs/dataleap/manage_project_member)

2. To access the Volcengine EMR Serverless Hive data source, you must first create the relevant queue resources in the EMR Serverless Spark console. For details, see [Queue Management](https://www.volcengine.com/docs/6491/1262219).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">EMR Serverless Spark is currently available only to whitelisted users. You can contact EMR support staff by <a href="https://console.volcengine.com/workorder/create">submitting a ticket</a>, and use the service after backend activation.   </div>
   

3. When configuring a Hive data source and selecting the EMR Hive access method, you need to provide EMR cluster information and database\-related information. You must first create an EMR Hadoop cluster type, and ensure that the cluster has a component service installed that includes OSSA.

4. To access the Volcano Engine EMR\-Hive data source, you must first bind the relevant EMR\-Hadoop cluster in **Project Console \> Service Binding \> Engine Binding**. For details, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

5. The VPC used by the EMR Hadoop cluster must be the same as the VPC in the dedicated integration resource group:

   * The subnets and security groups under its VPC should also be kept as consistent as possible.

   * If the VPCs are different, you need to add the IP range for the subnet of the dedicated integration resource group to the inbound rules of the Hadoop cluster's security group:

      1. On the EMR Hadoop cluster details page, go to the security group associated with the cluster, and add an inbound rule.

      2. In the popup window, enter the CIDR block information of the VPC where the dedicated integration resource group is located:


<span id="d6492a6e"></span>
## 3 Usage restrictions


* Offline reading:

   * For offline reading based on JDBC, you need to properly configure valid SQL statements. However, the data source integration method of EMR Serverless Hive does not currently support JDBC reading.

   * When the read method for the Hive data source is set to HDFS mode:

      * The Hive component version within the EMR Hadoop cluster must be 3.X.

      * Source fields that are manually added in field mapping do not support the configuration of functions or constants.

* Offline writing:

   * Currently, only offline writing based on HDFS files is supported.

   * A single execution can write to only one partition.

   * It is not currently supported for multiple offline or real\-time data integration tasks to write data to the same Hive table simultaneously.

* Real\-time writing:

   * Although data is written to Hive in near real time, due to partition visibility restrictions in Hive, by default, data written today can only be queried in Hive starting from T+1 (the next day). For example, a Hive table with day\-level partitions can be queried on the second day after the task is started, while a Hive table with hour\-level partitions can be queried in the second hour after the task is started.

      If you are interested in the principles behind this feature, you can refer to the following article: [ByteDance's real-time MQ-Hive data integration based on Flink – Big Data, ByteDance Technical Team, InfoQ Featured Article](https://www.infoq.cn/article/9uudtyzzprpqssb0x9hk)

   * Currently, writing data to the same Hive table simultaneously from multiple offline or real\-time data integration tasks is not supported.

   * If your business scenario requires viewing data in real time, you need to configure the following two parameters in Advanced Parameters:

      * Pre\-create partitions: job.writer.partition_strategy=partition_last;

      * Refresh data to Hive every minute: job.common.checkpoint_interval = 60000

         For details, see[6 高级参数可选配置](https://docs.byteplus.com/docs/dataleap/69123#_6-%E9%AB%98%E7%BA%A7%E5%8F%82%E6%95%B0%E5%8F%AF%E9%80%89%E9%85%8D%E7%BD%AE)


<span id="_4-支持的字段类型"></span>
## 4 Supported field types

Hive Reader and Writer obtain the metadata of the target Hive table through HiveServer2, allowing them to retrieve the type of each field and automatically complete the schema configuration for the task. Users only need to click **Auto Add** to complete the schema configuration.


|**Type classification** |**Column configuration types for data integration** |
|---|---|
|Integer types |tinyint、smallint、int、bigint |
|Floating point class |float、double、decimal |
|String class |string |
|Time class |date、timestamp |
|The Boolean class |boolean |
|Array classes |array |
|Dictionary classes |map |
|Binary types |binary |


<span id="_5-数据同步任务开发"></span>
## 5 Data synchronization task development

<span id="_5-1-数据源注册"></span>
### 5.1 Data source registration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在<strong>多环境模式</strong>的项目下，数据源能够开发环境与生产环境实现注册隔离。并且在进行离线集成任务配置时，多环境下的数据源信息均需要进行注册。新建数据源操作详见<a href="https://docs.byteplus.com/docs/6260/79676#_2-%E6%96%B0%E5%BB%BA%E6%95%B0%E6%8D%AE%E6%BA%90">2 新建数据源</a>。</div>


The following provides information about configuring Hive data sources for different access methods:


1. **EMR\-Hive data source**

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The VPC of the EMR Hadoop cluster must be the same as the VPC of the dedicated integration resource group to ensure mutual network access. For different VPC scenarios, see the relevant details in "<a href="https://docs.byteplus.com/docs/dataleap/69123#_2-%E4%BD%BF%E7%94%A8%E5%89%8D%E6%8F%90">2 使用前提</a>".   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">DataSail uses the <strong>root account</strong> to read and write EMR Hive table data, so the username and password fields in the data source configuration can be left blank.   </div>
   

   Parameters with an asterisk (\*) before their name are required parameters, while those without an asterisk are optional parameters.

   
   |Parameters |Note |
   |---|---|
   |Basic configuration ||
   |\*Data source types |Hive |
   |Access methods |EMR Hive |
   |\*Data source name |The name of the data source can be set by the user. It supports only Chinese, English letters, numbers, and the underscore (“_”), and must be no more than 100 characters long. |
   |Parameter settings ||
   |\*Authentication methods |When accessing a Hive data source, you can use **Kerberos** as the identity authentication method; if authentication is not required, select **None** as the authentication method.<br><br>For Kerberos authentication, you need to upload **the keyTab file and the conf file** to the data source configuration interface and enter the relevant principal authentication information. |
   |\*EMR cluster ID |Select the name of a successfully created EMR Hadoop cluster from the dropdown. If you have not yet created the relevant cluster, you can go to [EMR-控制台](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/home) to create it. For details, see [Create a cluster](https://www.volcengine.com/docs/6491/72162). |
   |\*Database name |In the drop\-down list, select the name of an existing Hive database in the cluster environment. |
   |The Hive version number |Based on the selected EMR Hadoop cluster, the Hive versions included in the cluster are automatically displayed. |
   |Username |Username information for users with permission to access the database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you subsequently configure Hive offline reading using visual configuration and read data via JDBC, you must enter the <strong>username</strong> and <strong>password</strong> in the configuration information for both EMR\-Hive and connection string\-based access.</div><br> |
   |Password |Enter the password for the username. |
   |The \*keyTab file |When Kerberos authentication is selected as the authentication method, the keyTab configuration file must be uploaded. |
   |\*conf files |When Kerberos authentication is selected as the authentication method, you need to upload the conf configuration file. |
   |\*principal |When Kerberos authentication is used, you must enter the Principal identity information. |
   |Access Key ID |When a task reads from or writes to Hive tables configured as Hive on TOS, the Access Key ID and Secret Access Key fields are required for TOS authentication. You must have read and write permissions for the TOS Bucket. For details about bucket permission policy operations, see [Bucket policy templates and parameter descriptions](https://www.volcengine.com/docs/6349/102127).<br><br>You can go to the [Key Management interface](https://console.volcengine.com/iam/keymanage/) in the Volcano Engine Access Console, copy the AccessKey ID, and enter it here. If you are a sub\-user, please contact the main account to obtain the key. |
   |Secret Access Key |Used together with AccessKey ID, it functions similarly to a login password and is used to sign your access parameters to prevent tampering. |
   |Extension configurations |You can enter optional extensions for HDFS configuration, for example, configuration information for Hadoop HA. |
   

2. **EMR Serverless Hive data source**

   Parameters with an asterisk (\*) before the name are required parameters; those without an asterisk are optional parameters.

   
   |Parameters |Note |
   |---|---|
   |Basic configuration ||
   |\*Data source type |Hive |
   |Access methods |EMR Serverless Hive |
   |\*Data source name |The name of the data source can be set by the user and may only contain Chinese characters, English letters, numbers, or underscores, with a maximum length of 100 characters. |
   |Parameter configuration ||
   |Hive version number |By default, only Hive 3.1.3 is supported. |
   |\*Accesskey ID |Go to Volcengine, access the console's [Key Management interface](https://console.volcengine.com/iam/keymanage/), copy the AccessKey ID, and enter it here. If you are a sub\-user, please contact the main account to obtain the key.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The AK/SK information you entered requires the following corresponding permissions:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="warning">You must have read and write permissions for the corresponding Hive database tables. The main account or the database Owner can go to the LAS Catalog console to grant these permissions. For details, see <a href="https://www.volcengine.com/docs/6492/1264534">LAS Catalog Permission Management</a>.</div><br><br><br>2. <div data-tips="true" data-tips-type="warning">You need to have <strong>bucket read and write</strong> permissions for the TOS Bucket specified as the underlying storage path in LAS Catalog. For details on bucket permission policy operations, see <a href="https://www.volcengine.com/docs/6349/102127">Bucket policy template and parameter descriptions</a>.</div><br> |
   |\*Secret Access Key |Used together with the AccessKey ID, it functions similarly to a login password and is used to sign your access parameters to prevent tampering. |
   |Catalog |From the dropdown, select the names of Catalog data directories that have already been created in the LAS Catalog service. |
   |\*database name |After entering the AK/SK information above, use this dropdown list to select an existing Hive database name in the corresponding Catalog directory. |
   |Extension configuration |You can enter optional configuration items for HDFS, for example, configuration information for Hadoop HA. |
   

3. **Hive data source in connection string form**

   Configure the Hive data source using a connection string. Parameters with an asterisk (\*) before the name are required, while those without an asterisk are optional.

   
   |Parameters |Note |
   |---|---|
   |Basic configuration ||
   |Data source type |Hive |
   |Access methods |Connection string |
   |\*Data source name |The name of the data source can be set by the user. Only Chinese characters, English letters, numbers, and the underscore (_) are supported, and the name must not exceed 100 characters. |
   |Parameter configuration ||
   |Authentication methods |When accessing a Hive data source, authentication using **Kerberos** is supported. If authentication is not required, select **None** as the authentication method.<br><br>Among them, for Kerberos authentication, you need to upload the **keyTab file and conf file** to the data source configuration interface and fill in the relevant principal authentication information. |
   |\*Database name |Enter the name of an existing Hive database. |
   |Username |Username information for users with permission to access the database.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you subsequently configure Hive offline reads using the visual interface and read data via JDBC, you must enter the <strong>username</strong> and <strong>password</strong> in the configuration information for both EMR\-Hive and connection string access.</div><br> |
   |Password |Enter the password information for the username. |
   |The Hive version number |Supports selecting the Hive 3.1.2 version from a dropdown menu. |
   |\*MetaStore URI |Enter the MetaStore URI address for Hive metadata storage in the format thrift://ip1:port,thrift://ip2:port. If there are multiple addresses, separate them with a comma. |
   |\*Hive JDBC URL |Enter Hive JDBC URL connection string information:<br><br><br>* When Kerberos authentication is not used, you must enter: jdbc:hive2://host:port/database<br><br>* When Kerberos authentication is enabled, you need to additionally provide authentication information: jdbc:hive2://host:port/database;principal= your principal |
   |\*KeyTab file |When Kerberos authentication is selected as the authentication method, you must upload the keyTab configuration file. |
   |\*.conf files |When Kerberos authentication is selected as the authentication method, the conf configuration file must be uploaded. |
   |\*principal |When the authentication method is Kerberos authentication, you must enter the Principal identity information for authentication. |
   |defaultFS |Enter the namenode address for Hadoop HDFS files in the format hdfs://ip:port. |
   |Extension configuration |Enter the required HDFS or Hive configuration; no additional configuration is required by default.<br><br>If you need to read data using HDFS in a self\-built high\-availability cluster, you can combine the core\-site.xml and hdfs\-site.xml files from the cluster into a single XML file and submit it. Refer to the following example of extended attribute configuration:<br><br>```XML```<br>```<?xml version="1.0" encoding="UTF-8"?>```<br>```<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>```<br>```<configuration>```<br>```    <property>```<br>```        <name>dfs.namenode.name.dir</name>```<br>```        <value>/data01/hadoop/hdfs/namenode</value>```<br>```    </property>```<br>```    <property>```<br>```        <name>dfs.nameservices</name>```<br>```        <value>test_name</value>```<br>```    </property>```<br>```    <property>```<br>```        <name>dfs.ha.namenodes.test_name</name>```<br>```        <value>namenode1,namenode2</value>```<br>```    </property>```<br>```    <property>```<br>```        <name>dfs.namenode.rpc-address.namenode1</name>```<br>```        <value>xxx.xx.x.xx:port</value>```<br>```    </property>```<br>```    <property>```<br>```        <name>dfs.namenode.rpc-address.namenode2</name>```<br>```        <value>xxx.xx.x.xx:port</value>```<br>```    </property>```<br>```    <property>```<br>```        <name>dfs.client.failover.proxy.provider.test_name</name>```<br>```        <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>```<br>```    </property>```<br>```    <!-- other configure of core-site.xml and hdfs-site.xml -->```<br>```</configuration>```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">In the above configuration example, you need to replace the nameservices and rpc\-address information with the corresponding values for your actual cluster.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When integrating Volcengine EMR HDFS using the high\-availability cluster mode, you do not need to configure any additional high\-availability\-related extended attributes.</div><br> |
   


<span id="_5-2-新建离线任务"></span>
### 5.2 Create an offline task

After successfully testing the connectivity of the Hive data source, go to the data development interface to start creating new Hive\-related channel tasks. For details on the methods for creating a new task, see [离线数据同步](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization) and [流式数据同步](https://docs.byteplus.com/docs/dataleap/streaming_data_synchronization).

<span id="4d6479dc"></span>
### 5.3 Visual configuration instructions

After the task is created successfully, you can, depending on your needs, configure channel tasks such as **Hive offline read**, **Hive offline write**, and other channel tasks.

<span id="a0ddb8be"></span>
#### 5.3.1 Visual configuration for Hive offline reading

Select Hive as the data source, and complete the following parameter settings:

Parameters with an asterisk (\*) before the name are required, while those without an asterisk are optional.


|Parameters |Note |
|---|---|
|\*Data source type |Select the Hive data source type from the dropdown. |
|\*Data source name |Hive data sources that have been successfully registered in data source management can be selected from the dropdown menu.<br><br>If you have not yet created the corresponding data source, you can click the **Data Source Management** button to go to the Hive data source creation page. |
|Data tables |Select the name of the data table from which data will be collected. Currently, each task only supports collecting data from a single table into a single target table.<br><br><br>* Create a table quickly: If the source table has not been created, you can click the **Quick table creation** button to go to the Data Map page and create an EMR Hive table.<br><br>* Modify the data table: If any fields in the source table need to be updated, you can click the **Modify Data Table** button to quickly modify the source table fields.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When EMR Serverless Hive is used as the data source access method, quick table creation and modifying data tables are temporarily not supported. The corresponding operations on the source database tables need to be performed in the <a href="https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/queue_manage">EMR Serverless Spark</a> console.</div><br> |
|Reading methods |Hive supports the following reading methods: “**HDFS\-based**” and “**JDBC\-based**”:<br><br><br>* For HDFS, you must specify the content of the partition field. Only reading from a single partition is supported.<br><br>* Based on JDBC: Data can be read using SQL, with field\-level filtering supported through the WHERE clause.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the JDBC method to read data, and the data source is configured as <strong>EMR\-Hive</strong> or <strong>connection string</strong>, the <strong>username</strong> and <strong>password</strong> in the data source configuration must be specified.</div><br> |
|Partition settings |When reading data using HDFS, the system obtains partition information from the Hive table based on the selected database table and specifies which partitions to read.<br><br><br>* Partition content can be configured using time variable parameters. For details, see [平台时间变量与常量说明](https://docs.byteplus.com/docs/6260/75002).<br><br>* It also supports configuration using the regular expression pattern "2025\-05\-.\*", which means reading all partition data for May 2025.<br><br>* Alternatively, configure the partition content in the form of "2025\-05\-(13<br><br><br>When you need to read data from multiple partitions at the same time, you can also click the **Add Partition** button to configure multiple partitions.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb2b34f0e61e465186167634f393d206~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When reading a Hive table as a non\-partitioned table, you do not need to set partitions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a Hive table partition or partition directory does not exist, the task will read as an empty partition.</div><br> |
|Data filtering |When reading data using JDBC, you can set filter conditions to synchronize only the data that meets your criteria. Enter only the SQL filter condition after the 'where' keyword, without including 'where' or the statement terminator (;). For example: create_time \> '${date}'.<br><br>After you have finished entering the statement, you can click the **Validate** button on the right to validate the filter statement.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This filtering statement is typically used for incremental synchronization. Filtering with the limit keyword is not currently supported, and its SQL syntax must correspond to the selected data source type.</div><br> |


<span id="_5-4-可视化配置-hive-离线写"></span>
#### 5.3.2 Visually configure Hive offline writing

Select Hive as the data target type, and complete the following parameters:

Parameters with an asterisk (\*) before their names are required, while those without an asterisk are optional.


|Parameters |Note |
|---|---|
|Target type |Select the Hive data source type from the drop\-down list. |
|\*Data source name |Hive data sources that have been successfully registered in data source management can be selected from the dropdown.<br><br>If you have not yet created the corresponding data source, you can click the **Data Source Management** button to go to the page for creating a Hive data source. |
|Data tables |Select the name of the Hive table to write data to; selectable from a dropdown list.<br><br><br>* Quick table creation: If the target Hive table has not been created, you can click the **Quick Table Creation** button to go to the data map interface and create EMR Hive and EMR Serverless Hive (LAS Catalog) tables based on the field information collected from the source.<br><br>* Modify data table: If there are updates to the fields collected from the source, you can click the **Modify Data Table** button to update the target table fields in a timely and efficient manner.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the data source access method is EMR Serverless Hive (LAS Catalog), if the target Hive table has not yet been created and the tables to be collected from the source have already been selected, you can also click the "One\-click <strong>Create Table</strong>" button to quickly edit and create the target table's DDL statements in a popup window, based on the field information collected from the source.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">It is currently not supported for multiple offline or real\-time data integration tasks to write data to the same Hive table simultaneously.</div><br> |
|Partition settings |Partition fields are automatically obtained from Hive tables.<br><br>Partition type can be set to either a dynamic partition type or a specific partition field type:<br><br><br>* Dynamic partitioning: Data is written dynamically based on the values of source fields. The fields used for dynamic partitioning must exist in the source columns. After selecting the dynamic partition type, the table partition fields can be automatically added to the field mapping below.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the source field corresponding to the dynamic partition field can be empty. In this case, the synchronization task will write it as a Hive empty partition, represented by an empty string ("").   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Presented in the form of "<strong>HIVE_DEFAULT_PARTITION</strong>".   </div><br>   <br><br>* Specific partition field type: The partition content can be configured to a specific time partition granularity, which can be represented by parameter variables such as ${date}, ${hour}, and others. For details about parameter variables, see [平台时间变量与常量说明](https://docs.byteplus.com/docs/6260/75002). |
|Data writing methods |Select the method for writing target data from the dropdown. The following two methods are supported:<br><br><br>* insert overwrite: Deletes existing data before writing new data;<br><br>* insert into: Directly write new data. |


<span id="_5-5-可视化配置-hive-实时写"></span>
#### 5.3.3 Visual configuration of Hive real\-time write

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b9115d58538a2bba19664ce2c6fa676.png) </span>

Streaming integration tasks write data in real time to a Hive data source. Select Hive as the data target type, and complete the configuration of the following related parameters:

Parameters with an asterisk (\*) before their names are required, while those without an asterisk are optional.


|Parameters |Note |
|---|---|
|\*Target type |Select the Hive data source type from the dropdown. |
|\*Data source name |Hive data sources that have been successfully registered in data source management are available for selection in the dropdown.<br><br>If the corresponding data source has not yet been created, you can click the **Data Source Management** button to go to the page where you can create a Hive data source. |
|Data tables |Select the Hive table name for data writing from the dropdown.<br><br><br>* Quick table creation: If the target Hive table has not yet been created, you can click the **Quick Table Creation** button. This will take you to the data map interface, where you can create an EMR Hive table based on the field information collected from the source.<br><br>* One\-click table creation: When the data source access method is EMR Serverless Hive, if the target Hive table has not yet been created and you have already selected the source table to be collected, you can click the **One\-click table creation** button to quickly edit and create the target table's DDL statement in a popup window, based on the field information collected from the source.<br><br>* Modify the data table: If any fields collected from the source are updated, you can click the **Modify Data Table** button to promptly modify the fields in the target table.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, writing data to the same Hive table simultaneously from multiple offline or real\-time data integration tasks is not supported.</div><br> |
|Partition frequency |Support for day\-level or hour\-level partition frequencies<br><br><br>* Daily partitions: One partition is generated each day<br><br>* Hourly level: A partition is generated every hour<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data is generated based on the time when Hive partitions are created, rather than being written in real time.</div><br> |
|Partition settings |Partition fields are automatically obtained from Hive tables. You can configure the partition content to use a specific time\-based partition granularity, which can be represented using expressions with parameter variables such as ${date}, ${hour}, and more.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of dynamic partitions in a partition type should not be too high, as this may reduce the consumption rate. It is recommended to keep the number below 10.</div><br> |


<span id="_5-6-字段映射"></span>
#### 5.3.4 Field mapping

Once the configuration of the data source and target is complete, you need to specify the field mapping between the source and target. Based on this mapping, the data integration task writes data from the source fields to the corresponding fields in the target.

字段映射支持选择**基础模式**和**转换模式**配置映射：

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">基础模式和转换模式不支持互相切换，模式切换后，将清空现有字段映射中所有配置信息，一旦切换无法撤销，需谨慎操作。</div>



* 转换模式：

   字段映射支持数据转换，您可根据实际业务需求进行配置，将源端采集的数据，事先通过数据转换后，以指定格式输入到目标端数据库中。

   转换模式详细操作说明详见[4.1 转换模式](https://docs.byteplus.com/docs/6260/74993#9180ba09)

   在转换模式中，你可依次配置：来源节点、数据转换、目标节点信息：

   
   |配置节点 |说明 |
   |---|---|
   |来源节点 |配置数据来源 Source 节点信息：<br><br><br>* 节点名称：自定义输入来源节点名称信息，只允许由数字、字母、下划线、\-和.组成；且长度不能超过10。<br><br>* 数据字段：通过**自动添加、手动添加**等方式添加数据来源字段信息。<br><br><br>配置完成后，单击**确认**按钮，完成来源节点配置。 |
   |数据转换 |单击数据转换右侧**添加**按钮，选择 **SQL 转换**方式，配置转换信息和规则：<br><br><br>* 节点名称：自定义输入来源节点名称信息，只允许由数字、字母、下划线、\-和.组成；且长度不能超过10。<br><br>* SQL 脚本：输入 SQL 脚本转换规则，目前仅支持添加一个转换的 SQL 语句，且不能包括 “;”。<br><br><br>配置完成后，单击**确认**按钮，完成数据转换节点配置。SQL 脚本示例详见[4.1.2 添加转换节点](https://docs.byteplus.com/docs/6260/74993#59a6e8f0)。 |
   |目标节点 |配置目标节点 Sink 信息：<br><br><br>* 节点名称：自定义输入来源节点名称信息，只允许由数字、字母、下划线、\-和.组成；且长度不能超过10。<br><br>* 数据字段：通过**自动添加、手动添加**等方式添加数据目标字段信息。<br><br><br>配置完成后，单击**确认**按钮，完成目标节点配置。 |
   

* 基础模式：

   You can manage field mapping relationships in the following three ways:

   * Auto add: Click the **Auto add** button to automatically populate the source and target field information based on the data tables on both sides.

   * Add manually:

      Click the **Manually Add** button. You can manually edit the field information for the source and target, and add fields one by one. In this case, when the data source is read using JDBC, the source field information supports configuring database **functions** and **constants** as input. When adding values manually, enter the required value in the source table field and select the function or constant type, for example:

      * Functions: You can enter now(), current_timestamp(), unix_timestamp(), and many other functions supported by the Hive database.

      * Constant: You can define your own constant values, such as '123', '${DATE+1}', '${hour}', and more. The input value must be enclosed in single quotes. You can also use it in combination with [时间变量参数](https://docs.byteplus.com/docs/6260/75002).

      * Partition field: When adding manually, you can select the **partition field** from the source table using the dropdown to configure the mapping.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When the Hive data source reading method is set to HDFS, functions and constants cannot be configured in manually added source fields.      </div>
      

   * Move or delete fields: You can also change the order of field mappings or delete fields as needed.


<span id="2a695e85"></span>
#### 5.3.3 The expected maximum concurrency setting

When setting the expected maximum concurrency (MAX_PARALLELISM) in Hive, the following differences exist between reading and writing Hive data:


* Read the Hive data:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When reading Hive data, if the <code>job.reader.reader_parallelism_num</code> parameter is also set in advanced parameters, the setting in advanced parameters takes precedence.   </div>
   

   * HDFS mode: Set the MAX_PARALLELISM value. The final concurrency for task execution is determined by factors such as the number of HDFS files, file size, block size (for HDFS\-like storage), and whether files can be split, but it will not exceed the configured MAX_PARALLELISM value.

   * JDBC method: By default, reading is performed with a single concurrent thread.

* Write Hive data:

   Controlled by the MAX_PARALLELISM concurrency setting, the actual number of concurrent tasks during execution will not exceed the configured MAX_PARALLELISM value. If the actual concurrency for reading from the data source is also less than MAX_PARALLELISM, then the concurrency for writing to Hive will match the concurrency for reading from the data source.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When performing batch writes to Hive data, if the <code>job.reader.writer_parallelism_num</code> parameter is also configured in the advanced parameters, the value set in the advanced parameters takes precedence.   </div>
   

<span id="52f27a64"></span>
### 5.4 DSL configuration instructions

The Hive data source supports configuration using script mode (DSL).

In certain complex scenarios, or when the data source type does not currently support visual configuration, you can use task scripts to write Hive Reader and Hive Writer parameter scripts in a unified JSON format to run data integration tasks.

<span id="91c596af"></span>
#### 5.4.1 Enter DSL mode

For details on the procedure to enter DSL mode, see [MySQL 数据源-4.4.1 进入DSL 模式](https://docs.byteplus.com/docs/6260/126105#_4-4-dsl-%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E).

<span id="babc1cf7"></span>
#### 5.4.2 Offline reading in Hive

Replace the corresponding parameters for offline reading in Hive as needed. The following is an example script for offline reading in Hive:

```Java
 "reader": {
        // [required] datasource type
        "type": "hive",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": 65xxx5,
        // [required] user parameter
        "parameter": {
          "partition": "date=20240304/hour=22",
          "columns": [{
                        "upperCaseName": "ID",
                        "name": "id",
                        "type": "int"
                },
                {
                        "upperCaseName": "NAME",
                        "name": "name",
                        "type": "string"
                }
          ],
          "table_name": "mysql2hive_testp",
          "readerMode": "hdfs"        
        }
    }
```


Reader parameter description

Parameters marked with an asterisk (\*) are required, while those without an asterisk are optional:


|Parameter name |Description |
|---|---|
|\*type |For the data source type, enter "hive" for the Hive type. |
|\*datasource_id |Registered Hive data source ID. You can find it in the **Project Console \> Data Source Management** interface. |
|\*table_name |Enter the name of the Hive table to be read from the data source. |
|\*readerMode |Hive data reading methods: HDFS and JDBC modes:<br><br><br>* Based on HDFS, you must specify the value of the partition field, and only reading from a single partition is supported.<br><br>* Based on JDBC, data can be read using SQL, enabling field\-level filtering with WHERE clauses. |
|partition |When readerMode is set to hdfs, you must configure the partition parameter, which is the partition field information of the Hive table. |
|filter |When readerMode is set to jdbc, you must configure the filter parameter, which specifies the criteria for selecting data to synchronize. Only data that meets the filter conditions will be synchronized. Enter the SQL filter statement directly after the where keyword.<br><br><br>* If the filter condition is set to: `date>=${date}`, only dates greater than or equal to ${date} will be synchronized.<br><br>* Filtering conditions enable effective incremental synchronization of business data. If not configured, all data will be synchronized by default. |
|\*columns |In the configured table, the set of column names to be synchronized is described using a JSON array.<br><br><br>* Column pruning: You can select specific columns for export.<br><br>* Support column reordering: Columns can be exported in an order different from the table schema.<br><br>* The column must display the set of columns specified for synchronization and must not be empty.<br><br>* Support adding columns using functions or constants:<br><br>   * Functions: MySQL Reader supports inputting functions such as now(), current_timestamp(), unix_timestamp(), and many other functions supported by the MySQL database.<br><br>   * Constant: MySQL Reader allows you to define custom constant values, such as '123', '${DATE}', and '${hour}'. Each value must be enclosed in single quotation marks. This feature can be used in combination with [时间变量参数](https://docs.byteplus.com/docs/6260/75002). |


<span id="7fa21400"></span>
#### 5.4.3 Hive offline writing

Replace the relevant parameters for Hive offline writing as needed. An example script for Hive offline writing is as follows:

```Java
 // writer config
    "writer": {
        // [required] datasource type
        "type": "hive",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": 65xxx5,
        // [required] user parameter
         "parameter": {
                "partition": "date=${date},hour=${hour}",
                "table_name": "dts_db_testxxx",
                "columns": [{
                                "upperCaseName": "BOOBLE",
                                "name": "booble",
                                "type": "boolean"
                        },
                        {
                                "upperCaseName": "ISODATE",
                                "name": "isodate",
                                "type": "date"
                        }
                ],
                "partitions": [{
                        "name": "date",
                        "type": "string",
                        "value": "20240122"
                }, {
                        "name": "hour",
                        "type": "string",
                        "value": "16"
                }],
                "writeMode": "overwrite"
        }
    }
```


Note: In the description of Writer parameters, a parameter name prefixed with \* indicates a required parameter, while a parameter name without \* indicates an optional parameter:


|Parameter name |Description |
|---|---|
|\*type |Data source type. For the Hive type, enter "hive". |
|\*datasource_id |Registered Hive data source ID. You can find it on the **Project Console \> Data Source Management** page. |
|\*db_name |Enter the name of the Hive database to be read. |
|\*table_name |Enter the name of the Hive table under the data source where data needs to be written. |
|partition |Configure the partition information for the Hive table. Expression\-based configuration is supported, and multiple partitions should be separated by commas. For example: date=${date},hour=$ |
|\*writeMode |Enter the method for writing data to Hive; both "overwrite" and "insert into" are supported.<br><br><br>* overwrite: First delete the original data, then write new data.<br><br>* insert into: Directly write new data. |
|\*columns |In the configured table, the set of column names to be synchronized is described using a JSON array. |


<span id="ab0622e1"></span>
#### 5.4.4 Hive real\-time write

Replace the corresponding parameters for Hive real\-time writing according to the actual situation. The following is an example script for Hive real\-time writing:

```Java
  // writer config
    "writer": {
        // [required] datasource type
        "type": "hive",
        // [optional] datasource id, set it if you have registered datasource
        "datasource_id": 65xxx5,
        // [required] user parameter
         "parameter": {
                "table_name": "kafka2hive_json_fq_not_delete",
                "enable_event_time": "true",
                "proto": {
                        "descriptor": "CsEBCg9QYk1lc3NhZ2UucHJvdG8SDHRlc3RfbWVzc2FnZSKfAQoJUGJNZXNzYWdlEg4KAmlkGAEgAigDUgJpZBISCgRuYW1lGAIgAigJUgRuYW1lEhgKB2FkZHJlc3MYAyACKAlSB2FkZHJlc3MSHwoLY3JlYXRlX3RpbWUYBCABKANSCmNyZWF0ZVRpbWUSHQoKZXZlbnRfdGltZRgFIAEoA1IJZXZlbnRUaW1lEhQKBXByaWNlGAYgAigBUgVwcmljZQ==",
                        "class_name": "PbMessage"
                },
                "hdfs": {
                        "dump_type": "hdfs.dump_type.pb"
                },
                "partition_infos": "[{\"name\":\"date\",\"type\":\"TIME\"},{\"name\":\"hour\",\"type\":\"TIME\"}]",
                "source_schema": "[{\"name\":\"id\",\"type\":\"bigint\"},{\"name\":\"create_time\",\"type\":\"bigint\"},{\"name\":\"price\",\"type\":\"double\"}]",
                "sink_schema": "[{\"name\":\"id\",\"type\":\"bigint\"},{\"name\":\"create_time\",\"type\":\"bigint\"},{\"name\":\"price\",\"type\":\"float\"}]",
                "event_time_fields": "create_time"
        }
    }
```


<span id="_6-高级参数可选配置"></span>
## 6 Optional configurations for advanced parameters

<span id="659d84a1"></span>
### 6.1 Examples of advanced parameters

When configuring advanced parameters, you need to add the following prefix to the corresponding parameter name: `job.common.` Prefix (general parameter), `job.writer.` Prefix (write parameter), as shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2802e1f466c34f2f9bde92185d079385~tplv-goo7wpa0wc-image.image) </span>


|Parameter name |Parameter description |Default value |
|---|---|---|
|job.common.checkpoint_interval |Set the Checkpoint refresh interval. The default value is 15 minutes. When writing to Hive in real time, the timing of the write operation is determined by this parameter. |900000 |
|job.common.host_ips_mapping |When connecting a Hive data source to a self\-hosted cluster using a connection string, you must use this advanced parameter to configure the mapping between the host and its actual IP address. For example:<br><br>```JSON```<br>```{```<br>```  "core-1-1.emr-1": "1xx.xx.0.11",```<br>```  "core-1-2.emr-2": "1xx.xx.0.12",```<br>```  "master-1-1.emr-1": "1xx.xx.0.13"```<br>```}```<br> |None |
|job.writer.partition_strategy |Strategies for creating parameter partitions<br><br>Parameter values: partition_first, partition_last<br><br>Usage scenario: When partition_first is set for a stream job writing data, you can view the current Hive partition data in real time. |partition_last |
|job.writer.partition.date_format |The dynamic date partition format can be configured as "yyyyMMdd" or "yyyy\-MM\-DD". |yyyyMMdd |
|job.writer.partition.hour_format |The dynamic hourly partition format can be configured as "hh" or "HH". |HH |
|job.writer.null_string_as_null |In complex types, the string type will, by default, write null as an empty string. If you need to configure default writing of null values, set this parameter to true. If there are columns in dirty data that cannot be converted, they will be automatically converted to null values. |false |
|job.writer.case_insensitive |By default, all data will be converted to lowercase. |true |
|job.writer.convert_error_column_as_null |Automatically set to null the values in columns of dirty data that cannot be converted. |false |
|job.writer.dump.directory_frequency |You can set the frequency for writing to HDFS folders using the following parameters:<br><br><br>* Day level: dump.directory_frequency.day<br><br>* Hourly level: dump.directory_frequency.hour |dump.directory_frequency.day |


<span id="7a6f28f1"></span>
### 6.2 The related parameters after enabling the Proton service on an EMR cluster

When the data source is accessed via EMR Hive, and you are reading from or writing to Hive tables on TOS, if the EMR cluster has enabled the Proton service but has not configured the parameters related to TOS authentication, you must add the following advanced parameters to your offline read/write tasks or real\-time write tasks.

Add TOS authentication configuration in advanced parameters

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b19a8d98ffdb4b679c69e13c712848f0~tplv-goo7wpa0wc-image.image" width="1000px" /></div>


Parameters:


|Advanced parameter key |Advanced parameter value |
|---|---|
|* job.writer.extra_config<br><br>* job.reader.extra_config | |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">If the Proton service is enabled on the EMR cluster, you can configure the TOS authentication parameters fs.tos.access\-key\-id and fs.tos.secret\-access\-key in the service parameter file <strong>core\-site.xml</strong> of the HDFS component. After restarting the HDFS component, no action is required for offline write integration jobs, and existing real\-time write integration jobs only need to be restarted. Neither type of job needs to add the above advanced parameters.</div>


   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30405f9a033d4ad7902b2ff866ee3ac4~tplv-goo7wpa0wc-image.image" width="842px" />   </div>
   

2. <div data-tips="true" data-tips-type="tip">You can obtain Access Key/Secret Key information by going to the <a href="https://console.volcengine.com/iam/keymanage/">Key Management page</a> in the Volcengine console. This refers to the Access Key ID/Secret Access Key information.</div>



<span id="8328a215"></span>
### 6.3 Parameters related to EMR clusters without the Proton service enabled

If the data source is connected using EMR Hive, when reading from or writing to a Hive on TOS table, and the EMR cluster has not enabled the Proton service and does not have the relevant TOS authentication parameters configured, you must add the following advanced parameters in the task:


* Description of offline read/write channel parameters:

   
   |Advanced parameter key |Advanced parameter value |
   |---|---|
   |* job.writer.extra_config<br><br>* job.reader.extra_config |{"fs.s3a.access.key":"your access key","fs.s3a.secret.key":"your secret key", "fs.s3a.endpoint": "https://tos\-s3\-cn\-beijing.ivolces.com:443"}<br><br>For details on endpoint addresses in different regions, see [Region and access domain names (Endpoint)](https://www.volcengine.com/docs/6349/107356). |
   

* Real\-time write channel parameter description:

   
   |The advanced parameter key |Advanced parameter value |
   |---|---|
   |job.writer.extra_config |{"fs.s3a.access.key":"your access key","fs.s3a.secret.key":"your secret key", "fs.s3a.endpoint": "https://tos\-s3\-cn\-beijing.ivolces.com:443"}<br><br>For details about endpoint addresses in different regions, see [Region and access domain names (Endpoint)](https://www.volcengine.com/docs/6349/107356). |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the Proton service is not enabled on the EMR cluster, you can configure the TOS authentication parameters—fs.s3a.access.key, fs.s3a.secret.key, and fs.s3a.endpoint—in the service parameter file of the HDFS component, <strong>core\-site.xml</strong>. After restarting the HDFS component, no action is required for existing offline write integration jobs, and existing real\-time write integration jobs only need to be restarted. For both types of jobs, you do not need to add the advanced parameters mentioned above.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3655d58600c42de894b7b84a441c706~tplv-goo7wpa0wc-image.image" width="2882px" /></div>
