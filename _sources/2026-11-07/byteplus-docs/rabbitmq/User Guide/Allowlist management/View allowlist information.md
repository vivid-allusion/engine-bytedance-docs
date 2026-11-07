---
title: "View allowlist information"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/View_allowlist_information"
---

After creating an allowlist, you can view its details on the allowlist and allowlist details pages, including IP address information, the number of IP addresses, the number of associated instances, and the instances list.

<span id="blPQNp7T"></span>
## View allowlist details


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located in the top menu bar.

3. View the basic information of the specified allowlist on the **Allowlist** page.

   The allowlist displays all IP allowlists in the current region. You can view allowlist names, the number of IP addresses, the number of associated instances, and descriptions through the allowlist.

4. Click the allowlist name to view detailed information on the details page.

   The allowlist details page displays basic allowlist information and the list of associated instances.


<span id="Dif9IKii"></span>
## Allowlist overview information

The **Allowlist** page displays basic information such as the allowlist name and the number of IP addresses. The description of each item is as follows.


|**Display items** |**Description** |
|---|---|
|Allowlist name |Name of the allowlist.<br><br>Hover over the name to the right to edit the allowlist name. |
|Allowlist ID |ID of the allowlist.<br><br>Hover your mouse over the right side of the name to copy the allowlist ID. |
|Number of IP addresses |Number of IP addresses or address ranges configured in the specified allowlist.<br><br>To view the list of IP addresses, click the number in Number of IP addresses column. |
|Number of associated instances |Number of RabbitMQ instances associated with the specified allowlist. |
|Description |Simple description information of the allowlist. |


<span id="upCeSQv1"></span>
## Allowlist details

The allowlist details page shows basic allowlist information and the list of associated instances. The description of each item is as follows.


|**Display items** ||**Description** |
|---|---|---|
|Allowlist information |Allowlist name |Name of the allowlist. |
||Description |Simple description information of the allowlist. |
||IP |List of IP addresses or address ranges that are configured in the allowlist. |
|Instances that are associated with allowlist |Instance name |The name of the RabbitMQ instance associated with the allowlist.<br><br>Only IP addresses in the allowlist can access these RabbitMQ instances. |
||Instance ID |RabbitMQ instance IDs associated with the allowlist. |
