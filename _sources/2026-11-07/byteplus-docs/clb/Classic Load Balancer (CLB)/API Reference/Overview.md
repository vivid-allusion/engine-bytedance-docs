---
title: "Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Overview"
---

Welcome to BytePlus Cloud Load Balancer (CLB). This document provides descriptions, syntax, parameters, and examples of CLB APIs. You can call these APIs to manage your cloud resources.

Calls to some CLB APIs may fail due to subaccount permission limits. In such cases, contact the primary account to obtain permissions. For more information, refer to [Permission management](https://docs.byteplus.com/en/docs/clb/Identity-and-Access-Management).

<span id="basic-concepts"></span>
## Basic concepts


|**Concept** |**Description** |
|---|---|
|Region |The local area network (LAN) of a region is fully separated from that of other regions. You should select the region nearest to your business to reduce the network latency and improve the access speed. |
|Availability zone |An availability zone is a physical area with an isolated power grid and network in a region. Availability zones within the same virtual private cloud (VPC) can connect to each other over the LAN. You are advised to deploy instances with low latency requirements in the same availability zone and deploy instances with disaster recovery requirements in different availability zones of the same region. |
|BytePlus account |An account, or a primary account, is an entity within BytePlus for which resources are allocated, measured, and billed. To use BytePlus services, you need to register a BytePlus account. Generally, the username is used as the login identifier of an account.<br><br>An account is the owner of all service resources under its name and has full control permissions on the resources. The account can purchase, renew, unsubscribe, and upgrade resources. It is the entity that orders and is billed for resources. Service resources can be accessed and operated by the account they belong to. |
|Subaccount |A subaccount, or an Identity and Access Management (IAM) account, is an authorized entity of the primary account and also a resource belonging to the primary account. An IAM account does not own any service resources and is not independently billed. An IAM account is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM account are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an AccessKey, the user can log on to the console and use open APIs to manage the resources of the primary account. |
|Project |A project is a task in your daily work. You can create multiple projects under the same account and create and purchase cloud resources for these projects. Cloud resources cannot be shared among projects. |
