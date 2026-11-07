---
title: "API overview"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Overview-3"
---

This topic provides the descriptions, syntax, parameter specifications, and examples of Cloud Monitor APIs. You can manage your Cloud Monitor service by calling these APIs.

<span id=".5Z-65pys5qaC5b-1"></span>
## Glossary


|**Name** |**Description** |
|---|---|
|Region |The internal networks between different regions are completely isolated. We recommend selecting a region closer to your business to reduce network latency and improve access speed. |
|Availability zone |An availability zone refers to a physically separated area within the same region, with independent power supply and network isolation. Within the same private network, availability zones are interconnected by default. We recommend deploying instances with low\-latency requirements in different availability zones of the same region for disaster recovery purposes. |
|Root user |A root user is the entity responsible for resource ownership, metering, and billing on BytePlus. Before using BytePlus services, you first need to register and create a BytePlus account, which typically uses your username as the login identifier.<br><br>A root user is the owner of all service resources and has full control over all resources (including permissions for operations such as purchasing, renewing, unsubscribing, and upgrading resources), and can access resource orders and bills. The root user has administrator permissions to operate all available resources. |
|IAM user |An IAM user is an authorized entity of the root user and is also a resource belonging to the root user.<br><br>An IAM user does not own any service resources, cannot be metered or billed independently, and can manage resources owned by the root user only if the root user grants them the required permissions. Resources managed by an IAM user belong to the root user (paid by the root user) and have no independent bills.<br><br>After being authorized by the root user, an IAM user can be assigned a password and an access key. These credentials allow the root user to log in to the console and use OpenAPI to manage resources owned by the root user. |
