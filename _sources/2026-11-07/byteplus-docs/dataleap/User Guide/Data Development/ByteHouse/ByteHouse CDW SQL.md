---
title: "ByteHouse CDW SQL"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/bytehouse_cdw_sql"
---

ByteHouse Cloud Data Warehouse Edition (ByteHouse CDW) is a cloud\-native data warehouse that supports real\-time data analysis and batch analysis of massive data volumes. It enables efficient analysis of PB\-level data, and its convenient elastic scalability, exceptional analytical performance, and comprehensive enterprise\-grade features help customers achieve digital transformation.

DataLeap Data Development integrates the capabilities of the ByteHouse Cloud Data Warehouse Edition Engine, enabling you to periodically schedule or manually execute maintenance operations on ByteHouse CDW Engine tables by creating ByteHouse CDW SQL tasks in data development. This improves job execution efficiency.

The following section describes how to create a ByteHouse CDW SQL task\-type node for data development.

<span id="96f37c73"></span>
## 1 Prerequisites for use


1. ByteHouse Cloud Data Warehouse Edition service has been enabled. See [Quick Start](https://docs.byteplus.com/en/docs/bytehouse/docs-quick-start) for details.

2. In the Project Console, you must bind the **ByteHouse Cloud Data Warehouse Edition** compute engine service before you can create ByteHouse CDW SQL tasks. Action: see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

3. Before sub\-users perform ByteHouse CDW SQL tasks, the following actions must be completed:

   1. **The main account** must first go to the **IAM control \> User \> Sub\-user Details \> Policy** tab, click the **Add Permissions** button, and add the **ByteHouseReadOnlyAccess** system policy to the sub\-account. Only then can the sub\-account log in to the [ByteHouse CDW Console](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/database).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a5911e8cb4544988098c0d149cd4ba7~tplv-goo7wpa0wc-image.image) </span>

   2. Required permissions for sub\-users when executing ByteHouse CDW SQL statements

      * Read and write permissions for database tables: Sub\-users need to go to the **Data Security** interface to perform the corresponding ByteHouse CDW table permission application. See details[Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission).

      * Calculation group access rights: Sub\-users must have access rights to the corresponding ByteHouse CDW calculation group in order to execute SQL. You can have the main account create the corresponding Role, add sub\-users to the Role, and in the calculation group, add the created Role and calculation group permissions such as Operate, Use, Peek, Describe, and more. See details in [Resource privilege management](https://docs.byteplus.com/en/docs/bytehouse/resource-privilege-management) and [Role management](https://docs.byteplus.com/en/docs/bytehouse/docs-access-control-administration).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Both read and write permissions for tables and calculation group permissions are required; neither can be omitted.      </div>
      

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">To manage permissions such as Create Database and calculation group management in ByteHouse CDW, the main account can go to the ByteHouse CDW Console \> Permission management \> User interface. Click a specific <strong>Username</strong>, then authorize on the <strong>Resource permission</strong> tab.      </div>
      

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">It is recommended that the main account <strong>should not</strong> directly or through the authorization command grant sub\-users the <strong>ByteHouseFullAccess</strong> global policy, <strong>AccountAdmin</strong>, or <strong>SystemAdmin</strong> role permissions. Otherwise, the sub\-user will bypass <strong>DataLeap\-Data Security</strong> and have superuser permissions for all ByteHouse CDW DB tables.      </div>
      

      4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If a sub\-user is unable to create a database using Data Development SQL statements due to permission issues, you can go to the “<strong>Data Catalog</strong>” interface to create the corresponding ByteHouse CDW Database. See details<a href="https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CDW_DB">Manage ByteHouse CDW DB</a>.      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For more information about ByteHouse CDW permissions, see <a href="https://docs.byteplus.com/en/docs/bytehouse/docs-access-control">ByteHouse Security and Access Control</a>.      </div>
      

<span id="433d4286"></span>
## 2 Create a new task


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. On the **Overview** interface, in the list of added projects, click **Data Development** to enter the corresponding project.

3. On the **Task development** interface, in the left navigation bar, click the **New Task** button to go to the **New Task** interface.

4. Select Task Type:

   1. Classification: **Data Development**.

   2. Bind engine: **ByteHouse Cloud Data Warehouse Edition**.

   3. Associated instance: The ByteHouse Cloud Data Warehouse Edition Engine instance selected in the dropdown list when performing project binding. For details about Engine Binding, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When multi\-environment isolation mode is enabled for the ByteHouse Cloud Data Warehouse Edition engine in a project, only engine instance information related to the production environment can be selected from the dropdown when creating a task. During task debugging, you can manually switch to a development environment instance for debugging.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After a task is created, it is temporarily not possible to adjust Engine service instances in the production environment.      </div>
      

   4. Select task: Batch Data **ByteHouse CDW SQL**.

5. Fill In Basic Task Info:

   1. Task name: Enter the name of the task. Only the following characters are allowed: period, letters, numbers, underscore, hyphen, square brackets ([]), Chinese brackets (【】), parentheses (()), and Chinese characters. The name must be no more than 127 characters. Example: bytehouse\-cdw_0101\-Chinese

   2. Save to: Choose the target folder directory where the task will be stored.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68fa4b036e44457f8aab7e230983b01f~tplv-goo7wpa0wc-image.image) </span>

