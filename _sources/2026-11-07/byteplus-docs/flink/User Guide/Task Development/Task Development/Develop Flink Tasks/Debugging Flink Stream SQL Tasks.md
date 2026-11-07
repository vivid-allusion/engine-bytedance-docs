---
title: "Debugging Flink Stream SQL Tasks"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Debugging_Flink_Stream_SQL_Tasks"
---

The task verification function can only validate the correctness of SQL syntax and cannot fully prevent errors that may occur during code execution. Before deploying Flink Stream SQL tasks, it is highly recommended to complete debugging to reduce data quality risks and improve development efficiency.

The system provides two methods for debugging tasks: online data and offline data. Please choose as needed.

<span id="a3594b95"></span>
## Function Limitations


* Only Flink Stream SQL task types support creating session resource pools and debugging tasks.

   When you choose the execution mode as **Streaming**, the **Debug** and **Debugging Session Cluster** options will be displayed. If the execution mode is chosen as Batch, it will be hidden.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/771ae1e9d7cb4bb88899ab89e1dcddd3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a84528d731a544e4a7ee91273ba54cf7~tplv-goo7wpa0wc-image.image) </span>


* CTAS and CDAS syntax do not support debugging tasks.

* The session debugging task will automatically stop running after 30 minutes.


<span id="a388d79f"></span>
## Precautions

The session cluster is intended only for a development and testing environment; it is not recommended to use the session cluster in an official production environment.

<span id="1fa5d2d2"></span>
## Prerequisites

Debugging tasks are generally performed by developers (Project_Dev). It is necessary to have added project members and associated roles. Please refer to [Add project members](https://docs.byteplus.com/docs/flink/Member_Management#a45bfca3).

<span id="12286d01"></span>
## Create Session Resource Pool


1. Log in to the [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management**, then click the project block to enter the project.

4. In the project's left navigation bar, select **Job Development**.

5. In the **task development** page, select the target Flink SQL streaming task, set the execution mode to **streaming**, and choose the correct engine version.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a38ffdc4e4240e586109f86ce6698b9~tplv-goo7wpa0wc-image.image) </span>


6. Click on the left navigation bar to enter **Compute resource \> Session clusters**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccc68e883b9041efae705cbdecd05a7e~tplv-goo7wpa0wc-image.image) </span>


7. On the **Session cluster** page, click **create cluster**.

8. In the **Create cluster** panel, set key parameters for **basic configuration** and **resource configuration**, then click **confirm**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/992ced72d6e74402bdc6e112e84ed4dc~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** ||**Description** |
|---|---|---|
|**Basic Configuration: Required parameters.**  |||
|Resource Pool Name ||Customize the name of the Session resource pool.<br><br>Supports lowercase letters, numbers, and hyphens (\-), and must start and end with a lowercase letter or number, with a character length range of 2 ~ 63. |
|Flink Resource Pool Selection ||Select the target Flink resource pool from the dropdown list. |
|Engine Version ||Currently supported versions include **Flink 1.11\-byted** and **Flink 1.16\-byted**, and it is recommended to choose a version that matches the task's engine version, otherwise, an engine version mismatch will be indicated during task debugging. |
|**Resource Configuration: Optional parameters, default basic resource configurations are already in place.**  |||
|Task Manager Settings |Minimum Number of Task Managers |The minimum number of Task Managers is set to 1 by default, but can be adjusted to 0. |
||Maximum Number of Task Managers |The minimum number of TaskManagers is 10 by default. |
||CPU |The number of CPU cores for TaskManager defaults to 2, with a minimum of 0.5. |
||Memory |The memory size of the TaskManager will automatically adjust based on the set number of CPU cores, in a 1C4G ratio. |
||Number of Slots |It is recommended that each slot uses resources of no less than 1 core 4 GiB, and each Task Manager can configure 2 slots. |
|Job Manager Settings |CPU |The number of CPU cores for the JobManager is 1 core by default, with a minimum of 0.5. |
||Memory |The memory size of the JobManager will be automatically adjusted based on the number of CPU cores you set, in a 1C4G relationship |
|Custom parameters |Parameters can be customized as needed, in a Key\-Value format ||



8. After creation, return to the Session resource pool list page, and click the **actions** column under the **start** button.

   After the Session resource pool is created, it is by default in **not started** state, and you need to start the resource pool.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00307f4a54be434cba1ff641f04b79d0~tplv-goo7wpa0wc-image.image) </span>

