---
title: "Upgrading instance specifications"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications"
---

Once an instance is created and business growth outpaces the current instance specification, you can upgrade both the instance type and storage specifications. This helps avoid decreased processing capability and impacts on business operations due to resource limits. This topic describes how to upgrade instance specifications in the Message Queue for Kafka console.

<span id="前提条件"></span>
## Before you begin

Create a Kafka instance and ensure that the instance status is **Running**.

<span id="注意事项"></span>
## Precautions

To upgrade instance specifications, be aware of the following limits and risks.


* Limits:

   * Currently, only upgrading instance configurations is supported. Downgrading the instance type or scaling in storage space is not supported.

   * Each instance type matches a specific range of storage space, so a storage space increase is required along with an instance type upgrade.

   * Pricing varies depending on instance types and storage space. Modifying the instance specifications results in configuration fee changes. Review the fee before placing an order.

* Risks:

   * When modifying the instance specifications, do not perform other operations on the instance to avoid issues such as instance status abnormalities.

   * The brokers experience a rolling restart in sequence through the upgrade period. We recommend that you perform the operation during off\-peak hours.

   * The client temporarily disconnects from and reconnects to some brokers, which may cause a small number of errors. The sent messages are not lost after an upgrade. For messages that fail to be sent during the upgrade, we recommend that you retry sending. A retry mechanism can be configured on the client side.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region.

3. On the **Instances** page, locate the instance, and click **Configure** in the **Actions** column.

4. Select a new instance type and a storage specification.

   
   |**Parameter** |**Description** |
   |---|---|
   |Calculation specification |The instance type of the Kafka instance. Instance types can only be upgraded or maintained, and cannot be downgraded. |
   |Storage Specifications |The storage specification of the Kafka instance. Storage specifications can only be upgraded or maintained, and cannot be downgraded. |
   |No. of Partitions |The number of partitions for the Kafka instance.<br><br>The number of partitions can only be increased. For more information on the range of partitions that can be created for each instance type, refer to [Product specifications](https://docs.byteplus.com/en/docs/kafka/specifications).<br><br>Additional partitions added when upgrading the instance specifications incur extra costs. For more information on the billing method of partitions, refer to [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |
   

5. Click **Next step**.

   Confirm the new instance specification, then read and agree to the related agreements.

6. Click **Buy Now**.

   The upgrade takes about 30 minutes, and overall services are not affected.


<span id="执行结果"></span>
## Result

On the **Instances** page, click the name of the upgraded instance.


* On the **Instance details** tab, you can view the instance configurations after the upgrade.

* On the **Background task management** tab, you can view the upgrade task details.
