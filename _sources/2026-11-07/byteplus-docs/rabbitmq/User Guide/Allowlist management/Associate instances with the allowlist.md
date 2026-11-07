---
title: "Associate instances with the allowlist"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Associate_instances_with_the_allowlist"
---

After the allowlist is associated with a RabbitMQ instance, only the IP addresses and address ranges configured in the allowlist can access the Message Queue for RabbitMQ instance. This topic introduces the steps to associate instance with allowlist.

<span id="jOnCfaAO"></span>
## Note


* When an instance is associated with multiple allowlists, the supported IP address range is the union of all allowlists.

* Each allowlist can be associated with up to 200 RabbitMQ instances.

* Each instance can be associated with up to 100 allowlists. The total number of IP addresses and CIDR\-formatted IP address ranges in all allowlists associated with an instance cannot exceed 1,000.

* If a RabbitMQ instance has never been associated with any allowlist since its creation, all IP addresses are allowed to access the instance. However, once an instance is associated with an allowlist and all allowlists are later disassociated, access from all IP addresses to the instance is denied.


<span id="e6MdCpxf"></span>
## Prerequisites  


* A Message Queue for RabbitMQ instance has been created, and the instance status is **Running**.

* An allowlist is created. For detailed instructions, see [Create allowlist](https://docs.byteplus.com/en/docs/rabbitmq/Create_allowlist).


<span id="MFoFvzt0"></span>
## Operation steps


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region of the instance from the top menu bar.

3. In the left navigation bar, click **Allowlist**.

4. Find the specified allowlist and click its name. In the **List of associated instances** section, click **Associate instance**.

   You can also directly click **Associate instance** in the **Actions** column of the allowlist.

5. Select the instance that needs to access the current allowlist and click **OK**.

   After successfully associating instances and the allowlist, the **List of associated instances** section will display the corresponding instance names and IDs. Only addresses and address ranges in the allowlist can access the associated RabbitMQ instances.
