---
title: "Overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Overview-2"
---

Welcome to the Direct Connect service provided by BytePlus. This topic introduces the APIs related to Direct Connect, their syntax, and parameters. To help you use them efficiently, usage examples are also provided. You can call the APIs using the Software Development Kit (SDK) to manage your cloud resources. For the download link of the SDK, refer to [SDK overview](https://docs.byteplus.com/en/docs/directconnect/DC_SDK_Overview).

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Term |tip |
|---|---|
|Regions |The internal networks of different Regions are isolated. A Region closer to your business is recommended because the network latency can be kept low, and access speed can be faster. |
|AZ |An Availability Zone refers to a physical area in the same Region that is isolated in electricity power and network. Internal networks of different Availability Zones in the same Virtual Private Cloud (VPC) are interconnected. It is recommended to deploy instances with low\-latency requirements in the same Availability Zone, and instances with disaster recovery needs in different Availability Zones in the same Region. |
|Primary account |An account, or a primary account, is an entity within BytePlus for which resources are allocated, measured, and billed. Before you use BytePlus services, you must create a BytePlus account. In most cases, a username is used as the login identity of an account. An Account is the owner of all the service resources under itself. It has full access to all the resources. You can use it to purchase, renew, Unsubscribe, and upgrade those resources. It also owns the purchase orders and bills of those resources. Service resources can be accessed and manipulated by accounts they belong to. |
|Subaccount |An IAM user, or an Identity and Access Management (IAM) user, is an authorized entity under a primary account and also a resource belonging to the primary account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account. Once authorized and granted a password and an access key by its primary account, an IAM user can log in to the console and use OpenAPI to manage the resources under the primary account. |
|ECS instances |An Elastic Compute Service (ECS) instance is a virtual machine that contains basic computing components, such as the CPU, memory, operating system, network settings, and disks. |
