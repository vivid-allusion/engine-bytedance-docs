---
title: "Limits"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Restriction_description"
---

The message queue for RabbitMQ has set limitations on several metrics. Please be cautious not to exceed these limits during usage to avoid abnormalities.


|**Limitation type** |**Limitation** |**Description** |
|---|---|---|
|Number of instances |5 items |It refers to the number of message queue for  RabbitMQ instances in a single region. You can also apply for an increase in the maximum number of instances per region (InstanceNum) through [the Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=RabbitMQ), up to a maximum of 10. |
|Disk high water level threshold |≥ 2GiB |When the remaining space on the disk is less than 2GiB, it automatically triggers the disk high watermark. At this time, the producer's message production process will be blocked. |
|Message size |32MB |Message size that can be accepted by the server. Messages that exceed the limit cannot be sent successfully. |
|RabbitMQ version |3.8 and 3.12 |We currently support RabbitMQ versions `3.8` and `3.12`. |
|Log in to deploy message queue for RabbitMQ Machine |Not supported |None |
|Change the region of the instance |Not supported |None |
|Number of connections |[Product specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications) |Different instance specifications have different connection limits. For detailed information, please refer to [Product specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications). |
|Number of channels |2047 |The number of channels that can be established on a single connection |
