---
title: "Modifying an allowlist"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/modifying-allowlist"
---

You can modify configurations such as allowlist names and IP addresses as needed. This topic describes how to modify an allowlist in the console.

<span id="注意事项"></span>
## Precautions

Each allowlist can contain up to 100 IP addresses or CIDR blocks.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the upper\-left corner of the top menu bar, select the Region of the instance.

3. In the left\-side navigation pane, click **Allowlist**.

4. Navigate to the **Allowlist** page, and click the target allowlist.

5. In the **AllowList Information** pane, click **Edit**.

6. Reset the basic information about the allowlist.

   
   |**Parameter** |**Description** |
   |---|---|
   |Allowlist Name |The name of the allowlist. It must meet the following requirements:<br><br><br>* Must be 1 to 128 characters in length.<br><br>* Cannot start with a digit or a hyphen ( \- ).<br><br>* Can only contain Chinese characters, letters, digits, underscores ( _ ), and hyphens ( \- ).<br><br>* The allowlist name is unique in the current Region. |
   |Description |A brief description of the allowlist, not exceeding 200 characters in length. |
   |IP |The IP addresses you want to add to the allowlist. Only the IP addresses and CIDR blocks in the allowlist can access the Message Queue for Kafka instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist can contain up to 100 IP addresses or CIDR blocks, separated by commas ( , ).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IP addresses must be unique.</div><br> |
   

7. Click OK.


<span id="相关操作"></span>
## Related operations

In addition to modifying the allowlist name, description, and IP addresses, you can also associate instances with or disassociate instances from the allowlist. For more information, refer to:


* [Associating an instance with an allowlist](https://docs.byteplus.com/en/docs/kafka/associating-allowlist)

* [Disassociating an instance from an allowlist](https://docs.byteplus.com/en/docs/kafka/disassociating-allowlist)
