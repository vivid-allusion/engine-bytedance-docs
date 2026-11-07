---
title: "Launch Flink Task"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Launch_Flink_Task"
---

Development and production environments are isolated. Once the task developers have completed development and debugging, they can deploy the task to the production environment.

<span id="b97a73a7"></span>
## Prerequisites

Please create the Flink resource pool in advance. See [Create VCI resource pool](https://docs.byteplus.com/docs/flink/Create_VCI_resource_pool).

<span id="a9e9e31a"></span>
## Points to Note

Flink Batch tasks do not support the GANG scheduling strategy, only the DRF scheduling strategy is supported.

<span id="a1a362bf"></span>
## Operation Steps


1. Log in to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. Select **Project Management** from the left navigation bar, perform a fuzzy search by project name in the search box, then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Development \> Jupyter lab**.

5. Under the **Task Development** page, locate and click the target task, then at the top of the edit area select the correct **execution method** and **engine version**, and click **deploy**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Flink Stream type tasks should select the execution method as <strong>STREAMING</strong>; Flink Batch type tasks should select the execution method as <strong>BATCH</strong>.   </div>
   

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5689e7474b2487dbe30852e9fd897a8~tplv-goo7wpa0wc-image.image) </span>


6. In the **Task Deployment Settings** dialog, select **runtime resource pool**, set **task priority** and **scheduling strategy**, then click **confirm**.

   After performing the task deployment operation, the system will indicate successful task deployment; you can visit the **Task Management** page to view it; after deployment, it will be displayed at the top of the task list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d75c4a81b6644109efc0f8e76cd929e~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Operation Resource Pool |Select the Flink resource pool in which the task will run from the dropdown list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the task you submitted has auto\-tuning enabled, it must run in a pay\-as\-you\-go type resource pool.</div><br> |
   |Task Priority |The system's default preset priority is L3. You can set task priorities as needed; the smaller the number, the higher the priority.<br><br>Task priority determines the internal scheduling order of tasks; higher\-priority tasks are scheduled first, meaning L3 is scheduled before L4. |
   |Scheduling Strategy |Configure the task scheduling strategy based on requirements:<br><br><br>* GANG: Ensures that all instances of a task are scheduled together; resources are only allocated when the remaining resources are sufficient for the normal operation of the task; if not, no allocation is made.<br><br>   This strategy prevents the phenomenon where resources are allocated but tasks cannot start, thus resolving the resource deadlock issue.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Flink Batch tasks do not support GANG scheduling strategy, only the DRF scheduling strategy. If the execution mode is chosen as Batch, the GANG strategy will not be displayed on the launch configuration page.   </div><br>   <br><br>* DRF: Considers multi\-dimensional resources to more reasonably distribute resources evenly among tasks within a resource pool, thereby enhancing utilization.<br><br>   For example: With remaining resources of 10 cores and 40 GB, Task A requires 10 cores and 20 GB; Task B needs 2 cores and 8 GB. If allocated to A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would choose to allocate to B, leaving 8 cores and 32 GB available for subsequent tasks. |
   |Scheduling duration |When set to GANG scheduling strategy, it is necessary to set the scheduling duration. Scheduling duration indicates the interval before scheduling again, meaning if a task does not start successfully, it will be rescheduled.<br><br>If it exceeds the scheduling duration, the task will fail to schedule. If set to 0, it will keep retrying. |
   |More settings |SQL tasks can skip the deep check before going online, allowing tasks to be forcefully launched.<br><br>Unchecked by default. Checking **skip pre\-launch checks** indicates that the SQL code deep check will be skipped, and tasks will go directly online. |
   


<span id="864087ba"></span>
## Subsequent operations

After task deployment, you can start, stop, undeploy, view Flink UI, and check task resource consumption from the Task Management page.
