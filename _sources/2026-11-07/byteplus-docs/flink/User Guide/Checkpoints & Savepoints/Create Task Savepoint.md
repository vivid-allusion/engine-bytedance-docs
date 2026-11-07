---
title: "Create Task Savepoint"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Task_Savepoint"
---

Savepoints are a fault\-tolerant mechanism for restoring task states in case of system failures. The system supports both automatic and manual savepoint creation methods; task states can be directly restored from existing savepoints upon task launch.

<span id="6b51e9f5"></span>
## Precautions


* Both system savepoints and manual savepoints are retained for only 5 days.

* Currently, only the BytePlus Flink 1.11\-byted version supports system savepoints, while the BytePlus Flink 1.16\-byted version does not.


<span id="fe87897a"></span>
## Prerequisites

By default, the task does not have the Checkpoint feature enabled. To use system savepoints or create manual savepoints, enable the Checkpoint feature in the Flink configuration parameters on the task development side in advance.

For related documentation, see [Configure Flink Parameters](https://docs.byteplus.com/docs/flink/Configure_Flink_Parameters).

<span id="19126b50"></span>
## System creates Savepoint

By default, the system savepoint feature is not enabled. To use automatic system savepoints, add the `savepoint.scheduler.default.interval` parameter in the Flink settings to set the system savepoint interval. The savepoint interval is measured in milliseconds, with a minimum value of 60000.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/807ea5126846431aa224296973c84048~tplv-goo7wpa0wc-image.image) </span>

The system automatically triggers the creation of a task savepoint at each savepoint interval, with the savepoint type as **automatically created**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b52ccf656425457d9ad6f62162e73211~tplv-goo7wpa0wc-image.image) </span>

<span id="f31a0652"></span>
## Manually create Savepoint

You can manually create a Savepoint for the task as needed. The savepoint includes all states and data of the task and can be used directly to recover (start) the task.


1. Log in to the [BytePlus Flink consol](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left\-hand navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the left\-hand navigation bar of the project, select **Task Operations & Management \> Task Management**, and click on the target task's name.

5. On the task details page, click on the **savepoint** tab, then click **Create savepoint**.

6. In the **Create savepoint** dialog, set the savepoint description, then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/998ac34a68f747848fe0b67edd2bc0c9~tplv-goo7wpa0wc-image.image) </span>
