---
title: "Restart instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Restart_instance"
---

The BytePlus message queue for RabbitMQ supports restarting RabbitMQ instances. This section describes the steps to restart an instance through the console.

<span id="前提条件"></span>
## Prerequisites

The RabbitMQ instance is **Running** with no ongoing background tasks.

<span id="注意事项"></span>
## Notes

During the RabbitMQ instance restart, the RabbitMQ cluster will reject message production from producers and message consumption from consumers. Please schedule the operation during the planned maintenance time.

<span id="操作步骤"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. On the **Instances** page, click **Restart** in the **Actions** column of the target instance.

3. In the pop\-up dialog, confirm the name and ID of the instance to restart, then click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Restarting the RabbitMQ instance takes about 1 to 5 minutes. During restart, the RabbitMQ instance status shows <strong>Restarting</strong>. After a successful restart, the status returns to <strong>Running</strong>.</div>