6. Click the **Confirm** button to complete task creation.


<span id="513c8179"></span>
## 3 Configuration tasks

After the task is created successfully, you will enter the ByteHouse CDW SQL task configuration interface, where you can write SQL statements supported by ByteHouse CDW as needed.

<span id="e49811b5"></span>
### 3.1 Edit Task

In the code editor interface, input the corresponding ByteHouse CDW SQL statement, for example:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a ByteHouse CDW SQL Node, when multiple queries are present and executed successfully, the results page returns only the result of the last successful query.</div>


```SQL
--If the sub-user does not have permission to execute SQL to create a database, you can go to the Data Catalog to create a ByteHouse CDW database. For example, the database name could be: bh_cdw_x;
CREATE DATABASE IF NOT EXISTS bh_cdw_x;

--Create Table
CREATE  TABLE bh_cdw_x.bh_cdw_table_test(
            id   Int64  COMMENT 'id for column',
            name String COMMENT 'name',
            age  Int64  COMMENT 'age',
            date date   COMMENT 'time'
        ) ENGINE = CnchMergeTree
PARTITION BY date 
UNIQUE key (id, date)
ORDER BY id;

--Insert data
INSERT INTO bh_cdw_x.bh_cdw_table_test VALUES(1, 'John', 25, '2024-01-01'),(2, 'Jane', 30, '2024-01-01');

--Query data
SELECT * FROM bh_cdw_x.bh_cdw_table_test WHERE date = '2024-01-01';
```


<span id="07cdee83"></span>
### **3.2 Navigation bar** functional area analysis

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b9760591dd84da6b0e24118fba470ec~tplv-goo7wpa0wc-image.image) </span>


