---
title: "ByteHouse CE SQL"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/bytehouse_ce_sql"
---

ByteHouse Enterprise Edition (ByteHouse CE) is an intelligent growth engine for enterprises. It is an enterprise\-level analytical database based on open\-source ClickHouse, supporting interactive analysis of PB\-level data and flexibly enabling various data analysis and applications through multiple proprietary table engines.

DataLeap Data Development integrates ByteHouse CE Engine capabilities, allowing you to create ByteHouse CE SQL task types within Data Development. This enables periodic scheduling or manual execution and maintenance of ByteHouse CE Engine tables, improving the efficiency of job execution.

The following describes how to create a ByteHouse CE SQL task type node to perform data development.

<span id="2f368add"></span>
## 1 Prerequisites for use


1. In the Project Console, you need to bind the **ByteHouse CE** compute engine service before you can create ByteHouse CE SQL tasks. For operation details, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before sub\-users perform ByteHouse CE SQL tasks, they must first perform the following actions:   </div>
   

   1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>main account</strong> must first go to the <strong>IAM control \> User \> Sub\-user Details \> Policy</strong> tab, click the <strong>Authorize</strong> button, and add the <strong>ByteHouseCEStandardAccess</strong> system policy to the sub\-user.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b59b904acad042dea46a44a282ffd34c~tplv-goo7wpa0wc-image.image" width="2878px" />   </div>
   

   2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After a <strong>sub\-user</strong> logs in to the <a href="https://console.byteplus.com/bytehouse-ce/region:bytehouse-ce+ap-southeast-1/data_object/databases">ByteHouse CE Console</a> once, they are automatically granted read permission on the Default DB in ByteHouse CE and assigned the corresponding <strong>Query User</strong> role. For more permission actions in ByteHouse CE, see <a href="https://docs.byteplus.com/en/docs/bytehouse/privilege-management">Permission management</a>.   </div>
   

   3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Sub\-users of the <strong>Query User</strong> Role cannot create a database using Data Development SQL statements. You can go to the <strong>Data Catalog</strong> interface to create the corresponding ByteHouse CE database. See details<a href="https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CE_Database">Manage ByteHouse CE DB</a>.   </div>
   

   4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If a sub\-user needs to operate more database tables, you can go to the “<strong>Data Security</strong>” page to apply for the corresponding ByteHouse CE database table permissions. See details<a href="https://docs.byteplus.com/docs/dataleap/Apply_Permission">Apply Permission</a>.   </div>
   


<span id="bbfb9419"></span>
## 2 Create a task


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. On the **Overview** page, in the list of added projects, click **Data Development** to enter the corresponding project.

3. In the **Task development** interface, in the left navigation bar, click the **New Task** button to enter the **New Task** page.

4. Select task type:

   1. Classification: **Data Development**.

   2. Bind engine: **ByteHouse CE**.

   3. Associated instance: In the dropdown list, select the ByteHouse CE engine instance to bind to the project. The project supports binding multiple ByteHouse CE clusters, and you can select the cluster instance where the task will be executed from the available cluster instances. For details on multi\-cluster binding, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

   4. Select task: Batch Data **ByteHouse CE SQL**.

5. Fill in basic task info:

   1. Task name: Enter the name of the task. Only the following characters are allowed: period (.), letters, numbers, underscore (_), hyphen (\-), square brackets ([]), Chinese brackets (【】), half\-width parentheses ( ), full\-width parentheses （ ）, and Chinese characters. The name must not exceed 127 characters. Example: bytehouse\-ce_0101\-Chinese

   2. Save to: Select the target folder where the task will be stored.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98cb9c551bd544aab712d641e7b86ca5~tplv-goo7wpa0wc-image.image) </span>

6. Click the **OK** button to complete task creation.


<span id="cfda78c4"></span>
## 3 Configure tasks

After the task is created successfully, you will enter the ByteHouse CE SQL task configuration interface, where you can write SQL statements supported by ByteHouse CE as needed.

<span id="e6ab35a4"></span>
### 3.1 Edit task

In the code editor interface, enter the corresponding ByteHouse CE SQL statement. An example is shown below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a ByteHouse CE SQL node, when there are multiple queries and all are executed successfully, the results page only returns the result of the last successful query.</div>


```SQL
--When operating as a sub-user, go to the Data Catalog to create a ByteHouse CE Database. For example, use "bh_ce" as the database name.

--Create a table
CREATE TABLE IF NOT EXISTS sample.createTable(
    id UInt32,
    name String DEFAULT '',
    age UInt32
) 
ENGINE=MergeTree
ORDER BY id

--insert data
insert into sample.createTable VALUES(1, 'John', 25),(2, 'Jane', 30);

--Modify data
ALTER table sample.createTable UPDATE name = 'Lisa' WHERE id = 1;

--Query data
SELECT * from sample.createTable;
```


<span id="bbf4ff9a"></span>
### **3.2 Navigation bar** functional area analysis

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6621cdb778044969a0709f3c2456930~tplv-goo7wpa0wc-image.image) </span>


