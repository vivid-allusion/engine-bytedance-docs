---
title: "Overview"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/API_Overview"
---

Welcome to use the BytePlus IPv6 gateway service. This topic introduces the description, syntax, parameters, samples, and other information about OpenAPIs of an IPv6 gateway. You can call OpenAPIs to manage your cloud resources.

<span id="concepts"></span>
## Concepts


|**Term** |**Description** |
|---|---|
|Region |The internal networks of different Regions are isolated. A Region closer to your business is recommended because the network latency can be kept low, and access speed can be faster. |
|AZ |An Availability Zone refers to a physical area in the same Region that is isolated in electricity power and network. Internal networks of different Availability Zones in the same Virtual Private Cloud (VPC) are interconnected. It is recommended to deploy instances with low\-latency requirements in the same Availability Zone, and instances with disaster recovery needs in different Availability Zones in the same Region. |
|Account |On VolcanoEngine, an account or a primary account is a principal that owns resources, by which resources are measured, and against which resources are billed. Before you use VolcanoEngine services, you must create a VolcanoEngine account. In most cases, a username is used as the login identity of an account.<br><br>An account is the owner of all service resources under its name and has full control permissions on the resources. The account can purchase, renew, unsubscribe, and upgrade resources. It is the entity that orders and is billed for resources. Service resources can be accessed and operated by the account they belong to. |
|Sub\-account |An IAM user, or an Identity and Access Management (IAM) user, is an authorized entity under a primary account and also a resource belonging to the primary account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |
|Elastic Compute Service (ECS) instance |An Elastic Compute Service (ECS) instance is a virtual machine that contains basic computing components, such as CPU, memory, operating system, networks, and disks. |
