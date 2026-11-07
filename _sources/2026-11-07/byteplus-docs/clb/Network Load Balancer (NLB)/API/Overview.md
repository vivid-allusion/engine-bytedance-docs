---
title: "Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-API-Overview"
---

Welcome to BytePlus Network Load Balancer (NLB) service. This document provides descriptions, syntax, parameters, and examples of NLB APIs. You can use these APIs to manage your cloud resources.

<span id="基本概念"></span>
## Concepts


|Name |explain |
|---|---|
|Region  |The internal networks of different Regions are isolated. A Region closer to your business is recommended because the network latency can be kept low, and access speed can be faster. |
|Root user |On BytePlus, an account or a primary account is a principal that owns resources, by which resources are measured, and against which resources are billed. Before you use BytePlus services, you must create a BytePlus account. In most cases, a username is used as the login identity of an account.<br><br>An account is the owner of all service resources under its name and has full control permissions on the resources. The account can purchase, renew, unsubscribe, and upgrade resources. It is the entity that orders and is billed for resources. Service resources can be accessed and operated by the account they belong to. |
|Sub\-account |A subaccount, or an Identity and Access Management (IAM) account, is an authorized entity of the primary account and also a resource belonging to the primary account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |


&nbsp;
