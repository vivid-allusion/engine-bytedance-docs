---
title: "Batch data synchronization"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/batch_data_synchronization"
---

DataSail provides offline data integration and synchronization capabilities, supporting high\-speed and stable data synchronization operations between a wide range of heterogeneous data sources. Data from the source database is synchronized to the target database in offline mode, ensuring that the data in the target database corresponds to that in the source database.

This article introduces the operating instructions for batch data synchronization.

<span id="_1-数据源"></span>
## **1** Prerequisites for use


* The DataLeap service has been enabled and a DataLeap project has been created. For details, see [DataLeap service activation](https://docs.byteplus.com/docs/undefined/689b492cf611e0051a33f318), [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

* A dedicated data integration resource group with appropriate resource specifications has been created and bound to the successfully created DataLeap project. For details on the purchase operation, see [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group); for details on the project binding operation, see [Data Integration Resource Group](https://docs.byteplus.com/docs/dataleap/datasail_resource_group).

* Register the data source in the project console, and ensure that the data source and the dedicated data integration resource group can communicate with each other over the network. For detailed network instructions, see [Network connectivity solution](https://docs.byteplus.com/docs/dataleap/network_connectivity_solution).


<span id="_2-配置任务"></span>
## **2 Create a batch data integration**

Steps for creating batch data integration tasks are as follows:


1. Log in to the [DataLeap tenant console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?) **.** 

2. In the left navigation bar, go to **Projects**, then click the corresponding **Project name** to enter the Data Development interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46ae8d1f94f14569978f09d4123fd9b9~tplv-goo7wpa0wc-image.image) </span>

3. In the Data Development interface, click the **New Task** button in the directory tree to enter the New Task interface.

4. Choose **Data Integration \> Batch Integration**, and fill in the task's Basic Info and Storage Path.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Enter the task name. Only the following characters are allowed: period, letters, numbers, underscore, hyphen, square brackets ([]), Chinese brackets (【】), both full\-width and half\-width parentheses (（） and ()), and Chinese characters. The name must not exceed 127 characters.   </div>
   

5. Click the **OK** button to complete the creation of the task.


<span id="7443f31c"></span>
## 3 Data source/target configuration

After creating a batch integration task, enter the visual configuration interface for batch integration tasks and configure the following data source and target items:


1. Configure data source information according to the actual business scenario.

2. Select the target data source information to be written as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64b26b3db0e643948b0ee943bf402a6c~tplv-goo7wpa0wc-image.image) </span>

<span id="6745d221"></span>
## 4 Field mapping configuration

After configuring the data source and target, you need to specify the field mapping between the source and target. Based on this mapping, the data integration task writes data from the source fields to the corresponding fields in the target.

Field mapping supports choosing **Basic Mode** and **Transition Mode** when configuring mapping.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Switching directly between basic mode and conversion mode is not supported. After switching modes, all configuration information in the current field mapping will be cleared. Once switched, this action cannot be undone. Proceed with caution.</div>


<span id="9180ba09"></span>
### 4.1 The Transition mode

Field mapping supports data conversion. You can configure various data transformation operations according to your actual business needs. The collected source data can be processed in advance and then imported into the target database in the specified format, meeting the requirements of different business scenarios.

Transition Mode can be applied to various lightweight data processing scenarios, such as:


* **Data cleaning**: You can use the Transition mode to filter redundant data, handle missing values, correct data errors, and more.

* **Data preprocessing**: You can use transformation modes to standardize, normalize, discretize, and otherwise preprocess data to better analyze and process data.

* **Data conversion**: You can use the conversion mode to Transition data from one format to another format.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, the Transition Mode supports all batch integration jobs, as well as real\-time integration jobs from <strong>non</strong> MQ (for example, Kafka) to Hive/HDFS.</div>


You can access the Transition Mode Configuration interface in the following ways:


1. Refer to the steps above [2 Create a batch data integration](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization#_2-%E9%85%8D%E7%BD%AE%E4%BB%BB%E5%8A%A1), and enter the visual task configuration interface.

2. Configure the data source and target data source information as needed.

3. Click the “**Transition Mode**” button to enter the Transition Mode configuration interface.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d01ccf14ea5342df9bfed4551a771756~tplv-goo7wpa0wc-image.image) </span>

In conversion mode, you need to configure the following in order: source node, data transformation, and target node information.

<span id="59a6e8f0"></span>
#### 4.1.1 Configure source nodes

By default, **Source Node** and **Target Node** will be automatically added to the node directory list, as shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47bcf880445544f39faed0e29aa69fdc~tplv-goo7wpa0wc-image.image) </span>


