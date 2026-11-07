---
title: "Associating an instance with an allowlist"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/associating-allowlist"
---

After Kafka instances are associated with allowlists, only IP addresses in the allowlists can access the instances. This topic describes how to associate an instance with an allowlist.

<span id="注意事项"></span>
## Precautions


* When an instance is associated with multiple allowlists, the supported IP address range is the union of multiple allowlists.

* If a Kafka instance is associated with the default allowlist, all IP addresses can access the Kafka instance. We recommend that you disassociate an instance from the default allowlist after associating it with another allowlist.

* Up to 200 Kafka instances can be associated with an allowlist.

* An instance can be associated with a maximum of 100 allowlists. The sum of IP addresses and CIDR blocks in all allowlists associated with an instance cannot exceed 300.


<span id="前提条件"></span>
## Before you begin


* Create a Message Queue for Kafka instance and ensure that the instance status is **Running**.

* Create an allowlist. For more information, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/kafka/creating-allowlist).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the upper\-left corner of the top menu bar, select the Region of the instance.

3. In the left\-side navigation pane, click **Allowlist**.

4. Locate the specified allowlist and click the name of the specified allowlist. In the **List of Bound Instances** pane, click **Binding Instance**.

   Alternatively, click **Binding Instance** in the **Actions** column of the allowlist list.

5. Select instances you want to associate with the current allowlist, and click **OK**.

   After instances are associated with the allowlist, the **List of Bound Instances** pane displays the instance names and IDs. Only IP addresses and IP address ranges in the allowlist can access the Kafka instance.
