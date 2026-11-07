---
title: "Overview"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Overview"
---

Welcome to BytePlus Elastic IP service. This article describes the description, syntax, parameter explanations, and examples of OpenAPI related to the elastic IP address (EIP). You can manage your cloud resources by OpenAPI calls.

<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Name |Description |
|---|---|
|Region |Intranets in different regions are completely isolated. We recommend that you select a region that is closest to your business to reduce network latency and improve access speed. |
|Availability zone |An availability zone is a physical area with an isolated power grid and network in the same region. Within the same Virtual Private Cloud (VPC), intranets between availability zones are connected by default. We recommend that you deploy instances requiring low\-latency in the same availability zone, and deploy instances requiring disaster recovery in different availability zones of the same region. |
|Root account |Account, also called Root Account, is the entity for resource ownership, metering, and billing in BytePlus. Before using BytePlus services, you first need to register a BytePlus account, usually using the username as the login identifier.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, unsubscription, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user is an authorized entity under the root account and a type of resource that belongs to the root account. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root account to manage resources under the root account. Fees of managed resources are on the root account, with no separate bills for IAM users.<br><br>After the IAM user is granted by the root account, you can set password and access key for logging in to the console and managing root account's resources by OpenAPI. |
|ECS instance |An Elastic Compute Service (ECS) instance is equivalent to a virtual machine, including basic computing components such as CPU, memory, operating system, network, and disk. |
|Project |A project is a collection of resources. You can create projects based on your organizational structure and business. Different projects are independent and have isolated resources. We recommend adding the applied EIP to the corresponding project for easier management and maintenance. An EIP can only belong to one project. |


<span id=".QVBJ5o6I5p2D"></span>
## API authorization

For the security of the root account, we recommend using the IAM user's identity credential to call OpenAPI. To use an IAM user to call OpenAPI, you need to associate the relevant resource policies with the IAM user.
