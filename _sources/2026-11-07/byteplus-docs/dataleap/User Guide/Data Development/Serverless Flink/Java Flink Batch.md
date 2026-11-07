---
title: "Java Flink Batch"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/java_flink_batch"
---

After integrating DataLeap with the **Serverless Flink** and associating Flink projects and resource pools, you can develop Java Flink Batch offline jobs to perform complex offline statistical analysis and processing of massive historical data.

This article will introduce the operations in the development process of Java Flink Batch jobs.

<span id="972b1afc"></span>
## 1 Usage limitations


* Only after enabling the **Professional (Big data analytics)**  services in the DataLeap product can you bind the **Serverless Flink Engine**. For details about the bind engine action, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

* Currently, the Flink 1.17 execution engine version is only available to users on the allowlist. You can [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2hvbWU%3D) to request that the DataLeap support staff add you to the allowlist. Once you have been added, you can use this version.

* If a task references Jar or File resources, and a custom connector and a built\-in connector in the resource type have the same name, using them in the same task is not supported; otherwise, a conflict exception may occur during the task run. For details about built\-in connectors, see the [connector list](https://docs.byteplus.com/en/docs/flink/Connector_Overview).


<span id="6f41301c"></span>
## 2 Prerequisites for use


1. When a sub\-account performs project binding for a Flink Engine instance:

   1. The main account must first import IAM users into the [Serverless Flink Console](https://console.byteplus.com/flink/region:flink+ap-southeast-1/overview). For operation details, see: [Accounts Management](https://docs.byteplus.com/en/docs/flink/Accounts).

   2. And add the sub\-account to the corresponding engine project. For operation details, see: [Engine project member management](https://docs.byteplus.com/en/docs/flink/Member_Management).


<span id="d491bc5a"></span>
## **3 Create a task**


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In a specific project, go to the **Data Development** interface and click the **New Task** button to create a new task.

3. Select **Data Development \> Serverless Flink \> Java Flink Batch** as the task type.

4. Fill in the Basic Task Info, click the **OK** button to complete the creation of the task.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In the Project Console management interface, if you add a new engine or modify an existing one, you need to refresh the entire DataLeap Data Development interface while in the Create Data Development task window. Only after refreshing will the new or modified engine task types become visible.</div>


2. <div data-tips="true" data-tips-type="warning">Task name information may only contain numbers, letters, underscores（_）and hyphens（\-）. The beginning and end character must be a number or letters, and the input must be between 1 and 63 characters in length.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13b655f842b44a81bd1e03a6c4a360cd~tplv-goo7wpa0wc-image.image) </span>

<span id="ef943e01"></span>
## 4 Task configuration description

<span id="c9052624"></span>
### **4.1 Reference resources**

Set the resource JAR package using the following parameters:


* When selecting a Jar package, you can choose resources in the following ways:

   * In the Resources Library, select the created **Serverless Flink** resource.

   * Create a New Resource directly in the dropdown, or create a Streaming Flink Resource in the **Resources Library** in the left navigation bar. see [Resources Library](https://docs.byteplus.com/docs/200/682aa9fee638492ec7c94266).

* The execution engine currently supports Flink 1.16 and Flink 1.17 versions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the Flink 1.17 execution engine version is available only through an allowlist. You can <a href="https://console.byteplus.com/workorder/create?ref=L2hvbWU%3D">submit a ticket</a> to consult with DataLeap support and request to be added to the allowlist. After being added, you can use it.   </div>
   

* Main Class: Fill in the main class of the JAR package program. Example: com.bytedance.openplatform.datastream.DatagenToPrint.


<span id="11b374eb"></span>
### **4.2 Flink running parameters**

Fill in Flink\-related dynamic parameters and execution parameters. The platform has provided some commonly used **SQL parameters, State parameters, and Runtime parameters** and more for you. You can select as appropriate, or input the required parameters yourself. For more parameters, see the [Flink official documentation](https://nightlies.apache.org/flink/flink-docs-release-1.11/ops/config.html).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For commonly used parameters provided by the platform, you must first set the appropriate <strong>Reference resources</strong> and specify the <strong>Execution engine</strong> version. Only then will the parameter appear in the dropdown box.</div>



* Single line edit mode: Fill in key\-value pairs. Only letters, numbers, decimal points, underscores, and hyphens are allowed in the key.

   a. Add a row of parameters

   b. Delete this row of parameters

   c. Clear parameter values already entered in the text box

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb4a855dd4b7477fb93698d653ecbe52~tplv-goo7wpa0wc-image.image) </span>

* Script edit mode: Fill in operation parameters using the JSON or YAML format.

* Subclass view mode: After you enter input parameters in the edit mode above, you can click **Subclass view mode**. This mode automatically classifies the added parameters, making it easier for you to understand the input Flink parameters when there are many parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the parameters you need to use within the corresponding category by keyword.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the corresponding parameters cannot be found under the specified category, you can enter them yourself in the "Other Parameters" category.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enter the parameters under the "Other Parameters" category. If they belong to the "SQL Parameter/State Parameter/Runtime Parameter" category, the system will attribute them to the corresponding category after editing is completed.   </div>
   


<span id="e49fb68f"></span>
### **4.3 User\-defined parameters**

User\-defined parameters allow you to fill in parameter information for related data source instances. For example, when connecting to a **kafka** message queue, you need to provide parameters such as the Topic and access point address. You can also fill in related parameters such as resource configuration for task execution or data processing time.


* Single line edit mode: Fill in key\-value pairs. The key may only contain letters, numbers, decimal points, underscores, and hyphens.

* Script edit mode: Fill in operation parameters using JSON or YAML format.


<span id="125ca403"></span>
### 4.4 Schedule settings

After completing the task configuration, click the **Scheduling Configuration** button in the right navigation bar to open the scheduling configuration window. Here, you can set information such as **Basic Info, Scheduling attributes, dependencies, task input and output**. For detailed parameter settings, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

<span id="4eb2a680"></span>
#### 4.4.1 Advanced parameters

For Java Flink Batch tasks, you can set **Advanced parameters,**  in the scheduling attributes. You can enter the parameters required for the Flink task here. You can add them in the following two ways:


* Single line edit mode: Enter key\-value pairs. Only letters, numbers, decimal points, underscores, and hyphens are supported for the key.

   * Add a row of parameters

   * Delete the current line of parameters

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dff4b1e71abd4a15b265528076e7cc60~tplv-goo7wpa0wc-image.image) </span>

* Script edit mode: Fill in operation parameters using the JSON or YAML format.


For a description of advanced parameters, see the [Flink parameter configuration document](https://nightlies.apache.org/flink/flink-docs-release-1.16/docs/dev/table/config/).

<span id="8d91c1bf"></span>
#### 4.4.2 Dependencies

Here, you can configure the upstream and downstream dependencies of batch tasks to complete data lineage construction. This ensures that, during downstream execution, the output data from upstream can be accurately obtained, thereby ensuring data quality and improving data development efficiency.

For details on the action for configuring upstream and downstream dependencies, see [Task scheduling depends on](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies).

<span id="a913f824"></span>
#### 4.4.3 Input and output parameters

After configuring upstream dependencies for a task, you can set the task's input and output parameters to enable parameter passing between upstream and downstream tasks. The value of these parameters can be sourced from the output results of upstream tasks, project parameters, or custom parameter values.

For details on input and output parameter operations, see [Input and Output Parameter Settings](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings).

<span id="afc1045c"></span>
#### 4.4.4 **Resource settings**

Configure resource allocation for task runtime:


|Parameter name |Description |
|---|---|
|TaskManager count |Set the number of TaskManagers in a Flink job. |
|Single TaskManager CPU count |Settings for the number of CPUs used by a single TaskManager |
|Single TaskManager memory size (MB) |Set the memory size for a single TaskManager. |
|Slots per TaskManager |Settings for the number of slots in a single TaskManager |
|JobManager CPU count |Set the number of CPUs used by a single JobManager |
|JobManager memory |Set the memory size for a single JobManager. |


<span id="5cef0f7c"></span>
## 5 Commit task

After the SQL statement and the required parameters for the task have been configured, you can submit and release the task to Batch Task Maintenance in the Operations Center for periodic execution.

Click the **Save** and **Commit for Deploy** buttons in the upper Action bar. In the **Commit for Deploy** dialog box, choose parameters such as **Backfill data, Monitor Settings, and Commit settings**. Finally, click the **Confirm** button to complete the job submission. For Commit for Deploy instructions, see [4 Commit for Deploy](https://docs.byteplus.com/docs/200/46949#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

For details on subsequent task operations, see [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).

&nbsp;
