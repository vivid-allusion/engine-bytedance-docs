---
title: "Viewing subscription task logs"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Viewing_subscription_task_logs"
---

Database Transmission Service (DTS) supports viewing task logs of data subscription tasks, helping you understand the timeline and status of events during task execution in detail. When a data subscription task encounters an abnormal state, you can troubleshoot the issue through the task log information. This topic introduces how to view data subscription task logs on the DTS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A subscription task has been created. For the method to create a subscription task, refer to [Creating a subscription task](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, find the target subscription task and click the task name.

5. Click the **Task log** tab. Under the **Task log** tab, you can view the event name, start time, and event state of each event in the current subscription task. If an event execution fails, **Task failed** is prompted. You can hover over the icon to view the task failed error message.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

If the pre\-check fails, the event shows a red state. You can click **View pre\-check** to see the basic information and pre\-check results. For more information, refer to [Pre-check items (Data verification)](https://docs.byteplus.com/en/docs/DTS/beta-pre-check-items-data-verification).
