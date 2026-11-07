---
title: "Reversing the DDL synchronization direction of the bidirectional synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Reversing_the_DDL_synchronization_direction_of_the_bidirectional_synchronization_task"
---

Database Transmission Service (DTS) supports reversing the DDL synchronization direction of the bidirectional synchronization task. In some scenarios, such as when primary\-secondary switchover is required, you can meet the requirements by reversing the direction of the synchronization task without creating a new synchronization task.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To ensure the stability of bidirectional synchronization tasks, DTS currently only supports synchronizing DDL operations of forward tasks to the target database and does not support synchronizing DDL of reverse tasks. If you need to synchronize DDL operations from the reverse task, you can first adjust the DDL synchronization direction of the bidirectional synchronization task and then perform the DDL operations to ensure data consistency.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A bidirectional synchronization task has been created. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions#.5ZCM5q2l5pa55qGI5qaC6KeI) for detailed operations.

* Both the forward and reverse synchronization tasks of the bidirectional synchronization task are in the incremental synchronization stage.

* The forward synchronization task in the bidirectional synchronization task must contain DDL.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Currently, only one\-click switchover for MySQL is supported.

* During the DDL synchronization direction switch of the bidirectional synchronization task, do not perform DDL operations. Otherwise, it may cause risks such as inconsistent data or data loss between the source and target ends.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Flexibility**: The one\-click switchover function can adjust the DDL synchronization direction of the bidirectional synchronization task at any time based on business needs or system state, so as to more flexibly support various business scenarios.

* **Data consistent**: Based on the bidirectional synchronization mechanism, even if the DDL synchronization direction of the bidirectional synchronization task is switched, the source and target data can still remain consistent.

* **Fault recovery**: In the event of a failure, the DDL synchronization direction of the bidirectional synchronization task is switched to ensure that the DDL statement can be normally synchronized to the target end.

* **Business continuity**: By switching the DDL synchronization direction of the bidirectional synchronization task, it can ensure uninterrupted business operation and improve system availability.

* **Load balancing**: In a complex system environment, the business traffic switch can be quickly responded to by adjusting the DDL synchronization direction.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the ** Data synchronization list** page, select  **...**  \> **One\-click switchover** on the right of the target bidirectional task.

5. In the **One\-click switchover** dialog box, confirm the bidirectional synchronization task that needs to be switched, and click **Confirm**.


<span id="faq"></span>
## FAQ

<span id=".6LCD6L2s5Y-M5ZCR5ZCM5q2l5Lu75Yqh55qELWRkbC3lkIzmraXmlrnlkJHmmK_lkKbkvJrlvbHlk43mlbDmja7nmoTkuIDoh7TmgKfvvJ8="></span>
### Will switching the DDL synchronization direction of a bidirectional synchronization task affect data consistency?

Under normal circumstances, switching the DDL synchronization direction of a bidirectional synchronization task does not affect data consistency. However, this requires the following conditions:


* Before the switchover, the forward and reverse synchronization tasks of the bidirectional synchronization task are in the incremental synchronization stage.

* During the switchover of the bidirectional synchronization task, do not perform DDL operations on the source or target end until the switchover is complete.


However, in practical applications, switching the DDL direction in bidirectional synchronization tasks involves certain risks. It is recommended to avoid performing any DDL operations during switchover.

Throughout the process, you should back up the data in advance. If any problems occur, you can recover to the state before the switchover in time. This can protect your data to the greatest extent and prevent data loss or inconsistency.

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[SetBiSyncDDLSource](https://docs.byteplus.com/en/docs/DTS/SetBiSyncDDLSource) |Call the SetBiSyncDDLSource API to switch the DDL synchronization direction of the bidirectional synchronization task. |
