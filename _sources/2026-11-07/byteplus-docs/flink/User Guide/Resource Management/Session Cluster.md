---
title: "Session Cluster"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Session_Cluster"
---

Session Cluster is a pre\-started and continuously running cluster, which allows multiple jobs to be submitted at different times and resources to be shared for execution, reducing the start\-up time overhead for jobs. In this product, the Session Cluster is mainly a tool for Flink users to quickly debug SQL code and diagnose code issues.

<span id="ccbbbce9"></span>
## Feature Limitations


* Only the Flink Stream SQL task type supports using Session Cluster for debugging tasks.

   When you select the execution mode as **STREAMING**, the **Session Debugging** and **Debug Resource Pool** options will be displayed. If the execution mode is selected as Batch, it will be hidden.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/487044e350ad40aeb7c996b7bf23d48a~tplv-goo7wpa0wc-image.image) </span>

* CTAS and CDAS syntax do not support debugging tasks.

* Session debugging tasks will automatically stop running after 30 minutes.


<span id="5eccfd31"></span>
## Precautions

The Session cluster is solely for development and testing environments and is not recommended for official production use.

<span id="7a717c83"></span>
## Prerequisites

Debugging tasks are typically performed by developers (Project_Dev), and require team members to be added and associated with roles, please see [添加项目成员](https://docs.byteplus.com/docs/flink/45840#a45bfca3).

<span id="9a67719d"></span>
## Create Session Cluster


1. Login to the [BytePlus Flink console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then click into the project block to enter the project.

4. In the left navigation bar of the project, select **Resource Management \> Session Clusters**.

5. On the **Session Clusters** page, click **Create Session Cluster**.

6. In the **Create Resource Pool** panel, set the key parameters for **Basic Configuration** and **Resource Configuration**, then click **Confirm**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63e5635d0a704aecb8bc71fb40dbabdf~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** ||**Instruction** |
|---|---|---|
|**Basic configuration: required parameters.**  |||
|Cluster Name ||Customize the Session cluster name.<br><br>Supports lowercase letters, numbers, and hyphens (\-), and must start and end with a lowercase letter or number, with a character length range of 2 to 63. |
|Flink Resource Pool Selection ||Select the target Flink resource pool from the dropdown list. |
|Engine Version ||Currently supports **Flink 1.16\-volcano** and **Flink 1.11\-volcano** versions, it is recommended to choose an engine version consistent with the task, otherwise, there will be a prompt about engine version mismatch during task debugging. |
|**Resource Allocation: Optional parameters, default basic resource configurations are already in place.**  |||
|Task Manager Settings |Task Manager Minimum Count |The minimum number of Task Managers is set to 1 by default, adjustable to 0. |
||Task Manager Maximum Count |The minimum number of Task Managers is set to 10 by default. |
||CPU |The number of CPU cores for a Task Manager is set to 2 by default, with a minimum value of 0.5. |
||Memory |The memory size for a Task Manager will automatically adjust based on your CPU core settings, following a 1C4G ratio. |
||Slot Count |Recommended minimum resource for a slot is not less than 1 core and 4 GiB. Each Task Manager can be configured with 2 slots. |
|Job Manager Settings |CPU |The number of CPU cores for JobManager, with a default value of 1 core and a minimum of 0.5. |
||Memory |The memory size for JobManager will automatically adjust based on the CPU cores you set, following a 1C4G relationship. |
|Custom Parameters |Parameters can be customized as needed, in a Key\-Value format. ||


<span id="0fa0351b"></span>
## Manage Session Clusters

In the **Resource Management \> Session Clusters** module, you can view and manage all the Session clusters under the current project. You can view information about Session clusters such as name, ID, status, engine version, CPU, and memory.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d99789c3071d437e9cb4e0e01757b08a~tplv-goo7wpa0wc-image.image) </span>

After creating Session clusters, you can perform the following operations on demand:


* **View Details**: Click on the resource pool name to view the details of the resource pool configuration.

* **Start/Stop Session Clusters**: Control the start and stop status of the resource pool as needed. Consider stopping if SQL tasks are not needed for an extended period.

* **View Flink UI**: In the running state of the resource pool, you can click **Flink UI** to view the running details of debugging tasks on the resource pool.

* **Edit Resource Pool**: When the resource pool is stopped, you can modify the resource pool configuration, including changing the engine version and adjusting resource settings.

* **Delete Resource Pool**: The resource pool can be deleted while in the stopped state.
