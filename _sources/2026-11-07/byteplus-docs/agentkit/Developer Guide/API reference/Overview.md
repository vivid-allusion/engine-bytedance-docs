---
title: "Overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Overview"
---

Welcome to our computing services. The following content provides descriptions, syntax, parameter descriptions, and examples for the AgentKit API. You can use it to manage your cloud resources.

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Term |Description |
|---|---|
|Region |Intranets in different regions are completely isolated. We recommend that you select a region that is closest to your business to reduce network latency and improve access speed. |
|Availability zone |An availability zone is a physical area with an isolated power grid and network in the same region. By default, internal networks between availability zones in the same VPC are interconnected. We recommend that you deploy instances with low\-latency requirements in the same availability zone, and deploy instances with disaster recovery needs in different availability zones in the same region. |
|Root user |Account, also called root user, is the entity for resource ownership, metering, and billing in BytePlus. Before using BytePlus services, you need to register a BytePlus account, and the username usually serves as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root user and a type of resource that belongs to the root user. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root user to manage resources under the root user. Fees of managed resources are on the root user, with no separate bills for IAM users. After being authorized by the root account, an IAM user can be assigned a password and access keys. With these credentials, the user can log in to the console and manage resources of the root account via OpenAPI. |
