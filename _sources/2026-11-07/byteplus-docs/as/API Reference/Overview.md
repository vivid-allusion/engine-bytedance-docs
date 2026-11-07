---
title: "Overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/OverviewAPI"
---

Welcome to use computing services. The following content provides the description, syntax, parameter descriptions, and examples for the Auto Scaling API, which you can use to manage your cloud resources.

You can call the relevant OpenAPI operations through the software development kit (SDK). For more information, refer to [SDK overview](https://docs.byteplus.com/en/docs/as/AS_SDK_overview).

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Name |Description |
|---|---|
|Region |Intranets in different regions are completely isolated. We recommend that you select a region that is closest to your business to reduce network latency and improve access speed. |
|Availability zone |An availability zone is a physical area with an isolated power grid and network in the same region. By default, internal networks between availability zones in the same VPC are interconnected. We recommend that you deploy instances with low\-latency requirements in the same availability zone, and deploy instances with disaster recovery needs in different availability zones in the same region. |
|Account |Account, also called Root Account, is the entity for resource ownership, metering, and billing in BytePlus. Before using BytePlus services, you first need to register a BytePlus account, usually using the username as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root account and a type of resource that belongs to the root account. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root account to manage resources under the root account. Fees of managed resources are on the root account, with no separate bills for IAM users. After the IAM user is granted by the root account, you can set password and access key for logging in to the console and managing root user's resources by OpenAPI. |
|Instance |An instance is a virtual machine that consists of essential computing components such as CPU, memory, operating system, network, and disks. |
