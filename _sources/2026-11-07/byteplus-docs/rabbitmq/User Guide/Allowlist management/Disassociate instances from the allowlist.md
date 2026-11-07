---
title: "Disassociate instances from the allowlist"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Disassociate_instances_from_the_allowlist"
---

After the allowlist is associated with a RabbitMQ instance, only the IP addresses and ranges configured in the allowlist can access the Message Queue for RabbitMQ instance. If you need to revoke the access permissions of the corresponding allowlist, you can promptly disassociate the instance from the allowlist. This topic describes the steps to disassociate instance from allowlist.

<span id="MU1JctXC"></span>
## Note

After disassociating all allowlists from the instance, no IP address can access the instance.

<span id="aZnuGwkv"></span>
## Prerequisites  


* The allowlist is created, and the instance is bound to the allowlist.

* Before disassociating the instance, ensure that the IP addresses in the allowlist to be deleted are disconnected from the corresponding instance. Otherwise, connection failures may cause exceptions in production or consumption.


<span id="cMZ6c4Sg"></span>
## Operation steps


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region of the instance from the top menu bar.

3. In the left navigation bar, click **Allowlist**.

4. Find the specified allowlist and click its name.

5. In the **Bound Instances List** section, click **Unbind Instance**.

6. Find the instance to unbind, and in the **Actions** column, click **Unbind Instance**.

   You can also select multiple instances to unbind and click **Unbind Instance**.

7. Click **OK** in the pop\-up dialog box.
