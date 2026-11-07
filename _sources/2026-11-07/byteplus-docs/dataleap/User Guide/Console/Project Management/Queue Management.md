---
title: "Queue Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/queue_management"
---

Through this feature, you can add queues already bound to the project to the queue management list and configure their use specifications, effectively constraining the queue usage in the project.

<span id="_1-约束限制"></span>
## Limit Restrictions

Only Project Administrators can manage queue information.

<span id="_2-管理队列信息"></span>
## Manage Queue Information


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left navigation bar to enter the **Project Management** page.

3. Select the **My managed projects** option to display the project list managed by you.

4. Click the  **... \>**  **Queue management** button in the **Action** column of the project you want to manage in the project list, enter the **Queue Management** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb264370d3e4e10a8dd23c77672eebf~tplv-goo7wpa0wc-image.image) </span>

5. The following actions can be performed:

   * Add Queue

      Click the **Add Queue** button, set the queue configuration information in the pop\-up window, then click the **OK** button to complete the addition of the queue.

      The parameter description for adding a queue is as shown in the table below. Parameters marked with \* are required, while those not marked are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Engine Type |Supports the selection of engine type **Serverless Flink**.<br><br>For detailed instructions on project engine binding, please refer to the service binding parameters **engine settings** of [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project). |
      |\*Engine Instance/Project |* Choose the engine instance information bound under the selected LAS or EMR engine.<br><br>* Select the engine project information bound under the Stream Computing Flink Edition engine. |
      |\*Queue |Select the queue or resource pool information added under the corresponding instance. |
      |Description |Add a queue description to facilitate subsequent management operations. |
      

   * Click the **Edit** button in the **Action** column of a queue listed, then in the **Edit Queue** pop\-up window, you can modify the queue's description.

   * Click the **Delete** button in the **Action** column of a queue listed, then in the pop\-up Confirm Deletion dialog, click the **OK** button to delete the queue.


<span id="_3-管理队列使用规范"></span>
## Queue Management Usage Specification


5. Log in to the DataLeap Console.

6. Click **Projects** on the left navigation bar to enter the **Project Management** page.

7. Check the **My managed projects** option to display a list of projects you manage.

8. Click the  **... \> Queue management** button in the **Action** column in the project list to enter the **Queue management** page.

9. Click the **Use Specification** button in the **Action** column of a queue in the list to enter the **Use Specification** management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34d13a9443814c5fb084d0195ed002f7~tplv-goo7wpa0wc-image.image) </span>

10. The following actions can be performed:

   * Add queue use specifications.

      Click the **Add Usage Specification** button, configure the queue usage specification information in the pop\-up window, then click the **OK** button to complete the creation of the usage specification.

      The following table shows parameter descriptions related to adding queue usage specifications. Parameters marked with \* are required, and those not marked with \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Specification Name |Queue Usage Specification \- Enter name information as required. |
      |Description |Description for the specification; input as necessary for subsequent management. |
      |\*Application Scope |Queue usage specification supports the following four options, which can be selected from a dropdown:<br><br><br>* Batch Task Configuration<br><br>* Batch Task Backfill<br><br>* Ad\-hoc Query<br><br>* Streaming Task Configuration<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Under the same queue, only one standard can be configured for the same application scope.</div><br> |
      |More Settings |After choosing **Application Scope**, you can add multiple scope restriction information.<br><br><br>* Batch Task Configuration<br><br>   * Set run time: **Belongs to** or **Exclusion** of set time periods, the batch task configuration actions will comply with the Use Specification.<br><br>   * Schedule Type: Choosing **Belongs to** or **Exclusion** a certain schedule type will comply with the Use Specification.<br><br>   * Task type: Choosing **Belongs to** or **Exclusion** a certain task type will comply with the Use Specification.<br><br>   * Execution Frequency: Choosing **Belongs to** or **Exclusion** of a certain execution frequency will comply with the Use Specification.<br><br>* Batch Task Backfill<br><br>   * Running period: **Belongs to** or **Exclusion** of the set time period for batch task backfill operations will hit the usage specification.<br><br>   * Backfill concurrency: **greater than** or **less than** the set concurrency number for batch task backfill operations will hit the usage specification.<br><br>* Ad\-hoc Query<br><br>   * Execution time: **Belongs to** or **Exclusion** of the set time period for Ad\-hoc Queries will hit the usage specification.<br><br>* Streaming task configuration<br><br>   * Task type: **Belongs to** or **Exclusion** of a certain task type will hit the usage specification.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Settings are in an "And" relationship, and all conditions must be met before a task can be reminded or prohibited.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the action hits the <strong>Specification settings under the application scope</strong>, it will prompt the queue to use the specification. Example: <strong>Application Scope</strong> choose <strong>Batch task backfill</strong>, <strong>More Settings</strong> choose "<strong>Running period Belongs to 10:00~19:00</strong>", when you Execute the backfill task within 10:00~19:00, it will hit the Use Specification.</div><br> |
      |Specification format |When queue usage hits the specification limit, the system adopts the corresponding specification format.<br><br>Supported multiple settings; when **Application Scope** selection differs, the options for this parameter are not completely the same.<br><br>Based on the selection, the system will exhibit two different specification formats:<br><br><br>* Weak Reminder: Pop\-up Notification<br><br>   When the queue usage hits the specification limit, the system will alert you but will not block subsequent processes. If you insist on using it, subsequent operations can still proceed normally.<br><br>* Strong Prohibition: Prohibiting task debugging/task deployment/initiating data backfill/ad\-hoc queries<br><br>   When the queue usage hits the specification limit, the system will block subsequent operations. You must use the queue according to the specification to normally execute debugging/deployment/running/backfilling operations. |
      

   * Click the **View** button in the **Action** column of a specific entry in the specification list to see detailed information about the specification.

   * Click the **Edit** button in the **Action** column of a specific entry in the specification list to modify the configuration information of that specification.

   * Click the **On/Off** toggle button in the **Action** column of a specific entry in the specification list to disable/enable that specification.

   * Click the  **... \> Delete** button in the **Action** column of a specific entry in the specification list, and in the confirmation dialog that appears, click the **Confirm** button to delete the specification.


<span id="_4-操作结果"></span>
## Operation Result

After successfully adding the queue usage specification, tasks within the range of the specification will trigger the use specification during the corresponding stages, as shown in the following table.


|Reminder Type |Trigger Timing |
|---|---|
|Weak Reminder |* When configuring a task, click the **Save** button.<br><br>* For ad\-hoc queries, click the **run** button.<br><br>* On the data backfill page, click the **Confirm** button.<br><br>* Instance rerun page, click on the **Confirm** button.<br><br>* Backfill approval page, click on the **Confirm** button. |
|Strongly prohibited |* Task deploy prohibited: After configuring the task, click on the **Submit for Deploy** button.<br><br>* Task debugging prohibited: After configuring the task, click on the **Debug** button.<br><br>* Ad\-hoc query prohibited: At the ad\-hoc query node, click on the **run** button.<br><br>* Data backfill prohibited: On the data backfill page, click on the **Next** button. |
