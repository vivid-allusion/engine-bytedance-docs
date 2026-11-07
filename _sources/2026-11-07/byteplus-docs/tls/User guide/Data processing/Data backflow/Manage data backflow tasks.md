---
title: "Manage data backflow tasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_data_backflow_task_for_ModelArk_high-code_applications"
---

After creating a data backflow task, you can modify or delete it according to business requirements. This document describes common management operations for data backflow tasks.

<span id="ba4d30e3"></span>
## View data backflow tasks

After a data backflow task is created successfully, a schedule SQL task is automatically created in the schedule SQL analysis task list. If delivery to TOS is configured, a TOS delivery task is also automatically created. You can view an overview of the tasks in the data backflow list.


|Task type |Task name |
|---|---|
|Data backflow task |Customize the task name, such as `data-backflow-name` **.**  |
|Data backflow task \> Scheduled SQL analysis task |Automatically created based on the data backflow task name, such as `data-backflow-name` **`-bf_schedule_sql`** **.**  |
|Data backflow task \> TOS delivery task |Automatically created based on the data backflow task name, such as `data-backflow-name` **`-bf_shipper`** **.**  |


<span id="aefa0def"></span>
### View data backflow tasks


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Data processing** \> **Data backflow**.

4. On the **Data backflow list** page, view the overview information of the tasks.

   In the task list, view the overview information of all tasks in the current region, such as data backflow task name/ID, status, data source type, data source log topic name, target type, automatically created schedule SQL task name, TOS delivery task name, creation time, and more.


<span id="a84cbe91"></span>
### View schedule SQL analysis tasks for data backflow


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Data processing** \> **Schedule SQL analysis**.

4. On the **Schedule SQL analysis task list** page, view the overview information of the tasks.

   In the task list, view the overview information of all tasks in the current region, such as task status, source log topic, and more.

5. Click the specified task name to view the detailed information of the task.

   On the task details page, view the basic information and execution status of the specified task. For more details, refer to [View Task Details ](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2F1130974).


<span id="d15785a1"></span>
### View log delivery tasks for data backflow


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Data processing** \> **Log delivery**.

4. On the **Delivery Configuration List** page, under the **TOS Delivery Configuration** tab, view the overview information for the task.

   In the task list, view the overview information for all tasks in the current region, such as delivery status, source log topic, delivery target, delivery file size, and more.

5. Click the specified task name to view detailed information about the task.

   On the task details page, view the basic information and execution status of the specified task. For details, refer to [View delivery configurations and task details](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2F155602).


<span id="b57f6355"></span>
## Edit data backflow tasks

After creating a data backflow task, if you need to adjust the upper limit per backflow operation, scheduling cycle, SQL time window, backflow fields, or other configurations, you can modify them by editing the task.


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Data Processing** \> **Data Backflow**.

4. On the **Data Backflow List** page, find the backflow task to be modified, then click **Edit** in the corresponding **Actions** column.

5. Modify the rule configuration as needed. After completing the modifications, click **Preview Filter Results**, then click **Submit**.

   * Only the **rule configuration** of data backflow tasks can be modified.

   * For details about **rule configuration**, refer to [Create data backflow task](https://docs.byteplus.com/en/docs/38/%2F66o8pm3q%2F1jqpe7s2).


<span id="e09e7eb1"></span>
## Delete data backflow tasks

To delete and clean up related resources in a timely manner when certain data backflow tasks are no longer needed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">Data backflow deletion is irreversible. Please proceed with caution.</div>



&nbsp;

1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **TLS** \> **Project Management**, click the project name, then select **Data Processing** \> **Data Backflow**.

4. On the **Data Backflow List** page, find the backflow task to be deleted, and click **Delete** in the **Actions** column.

5. In the pop\-up dialog box, confirm the information of the task to be deleted, then click **Delete**.