|Function name |Description |
|---|---|
|Format |Format the code that has been edited according to the SQL formatting style settings in [Personalize settings](https://docs.byteplus.com/docs/undefined/682aa7e55df38404fda1396d), so that its syntax structure appears clear and concise. |
|Parse |Parse and check the syntactic and semantic correctness of the written SQL code, and check for syntax error messages before execution to prevent runtime errors. |
|Execution engine |Support for ByteHouse CE execution engine. |


<span id="ca242869"></span>
### 3.3 Schedule settings

After completing task configuration, click the **Scheduling Configuration** button in the right navigation bar to open the scheduling configuration window. Here, you can set **basic info, scheduling attributes, dependencies, task input and output parameters**, and other information. See [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings) for detailed parameter settings.

<span id="5a535f3b"></span>
#### 3.3.1 **Task output data registration**

Task output data registration is used to record information about the task and data lineage, and does not affect code logic. You can set information related to output registration in the **Schedule Settings \> Register the data produced by the task** section.

For other tasks where the system cannot obtain output information by parsing, ByteHouse CE SQL tasks can register their output information automatically or manually. If the task involves ByteHouse CE database and table data output, it is strongly recommended to fill in the relevant fields to facilitate subsequent maintenance of task data lineage.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When performing manual registration of task output data configuration, you must first complete ByteHouse CE metadata ingestion. You can go to <strong>Data Catalog \> Metadata Ingestion</strong> to configure the corresponding collector. See details at <a href="https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion">Metadata Ingestion</a>.</div>



* Automatic registration:

   If task output data uses Automatic registration mode, then each time the task is deployed, the system will automatically update based on the code parsing results. You can click the **View output data for "Online version" and "Draft version"**  button to view the automatically registered output data results for different versions of the current task.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When choosing Automatic registration, if a field name in the SQL code query contains an SQL keyword, you must escape it by adding escape characters. For example, escape group as `group` and order as `order`. If escaping is not performed, it will affect the display of data lineage graphs, table production information, and other content in the Data Catalog. Alternatively, you may use the <strong>Manual registration</strong> option below to manually register task output data.   </div>
   

* Manual registration:

   The content you manually fill in is the task output. You can fill in multiple pieces of content. When configuring task dependencies for other tasks, you can use their **Schedule Settings** interface to add dependencies through **Dependency Recommendations** or **manual addition**. Search for and add dependencies based on the Database/Table name information output by the ByteHouse CE SQL task here. The specific content to be registered includes the following data types:

   * ByteHouse CE: This task logic writes data into a ByteHouse CE table. You need to specify the ByteHouse CE database name, table name, and partition name. Partition content can use variables, for example, in the form of ${date}, ${hour}.

   * Other: The logic of this task does not write data to the ByteHouse CE table.


<span id="1e65b03e"></span>
## 4 **The query console**

<span id="eae77ea2"></span>
### 4.1 Debug tasks

After the task code logic and parameter configuration are complete, you can click the **Save** and **Debug** buttons in the Action bar at the top of the editor to perform task debugging.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Debug action: Directly use online data for debugging. Exercise caution when performing this action.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days. You can view the corresponding debug log details within 15 days.</div>


* <div data-tips="true" data-tips-type="warning">If relevant standardized table creation management has been created in DataLeap Console \> Smart Markets, then in a ByteHouse CE SQL statement, if it contains table creation logic and the created table is within the validity scope of the table creation standard\*\*\*\*, a corresponding table creation standard check will be triggered when you <strong>parse</strong>, <strong>run</strong>, or <strong>submit</strong> the task. For the operating instructions for the Create Table standard, see <a href="https://docs.byteplus.com/docs/dataleap/data_warehouse_table_creation_specification">Data Warehouse Table Creation Specification</a>.</div>


* <div data-tips="true" data-tips-type="warning">This task type supports sending message notifications after a debug execution succeeds or fails. Based on your business needs, you can go to <strong>Project Console \> Configuration Information \> Message Notification Settings</strong> to choose whether to enable <strong>Task Debugging Success</strong> or <strong>Failure</strong> notifications. The default notification method is email. You need to link the appropriate <strong>security email</strong> to "Account Management" in advance.</div>



<span id="32239fcc"></span>
### 4.2 Debug records

After the Debug Task starts running, you can view the Debug records below. You can also view the task's historical Executions, including State, Business date, Start time, End time, Time spent, Committer, and more.

Click Debug records to view the following details:


* Results: Display query results after code execution.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because the preview data on the results page is limited to 1000 and there are restrictions in project data security settings, the data displayed in query results may be less than the actual data volume. It is recommended to handle as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Go to the <strong>Project Console</strong> and set the upper limit for project data security settings to 10,000 rows.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Project Console \> Configuration information \> Data security settings</strong> \> In the query results, select <strong>Enable Download</strong>. You can then click the <strong>download</strong> button in the query results area to download the complete data to your local device for viewing.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, see <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.   </div>
   

* Overview: View the code for the run result.

* Log: View run details, and you can download the log.


<span id="a8589d26"></span>
## 5 **Commit task**

After confirming that the query results are correct, click the **Save** and **Commit for Deploy** buttons in the action bar above. In the **Commit for Deploy** dialog box, choose **Backfill data, Monitor Settings, Commit settings** and other parameters. Finally, click the **Confirm** button to complete the job submission. see [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

For details on subsequent task operations, see [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).