1. Click the "Source" node under the Source node, and configure the field info for the data source in the right panel.

2. Configure the source node name information. You can input a custom source node name, which may only contain numbers, letters, underscores, hyphens, and periods, and must not exceed 10 characters in length.

3. To configure data field info, you can add data source field info using two modes: **Add automatically, Add manually**.

4. After the source node information configuration is complete, click the **OK** button. The gray dot ( **·** ) to the left of the source node name in the node directory list will then turn green ( **·** ), indicating that the source node configuration is complete.


<span id="59a6e8f0"></span>
#### 4.1.2 Add a Transition node

The data conversion node supports adding SQL conversion nodes and supports implementing various conversion operations through Flink SQL functions, for example, delete column, rename field, data type conversion, and more. To add an SQL Transition node, follow these steps:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4baa841df70f47648b1a120a421d0f3a~tplv-goo7wpa0wc-image.image) </span>


1. Click the **Add** button on the right side of the Data Conversion Node, select the **SQL transform** method, and configure the conversion information and rules.

2. Configure the conversion node name. You can input a custom node conversion name, which may only consist of numbers, letters, underscores, hyphens, and periods, and the length must not exceed 10 characters.

3. Input the SQL script conversion rule. Currently, only one SQL statement for conversion can be added, and it must not include a semicolon (';').

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Input conversion SQL statements only support Flink's internal SQL statements; the SQL syntax of the source or target datasource types is not supported.   </div>
   

   The following are Flink SQL\-related conversion examples (assuming the source table name is Source):

   * **Field reorganization, splitting, and merging**

      ```SQL
      -- Field reorganization: The source table has three fields: a, b, and c, but the downstream target table has only two fields: c and b.
      SELECT c, b FROM Source
      
      -- Field merge: Concatenate the first_name field and the last_name field from the source table with a space, and use the result as a new field named full_name
      SELECT first_name || ' ' || last_name AS full_name FROM Source
      
      -- Field split: Split the full_name field in the source table by space to generate the new first_name and last_name fields
      SELECT SPLIT_INDEX(full_name, ' ', 1) AS first_name, SPLIT_INDEX(full_name, ' ', 2) AS last_name FROM Source
      ```
      

   * **Time format conversion**

      ```SQL
      -- Transition a 10-digit Unix timestamp string to date and date-time strings (year-month-day, year-month-day hour:minute:second)
      SELECT id, `name`, FROM_UNIXTIME(CAST(t_time AS BIGINT),'yyyy-MM-dd') as t_time FROM Source
      SELECT id, `name`, FROM_UNIXTIME(CAST(t_time AS BIGINT),'yyyy-MM-dd HH:mm:ss') as t_time FROM Source
      
      -- Transition 13-digit Unix timestamp strings to date and date-time strings (year-month-day, year-month-day hour:minute:second)
      SELECT id, `name`, FROM_UNIXTIME(CAST(t_time AS BIGINT)/1000,'yyyy-MM-dd') as t_time FROM Source
      
      SELECT id, `name`, FROM_UNIXTIME(CAST(t_time AS BIGINT)/1000,'yyyy-MM-dd HH:mm:ss') as t_time FROM Source
      
      -- Transition current Date to yyyy-mm-dd
      SELECT id, `name`, DATE_FORMAT(CURRENT_TIMESTAMP，'yyyy-MM-dd') as t_time FROM Source
      
      SELECT  Transition_TZ(REPLACE(acceptTime, 'T', ' '), 'UTC', 'UTC') AS acceptTime  FROM Source
      ```
      

   * **Condition check**

      ```SQL
      -- Determine whether the name field contains only whitespace characters. If so, output NULL; otherwise, output the original string.
      SELECT
          CASE
               WHEN IS_SPACES(name) THEN NULL
               ELSE name
          END
      FROM Source
      
      -- Filter data by conditions
      SELECT name, age FROM Source WHERE age > 10
      ```
      

   * **Field segment extraction**

      ```SQL
      SELECT id, o_name, SUBSTRING(tb, 2) FROM Source
      ```
      

   * **Condition filter**

      ```SQL
      SELECT id, o_name FROM Source where id>100 and name='test'
      ```
      

   For a more comprehensive list of conversion functions supported by SQL nodes, see [all scalar functions in Flink 1.11](https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/functions/systemFunctions.html#scalar-functions).

   The following are descriptions of some functions unique to DataSail's internal use:

   
   |**Function name** |**Usage** |**Return value type** |**Example** |
   |---|---|---|---|
   |IS_NUMBER |Determine whether a string is in number format. |Boolean |`IS_NUMBER(price)`, if price is a string in numeric format, such as `'1'`, `'2.3'`, and so on, returns `true` |
   |IS_SPACES |Determine whether a string consists entirely of blank space characters |Boolean |`IS_SPACES(name)`: Returns `true` if name is a string consisting only of blank space characters such as `' '`. |
   |GET_JSON_OBJECT<br><br>GET_JSON_STRING (returns only a String) |Extract the corresponding field values from the given JSON string according to the specified JSONPath.<br><br>If the specified JSONPath path cannot be obtained, the default value specified by the third parameter is returned. |The type of parameters |`GET_JSON_OBJECT(json_field, '$.b', 'None')`<br><br><br>* If json_field is `{"a":1,"b":"hello"}"`, then return `'hello'`.<br><br>* If json_field does not have the b field, then return the given default value `'None'`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Be sure to set <strong>a non\-null default value</strong>, because the function's output type will be defined by the type of this field. If a null value is indeed required as the default value, please use it with the <code>CASE WHEN</code> statement.</div><br> |
   |CREATE_LIST |Create a List object according to the specified parameters.<br><br>Typically used to construct the third parameter (default value) of the GET_JSON_OBJECT function, so that the function returns results of type List. |List |* Empty list: `CREATE_LIST()`<br><br>* Integer list: `CREATE_LIST(1, 2, 3)`<br><br>* String List: `CREATE_LIST('a', 'b', 'c')` |
   |TO_JSON |Transition a complex object such as an array (list) or a map to a JSON string |String |* Transition MAP field to JSON string:`TO_JSON(map_field)`<br><br>* Transition LIST field to JSON string: `TO_JSON(list_field)` |
   |SUBSTRING |Extract a substring from a string |String |`SUBSTRING(string_field FROM 2 FOR 4)` |
   |SUBSTR |Extract a substring |String |`SUBSTR(string_field, 2, 4)` |
   |AES_ENCRYPT |AES encryption function |String |AES_ENCRYPT(string_field, key)<br><br>key: base64(password), the password must be 32 bytes long |
   

4. After you have entered the SQL, you can also click the **Format** button above the text box to format the entered SQL.

5. After completing the Transition information configuration, click the **Confirm** button. After passing the check, the gray dot ( **·** ) to the left of the Transition node name in the node directory list will also turn green ( **·** ), indicating that the Transition node configuration is complete. If the check fails, an error message will appear. You need to modify the parameters based on the information provided.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60b2d02007fd4d6cbec2145a633ae85d~tplv-goo7wpa0wc-image.image) </span>

