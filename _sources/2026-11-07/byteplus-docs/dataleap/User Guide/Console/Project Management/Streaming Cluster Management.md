---
title: "Streaming Cluster Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/streaming_cluster_management"
---

This feature interfaces with the SF (Serverless Flink) engine, used to create and manage session clusters for Flink SQL task debugging.

<span id="_1-约束限制"></span>
## Constraints

Currently, roles from developer level and above can configure session clusters. Permissions will be withdrawn in the future, and only project administrators will have the configuration rights.

<span id="_2-前提条件"></span>
## **Prerequisites**

Purchased and configured the Serverless Flink engine service. For configuration engine service operations, please refer to [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

<span id="_3-操作步骤"></span>
## **Operation Steps**


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left sidebar to enter the **Project Management** page.

3. Check the **My managed projects** option to display the list of projects managed by you.

4. Click any **Action** button in the project list to enter the **Project Console**.

5. Click **Streaming Cluster** in the left sidebar to enter the **Streaming Cluster** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5906e78ff51f4d57858bdaae67c56073~tplv-goo7wpa0wc-image.image) </span>

6. The following actions can be performed:

   * Create Cluster

      Click the **New Cluster** button, set the relevant information in the popup **New Cluster** window, and then click the **OK** button to complete the creation. The newly created cluster is in a terminated state and needs to be manually started.

      The parameters for creating a session cluster are described in the following table. The parameters marked with \* are required, while those not marked with \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Cluster Name |The name of the Session cluster can be set by you, supporting English, numbers, or underscores, with a length not exceeding 50 characters. |
      |Description |Description information of the cluster, not exceeding 200 characters. |
      |\*Parameter Setting |Settings for cluster\-related resource parameters, including three parts: JobManager, TaskManager, and Custom parameters.<br><br><br>* JobManager<br><br>   * \*CPU: The number of CPUs occupied by a single JobManager, default is 1, adjustable as needed.<br><br>   * \*MEM: The memory size occupied by a single JobManager, default is 4096, not editable, and will change according to the CPU changes.<br><br>* TaskManager<br><br>   * \*CPU: The number of CPUs occupied by a single TaskManager, default is 1, adjustable as needed.<br><br>   * \*MEM: The memory size occupied by a single TaskManager, default is 4096, not editable, and will change according to the CPU changes.<br><br>   * \*Slots: The number of slots in a single TaskManager, default is 1, adjustable as needed.<br><br>   * \*Minimum TM quantity: The minimum threshold for TaskManager numbers, default is 4, adjustable as needed.<br><br>   * \*Maximum TM quantity: The maximum threshold for TaskManager numbers, default is 8, adjustable as needed.<br><br>* Custom parameters: User\-defined parameters set on demand in a key\-value pair format. |
      |\*Engine Project |Select the engine project to use from a dropdown list of created engine projects.<br><br>For instructions on creating engine projects, refer to [Import Project](https://docs.byteplus.com/en/docs/flink/Import_Project_From_BytePlus) in Serverless Flink. |
      |\*Computing Resources |Computing resources under the engine project, selectable from a dropdown of created resources.<br><br>For instructions on creating computing resources, refer to [Resource Management](https://docs.byteplus.com/en/docs/flink/Resource_Management) in Serverless Flink.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting this parameter is only possible after selecting <strong>Engine Project</strong>.</div><br> |
      |\*Engine Version |Supported versions are Flink\-1.11, Flink\-1.16, and Flink\-1.17, selectable from a dropdown. |
      

   * Start Cluster

      Click the **Start** button in the **Action** column of an information item in **terminated** state. After confirming twice, you can start the cluster.

   * Stop Cluster

      Click the **Stop** button in the **Action** column of an information item in **Running** or **Not ready** state. After confirming twice, you can stop the cluster.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Stopping the cluster will terminate all instances currently running in the cluster. Please proceed with caution!      </div>
      

   * Edit Cluster

      Click the **Edit** button in the **Action** column of an information item to modify the cluster's configuration information.

   * Delete Cluster

      Click the  **...**   **\> Delete** button in the **Action** column of an information item in **Terminate** state, after double confirmation, you can delete the cluster

   * View the launch log

      Click the  **...**   **\> Task start log** button in the **Action** column of some information item to view the cluster's start log and search the log as needed

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only clusters that have been started can view logs. Otherwise, this button will be disabled.      </div>
      

   * View Flink UI

      Click the  **...**   **\> Flink UI** button in the **Action** column of an information item in **Running** state,

      and then you can jump to the Flink management page to view the cluster's metric information.

   * View debugging task information

      * Click the **Expand/Collapse** icon button for a cluster information to view the debugging task information for that cluster

      * You can click the **View Task** button on a particular task to jump to its page and view detailed information.


<span id="_4-后续操作"></span>
## Subsequent Actions

After configuring the session cluster, you can go to the **Data Development** page of the project to perform FlinkSQL task debugging.
