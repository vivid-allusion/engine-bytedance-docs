---
title: "Introduction​"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/API-Overview"
---

Welcome to BytePlus Bandwidth Package. This topic describes the description, syntax, parameter explanation, and examples related to the Bandwidth Package OpenAPI. You can manage your cloud resources by calling OpenAPI.

<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Name |Description |
|---|---|
|Region |Intranets in different regions are completely isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |
|Availability Zone |Availability Zones (AZs) are physically isolated locations within the same region, with independent power and network infrastructure. Within the same Virtual Private Cloud (VPC), intranets between availability zones are connected by default. We recommend that you deploy instances requiring low\-latency in the same availability zone, and deploy instances requiring disaster recovery in different availability zones of the same region. |
|Account |Account, also called Root Account, is the entity for resource ownership, metering, and billing in BytePlus. Before using BytePlus services, you first need to register a BytePlus account, usually using the username as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, unsubscription, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root account and a type of resource that belongs to the root account. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root account to manage resources under the root account. Fees of managed resources are on the root account, with no separate bills for IAM users.<br><br>After the IAM user is granted by the root account, you can set password and access key for logging in to the console and managing root account's resources by OpenAPI. |
|Project |A project is a collection of resources. You can create projects based on your organizational structure and business. Different projects are independent and have isolated resources. We recommend adding the created Bandwidth Package to the corresponding project for easier management and maintenance. One Bandwidth Package instance can only be added to one project. |


<span id=".QVBJ5o6I5p2D"></span>
## API authorization

For the security of the root account, we recommend using the IAM user's identity credential to call OpenAPI. To use an IAM user to call OpenAPI, you need to associate the relevant resource policies with the IAM user. For related actions, see [Policy management](https://docs.byteplus.com/en/docs/6257/65058).