<span id="144a79ca"></span>
#### 4.1.3 Configure the target node

Similar to the source node, configure target node Sink information:


1. Click the Sink node under the target node, and configure the field information for the data destination on the right.

2. Configure the target node name. You can enter a custom target node name. Only numbers, letters, underscores, hyphens, and periods are allowed, and the length must not exceed 10.

3. You can configure target data field info by adding data source field info in two modes: **Add Automatically, Add Manually**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The field name of the target node should be consistent with the output field of the upstream SQL node to avoid runtime exceptions.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, if the upstream node is an SQL conversion node and the SQL statement is <code>SELECT name || '-SUFFIX' AS new_name, address FROM Source</code>, then the fields required for the target node are <code>new_name</code> and <code>address</code>.   </div>
   

4. After configuring the target node information, click the **Confirm** button. After confirming that a green dot ( **·** ) appears to the left of the node name, this indicates that the target node configuration is complete.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6f35c68316b4e4d9465e671ce2455a8~tplv-goo7wpa0wc-image.image) </span>

<span id="59a6e8f0"></span>
#### 4.1.4 Execute conversion debugging

After the data conversion node configuration has been completed, when the left side of all nodes has turned into green dots, the task can be submitted for execution. For batch integration jobs, you can click the **Debug** button in the action bar above to execute.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a25448554da94810a821dde92aebc46e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If any changes are made to the data conversion node in the future (including renaming, modifying parameters, deleting nodes, or other actions), the state of <strong>the current node and all downstream nodes</strong> will change from <strong>green</strong> to <strong>gray.</strong> At this point, you are required to click the <strong>Confirm</strong> button in each node in sequence. Only after confirming that all nodes have turned <strong>green</strong> can you continue to submit and execute the task. Otherwise, the following error message will be displayed:</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e7f724b81c947f39ca46d1d8a45aee3~tplv-goo7wpa0wc-image.image" width="2232px" />   </div>
   

