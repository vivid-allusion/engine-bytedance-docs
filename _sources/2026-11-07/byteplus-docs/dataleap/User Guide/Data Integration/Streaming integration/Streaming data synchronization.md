---
title: "Streaming data synchronization"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/streaming_data_synchronization"
---

DataSail global data integration provides streaming data synchronization capabilities, supporting high\-speed and stable real\-time data synchronization between a wide range of heterogeneous data sources. It enables real\-time synchronization of data from the source database to the target database, ensuring that the data in the target database is kept in real\-time correspondence with the data in the source database.

This article provides operational instructions for streaming data synchronization.

<span id="_1-数据源"></span>
## **1** Prerequisites for use


* The DataLeap service has been enabled and a DataLeap project has been created. For details, see [DataLeap service activation](https://docs.byteplus.com/docs/undefined/689b492cf611e0051a33f318), [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

* A dedicated data integration resource group with appropriate resource specifications has been created and bound to the successfully created DataLeap project. For details on the purchase operation, see [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group); for details on the project binding operation, see [Data Integration Resource Group](https://docs.byteplus.com/docs/dataleap/datasail_resource_group).

* Register the data source in the project console, and ensure that the data source and the dedicated data integration resource group can communicate with each other over the network. For detailed network instructions, see [Network connectivity solution](https://docs.byteplus.com/docs/dataleap/network_connectivity_solution).


<span id="_2-新建流式数据集成"></span>
## **2 Create a streaming data integration**

Steps for creating a streaming data integration task are as follows:


1. Log in to the [DataLeap tenant console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?) **.** 

2. In the left navigation bar, click **Project** to enter the project list page.

3. Click the corresponding **project name** to enter the data development interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaf6e7dd49944667ac5b717c3aa9e0bf~tplv-goo7wpa0wc-image.image) </span>

4. In the data development interface, click the **New Task** button on the directory tree to enter the new task creation interface.

5. Select a task type:

   1. Category: **Data integration**.

   2. Select a task: **Streaming integration**.

6. Enter the basic information for the task:

   1. Task name: Enter a task name using only letters, numbers, underscores, or hyphens, and ensure it is no more than 63 characters. For example: stream_0101\-test

   2. Save to: Select the destination folder to store the task.

7. Click the **OK** button to finish creating the task.


<span id="_3-任务配置"></span>
## 3 Task configuration

<span id="_3-1-任务配置"></span>
### **3.1 Task configurations**

After creating a new streaming integration task, you need to configure the relevant task information. Streaming integration tasks now support configuration in both visual and script modes. The steps are as follows:

<span id="20ba259e"></span>
#### 3.1.1 Visualization configurations


1. Select data sources.

   1. Select data source information; supports selecting BMQ, DataSail, Kafka, RocketMQ, TDengine, and TLS data source types.

   2. Select the information of the target data source for writing. It supports selecting ByteHouse_CE, CFS, ClickHouse, Doris, Elasticsearch, and more than ten other types of data sources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For configuration instructions for each data source, see the <a href="https://docs.byteplus.com/en/docs/dataleap/datasource_list">data source list</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When writing to some data sources, you need to select a data writing method. There are different write methods for different data sources.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edb4cb1747914b739dc8532c6798ded6~tplv-goo7wpa0wc-image.image) </span>

2. Configure the mapping between source and target fields.

   You can choose **basic mode** or **transition mode** when configuring field mapping:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Switching between basic mode and transition mode is not supported. After switching modes, all configuration information in the current field mapping will be cleared. This operation cannot be undone, so proceed with caution.   </div>
   

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

   * Click **Auto Add** to automatically add fields based on the data source schema. Some data source types support automatically adding fields by retrieving the schema.

   * Click **Manual Add** to add a blank field entry, and manually enter the field name, type, and other information.

   * Click **Same\-Name Mapping**. Based on the fields added to the **target/source**, you can use same\-name mapping to add field information from the **source/target**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Same\-name mapping is supported by only some data sources, such as the Cloud\-Native Message Engine BMQ data source.      </div>
      

   * Click **Delete All** to delete all field information.

   * You can adjust the order of fields by dragging the button on the left side of the field.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Caution: Please note whether the data types of fields mapped between columns are compatible.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d36d6fbabed4001aa44051074786262~tplv-goo7wpa0wc-image.image) </span>

