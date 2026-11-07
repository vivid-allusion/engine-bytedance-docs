---
title: "Set public network parse"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_parse"
---

The private network VPC domain name of Message Queue for RabbitMQ supports parsing to a private IP address in a public network environment. This section describes the manual operation steps to open public network parse.

<span id="背景信息"></span>
## Background information

The message queue for RabbitMQ provides access points for various protocols. When accessing private network VPC access points, you need to parse the private domain name. However, they can only be parsed to a private IP address within the BytePlus private network environment by default. You can open public network parse for the instance. After opening, the private domain name can successfully parse a private IP address even in a public network environment. Public network parse applies to non\-production environments such as testing. For example, a test environment can directly connect to a message queue for RabbitMQ instance or access private network domain via personal devices.

<span id="注意事项"></span>
## Note


* The private domain name parses to a BytePlus private IP address after being parsed through the public network. Your local environment needs to access the BytePlus private network via VPN or other means. Otherwise, you will not be able to successfully access this private IP address.

* Due to the complexity of public network environments, the accuracy and timeliness of domain name parse can not be guaranteed. Therefore, the public DNS parse function is only suitable for non\-production environments. We sincerely recommend that you adopt the DNS Forward solution in the production environment by configuring Forward to BytePlus DNS in the local DNS Server to achieve private network domain name parse.

    &nbsp;


<span id="前提条件"></span>
## Prerequisites

The instance status is **Running**.

<span id="开启公网解析"></span>
## Open public network parse


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. On the **Instances** page, click the target instance name.

3. On the **Instance information** tab, in the **Service access** area, click **Open public network parse**.

4. Confirm the domain names involved in this operation in the pop\-up dialog, then click **Determine Open**.

    &nbsp;


<span id="关闭公网解析"></span>
## Close public network parse

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After close public network parse, private network domain names can not be parsed in the public network environment. However, you can continue to access private IP addresses parsed during the enabled period.</div>



1. Log in to the [message queue for RabbitMQ console](https://console.byteplus.com/rabbitmq/).

2. On the **Instances** page, click the target instance name.

3. On the **Instance information** tab, in the **Service Access** section, click **Close public network parse**.

4. Confirm the domain names involved in this operation in the pop\-up dialog, then click **Determine Close**.