* <div data-tips="true" data-tips-type="warning">For SQL nodes, we recommend using only <a href="https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/functions/systemFunctions.html#scalar-functions">scalar functions in Flink 1.11</a> to perform lightweight data conversion. <strong>Please avoid</strong> using stateful statements such as JOIN, GROUP BY, DISTINCT, or WINDOW, to prevent jobs from running slowly or even crashing.</div>


* <div data-tips="true" data-tips-type="warning">Currently, only one SQL Node can be added.</div>



<span id="5684ce4b"></span>
### 4.2 The basic mode

In basic mode, you can manage the field mapping relationship in the following ways:


* Click **Add Automatically** to automatically add fields based on the Datasource Schema. Some source types support obtaining the schema and automatically adding fields.

* Click **add manually** to add a blank Field Info entry, and manually input the Attribute, Type, and other details.

* Click **Same name mapping**. Based on how fields have been added to the **target/source**, perform same name mapping and add Field Info for the **source/target**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Same name mapping capability is supported only by some Datasources, such as FTP/SFTP Datasources.   </div>
   

* Click **Delete All** to delete all Field Info.

* By dragging the button on the left side of the field, you can adjust the order of the fields.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Caution: Ensure that the field types mapped between columns are data compatible.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/918a2d4f886441c3ba681a0e63241ec3~tplv-goo7wpa0wc-image.image) </span>

<span id="c1ab6263"></span>
## 5 Task operating parameters

After the field mapping configuration is complete, you can set the following task operating parameters as needed:


|Parameters |Note |
|---|---|
|Expected maximum concurrency |Within a data synchronization task, this is the maximum number of threads that can be used to read from the source or write to the data storage in parallel. |
|Dirty data settings |In the task, there is data not matched in field mapping. This may be due to an invalid format or an exception occurring when source data enters the target. For example, when data of the String type from the source is written to a target field of the INT type, the data cannot be written due to improper type conversion.<br><br>When configuring synchronization tasks, you can set the maximum number or percentage of dirty data allowed. If the configuration is set to 0, dirty data is not allowed, and the task will fail during execution and exit. |
|Custom parameter settings |* Single line edit mode requires setting the 'Key' and 'value' parameters.<br><br>* In Script edit mode, input of JSON string parameters is required.<br><br><br>For details on the use of common advanced parameters for each datasource, see [Advanced parameters](https://docs.byteplus.com/docs/dataleap/advanced_parameters). |


<span id="00f29a25"></span>
## 6 Script mode configuration


1. In the visual task editing interface, click the **Switch to Script Mode** button in the top toolbar to enter the script editing interface.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Switching to script mode will clear the current visual interface configuration. Once switched, this action cannot be withdrawn.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4925c42b9d94b788e9f62889f1f4a20~tplv-goo7wpa0wc-image.image) </span>

