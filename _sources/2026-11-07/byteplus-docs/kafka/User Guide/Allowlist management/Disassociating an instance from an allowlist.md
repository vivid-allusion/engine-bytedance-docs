---
title: "Disassociating an instance from an allowlist"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/disassociating-allowlist"
---

After Kafka instances are associated with allowlists, if you want to cancel allowlists, disassociate the instances from the allowlists. This topic describes how to disassociate an instance from an allowlist.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After an instance is disassociated from all allowlists, any IP address can access the instance.</div>


<span id="前提条件"></span>
## Before you begin


* Create an allowlist and associate an instance with the allowlist.

* Before disassociating an instance, make sure that the IP addresses in the allowlist to be removed are disconnected from the instance. Otherwise, production or consumption issues occur due to connection failures.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the upper\-left corner of the top menu bar, select the Region of the instance.

3. In the left\-side navigation pane, click **Allowlist**.

4. Locate the specified allowlist and click the allowlist name.

5. In the **List of Bound Instances** pane, locate the instance you want to disassociate, and click **Unbinding Instance** in the **Action** column.

6. In the pop\-up dialog box, click **OK**.
