---
title: "Deleting an instance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/deleting-instance"
---

If a Kafka instance is no longer needed, we recommend that you promptly clean up resources and delete the instance, saving resources and cost. This topic describes how to delete a Kafka instance in the Message Queue for Kafka console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once the instance is deleted, all data in the instance cannot be restored. Proceed with caution.</div>


<span id="前提条件"></span>
## Before you begin


* Make sure that the Kafka instance is in the **Running** state and has no background tasks in progress.

* Before deleting an instance, perform the following operations:

   * Delete all topics and groups in the instance.

   * Unsubscribe from the connector of the instance.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, switch to the Region where the instance you want to delete is located.

3. On the **Instances** page, choose  **... \> Delete** in the **Actions** column for the target Kafka instance.

4. In the pop\-up dialog box, confirm the instance you want to delete and click **Delete**.