2. When configuring DSL Mode for the first time, you can click the **Import Script Template** button on the interface. Then, make the necessary configuration changes based on the template, thereby improving the efficiency of task configuration. Configuration description for each datasource script.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a20eb333743c49e38c4a7c979a8c446a~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Importing a new script template will clear the existing content. Once imported, this action cannot be undone.   </div>
   

<span id="4b3a4be8"></span>
## 7 Scheduling attribute/Integrated Resource Group configuration

After completing the configuration of task execution logic, you can proceed with subsequent configuration related to scheduling attributes and the Data Integration Resource Group:


* Configure scheduling attributes:

   1. Click **Schedule Settings** on the right to enter the schedule settings page for this task.

   2. You can set the run schedule, running delay, scheduling dependencies, and other properties for a Batch Integration task. For more information, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

* Configure data integration resource groups

   1. Click the **Data Integration Resource Group** on the right to go to the Data Integration Resource Group page.

   2. From the dropdown in the Project Console, select a Data Integration Resource Group that has completed the resource group connectivity test to ensure that the task network is connected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To display the Data Integration Resource Group in the dropdown menu, you must first bind the Data Integration Resource Group in Project Console \> Configuration information \> Service binding. See details <a href="https://docs.byteplus.com/docs/dataleap/datasail_resource_group#_4-%E7%8B%AC%E4%BA%AB%E9%9B%86%E6%88%90%E8%B5%84%E6%BA%90%E7%BB%84%E4%BD%BF%E7%94%A8">4 Use the Exclusive Integrated Resource Group</a>.      </div>
      

<span id="ecef9bf3"></span>
## 8 Debug Task

After completing the task code logic and parameter configuration, you can click the **Save** and **Debug** buttons in the action bar at the top of the editor to debug the task.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Caution: In Single Environment Mode projects, debug actions directly use production data for debugging. Proceed with care.</div>


* <div data-tips="true" data-tips-type="warning">In a multi\-environment mode project, debug actions use DB and table information from the development environment datasource to perform debugging.</div>



<span id="5f6e8fc1"></span>
### 8.1 Debug records

After the Debug Task starts running, you can view the Debug records below. Click the **Debug records** button to view the following details:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ed1017b2d52437abc218a3e28b6231f~tplv-goo7wpa0wc-image.image) </span>


* Overview: View task execution status, business date, run duration, start time, and other task overview information.

* Monitor: Batch Integration tasks support viewing task read\-write metrics. You can click the **Data Integration Monitor** button to go to the cloud monitoring interface and view integration read\-write metrics, resource group usage, and other monitoring information.

* Scheduling log: View log information for tasks during the scheduling and dispatch phase.

* Execution log: View detailed execution logs when a task runs in the Exclusive Integrated Resource Group. From here, you can view the actual size of the data read by the task, the number of data entries, the reason for failure, and other information. To view the execution log, see details at [DataSail log viewing and diagnostics](https://docs.byteplus.com/docs/undefined/68c04b5ad4b05a04fd3d9fcb).

* Task run events: View events that occur during task execution, such as task status changes, task failures, restarts, and other events.


<span id="4d783935"></span>
## 9 **Commit task**

After task debugging is successful and the results are confirmed to be correct, click the **Save** and **Commit for Deploy** buttons in the upper action bar. In the **Commit for Deploy** dialog box, select parameters such as **Backfill data, Monitor Settings, and Commit settings**. Finally, click the **Confirm** button to complete the job submission. For details on the deploy instructions, see [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

For details about subsequent task operations, see [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).