3. Set the following task runtime parameters.

   * Enable archiving: For Kafka, Bmq, RocketMQ, and DataSail data source types, you can choose whether to enable archiving. After archiving is enabled, you can select the archive field type and its corresponding archive field:

      * When the archive field type is **integer**, enter the name of the integer field from the source. The corresponding integer field can support **millisecond and second** granularity.

      * When the archive field type is **string**, you must enter the name of the string field in the source and its corresponding field format. The field format must comply with the Java Date Format standard, for example

         * If the date format is: 20181017, enter: yyyyMMdd

         * If the date format is: 2018\-10\-17, enter: yyyy\-MM\-dd

         * If the date format is 20181017 12:08:56, then enter: yyyyMMdd HH:mm:ss

         * If the date format is: 2018\-10\-17 12:08:56, fill in: yyyy\-MM\-dd HH:mm:ss

         * If the date format is: 2018\-10\-17T12:08:56, then enter: yyyy\-MM\-dd'T'HH:mm:ss

         * If the date format is "2018\-10\-17T12:08:56.235", then enter: yyyy\-MM\-dd'T'HH:mm:ss.SSS

   * The default consumption starting point: The default consumption position in Kafka when the current task starts.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For stream integration tasks of the Kafka, Bmq, or RocketMQ data source type, when performing the <strong>restart</strong> task operation in the streaming operations interface, you can also enable the <strong>reset offset</strong> operation as needed, and specify the consumption starting position as <strong>latest, earliest, timestamp</strong>, or <strong>partition offset</strong>. For detailed instructions, see <a href="https://docs.byteplus.com/docs/undefined/689b13f8a8453604ecb6069e#_3-1-%E5%8D%95%E4%BB%BB%E5%8A%A1%E6%93%8D%E4%BD%9C">Single task operation</a>.      </div>
      

   * Advanced parameters: When you select **Enable**, you need to set the key and value for the advanced parameters. You can add them using both **single\-line editing mode** and **script editing mode**. For example, to add the global concurrency parameter for a streaming integration task in single\-line editing mode, you can refer to the following configuration:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd6b600c7ea6401b998f01c96f91a5f8~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default global parallelism for streaming integration jobs is set to the number of MQ partitions divided by four. If the MQ traffic is low, you can directly add the following parameter in the advanced task settings: <code>job.common.global_parallelism_num = n</code>. This allows you to specify the global parallelism for the job, and this parameter ultimately determines how many TaskManagers will be started. If there are many partitions but the overall traffic is low, you can also specify this parameter to reduce the actual resources used for task execution.   </div>
   

<span id="32906e9b"></span>
#### 3.1.2 Script mode configuration


1. Enter the streaming integration task configuration page. Click the **Switch to script mode** button in the top toolbar to enter the script configuration page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Switching from visual mode to script mode will clear all existing configurations in visual mode, and once switched, this action cannot be undone.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1adc05247ca846acb34680a55b5cc4be~tplv-goo7wpa0wc-image.image) </span>

2. Click the **Import Script Template** button in the toolbar, and select the script template source type, target type, template library, and more:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a9487791e724cf599939d9218074a7a~tplv-goo7wpa0wc-image.image) </span>

