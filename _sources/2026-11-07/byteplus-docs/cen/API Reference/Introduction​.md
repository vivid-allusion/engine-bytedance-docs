---
title: "Introduction​"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/API-Reference-02"
---

Welcome to use Cloud Enterprise Network (CEN) service. This document introduces the CEN API description, syntax, parameter explanations, and examples, allowing you to manage your cloud resources through API calls.

You can call the relevant OpenAPI through the software development kit (SDK). Please refer to [SDK Overview](https://docs.byteplus.com/en/docs/6405/114432).

## Terms

|Name |Explanation |
|---|---|
|Regions |Intranets in different regions are completely isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |
|Availability zone |An availability zone refers to a physical area isolated by power and network within the same region. Within the same Virtual Private Cloud (VPC), intranets between availability zones are connected by default. We recommend that you deploy instances requiring low\-latency in the same availability zone, and deploy instances requiring disaster recovery in different availability zones of the same region. |
|Account |An account, also called the main account, is the principal entity for resource ownership, resource metering, and billing. Before you use services, you must register and create an Account. Generally, a username is used as the login identifier of the Account.<br><br>The account owns all service resources under it, has full control over all resources, and can perform actions such as purchase, renewal, unsubscription, and upgrade. It also holds orders and bills for resources. You can freely access and operate service resources using the account. |
|IAM user |An IAM user, also called a sub\-account, is an authorized entity under the main account and a type of resource belonging to the main account. IAM users do not own any service resources, cannot be metered or billed independently, and can only be authorized by the root account to manage resources under the root account. Fees of managed resources are on the root account, with no separate bills for IAM users.<br><br>After the IAM user is granted by the root account, you can set password and access key for logging in to the console and managing root account's resources by OpenAPI. |
