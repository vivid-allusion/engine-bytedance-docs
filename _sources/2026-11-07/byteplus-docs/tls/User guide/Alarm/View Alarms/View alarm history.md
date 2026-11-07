---
title: "View alarm history"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/alarm_history"
---

Once an alarm policy takes effect, it periodically executes monitoring tasks, and each task execution is recorded in the log service. The log service displays alarm history information at the project level. This article explains how to view all alarm history for a specific project in the console.

<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **log alarm** \> **alarm history**.

4. View alarm history.

   The **alarm history** page shows all alarm entries triggered by the alarm policies in the current project. Supports filtering by time range, monitored object, and alarm policy keywords.


<span id=".5ZGK6K2m5Y6G5Y-y5L-h5oGv6K-05piO"></span>
## Alarm history information description

After filtering alarm history, the alarm history page displays alarm history information that meets the filter criteria. You can view records of alarm policy executions to trace alarm tasks historically.

The list shows alarm occurrence time, alarm policy name, alarm status, project, monitored object, trigger conditions, notification group, and other information. The types and descriptions of alarm status are as follows.


|Alarm status |Description |
|---|---|
|Alarming |The alarm task is running, and the trigger conditions continue to be met, activating the alarm. |
|Not triggered |The trigger conditions are not met within the current monitoring cycle. |
|Recovered |After the alarm triggers and the first alarm recovers, the status changes to **recovered**. |


Click **View details** in the **Actions** column corresponding to the alarm to navigate to the **Execution information** page of the alarm policy for more details. For detailed explanation of execution information, please refer to [View execution information](https://docs.byteplus.com/docs/6470/103029#.5p-l55yL5omn6KGM5L-h5oGv).
