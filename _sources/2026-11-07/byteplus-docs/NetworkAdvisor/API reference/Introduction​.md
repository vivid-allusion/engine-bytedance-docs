---
title: "Introduction​"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/API-Introduction"
---

Welcome to the BytePlus Network Advisor (NA). This topic introduces the descriptions, syntax, parameters, and examples of OpenAPIs related to the NA. You can manage your cloud resources by calling these OpenAPIs.

## Terms

|Name |Explanation |
|---|---|
|Regions |Intranets in different regions are completely isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |
|Availability zone |Availability Zones (AZs) are physically isolated locations within the same region, with independent power and network infrastructure. Within the same Virtual Private Cloud (VPC), intranets between availability zones are connected by default. We recommend that you deploy instances requiring low\-latency in the same availability zone, and deploy instances requiring disaster recovery in different availability zones of the same region. |
|Account |The account, also known as the main account, is the entity responsible for resource ownership, resource metering, and resource billing on the BytePlus . Before using BytePlus  services, you first need to register a BytePlus  account, usually using a username as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, unsubscription, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root user and a type of resource that belongs to the root user. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root user to manage resources under the root user. Fees of managed resources are on the root user, with no separate bills for IAM users.<br><br>After the IAM user is granted by the root user, you can set password and access key for logging in to the console and managing root user's resources by OpenAPI. |
|ECS instance |An Elastic Compute Service (ECS) instance is equivalent to a virtual machine, including basic computing components such as CPU, memory, operating system, network, and disk. |
|Project |A project is a collection of resources. You can create projects based on your organizational structure and business. Different projects are independent and have isolated resources. |

## API authorization

For the security of the root user, we recommend using the IAM user's identity credential to call OpenAPI. To use an IAM user to call OpenAPI, you need to associate the relevant resource policies with the IAM user. For related operations, see [Policy management](https://docs.byteplus.com/en/docs/6257/65058).

## Service authorization

When using the NA service for the first time, please follow the on\-screen instructions to complete the authorization.