<span id="8fd61e2b"></span>
## **Debug tasks with online data**


1. Choose **Task development** from the left navigation bar of the project.

2. On the **Task development** page, select the target Flink Stream SQL task, set the execution mode to **Streaming**, and choose the correct engine version.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a38ffdc4e4240e586109f86ce6698b9~tplv-goo7wpa0wc-image.image) </span>

3. Above the editing area, click **Debug**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d64cd6182baf427fb7caa719cd46f739~tplv-goo7wpa0wc-image.image) </span>

4. In the **debugging task** dialog, select the **use online data** type and **Session resource pool**, then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/494a5dd6e18b448e80ba3ef357fc8c25~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only select a Session resource pool that matches the version of your task engine. If the versions do not match, the option will be grayed out and unavailable, and a corresponding message will be displayed   </div>
   

5. View the task debugging results, then click the red stop task button.

   The system returns to the task editing page, where you can view the debugging results below the task editing area. Once the task debugging results meet expectations, stop the debugging promptly to avoid occupying resources for an extended period.

   You can also choose to pause the debugging, view the Flink UI, and check the operation logs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f36da424cfe4decb301a555747ea070~tplv-goo7wpa0wc-image.image) </span>


<span id="b03d55d3"></span>
## Debug tasks using offline data

The system generates a debugging data template based on the task's SQL statement (a `.csv` file), which you can download, fill with debugging data, and then upload to the console for debugging to determine if the results match the expected results.


1. In the project's left navigation bar, select **Task Development \> Tasks**.

2. Above the editing area, click **Debug**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d64cd6182baf427fb7caa719cd46f739~tplv-goo7wpa0wc-image.image) </span>

3. In the **debug task** dialog, click on **debug data template** to download the template to your local machine.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37ba6e5cd5894c269d9d129b46cf1f9f~tplv-goo7wpa0wc-image.image) </span>

4. Open the debug file template locally and fill in the debug data.

5. In the **debug task** dialog, select **use debug file** and **Session resource pool**, then upload the debug file and click **next**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When uploading local offline debugging data files, you should note the following two points:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system only supports uploading files in CSV format, and the file must contain a Schema header, such as id(INT)   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maximum memory size of the uploaded file is 1 MB, or a maximum of 1000 data rows for testing   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only select a Session resource pool that matches the version of your task engine. If the versions do not match, the option will be grayed out and unavailable, and a corresponding message will be displayed   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbac1499a8274892a2c150a23da8422c~tplv-goo7wpa0wc-image.image) </span>

6. After confirming the test data is uploaded correctly, click **confirm**.

7. View the debug results of the task.

   The system returns to the task editing page, where you can view the debug results below the task editing area. Once you confirm the debug results meet expectations, please stop debugging promptly to avoid prolonged resource occupation.

   You can also choose to pause debugging, view Flink UI, or view the operation logs.


<span id="8bd847d2"></span>
## View the Session debug results

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b217b0f97f744fa1a52f65489b9f15f4~tplv-goo7wpa0wc-image.image) </span>

In the lower part of the task editing area, you can view the debug results:


* Pause/Restart Button: For running debug tasks, you can choose to pause the task; for paused debug tasks, you can choose to restart the task.

* Stop Button: Stop the debugging task.

* Flink UI: Navigate to the Dashboard page to view the operation details of the current Session debugging task.

* Run Results: View the output results of the current Session debugging task.

* Run Logs: Supports viewing Client logs to understand how the tasks are running.

* Collapse/Expand Button: Controls the display button for debugging results.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abae7cc551f146079c9aea7230605148~tplv-goo7wpa0wc-image.image) </span>

When a debugging task fails, the reason for failure will be returned. Please solve the problem according to the prompts, then retry the Session debugging task.

<span id="393bc617"></span>
## Manage Session Cluster

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df293aecb8fa4a51abd27f5f3032735a~tplv-goo7wpa0wc-image.image) </span>

After creating a Session cluster, the following operations can be performed as needed:


* View details: Click the cluster name to view the details of the resource pool configuration.

* Start/Stop Cluster: Control the start and stop status of the cluster as needed.

* View BytePlus Flink UI: When the cluster is running, you can click **BytePlus Flink UI** to view the details of debugging tasks on the cluster.

* Edit Cluster: When the cluster is stopped, you can modify the cluster configuration, including engine version switching and resource configuration adjustments.

* Delete Cluster: When the cluster is stopped, you can delete the Session cluster.
