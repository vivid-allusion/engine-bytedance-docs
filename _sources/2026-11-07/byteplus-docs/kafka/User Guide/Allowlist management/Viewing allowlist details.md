---
title: "Viewing allowlist details"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-allowlist"
---

After creating an allowlist, you can view its details in the allowlist list and on the allowlist details page, such as IP addresses, the number of IP addresses, the number of associated instances, and the list of instances.

<span id="查看白名单详情"></span>
## Viewing details of an allowlist


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Allowlist** page, view the basic information about an allowlist.

   The allowlist list displays the IP allowlists for the current Region, including allowlist names, the number of IP addresses, the number of associated instances, and descriptions.

4. Click the allowlist name to view its detailed information on the details page.

   The allowlist details page displays basic information about the allowlist and a list of associated instances.


<span id="白名单概览信息"></span>
## Allowlist overview

The **Allowlist** page displays basic information like allowlist names and the number of IP addresses. The items are described as follows:


|**Item** |**Description** |
|---|---|
|Allowlist name |The name of the allowlist.<br><br>To modify the allowlist name, move the point over the right side of the name. |
|Number of IP addresses |The number of IP addresses or CIDR blocks in the allowlist.<br><br>To view the list of IP addresses, click the number. |
|Describe |The brief description of the allowlist. |


<span id="白名单详细信息"></span>
## Allowlist details

The allowlist details page displays basic information about the allowlist and a list of associated instances. The items are described as follows:


|**Item** ||**Description** |
|---|---|---|
|AllowList Information |Allowlist name |The name of the allowlist. |
||Describe |The brief description of the allowlist. |
||IP |The list of IP addresses or CIDR blocks in the allowlist. |
|List of Bound Instances |Instance Name |The names of Kafka instances associated with the allowlist.<br><br>Only IP addresses in the allowlist can access these Kafka instances. |
||Instance ID |The IDs of Kafka instances associated with the allowlist. |
