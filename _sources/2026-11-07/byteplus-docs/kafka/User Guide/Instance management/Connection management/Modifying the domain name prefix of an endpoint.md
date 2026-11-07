---
title: "Modifying the domain name prefix of an endpoint"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/modifying-domainname-prefix"
---

In scenarios with many instances, to differentiate between different instance endpoints and facilitate instance management, you can modify the domain name prefix of instance endpoints. This topic describes how to modify the domain name prefix of endpoints.

<span id="78c520da"></span>
## Background information

When many instances are managed under a BytePlus account, it becomes challenging to quickly distinguish various endpoints of different instances in the production and consumer related business code of the project. Message Queue for Kafka allows you to modify the domain name prefix of instance endpoints from an instance ID to a user\-friendly prefix. For example, if the original public endpoint is `kafka-cnngtu6ea2b8****.kafka.ibytepluses.com:9092`, you can modify the domain name prefix from `kafka-cnngtu6ea2b8****` to `tcpmodule`, and the full address of the new endpoint is `tcpmodule.kafka.ibytepluses.com:9092`.

<span id="7e89b5bc"></span>
## Precautions


* The domain name prefix of an endpoint must be globally unique. It must be different from that of any instance under any BytePlus account or in any Region.

* Before modifying the public domain name prefix, enable internet\-facing access for the instance. For more information, refer to [Enabling internet-facing access](https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing).


<span id="09d393c3"></span>
## Before you begin

The instance status is **Running**.

<span id="6943e661"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, click the name of the target instance.

3. In the **Service access** pane on the **Instance Details** tab, locate the endpoint whose domain name prefix you want to modify, and click the Edit icon.

4. Reset the domain name prefix for the endpoint.

   The domain name prefix must meet the following requirements:

   * Contain uppercase and lowercase letters, digits, underscores, and hyphens.

   * Must start with a letter and end with a letter or digit.

   * Must be at least 8 characters in length. The total length of prefix and suffix cannot exceed 63 characters.

5. In the pop\-up dialog box, confirm the domain name and click **OK**.