3. After selecting a streaming task template, you can modify the script based on the actual data source information. For details on configuring scripts for each data source, see [data source list](https://docs.byteplus.com/en/docs/dataleap/datasource_list).


<span id="_3-2-设置参数"></span>
### 3.2 Parameters Setting

After completing the configuration of data source\-related tasks, you can click the **Parameter Setting** on the right to enter the parameter settings page for this streaming task, where you can set the basic information for the streaming task.


|Parameter classification |Parameter name |Description |
|---|---|---|
|Basic information |Task name |The task name entered when creating a task is displayed and cannot be modified in the parameter settings. To change it, in the task directory structure on the left, click **More** to the right of the task name, then click **Rename**. |
||Task types |Streaming integration |
||Description |Optional. You can provide a detailed description of the task to facilitate future viewing and management. |
||Owner |Only one member is allowed. By default, the task creator is the recipient of notifications when task execution fails or when a review passes or fails. The recipient can be changed to another project member as needed.<br><br><br>* The responsible person must be a member with editing permissions for the project, and project permissions must be granted by the project administrator.<br><br>* DataLeap enables collaborative development through project spaces. Roles with editing permissions within a project can edit all tasks under that project, so there is no need to assign multiple responsible persons to tasks to achieve collaborative cooperation. |
|Resource settings |Number of TaskManagers |To set the number of concurrent tasks, navigate to Task Runtime Parameters \> Advanced Parameters and refer to the `job.common.global_parallelism_num = n` parameter configuration.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Here, the setting for the number of TaskManager instances is temporarily ineffective for streaming integration tasks.</div><br> |
||Number of CPUs per TaskManager |Set the number of CPUs used by a single TaskManager. |
||Memory size (MB) for a single TaskManager |Set the memory size used by a single TaskManager. |
||Number of slots per TaskManager |Set the number of slots in a single TaskManager. |
||JobManager CPU count |Set the number of CPUs allocated to a single JobManager. |
||JobManager memory |Set the memory size used by a single JobManager. |
|Flink runtime parameters | |For configuration details of Flink\-related dynamic parameters and execution parameters, see [Flink official documentation](https://nightlies.apache.org/flink/flink-docs-release-1.11/ops/config.html).<br><br><br>* Single\-line editing mode: Enter key\-value pairs. The key can contain only letters, numbers, periods, underscores, and hyphens.<br><br>   * Add a row of parameters<br><br>   * Delete the parameter in this row<br><br>   * Clear the parameter values entered in the input box<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b7a70c68ac14bada7d7d08c230c7252~tplv-goo7wpa0wc-image.image) </span><br><br>* Script editing mode: Enter runtime parameters in JSON or YAML format |


<span id="_3-3-配置数据集成资源组。"></span>
### 3.3 Configure a data integration resource group

After completing the parameter configuration, you can click the configuration button for **Data Integration Resource Group** on the right to go to the Data Integration Resource Group page.

In the project console, select from the dropdown a data integration resource group that has already passed the resource group connectivity test to ensure that the task network is connected. For more information, see [Data Integration Resource Group](https://docs.byteplus.com/docs/dataleap/datasail_resource_group).

<span id="3112f5ff"></span>
### 3.4 Configure image versions

The update cycle for the global data integration product is relatively fast. Streaming integration tasks require you to specify a streaming image version number. It is recommended to promptly upgrade historical streaming tasks to the latest image version so that you can take advantage of new features and capabilities, ensure task stability and execution efficiency, and reduce operation and maintenance costs.


1. Click the configuration button for **Image Version** on the right to enter the image version number selection page.

2. In the streaming image version dropdown menu, select the image version number that currently has the **recommended** tag.


For more information and important notes about image versions, see [Management of datasail engine version upgrades](https://docs.byteplus.com/docs/dataleap/management_of_datasail_engine_version_upgrades).

<span id="_4-提交任务"></span>
## 4 Submit tasks

After configuring the required parameters for the task, submit and publish the task to the real\-time task operations section of the operations center for execution. Click the **Save** and **Submit for Launch** buttons in the operation bar. In the popup window, you must first go through the **Submit for Launch** process, and finally click the **Confirm** button to complete the task submission. For details, see [4.2 Submit Streaming Task](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-2-%E6%B5%81%E5%BC%8F%E4%BB%BB%E5%8A%A1%E6%8F%90%E4%BA%A4).

For details on operations and maintenance for subsequent tasks, see [Operations and maintenance of tasks](https://docs.byteplus.com/docs/undefined/689b13f8a8453604ecb6069e).
