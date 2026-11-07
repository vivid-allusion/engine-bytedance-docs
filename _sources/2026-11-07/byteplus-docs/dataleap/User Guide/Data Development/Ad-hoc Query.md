---
title: "Ad-hoc Query"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/ad_hoc_query"
---

Ad\-hoc query supports multiple engine type statements for creating, running, data preview, and export functionalities, facilitating real\-time testing of code performance against expectations, and troubleshooting code errors during the data development process.

<span id="_1-概述"></span>
## **1 Usage Scenarios**

If you only need to quickly check if the data in tables under certain engines meet expectations or just verify the correctness of SQL scripts without the need for task submission, activation, or setting periodic scheduling parameters, you can achieve this through the ad\-hoc query feature.

The supported engine types and corresponding query types for ad\-hoc queries are as follows:


|Engine type |Task type |
|---|---|
|BytePlus E\-MapReduce (EMR) Serverless Spark |* EMR Serverless Spark SQL |
|BytePlus E\-MapReduce (EMR) Serverless Presto |* EMR Serverless Presto SQL |
|ByteHouse Enterprise Edition (ByteHouse CE) |* ByteHouse CE SQL |
|ByteHouse Cloud Data Warehouse Edition (ByteHouse CDW) |* ByteHouse CDW SQL |
|Generic |* Notebook<br><br>* MySQL |


<span id="540b50f7"></span>
## 2 Usage Restriction


* EMR Serverless Spark SQL, EMR Serverless Presto SQL, Notebook, MySQL temporary query types are not yet supported for message notification after task execution success or failure.

   For other task types, you can go to **Project Console \> Configuration Information \> Message Notification Settings** based on business conditions, to choose whether to enable notification for successful or failed runs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/791b8accf70e49eaa55bfab806f3a9f4~tplv-goo7wpa0wc-image.image) </span>

   * The default notification method is Email, and you need to bind the corresponding **Security Email** information in "Account Management" in advance.;

* MySQL query types are not yet supported to switch from **Ad\-hoc Query** Node to **Data Development** Scheduling Tasks.


<span id="_2-使用前提"></span>
## 3 Pre\-conditions for Use


