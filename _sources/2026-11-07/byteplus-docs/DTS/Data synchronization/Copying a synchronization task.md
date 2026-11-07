---
title: "Copying a synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/replicating_a_synchronization_task"
---

Database Transmission Service (DTS) supports copying synchronization tasks, meaning it can copy a task with the same configuration as an existing synchronization task. At the same time, you can adjust parameters for the successfully copied task. This topic explains how to copy a synchronization task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

[A synchronization task has been created](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During task replication, ensure the availability of the source and target databases, as well as consistency in the synchronization task user permissions. Otherwise, the task replication may fail.

* If a data verification task was enabled in the original synchronization task, the built\-in data verification task will not be copied when replicating the task. If you need to perform data verification on the synchronized data, you must manually configure the data verification task in the configuration interface.

* Task copy operation retains all settings including data verification configuration, ensuring the new task behaves consistent with the source task.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, select **More operations \> Copy task** on the right side of the target synchronization task.

5. In the **Do you want to copy the selected task?**  dialog box, click **Copy**.


<span id=".5omn6KGM57uT5p6c"></span>
### Execution result

After successfully copying the synchronization task, the copied task will be in the **To be started** state and named **original task name_bak_random number**. To start the task, click **Configure**. After setting the relevant parameters, you can start the task. Select actions as needed:


* [Configuring forward synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization)

* [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization)
