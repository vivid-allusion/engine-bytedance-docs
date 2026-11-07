---
title: "Adjusting the full synchronization rate"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/adjusting_full_synchronization_rate"
---

You can adjust the full synchronization rate during the data synchronization process based on business data pressure. This topic introduces how to adjust the full synchronization rate on the DTS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A full synchronization task has been created and configured, in which,


* If the synchronous topology selected when creating the task is **Unidirectional synchronization**, you can only adjust the full synchronization rate of the forward synchronization task. For how to configure a synchronization task, refer to [Configuring forward synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization).

* If the synchronous topology selected when creating the task is **Bidirectional synchronization**, you can adjust the full synchronization rate of forward and reverse synchronization tasks separately. For how to configure a reverse task, refer to [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The full synchronization rate can only be adjusted when the synchronization has progressed to full synchronization. For methods of viewing synchronization progress, refer to[ Viewing synchronization progress](https://docs.byteplus.com/en/docs/DTS/viewing_synchronization_progress).

* If the synchronization rate is too high, it may affect the performance of the source database. You can appropriately adjust the synchronization rate based on the read and write pressure of the source and target databases.

* Only tasks with instance types of RDS for MySQL, Document Database for MongoDB, and RDS for PostgreSQL support setting the full synchronization rate.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.


4. Find the target synchronization task on the synchronization task list page, and select **More operations \> Task details** to the right of task progress.

5. On the data synchronization page, click the **Monitor** tab.

6. On the **Monitor** tab, click **Adjust full synchronization rate**.

7. In the pop\-up dialog box, set the following parameters.

   
   |**Name** |**Description** |
   |---|---|
   |**Rows synchronized per second** |Enable and set the rows synchronized per second as needed to prevent excessive synchronization speed from affecting the performance of the source database. You can adjust the rows based on the read and write pressure of the source and target databases. The default value is 100000, and the value range is 1\-100000. |
   |**Data synchronization volume per second** |Enable and set the data volume synchronized per second (Unit: KB) as needed to prevent excessive synchronization speed from affecting the performance of the source database. You can adjust the data volume based on the read and write pressure of the source and target databases. The default value is 25,000, and the value range is 1 to 25,000. |
   |**Synchronization task concurrency** |Set the concurrency of the synchronization task as needed. This concurrency can improve the performance and efficiency of the synchronization task, ensuring it completes quickly and stably. The default value is 8, and the valid range is 1 to 64. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An excessively high synchronization rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases.   </div>
   

8. Click **OK**.
