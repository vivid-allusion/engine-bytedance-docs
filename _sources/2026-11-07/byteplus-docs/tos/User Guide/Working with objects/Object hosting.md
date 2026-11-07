---
title: "Object hosting"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Object_hosting"
---

This topic introduces object hosting, a new feature offered by TOS.

<span id="PDShVwyE"></span>
## Introduction

TOS now allows you to use another service to host objects in your buckets. Hosting occurs on the hosting service's end. Once an object is hosted, the hosting service uniformly manages it to ensure that it remains intact and is not accidentally altered during continuous reading or processing.

<span id="oyIPG1AR"></span>
### Notes


|**Category** |**Description** |
|---|---|
|**Ability provider** |TOS allows other services to host its objects. The hosting action itself takes place at the corresponding hosting service. |
|**Permission changes** |Once an object is hosted, it becomes read\-only. It cannot be deleted, overwritten, or modified through the TOS console or API. Hosting protection also applies to asynchronous write, delete, or modify operations affecting the object. This includes deleting objects using lifecycle rules or overwriting existing objects through replication. You can manage the object from the hosting service side according to the relevant procedures. |
|**Hosting service identifier** |The TOS console displays **the name of the hosting service** if an object is hosted by another service. For example, an object hosted by VeArk shows "Ark host". |
|**Canceling hosting** |The hosting service initiates hosting actions. You cannot cancel hosting directly on the TOS side. Contact the hosting service provider to find out if canceling hosting is possible. |


<span id="Yefmuswk"></span>
## Use cases

Object hosting is ideal for situations in which you need to delegate the management of your objects to another service while maintaining data consistency.


|**Use case** |**Description** |
|---|---|
|**Objects hosted by another service** |Scenarios where you need to entrust another service to host objects in your bucket. This service manages the state and lifecycle of the objects. |
|**Continuous data access** |Scenarios where an object is continuously read or processed by the hosting service, and the object must remain intact and unaltered throughout the process. Examples include VeArk inference and fine\-tuning. |
|**Data consistency** |Scenarios where you need to protect objects from accidental deletion or modification. In these cases, you can rely on read\-only permissions to ensure data consistency. |


<span id="Mv2UN2Bn"></span>
## Billing notes

Once an object is hosted by another service, the associated costs are divided as follows:


|**Billable item** |**Payer** |**Description** |
|---|---|---|
|**Data processing** |Hosting service provider |The hosting service provider covers the data processing fees for hosting objects. You do not need to pay for them. |
|**Others** |User |Except data processing fees, you are responsible for all other costs associated with the hosted objects. These include storage, data transfer, request, and data retrieval fees. All costs are calculated according to the TOS billing rules. For more information, see [TOS billing overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview?lang=en). |


<span id="54q5BMIa"></span>
## Usage notes

<span id="7jqWdSU4"></span>
### Prerequisites


* You have activated TOS and created a **bucket**.

* You have enabled the other service, such as VeArk, to host your objects.


<span id="mJUPbk4c"></span>
### Workflow


1. Create an object through the hosting service.

2. Once your hosting is set up, the object becomes read\-only. You retain only read permission on the object.

3. In the TOS console, you can view the hosted object, which displays the name of the hosting service (e.g., "Ark host").

4. To cancel hosting or modify the object, contact the hosting service provider.


<span id="ETOHdfZE"></span>
## FAQ

<span id="rFiNNPdG"></span>
### Can I delete or modify an object after it is hosted?

No. Once an object is hosted, it becomes read\-only. It cannot be deleted, overwritten, or modified through the TOS console or API. Hosting protection also applies to asynchronous write, delete, or modify operations affecting the object. This includes deleting objects using lifecycle rules or overwriting existing objects through replication. You can manage the object from the hosting service side according to the relevant procedures. Therefore, exercise caution when hosting objects.

<span id="xmWQ9PiD"></span>
### How do I cancel the hosting of an object?

Hosting actions are initiated by the hosting service. To cancel hosting, please contact the service provider because it cannot be undone directly on the TOS side.

<span id="oLEGrclu"></span>
### What fees are associated with hosting an object, and who is responsible for them?

The hosting service provider covers the data processing fees for hosting objects, so you do not need to pay for them. However, you are responsible for other costs, such as storage, data transfer, requests, and data retrieval. For more information, see [TOS billing overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview?lang=en).

<span id="tefe2pyZ"></span>
### How can I confirm if an object is being hosted, and if so, which service is hosting it?


1. In the TOS console, a hosted object displays the name of the hosting service. For example, an object hosted by VeArk shows "Ark host". Operations such as deletion or modification are prohibited. This helps you determine whether the object is hosted and by which service.

2. You can also find this information by using the [HeadObject](https://docs.byteplus.com/en/docs/tos/reference-headobject?lang=en) or [GetObject](https://docs.byteplus.com/en/docs/tos/reference--getobject?lang=en) API. The response header `x-tos-service-managed-by` includes the name of the hosting service.

3. You can also find this information by using the [ListObjects](https://docs.byteplus.com/en/docs/tos/reference-listobjects?lang=en) or [ListObjectsV2](https://docs.byteplus.com/en/docs/tos/reference-listobjectsv2?lang=en) API. The `ServiceManagedBy` field in the response contains the name of the hosting service.
