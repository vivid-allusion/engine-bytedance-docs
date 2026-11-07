---
title: "Serverless Java Flink"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/serverless_java_flink"
---

DataLeap has integrated **Serverless Flink**. After associating the Flink project and resource pool, you can develop Flink jobs. Hosting and operations of native tasks can be achieved through Serverless Java Flink jobs. This article will introduce to you, using a simple example, the operations involved in the development process for Serverless Java Flink jobs.

<span id="b55134f6"></span>
## 1. Usage limitations


* Only after enabling **Professional (Big data analytics)**  services, you can bind the **Serverless Flink engine**. For details on binding engine operations, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

* Serverless Java Flink does not support the **automatic parsing** feature for registering Datasource yet.


<span id="_2-使用前提"></span>
## 2 Use prerequisites


* When a sub\-account performs project binding on a Flink Engine instance:

   1. The main account must first import IAM users into the [Serverless Flink Console](https://console.byteplus.com/flink/region:flink+ap-southeast-1/overview). For operation details, see: [Accounts Management](https://docs.byteplus.com/en/docs/flink/Accounts).

   2. And add the sub\-account to the corresponding engine project. For operation details, see: [Engine project member management](https://docs.byteplus.com/en/docs/flink/Member_Management).

* Currently, the Flink 1.17 execution engine version is available only through a whitelist. You can [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2hvbWU%3D) to contact us. After we add you to the whitelist, you will be able to use it.


<span id="_3-任务配置说明"></span>
## 3 Task configuration description

<span id="_3-1-新建任务"></span>
### **Create a task**


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In a specific project, enter the **Data Development** interface and click the **New Task** button to create a new task.

3. Sequentially select **Data Development \> Serverless Flink \> Serverless Java Flink** task type.

4. Fill in the basic task info, then click the **OK** button to complete task creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In the project console management interface, if you add or modify an engine, you need to refresh the entire DataLeap data development interface in the task creation window to see the newly added or modified engine task types.</div>


2. <div data-tips="true" data-tips-type="warning">Task name information may only contain numbers, letters, underscores（_）and hyphens（\-）. The beginning and end character must be a number or letters, and the input must be between 1 and 63 characters in length.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/271a2043712e4ff09890715db0e590aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-引用资源"></span>
### **3.2 Reference resources**

Set the JAR package using the following parameters:


* To select a Jar package, you can choose resources using the following methods:

   * Select existing resources in the Resources Library.

   * Create a new resource directly in the dropdown menu, or create a **streaming compute Flink resource** in the **Resources Library** in the left navigation bar. For details, see [Resources Library](https://docs.byteplus.com/docs/200/682aa9fee638492ec7c94266).

* Execution engine: The execution engine allows you to choose Flink version 1.11, 1.16, or 1.17.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the Flink 1.17 execution engine version is only available via the allowlist. You can <a href="https://console.byteplus.com/workorder/create?ref=L2hvbWU%3D">submit a ticket</a> to contact us. After being added to the allowlist, you can use it.   </div>
   

* Main Class: Enter the main class of the Jar package. For example: com.bytedance.openplatform.datastream.DatagenToPrint.


<span id="005df2cd"></span>
### 3.3 Resource settings

Configure allocation of related resources at task runtime


|Parameter name |Description |
|---|---|
|TaskManager count |Set the number of TaskManagers in a Flink job |
|Single TaskManager CPU count |Set the number of CPUs used by a single TaskManager |
|Single TaskManager memory size (MB) |Set the memory size used by a single TaskManager. |
|Number of slots per TaskManager |Set the number of slots in a single TaskManager |
|JobManager CPU count |Set the number of CPUs used by a single JobManager. |
|JobManager memory |Set the memory size for a single JobManager. |


<span id="_3-3-flink运行参数"></span>
### **3.3 Flink running parameters**

Fill in Flink\-related dynamic and execution parameters. The platform provides some commonly used **SQL parameters, State parameters, Runtime parameters, and more**. You can select parameters as needed or enter your own. For more parameters, see the [Flink official documentation](https://nightlies.apache.org/flink/flink-docs-release-1.11/ops/config.html).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The commonly used parameters provided by the platform will only be displayed in the dropdown box after you have set the corresponding execution engine version in <strong>Reference resources</strong> in advance.</div>



* Single line edit mode: Fill in key\-value pairs, where:

   * Only letters, numbers, decimal points, underscores, and hyphens are allowed for the key value;

   * For the value field, you can input a fixed value or, depending on the actual scenario, input a **project or custom parameter variable** in the form of, for example, {{project_param_rows}}. Using parameter variables improves task execution efficiency in different environments. For an introduction to project or custom parameter variables, see [3.4.5 Task input parameters](https://docs.byteplus.com/docs/dataleap/serverless_flink_sql#_3-4-4-%E4%BB%BB%E5%8A%A1%E8%BE%93%E5%85%A5%E5%8F%82%E6%95%B0) for details.

      The remaining operating instructions are as follows:

      a. Add Row

      b. Delete the current line of parameters

      c. Clear parameter values already entered in the text box

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/525ecd59bf7449f0b88c1bbf885262f2~tplv-goo7wpa0wc-image.image) </span>

* Script edit mode: Fill in operation parameters using the JSON or YAML format.

* Subclass view mode: After you input parameters in the Edit mode above, you can click **Subclass view mode**. This supports the automatic classification of added parameters, helping you more easily understand the input Flink parameters when dealing with a large number of parameters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">You can search for the parameters you need to use under the corresponding category using keywords.</div>


2. <div data-tips="true" data-tips-type="tip">If the corresponding parameters cannot be found under the specified category, you can enter them yourself in the "Other Parameters" category.</div>


3. <div data-tips="true" data-tips-type="tip">Enter the parameters under the "Other Parameters" category. If they belong to the "SQL Parameter", "State Parameter", or "Runtime Parameter" category, the system will assign them to the corresponding category after editing is completed.</div>



<span id="_3-4-用户自定义参数"></span>
### **3.4 User\-defined parameters**

User\-defined parameters require you to provide relevant instance information for the real\-time data source. For example, when integrating with the **kafka** message queue, you need to provide parameters such as the Topic, the access point address, and other parameter information.


* Single line edit mode: Fill in key\-value pairs as follows:

   * Only letters, numbers, decimal points, underscores, and hyphens are allowed in key values.

   * For the value, you can enter a fixed value or, depending on the actual scenario, a **project or custom parameter variable** in a format such as {{project_param_rows}}. Using parameter variables improves the efficiency of task execution in different environments. For detailed instructions on using project or custom parameter variables, see [3.4.5 Task input parameters](https://docs.byteplus.com/docs/dataleap/serverless_flink_sql#_3-4-4-%E4%BB%BB%E5%8A%A1%E8%BE%93%E5%85%A5%E5%8F%82%E6%95%B0).

* Script edit mode: Fill in operation parameters in JSON or YAML format.


<span id="_3-5-参数设置"></span>
### **Parameter setting**

Click **Parameter Setting** in the right navigation bar to configure the task's **Basic Info, Resource settings, and Data source registration**.

<span id="_3-5-1-基本信息"></span>
#### 3.5.1 **Basic info**

Basic Info configuration for a Serverless Java Flink task:


|Parameter name |Description |
|---|---|
|Task name |Show the Task name entered when creating the task. Modification is not supported in Parameter Setting. To modify it, click **More** to the right of the Task name in the left Task directory structure, then click **Rename**. |
|Task type |Serverless Java Flink |
|Engine type |Serverless Flink. |
|Associated engine project |Name of the engine project associated with DataLeap. |
|Description |Optional. You can provide a detailed description of the task to facilitate subsequent viewing and management. |
|Owner |Only one member is allowed. By default, this is the task creator, who is also the default recipient when task execution fails or when the review is passed or fails. You can change this to another project member as needed.<br><br><br>* The Owner must be a Project Member with Edit permissions, and Project Auth must be authorized by the Project Administrator.<br><br>* DataLeap enables collaborative development through Project Space. Roles with edit permissions in a project can edit all tasks within that project, so there is no need to assign multiple owners to a task in order to achieve the effect of collaborative cooperation. |
|Computing resources |Choose the target resource pool from the related engine project. |


<span id="5aa5826d"></span>
#### 3.5.2 Import resources

Serverless Java Flink tasks support importing resource types such as Jar packages and file resources, allowing you to customize connector within Jar or file resources. You can perform actions such as editing Flink SQL tasks, session debugging, Commit for Deploy and Execute, and other actions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When a custom connector and a built\-in connector have the same name in the Jar or File resource type, using them in the same task is not supported; otherwise, a conflict exception may occur during task execution. See the <a href="https://docs.byteplus.com/en/docs/flink/Connector_Overview">connector list</a> for details.</div>


* <div data-tips="true" data-tips-type="tip">When a production Java Flink task is running and contains a resource reference, if the resource file is updated, then after the resource library updates the resource file, you need to go to the operations center to <strong>restart</strong> the streaming task for the resource change to take effect.</div>



In the dropdown, choose Jar and File resources that have been uploaded to the Resources Library and approved. Multiple selection is supported. If you have not uploaded any resources yet, you can click the “**New Resource**” button to go to the Resources Library and create resources. For details, see [Resources Library](https://docs.byteplus.com/docs/undefined/682aa9fee638492ec7c94266).

<span id="da04d2f5"></span>
#### 3.5.3 Task input parameters

If you want the same code to automatically differentiate between engine environmental parameters, project parameters, custom parameters, and more depending on the execution environment, you can meet this requirement by setting the input parameters for the task.

Task input parameters allow you to use custom parameters and project parameters in streaming tasks by passing them as variables or constants. You can access them in code using the {{Parameter name}} format. For details about configuration actions, see [3.4.5 Task input parameters](https://docs.byteplus.com/docs/dataleap/serverless_flink_sql#_3-4-4-%E4%BB%BB%E5%8A%A1%E8%BE%93%E5%85%A5%E5%8F%82%E6%95%B0).

<span id="d85f2b34"></span>
#### 3.5.4 Data source registration

Register the Source and Sink information used by this task so that it can be used for subsequent monitoring configuration and lineage construction. Manual addition is supported via **add manually**.


* Add manually: Click the **add manually** button to register the upstream and downstream of the datasource based on SQL logic.

   * Source/Target: Selection of Source and Sink is supported.

   * Source type: Supports automatic parsing of datasources when using the following connectors: DataGen, Rmq, Bmq, JDBC, Abase, Volcengine, or self\-hosted Kafka.

   * For each data source type, you need to provide the corresponding information. You can configure each data source type according to your actual scenario. For example, for the Kafka data source type, you need to specify details such as the Bootstrap Servers, Topic name, and consumer group.

   * Direct upstream tasks: You can search for upstream tasks by manually entering the task name and click the **Add** button to add manually.

   * Manual addition is not allowed; only results that have been matched through the datasource are displayed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Abase and Rmq source types only support the Parse action; running after activation and posting is not supported yet. Abase data sources are typically used during the cloud migration of internal BytePlus business\*\*.\*\*   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Serverless Java Flink does not yet support the <strong>automatic parsing</strong> feature for registering datasources.   </div>
   

* Batch delete: To delete **manually added** datasources, select the registered datasources, then click the **Delete** or **Batch Delete** button on the right to remove the selected datasources.

* View upstream and downstream tasks: Upstream and downstream tasks parsed from data source registration are displayed. You can edit, add, delete, or disable upstream dependent tasks. You can only view downstream tasks.


<span id="_4-提交发布"></span>
## **Step 4: Commit for Release**

After configuring the task parameters, commit the task for release to Stream Task Maintenance in the Operations Center for execution.

Click the **Save** and **Commit for Deploy** buttons in the Action bar. In the popup, you must first complete the **Online Check** and **Commit for Deploy** steps in the deployment process. Finally, click the **Confirm** button to complete the task submission. For details, see [4.2 Submit Streaming Task](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-2-%E6%B5%81%E5%BC%8F%E4%BB%BB%E5%8A%A1%E6%8F%90%E4%BA%A4).

For details on operation and maintenance actions for subsequent tasks, see [Operations and maintenance of tasks](https://docs.byteplus.com/docs/200/689b13f8a8453604ecb6069e).
