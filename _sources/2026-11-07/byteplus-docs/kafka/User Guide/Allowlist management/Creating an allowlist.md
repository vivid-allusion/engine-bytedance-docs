---
title: "Creating an allowlist"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-allowlist"
---

Once an allowlist is created and an instance is associated with the allowlist, only IP addresses or CIDR blocks in the allowlist can access the instance. This topic describes how to create an allowlist.

<span id="注意事项"></span>
## Precautions


* Each BytePlus account can create up to 100 allowlists in each Region.

* Each allowlist can contain up to 300 IP addresses and CIDR blocks.


<span id="背景信息"></span>
## Background information

When creating a Kafka instance, you can associate it with an allowlist as needed. This way, only the IP addresses and CIDR blocks in the allowlist can access the Kafka instance. For security reasons, we recommend that you create an allowlist and add the IP addresses or CIDR blocks of your client to the allowlist of the Kafka instance. We recommend that you regularly maintain and manage allowlists to improve the security of your Kafka instance access.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a Kafka instance, the allowlist defaults to default, with the IP address being 0.0.0.0/0. This indicates that all IP addresses can access the Kafka instance. The default allowlist cannot be deleted or modified, but you can disassociate the instance from the default allowlist and associate it with a more suitable allowlist with an appropriate IP address range.</div>


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the upper\-left corner of the top menu bar, select the Region of the instance.

3. In the left\-side navigation pane, click **Allowlist**.

4. On the upper\-left corner of the **Allowlist** page, click **Create Allowlist**.

5. Specify the allowlist configuration.

   
   |**Parameter** |**Description** |
   |---|---|
   |Allowlist name |The name of the allowlist. It must meet the following requirements:<br><br><br>* Must be 1 to 128 characters in length.<br><br>* Cannot start with a digit or a hyphen ( \- ).<br><br>* Can only contain Chinese characters, letters, digits, underscores ( _ ), and hyphens ( \- ).<br><br>* The allowlist name is unique in the current Region. |
   |Describe |A brief description of the allowlist, not exceeding 200 characters in length. |
   |IP addresses |The IP addresses you want to add to the allowlist. Only IP addresses and CIDR blocks in the allowlist can access the Message Queue for Kafka instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist can contain up to 300 IP addresses or CIDR blocks, separated by commas ( , ).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IP addresses must be unique in the allowlist.</div><br> |
   

6. Click **Create**.


<span id="后续操作"></span>
## What to do next

After creating an allowlist, associate instances with the allowlist. For more information, refer to [Associating an instance with an allowlist](https://docs.byteplus.com/en/docs/kafka/associating-allowlist).
