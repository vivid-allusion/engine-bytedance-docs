---
title: "Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/API-Overview"
---

Welcome to use the Virtual Private Cloud (VPC) service. This document introduces the description, syntax, parameter explanations, and examples of the VPC API. You can call the API to manage your cloud resources.

When you use an IAM user to call the VPC OpenAPI, some interface calls may be restricted due to permission limits. You can contact the root user to add authorization for you. For more information about authorization, [refer to Permission management](https://docs.byteplus.com/en/docs/vpc/IAM-Overview).

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Term |Description |
|---|---|
|Region  |Private networks in different regions are isolated from each other. We recommend that you select a region that is nearest to your business to reduce network latency and improve access speed. |
|AZ |Availability zones are physical locations that are isolated from each other in the same region. Each availability zone has separate power supplies and networks. Resources in different availability zones within the same Virtual Private Cloud (VPC) can connect to each other. It is recommended that you deploy instances that require low latencies in an Availability Zone and deploy instances that have disaster recovery needs in different Availability Zones in the same Region. |
|Account |An Account, or root user, is the principal subject for resource ownership, resource metering, and billing in BytePlus. Before you use BytePlus services, you must create a BytePlus account. In most cases, a username is used as the login identity of an account.<br><br>An account is the owner of all service resources under its name and has full control permissions on the resources. The account can purchase, renew, unsubscribe, and upgrade resources. It is the entity that orders and is billed for resources. Service resources can be accessed and operated by the account they belong to. |
|IAM user |An IAM user, or an Identity and Access Management (IAM) user, is an authorized entity under a primary account and also a resource belonging to the primary account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |
