---
title: "Data subscription process"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/data_synchronization_process_for_subscription"
---

This topic introduces the usage process of data subscription, helping you quickly master creating and managing data subscription tasks.

<span id=".6K6i6ZiF5rWB56iL"></span>
## Subscription process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5947b5f04a2805d20809b64b4a5a70cf.png) </span>


|**Procedure** |**Description** |
|---|---|
|[1. Preparations](https://docs.byteplus.com/en/docs/DTS/Preparations) |Before using DTS for data subscription, you must make some preparations for the source database or target database to meet the environment requirements of DTS. |
|[2. Create a subscription task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_data_subscription_task) |You can create and start a subscription task with simple operations in the console. |
|3. Manage subscription channels |* [Add a consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group)<br><br>   After successfully creating a data subscription task, create a consumer group in the DTS console or through the open\-source Kafka SDK based on the consumer type.<br><br>* [Manage consumer groups](https://docs.byteplus.com/en/docs/DTS/editing_a_consumer_group)<br><br>   Modify consumer group passwords or delete consumer groups in DTS.<br><br>* [Modify subscription objects](https://docs.byteplus.com/en/docs/DTS/changing_subscription_objects)<br><br>   Support changing the subscription object in the data subscription task during the data subscription process. |
|[4. Consume subscription data](https://docs.byteplus.com/en/docs/DTS/Data_subscription) |DTS supports using Kafka and RocketMQ clients to consume subscription data from BytePlus |
|[5. End the subscription task](https://docs.byteplus.com/en/docs/DTS/terminating_a_subscription_task) |You can end the subscription task when you no longer need to obtain real\-time data changes from the source database. |
