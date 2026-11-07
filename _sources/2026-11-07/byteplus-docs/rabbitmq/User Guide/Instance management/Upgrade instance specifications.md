---
title: "Upgrade instance specifications"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications"
---

After creating an instance, if your business scale grows and the current instance specifications no longer meet your needs, you can upgrade the instance's computing and storage specifications appropriately. It helps to avoid performance degradation due to resource limitations and ensures normal business operations. This article explains how to upgrade instance specifications in the Message Queue for RabbitMQ console.

<span id="前提条件"></span>
## Prerequisites

A RabbitMQ instance has been created, and the instance status is **Running**.

<span id="注意事项"></span>
## Notes

When upgrading instance specifications, pay attention to the following restrictions and risks.


* Change restrictions:

   * Cluster instances do not support the conversion to standalone instances.

   * Currently, only upgrading instance configurations is supported. Downgrading computing specifications or reducing storage space is not supported.

   * Different computing specifications correspond to different storage capacity ranges. When upgrading the instance's computing specification, the storage capacity must be upgraded synchronously.

   * Pricing varies based on computing specifications and storage capacity. After changing the instance specification, configuration fees will change. Please confirm the related fees in the order.

* Risk description:

   * Do not perform other operations on the instance during the specification change process to avoid abnormal instance status or other issues.

   * During specification upgrades, server nodes will restart sequentially. It is recommended to perform this operation during off\-peak hours.

   * The client of the stand alone instance will briefly disconnect and reconnect with some nodes. This may cause a few errors. Messages already sent successfully will not be lost after the upgrade. For messages that fail to send during the upgrade, a retry is recommended. A retry mechanism can be configured on the client.


<span id="操作步骤"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select a region in the top menu bar.

3. Find the specified instance on the **Instances** page, then click **Change Configuration** in the **Actions** column.

4. Select the new instance computation and storage specifications.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only instance specification upgrades are supported. Downgrades are not supported.   </div>
   

5. Click **Confirm order**.

6. Confirm the upgraded specifications. Read and agree to the related agreement, then click **Submit the order**.

7. Confirm the order details and follow the page prompts to make payment.

   The upgrade will take approximately 30 minutes and will not affect overall service availability.


<span id="执行结果"></span>
## Execution result

On the **Instances** page, click the name of the upgraded instance.


* View the upgraded instance configuration on the **Basic information** tab.

* View task details of the upgrade specification operation on the **Task management** tab.