|Function Name |Description |
|---|---|
|Format |According to the SQL formatting style settings in [Personalize settings](https://docs.byteplus.com/docs/undefined/682aa7e55df38404fda1396d), format the edited code so that its syntax appears clear and concise. |
|Parse |Parse and check the syntax and semantic correctness of the written SQL code, and check for syntax error messages before running the code to prevent errors during execution.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Parse action for the following statement types is not supported yet:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">DDL statements, such as Create, Alter, Show, Drop, and other statements related to DDL operations;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">INSERT INTO VALUES statement. For example: INSERT INTO example_table VALUES (VALUES1, VALUES2, VALUES3);</div><br> |
|Execution engine |The ByteHouse CDW execution engine is supported by default. |
|Parameter description |ByteHouse CDW SQL supports the use of system\-provided time variables and custom input parameters defined in tasks. See [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |


<span id="5f14613f"></span>
### 3.3 Schedule settings

After completing the task configuration, click the **Scheduling Configuration** button in the right navigation bar to enter the Scheduling Configuration window. Here, you can set **basic information, scheduling attributes, dependencies, and task input and output parameters**, as well as other information. For detailed parameter settings, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

<span id="a69db89b"></span>
#### 3.3.1 **Register the data produced by the task**

Register the data produced by the task to record task and data lineage information. This does not affect code logic. You can configure related information for output registration in the **Schedule Settings \> Register the data produced by the task** section.

For other tasks for which the system cannot obtain output information through parsing, ByteHouse CDW SQL tasks can register their output information in either **automatic** or **manual** mode. If the task involves outputting ByteHouse CDW database and table data, it is strongly recommended to fill in this information to facilitate subsequent maintenance of task data lineage.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When manually registering the configuration of task output data, you must first complete ByteHouse CDW metadata ingestion. You can go to <strong>Data Catalog \> Metadata Ingestion</strong> to configure the corresponding Collector. See <a href="https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion">Metadata Ingestion</a> for details about the action.</div>



* Automatic registration:

   If the task output data uses automatic registration mode, each time the task is launched, the system will automatically update the task output data based on the code parsing results. You can click the  **"View Production version output data" or "View Draft version output data"**  button to view the automatic registration results for the output data of different versions of the current task.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When choosing Automatic registration, if a field name in the SQL code query contains an SQL keyword, you must escape it by adding escape characters. For example, escape group as `group` and order as `order`. If escaping is not performed, it will affect the display of data lineage graphs, table production information, and other content in the Data Catalog. Alternatively, you may use the <strong>Manual registration</strong> option below to manually register task output data.   </div>
   

* Manual registration:

   The content you manually fill in is the output. Multiple entries are supported. When configuring dependencies for other tasks, you can go to its **Schedule Settings** page and use the **add manually** option to search for and add dependencies based on the Database/Table name information output by the ByteHouse CDW SQL task here. The specific registration content includes the following data types:

   * ByteHouse CDW: This task logic writes data to a ByteHouse CDW table. You need to provide the ByteHouse CDW database name, table name, and partition name. Partition content can use variables, for example, ${date} or ${hour}.

   * Other: This task logic does not write data to the ByteHouse CDW table.


<span id="e9bbae5e"></span>
## 4 **Query Console**

<span id="a2d9dd77"></span>
### 4.1 Debug Task

After completing the task code and parameter configuration, you can click the **Save** and **Debug** buttons in the Action bar at the top of the editor to debug the task.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This task type supports sending message notifications after a debug execution succeeds or fails. Depending on your business needs, go to <strong>Project Console \> Configuration information \> message notification settings</strong> to choose whether to enable notifications for <strong>Task Debugging run succeeded</strong> or <strong>Failed</strong>. The default notification method is email. You need to bind the corresponding <strong>security email</strong> information to "Account management" in advance.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days. You can view the corresponding debug log details within this period.</div>



<span id="c55abf44"></span>
### 4.2 Debug records

After the debug task starts running, you can view the debug records below. You can also view the task's execution records, including state, business date, start time, end time, duration, committer, and more.

Click Debug records to view the following details:


* Results: Displays the query results after code execution.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because the preview data on the results page is limited to 1000 and there are restrictions in project data security settings, the data displayed in query results may be less than the actual data volume. It is recommended to handle as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Go to the <strong>Project Console</strong> and set the upper limit for project data security settings to 10,000 rows.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Project Console \> Configuration information \> Data security settings</strong> \> In the query results, select <strong>Enable Download</strong>. You can then click the <strong>download</strong> button in the query results area to download the complete data to your local device for viewing.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, see <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.   </div>
   

* Overview: View the code for the run result.

* Log: View run details, and download the log.


<span id="09ca8cae"></span>
## 5 **Commit task**

After confirming that the query results are correct, click the **Save** and **Commit for Deploy** buttons in the upper action bar. In the **Commit for Deploy** dialog box, select parameters such as **Backfill data, Monitor Settings, Commit settings**, and finally click the **Confirm** button to complete the job submission. see [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

See details on subsequent task operations [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).
