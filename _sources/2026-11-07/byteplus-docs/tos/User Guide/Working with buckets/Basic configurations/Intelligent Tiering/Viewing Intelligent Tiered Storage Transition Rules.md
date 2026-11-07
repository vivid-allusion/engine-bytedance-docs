---
title: "Viewing Intelligent Tiered Storage Transition Rules"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-viewing-intelligent-tiering-storage-transition-rules"
---

Files uploaded or transitioned to Intelligent Tiered Storage the first time are stored in the Frequent Access tier by default. They will be automatically transitioned to the Infrequent Access or Flashback Archive tier based on the transition rules. This topic describes how to view Intelligent Tiered Storage transition rules.

<span id="7e87770e"></span>
## **Note**


* You cannot modify Intelligent Tiered Storage transition rules. If you need to, submit a ticket for technical support. You can modify the following parameters through a ticket:

   * The number of days before transition to the Infrequent Access tier: Valid values are **30**, **60**, and **90**. **30** is the default value.

   * The number of days before transition to the Flashback Archive tier: Valid values are **90**, **120**, and **180**. **90** is the default value.

* Files smaller than 64 KiB will remain in the Frequent Access tier and will not be transitioned to the Infrequent Access or Flashback Archive tier.


<span id="6eb8a88e"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Basic Settings \> Intelligent Tiered Storage**. On the **displayed** page, view the rule details. Below are the transition rules:

   * Files that have not been accessed for **30** consecutive days will sink to the Infrequent Access tier of Intelligent Tiered Storage.

   * Files that have not been accessed for **90** consecutive days will sink to the Flashback Archive tier of Intelligent Tiered Storage.
