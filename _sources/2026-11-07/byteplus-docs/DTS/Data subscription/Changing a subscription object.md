---
title: "Changing a subscription object"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/changing_subscription_objects"
---

Database Transmission Service (DTS) supports changing the subscription objects in data subscription tasks. This topic describes how to modify subscription objects on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A subscription task has been created, and the task status is **In progress**. For the procedure of creating subscription tasks, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only RDS for MySQL and RDS for PostgreSQL subscription tasks that are in progress and have entered the incremental subscription phase support modifying subscription objects.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, find the target task and click **Configure**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a task enters the "To be started" state due to an unpaid order, you must re\-enter the account passwords for the source and target instances when configuring the task.   </div>
   

1. On the **Configure subscription object** page, you can modify the **Subscription scope**, **Subscription object**, and **Advanced configuration**.

2. Click **Save task** at the bottom\-right corner of the page.
