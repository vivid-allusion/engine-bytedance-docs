---
title: "Copying a subscription task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Copying_a_subscription_task"
---

Database Transmission Service (DTS) supports copying data subscription tasks, meaning it can copy a task with the same configuration as an existing subscription task. At the same time, you can adjust parameters for the successfully copied task. This topic describes how to copy a subscription task.

<span id="pykYXDXX"></span>
## Prerequisites

A subscription task has been created. For the procedure of creating subscription tasks, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id="MMkqBRiD"></span>
## Precautions

During the copying process, ensure the availability of the source database and middleware, and the consistency of the subscription task user permissions. Otherwise, the task copy may fail.

<span id="BoPECVPk"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Synchronization subscription list** page, select **More operations \> Copy task** to the right of the target subscription task.

5. In the **Do you want to copy the selected task?**  dialog box, click **Copy**.


<span id="n3XY8kZe"></span>
### Execution result

After the subscription task is copied successfully, the copied task is in the **To be started** state, and the name is **source task name_bak_random number**. To start the task, click **Configure**. After setting the relevant parameters, you can start the task. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions) for the subscription information configuration steps.
