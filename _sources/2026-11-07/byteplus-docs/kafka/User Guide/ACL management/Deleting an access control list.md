---
title: "Deleting an access control list"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/deleting-an-ACL"
---

We recommend that you promptly delete an access control list (ACL) whose associated permissions are no longer needed to maintain minimal permissions.

<span id="7ad3431c"></span>
## Before you begin


* Make sure that the status of the Kafka instance is **Running**.

* Before deleting an ACL, make sure that no running applications use the ACL for authentication to avoid impacting online business.


<span id="1b89ff19"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. On the **ACL Management** tab, locate the ACL you want to delete.

   You can also filter ACLs by user name, resource name or prefix, or IP address on the upper\-right corner of the tab.

5. In the **Actions** column, click **Delete**.

6. In the pop\-up dialog box, confirm the ACL you want to delete and click **OK**.
