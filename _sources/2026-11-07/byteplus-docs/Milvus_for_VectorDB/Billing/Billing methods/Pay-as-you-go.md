---
title: "Pay-as-you-go"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Pay-as-you-go"
---

Pay\-as\-you\-go is a postpaid billing method where you pay after usage. You do not need to purchase large amounts of resources in advance, and you can activate and release resources on demand at any time.

<span id="qdVovlCQ"></span>
## Overview

Pay\-as\-you\-go is suitable for scenarios with rapid short\-term business growth, such as flash sales. The system charges for your actual resource usage on a second basis and deducts fees hourly from your account, achieving true pay\-as\-you\-go. If purchased resources are no longer needed, you can delete them at any time. Billing stops immediately after deletion.

<span id="Fpr4QikE"></span>
## Purchase requirements


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* Cross\-service access has been authorized to allow Redis to access other services (such as VPC and EIP). For specific procedures, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization).


<span id="YsojUzm3"></span>
## Billing duration

Excluding overdue shutdowns, the billing duration for a Milvus for VectorDB pay\-as\-you\-go instance covers its entire lifecycle: billing starts when the instance is created and ends when the instance is released.

<span id="WQKnszFJ"></span>
## Settlement period

A Milvus for VectorDB pay\-as\-you\-go instance charges on a second basis, and is settled hourly. The system settles fees at each full hour based on UTC+8 time. If your available balance (including account balance and vouchers) is less than the bill to be settled, you will receive an insufficient balance SMS or email notification.

<span id="BSNz21cR"></span>
## Delete an instance

Billing stops immediately when a Milvus for VectorDB pay\-as\-you\-go instance is deleted. For the method to delete an instance, see [Delete an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Delete_an_instance).

<span id="yp46lDoD"></span>
## Modify the configuration

Pay\-as\-you\-go instances support real\-time configuration changes. After you chang the instance specifications, such as sharding number and shard nodes, you can view the new specification of the instance on the **Instance list** page. For the method to change the configuration, see [Modify the instance configuration](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_the_instance_configuration).
