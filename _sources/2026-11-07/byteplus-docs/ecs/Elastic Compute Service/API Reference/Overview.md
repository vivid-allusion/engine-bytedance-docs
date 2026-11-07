---
title: "Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-4"
---

Welcome to BytePlus Elastic Compute Service. The following content provides the description, syntax, parameter descriptions, and examples for the ECS API, which you can use to manage your cloud resources.

You can call the relevant OpenAPI operations through the software development kit (SDK). For more information, see [SDK overview](https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-SDK-overview).

<span id=".5Z-65pys5qaC5b-1"></span>
## Concept


|Name |Description |
|---|---|
|Region |Intranets in different regions are completely isolated. We recommend that you select a region that is closest to your business to reduce network latency and improve access speed. |
|Availability zone |An availability zone is a physical area with an isolated power grid and network in the same region. By default, internal networks between availability zones in the same VPC are interconnected. We recommend that you deploy instances with low\-latency requirements in the same availability zone, and deploy instances with disaster recovery needs in different availability zones in the same region. |
|Account |Account, also called root account, is the entity for resource ownership, metering, and billing in BytePlus. Before using BytePlus services, you need to first register a BytePlus account, and the username usually serves as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root user and a resource belonging to it. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root user to manage resources under the root user. Fees for managed resources are charged to the root user, with no separate bills for IAM users. After the IAM user is granted permissions by the root user, you can set a password and an access key for logging in to the console and managing the root user's resources by OpenAPI. |
|Instance |An instance is a virtual machine that consists of essential computing components such as CPU, memory, operating system, network, and disk. |
