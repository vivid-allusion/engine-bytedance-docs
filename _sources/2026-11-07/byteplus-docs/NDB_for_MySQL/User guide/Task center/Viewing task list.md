---
title: "Viewing task list"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_task_list"
---

The task center displays the details of the real\-time tasks that were initiated on the target instance during the non\-maintainable time period. Tasks scheduled for a maintainable time period are also displayed in the task center after execution.

<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* Currently, only task information within 30 days is supported.

* After the instance is deleted, the task center still retains the task information corresponding to the instance.

* Planned events (including configuration changes and parameter modifications) will be displayed in the Task Center after they are completed within the maintainable time period.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **NDB for MySQL** \> **Task center**.

4. In the **Task center** list, you can view real\-time task information initiated by the target instance, as shown in the following table.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports searching for target tasks by instance name, instance ID, task name, and start and end time. The instance ID only supports precision search.   </div>
   

   
   |Column name |Description |
   |---|---|
   |**Instance name/ID** |The instance name and instance ID corresponding to the task. |
   |**Task name** |The task name is the API interface name corresponding to the target operation, and only tasks of the create, delete, and update types are displayed. |
   |**Task status** |Shows the execution status and progress of the task, including **Succeeded**, **Pending**, **Running**, **Failed**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can filter tasks by <strong>Task status</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the task status is <strong>Failed</strong> or <strong>Pending</strong> Intervention, place the mouse on the <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_760ef81da1bdaa89017068f8fe1f2383.png" width="15px" /> icon after Failed or Pending Intervention to view the reason.</div><br> |
   |**Task start time** |Task start time. |
   |**Task end time** |Task end time. |
   |**Actions** |Click **View details** in the **Actions** column to view details about the target task. It includes the basic information of the task, the time of the task, and the request parameters of the task. |