1. Ad\-hoc queries must first bind **EMR Serverless** **Spark/Presto,**  **ByteHouse CE** or **ByteHouse CDW** and other related computing engines or MySQL data source services to create corresponding ad\-hoc query tasks. For operation details, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project)、[MySQL Data source](https://docs.byteplus.com/docs/dataleap/69127) **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Sub\-users operating ByteHouse CE SQL tasks need to perform the following actions first:   </div>
   

   1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Main account</strong> needs to go to <strong>Access control \> User \> Sub\-user Details \> Permissions</strong> tab, click <strong>Add Permissions</strong> button, to add <strong>ByteHouseCEStandardAccess</strong> system policy to the sub\-user.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0ab2c9ad37545158987f86d1f11d80f~tplv-goo7wpa0wc-image.image" width="2878px" />   </div>
   

   2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Sub\-user</strong> after logging into the <a href="https://console.byteplus.com/bytehouse-ce/region:bytehouse-ce+ap-southeast-1/data_object/databases">ByteHouse CE Console</a> once, will be automatically granted read permission to the 'Default' database in ByteHouse CE and the corresponding <strong>Query User</strong> role. For more permission operations in ByteHouse CE, see <a href="https://docs.byteplus.com/en/docs/bytehouse/privilege-management">Permission management</a>.   </div>
   

   3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Query User</strong> sub\-users cannot create databases through ByteHouse CE SQL ad\-hoc queries. Visit the <strong>Data Catalog</strong> interface to create the corresponding ByteHouse CE database. See details <a href="https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CE_Database">Manage ByteHouse CE DB</a>.   </div>
   

   4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If a sub\-user needs to operate more database tables, you can visit the <strong>Data Security</strong> interface to apply for the corresponding ByteHouse CE table permissions. See details<a href="https://docs.byteplus.com/docs/dataleap/Apply_Permission">Apply Permission</a>.   </div>
   

   See details [创建项目](https://docs.byteplus.com/docs/dataleap/create_project).


<span id="_3-1-进入临时查询"></span>
## 4 Create New Query


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In the **Overview** interface, navigate to the **IDE Development** interface for a specific project, and in the left sidebar, click the **Ad\-hoc Query** button to enter the **Ad\-hoc Query** page.

3. Click the **Create new query** button, fill in the following Parameter information in the dialog, and after clicking **Confirm**, proceed to the Ad\-hoc Query statement editing interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/067568fe0328480bba4d9e3547f1bcb2~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Description |
   |---|---|
   |Bind engine |Supports selecting engines bound to EMR Serverless Spark, EMR Serverless Presto, ByteHouse CE, ByteHouse Cloud Data Warehouse Edition, and Generic (Notebook, MySQL Query Type). |
   |Associated instance |Show the default engine instance under the corresponding engine. |
   |Query type |* When choosing to bind the **EMR Serverless Spark/Presto** engine, the default query type is EMR Serverless StarRocks/Spark/Presto SQL.<br><br>* When choosing to bind the **ByteHouse CE/Cloud Data Warehouse Edition** engine, the default display is ByteHouse CE SQL/ByteHouse CDW SQL.<br><br>* When choosing to bind the **Generic** engine, the query type supports dropdown selection of Notebook, MySQL type. |
   |Name |Input the task name for ad\-hoc query, only letters, numbers, underscores, [], 【】, ( ), () , periods, and Chinese characters are allowed, and it must be within 127 characters. Example: emr_hive_sql_0101 \- Ad\-hoc Query |
   |Save to |Select the target directory to store the ad\-hoc query task. |
   


<span id="_3-3-开发编辑"></span>
## **5 Development editing**

<span id="3b480dab"></span>
### 5.1 SQL Engine Development

In the actual development process of SQL types like ByteHouse CE/ByteHouse Cloud Data Warehouse Edition SQL, Ad\-hoc Query provides an Action bar that can help you develop better.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e7459b62ec640aaaa7df6727ec1750c~tplv-goo7wpa0wc-image.image) </span>


|No |Action |Description |
|---|---|---|
|1 |Save |Save the current code entered. |
|2 |Run/Terminate |Use online data directly to run code, operate with caution; or stop a running ad\-hoc query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If your SQL code contains platform time variable parameters like ${date}, ${hour}, etc., a dialog will pop up when debugging, prompting you to select the business date for the query as needed. Example:</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33a3fabc11454eb88aceae7d6e25c077~tplv-goo7wpa0wc-image.image" />   </div><br>   <br><br>* <div data-tips="true" data-tips-type="tip">If the SQL code does not contain time variable parameters or the time variable parameters are expressed as ${DTF\-xxxxxxxx}, then no dialog will pop up to prompt for business date selection. For more details on time variable parameters, see <a href="https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252">Description of platform time variables and constants</a>.</div><br> |
|3 |Convert to Task Development |Support converting temporary query nodes into new data development tasks, which can be submitted for deployment, and configuring scheduling properties among other things.<br><br><br>* Select directory: Choose the storage path after converting to a Data Development task from the dropdown.<br><br>* Conversion mode: Supports choosing either **Retained copy conversion** or **Direct conversion**. Direct conversion converts the current temporary query task into a data development task, but does not retain this temporary query task node.<br><br>* Task name: Set the name of the task after conversion. Only supports letters, numbers, underscores, [],【】,（）, (), periods, and Chinese characters are allowed, and must be within 127 characters.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ad\-hoc queries for MySQL are currently not supported to be converted into Data Development scheduling tasks.</div><br> |
|4 |Calculation Queue/Select Calculation Group |* When selecting an engine instance of the EMR Serverless Spark/Presto type, you need to choose from the **Queue Information** bound to the project. You can add multiple queues information when binding **Create project \> Service binding \> EMR Serverless Spark/Presto Queue**. See details [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project)。<br><br>* When selecting an engine instance of the ByteHouse Cloud Data Warehouse Edition type, you need to drop\-down choose the computation group already bound to the current project and queried in the ByteHouse_CDW console. For computation group creation, see details [ByteHouse CDW calculation group](https://docs.byteplus.com/en/docs/bytehouse/docs-virtual-warehouses). |
|5 |Format |Arrange the current node code according to keywords; commonly used for cases where a single line of code is too long. |
|6 |Parse |EMR Serverless Spark SQL, ByteHouse CE SQL, ByteHouse CDW SQL types support automatic detection of SQL syntactic errors, helping to identify errors in the code before SQL execution, thus enhancing the query efficiency. |
|7 |Engine |ByteHouse CE and ByteHouse CDW select the corresponding execution engines by default. |
|8 |Parameter description |Time variable description can be used in code, such as ${DATE}. For more details on using time variable parameters, see [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |
|9 |SQL Editing Area |You can enter SQL statements for different query types in this editing area, supporting common statements such as DDL and DML.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In a temporary query task, when there are multiple Queries in the query node, and multiple Queries are executed successively, only the results of the last successful Query are returned on the results page.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">EMR Serverless Spark/Presto SQL only support submitting one Query at a time.</div><br> |


<span id="6be8bb7c"></span>
### 5.2 Notebook Type

The Notebook query type under the Generic engine supports Kernel types such as Python on K8s, Python Spark on EMR, and Spark on EMR Serverless; the Ad\-hoc Notebook type does not support Schedule Settings or Commit for Release actions.


* For details on how to use the Kernel type of Python on K8s, see [3 Task configurations](https://docs.byteplus.com/docs/dataleap/notebook#_4-%E4%BB%BB%E5%8A%A1%E9%85%8D%E7%BD%AE).

* Kernel types of Spark on EMR Serverless, can only be executed through **Common Computing Resource Group**, for operation details, see [Ad hoc queries: Spark on EMR Serverless Kernel practical guide](https://docs.byteplus.com/docs/undefined/689db5998d8d50053b67195e).


<span id="16a5d843"></span>
### 5.3 MySQL Type

Under the generic engine, temporary query MySQL query types can perform data development actions such as querying, creating tables, and inserting data by directly accessing the MySQL data source, targeting the MySQL data source. After creating a MySQL query type, you can perform the following actions:


|Configuration Item |Description |
|---|---|
|Select data source |Click the drop\-down box and select the successfully created MySQL data source. If you have not yet created a data source, you can click the **New Data Source** button on the right to go to data source management and create one. See details [MySQL Data source](https://docs.byteplus.com/docs/dataleap/69127) . |
|SQL Editing Area |You can enter MySQL\-related SQL statements in this editing area, supporting common statements such as DDL and DML. |
|Network Configuration |If the MySQL data source is accessed via a **Connector**, you must manually select the same private network (VPC), subnet, and security group as the target MySQL data source.<br><br>If the target MySQL data source's VPC is not consistent with BytePlus VPC, you can connect via dedicated lines or public networks and add the necessary allowlist information. For network connection details, see details [Network connectivity solution](https://docs.byteplus.com/docs/dataleap/network_connectivity_solution), and for allowlist operations, see details [MySQL Data source](https://docs.byteplus.com/docs/dataleap/69127).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a sub\-account logs in to create a task, selection of network environments must have related service usage permissions; the main account must add VPCReadOnlyAccess or VPCFullAccess permissions to Access Control.</div><br> |


<span id="7b441d69"></span>
## 6 Temporary query debugging

After completing code logic and queue information configuration, you can perform debugging operations on the interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For debugging operations, use online data directly and proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Temporarily query debugging log data, which will be retained for 15 days. You can view the details of the corresponding debugging logs within 15 days.</div>



At the top of the editor, click **Save** button, then click **Debug** button to start running the task, wait for the task debugging to complete, and then view the debugging records below:


* In the left side of the debugging records, you can filter out different debug status historical running records by selecting **Debug status**.

   * Move the mouse over the debugging records can view information including debug ID, business date, and committer.

   * **Double Click** the debug records to edit the debug name information and press enter to save.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d767988e4cd4cae94bc20b78f23fd6b~tplv-goo7wpa0wc-image.image) </span>

* Click on the debug records, on the right side of the debug records, you can view details such as the overview of the run records, timeline (if available), logs, and results.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For debugging records of different ad\-hoc query types, see the task descriptions for data development scheduling under each engine, like <a href="https://docs.byteplus.com/docs/dataleap/emr_sql">EMR SQL</a>、<a href="https://docs.byteplus.com/docs/dataleap/bytehouse_cdw_sql">ByteHouse CDW SQL</a>、<a href="https://docs.byteplus.com/docs/dataleap/bytehouse_ce_sql">ByteHouse CE SQL</a>、<a href="https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_sql">EMR Serverless Spark SQL</a> among others.   </div>
