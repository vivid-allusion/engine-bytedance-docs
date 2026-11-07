---
title: "Synchronizing a trigger"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_a_trigger"
---

When creating a MySQL data synchronization task, and the synchronization method of the pre\-synchronize trigger is configured as manual trigger synchronization, you can manually synchronize the trigger before the incremental synchronization is started. This topic introduces how to manually synchronize the trigger.

<span id="paYePnnt"></span>
## Prerequisites

A MySQL data synchronization task is created, and the synchronization method of the pre\-synchronize trigger in the data synchronization task is manual trigger synchronization. For the method to create a synchronization task, refer to [Creating a synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

<span id="A4go8lSx"></span>
## Precautions


* This feature is released in the allowlist. To use it, [submit tickets](https://console.byteplus.com/workorder/create/) to contact technical support.

* Manual synchronization trigger is only supported when the synchronization task progresses to the incremental synchronization phase.

* When the task is in a pause state, a manual synchronization trigger is supported if the task is in the incremental synchronization phase.


<span id="Y32egjzj"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, select the  **...\> Synchronization trigger** on the right side of the target synchronization task.

5. In the synchronization trigger pop\-up, click **OK**.


<span id="AVjagIbO"></span>
### Execution result

You can view the task progress of the target synchronization task in the data synchronization list.
