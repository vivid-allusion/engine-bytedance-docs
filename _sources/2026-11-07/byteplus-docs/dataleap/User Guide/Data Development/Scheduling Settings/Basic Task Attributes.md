---
title: "Basic Task Attributes"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/basic_attribute_of_task"
---

<span id="bbd505c7"></span>
## **1 Overview**

Task scheduling refers to the process where the system automatically executes tasks at a specific scheduled time to enhance development efficiency. Scheduling settings are divided into parts such as basic information, scheduling attributes, dependencies, and input\-output parameters.

This article will introduce explanations related to basic task attributes.

<span id="8204fffb"></span>
## **2 Access Points**


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc) **.** 

2. In the **Overview** interface, within the projects you have joined, click on **IDE development** to access the relevant project.

3. In the **Data Development** interface, in the left\-side navigation bar, double click to open a batch task to enter the node's editing interface.

4. Click the **Schedule** button on the right navigation bar to enter configuration.


<span id="02b312e1"></span>
## **3 Basic Info**

The basic task info is introduced as the following table shows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5719c64f54548488a4dfc01f9fbe563~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Description |
|---|---|
|Task Name |Displays the task name entered during creation, which cannot be modified in the Schedule Settings. It can be modified by clicking **More** next to the task name in the task directory tree structure, then clicking on **Rename**. |
|Task Type |Different engine types support different types of tasks. |
|Engine |Supported engine types include Serverless Flink Edition, ByteHouse Enterprise Edition (ByteHouse CE), ByteHouse Cloud Data Warehouse Edition (ByteHouse CDW), and EMR Serverless Spark. |
|Associated instance |When the engine type is **ByteHouse CE, or Serverless Flink Edition**, it simultaneously displays the associated instances or engine projects. |
|Description |Optional, allows for a detailed description of the task for easy viewing and management later. |
|Owner |Only one member is allowed by default, who is the task creator and the default recipient when the task execution fails, passes review, or fails review. You can modify this to other project members as needed.<br><br><br>* The responsible person must be a member with edit permissions in the project, and these permissions must be granted by the project administrator.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the selected owner only has visitor member role here, i.e., no project edit permissions, no one can submit tasks to the Operations Center, including the project administrator.   </div><br>   <br><br>* DataLeap facilitates development collaboration through project spaces. Members with edit permissions can edit all tasks within the project, making it unnecessary to set multiple responsible persons for a task to achieve collaboration. |
|Computing resources |When the task engine type is **Serverless Flink Edition**, you need to select the computing resources required for running the task. For detailed operations on Streaming Compute Flink resource information, see [Create Resource Pool](https://docs.byteplus.com/en/docs/flink/Create_VCI_resource_pool).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Resource pools created on the Streaming Computing Flink Edition console need to go to DataLeap <strong>Create Project \> Engine Service Binding</strong> for related binding operations. See details <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.</div><br> |
|Scheduling resource group |Select a resource group provided by DataLeap's platform for generating regular scheduling instances, which offers both public and exclusive scheduling resource groups. Among:<br><br><br>* **Public scheduling resource group**, offered by default on the platform;<br><br>* **Exclusive scheduling resource group**, which you can purchase based on actual circumstances, see details [Exclusive Scheduling Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_scheduling_resource_group).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In Notebook, Python, and Shell task types, if the computing resource group is an <strong>Exclusive computing resource group</strong>, the scheduling resource group will be cleared, i.e., these three types of tasks do not need to configure a scheduling resource group.</div><br> |
|Use project template |You can choose to use a template already created in **Project Console \> Template Management** for the current task  **.**  You can improve the configuration efficiency of the computing queue, priority, set parameters, and more when creating new tasks through template management.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only EMR Serverless Spark SQL task type supports the selection of using a project template. Other task types, please stay tuned.</div><br> |
|Project template |If the task chooses to use a project template, you need to select a successfully created template name from this dropdown. The content configured in the template, such as **resource queue, priority** and other contents, can overwrite the original configuration of the task, and these configurations cannot be modified within the task. See details[模板管理](https://docs.byteplus.com/docs/undefined/66ecf0731e6074032c015e5f)。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you need to modify the template parameters, you need to go to <strong>Project Console \> Template Management</strong> to make changes. This operation will affect all tasks using this template, so it must be handled with caution.</div><br> |
|Computing Queue |EMR Serverless Spark job type requires configuration of EMR Serverless Spark Jar, EMR Serverless Spark SQL job's Spark computing queue information. Supports dropdown selection of computing queues already bound in the project console. For details on Spark computing queue operations, see [Queue management](https://www.volcengine.com/docs/6491/1262219). |
|Calculation group |ByteHouse CDW SQL job type requires selecting computing groups already bound to the current project and used for querying in the ByteHouse_CDW console. For creation of calculation groups, see [ByteHouse CDW computation group](https://www.volcengine.com/docs/6517/76332). |


<span id="125e7adf"></span>
## 4 Subsequent Actions

After completing the Basic task info configuration, you can continue to configure the task scheduling properties. See details[Scheduling Attributes](https://docs.byteplus.com/docs/dataleap/scheduling_attributes)
