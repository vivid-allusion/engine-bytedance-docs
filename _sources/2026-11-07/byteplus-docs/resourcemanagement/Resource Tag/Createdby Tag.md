---
title: "Createdby Tag"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Createdby_Tag"
---

The createdby tag is a system tag automatically generated and associated with the corresponding resource by the BytePlus tag service. The tag is used to identify the source of the resource creator and is often used to trace the resource creator and split the bill by creator.

<span id="createdby-tag-format"></span>
## Createdby tag format


1. The tag key for the createdby tag is `sys:tag:createdBy`.

2. Three types of tag values supported by the createdby tag:

   1. `account-type:account-id`

   2. `account-type:user-id:user-name`

   3. `account-type:role-name` Where the valid values of `account-type` include `Root`, `IAMUser`, and `AssumedRole`. Relevant examples are as follows:


```json
sys:tag:createdBy : Root:1234567890 
sys:tag:createdBy : IAMUser:111122223333:exampleUser 
sys:tag:createdBy : AssumedRole:exampleRole
```


<span id="resource-types-that-support-createdby-tags"></span>
## Resource types that support createdby tags

Currently, only the resources of some services can be automatically associated with createdby tag through the specified API operations.

<span id="use-of-createdby-tag"></span>
## Use of createdby tag


1. When the createdby tag feature is enabled, a service\-associated role named ServiceRoleForTag is created, which queries the operation logs and actively associates the createdby tag with the newly created resource.

> Note: When the createdby tag feature is enabled, it is only applicable to newly created cloud resources. When the createdby tag feature is disabled, the disabling operation does not affect the createdby tags created before.


2. The system automatically associates the createdby tag with the newly created resource, and you can view the createdby tag information on the System tag tab on the Tag page (tag key: `sys:tag:createdBy`).

3. You can use the createdby tag in specific business scenarios such as billing and access control.
