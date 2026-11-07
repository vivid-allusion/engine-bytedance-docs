---
title: "Data synchronization process"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/data_synchronization_process"
---

This topic introduces the usage process of data synchronization, helping you quickly master creating and managing data synchronization tasks.

<span id=".5ZCM5q2l5rWB56iL"></span>
## Synchronization process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a9177d71b9013c733f9768c8088edad.png) </span>


|**Procedure** |**Description** |
|---|---|
|[1. Preparations](https://docs.byteplus.com/en/docs/DTS/preparations_for_synchronization) |Before using DTS for data synchronization, you must make some preparations for the source database or target database to meet the environment requirements of DTS. |
|[2. Create a synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task) |You can create and start a synchronization task with simple operations in the console. |
|3. Optional. Manage synchronization tasks |* [View task progress](https://docs.byteplus.com/en/docs/DTS/Viewing_synchronization_progress)<br><br>   After the synchronization task starts, you can view the progress of the synchronization task based on the running status on the data synchronization list page.<br><br>* [Modify synchronization objects](https://docs.byteplus.com/en/docs/DTS/managing_synchronization_objects)<br><br>   You can add or delete synchronization objects during synchronization.<br><br>* [Set alerts](https://docs.byteplus.com/en/docs/DTS/setting_alerts)<br><br>   Cloud Monitor allows you to set alert policies. You can monitor DTS's data transmission performance and running status on Cloud Monitor. |
|[4. Business switching](https://docs.byteplus.com/en/docs/DTS/Migrating_on-premises_self-managed_databases_to_the_cloud_via_DTS) |After verifying and confirming that the data of the target database and source database is consistent, switch the business database service to the target database and recover the business. |
|[5. End the synchronization task](https://docs.byteplus.com/en/docs/DTS/terminating_a_synchronization_task) |Switch the business database service to the target database and recover the business for a period of time. After confirming there are no abnormalities in the data, you can end the data synchronization task. |
