---
title: "Manage data transformation tasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_data_transformation_tasks"
---

After a data transformation task is created, you can modify or delete the data transformation task based on your business requirements. This topic describes common management operations on data transformation tasks.

<span id=".5ZCv5Yqo5oiW5pqC5YGc5pWw5o2u5Yqg5bel5Lu75Yqh"></span>
## Start/Pause data transformation tasks

If you disable **Task status** when you create a data transformation task, the task is paused by default. Manually start the data transformation task as needed. During data transformation, you can pause or start the task at any time as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you stop a task, Torch Log Service (TLS) records the transformation progress and position in the background. If you restart the task, TLS continues transformation from the position where the task is stopped.</div>


Perform the following steps:


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Data transformation**.

4. Find the task of which the status you want to modify, then click **start** or **Pause** in its corresponding **Actions** column.


<span id=".57yW6L6R5pWw5o2u5Yqg5bel5Lu75Yqh"></span>
## Edit data transformation tasks

To adjust configuration items for a data transformation task, such as the task name, description, target topics, and transformation rules, edit the task. Perform the following steps:


5. Log in to the [TLS console](https://console.byteplus.com/tls).

6. In the top menu bar, select the region where TLS resides.

7. In the left\-side navigation pane, choose **Data processing** \> **Data transformation**.

8. Find the target task, then click **Edit** in its corresponding **Actions** column.

9. Reset the basic configuration and transformation rule configuration.

   For more information on the parameter description and configuration process, refer to [Create a data transformation task](https://docs.byteplus.com/docs/tls/create_a_data_transformation_task).


<span id=".5Yig6Zmk5pWw5o2u5Yqg5bel5Lu75Yqh"></span>
## Delete data transformation tasks

Paused data transformation tasks still consume your quota. If you do not need specific data transformation tasks, we recommend that you delete and clean the related resources in a timely manner.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data transformation tasks cannot be restored after deletion.</div>



10. Log in to the [TLS console](https://console.byteplus.com/tls).

11. In the top menu bar, select the region where TLS resides.

12. In the left\-side navigation pane, choose **Data processing** \> **Data transformation**.

13. Find the target task, then click  **...**  \> **Delete** in its corresponding **Actions** column.

14. In the pop\-up dialog box, confirm information on the task to be deleted, then click **Delete**.
