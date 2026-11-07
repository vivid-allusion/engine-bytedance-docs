---
title: "Overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Overview-3"
---

Welcome to the BytePlus Virtual Private Network (VPN) connection service. This topic introduces the description, syntax, parameters, and samples of APIs related to the VPN connection service. You can use Software Development Kits (SDKs) to call related open APIs to manage your cloud resources.

<span id="basic-concepts"></span>
## Basic concepts


|Name |Description |
|---|---|
|Region |Internal networks in different Regions are completely isolated. We recommend that you select a Region closer to your business to reduce the network latency and increase the access speed. |
|Availability Zone |An Availability Zone is a physically isolated area that has independent power and networking infrastructure within a specific Region. By default, internal networks between Availability Zones in the same virtual private cloud (VPC) are interconnected. We recommend that you deploy instances requiring low latency in the same Availability Zone and deploy instances requiring disaster recovery in different Availability Zones of the same Region. |
|BytePlus account |A BytePlus account is an account or a main account to which your recourses belong and is used for resource metering and resource billing. You are required to register a BytePlus account before using BytePlus services. Generally, you can use your username as the login ID of the account.<br><br>The account is the owner of all service resources under it and has full control over all these resources. It allows you to buy, renew, unsubscribe from, and upgrade these resources, and contains resource\-related orders and bills. You can use your account to access and perform operations on these resources. |
|IAM user |An Identity Access Management (IAM) user is a sub\-account, and it is an authorized entity under a BytePlus account. It is also a kind of resource within the BytePlus account. An IAM user does not own any service resources or support independent metering and billing. It can only be authorized by the BytePlus account to manage various resources under the account, and the resources managed by the IAM user belong to the BytePlus account. The BytePlus account pays for these resources, and the IAM user has no separate bills.<br><br>After an IAM user is authorized by the BytePlus account, you can set a password and an access key for this user. This enables the user to log in to the console and use the open API to manage the resources under the BytePlus account. |
|Elastic Compute Service instance |An Elastic Compute Service instance is equivalent to a virtual machine that contains basic computing components such as CPU, memory, OS, network, and disk. |
|Project |A project refers to a task in your routine work. You can create multiple projects under the same account and create and subscribe to cloud resources for the projects. Cloud resources cannot be shared or migrated between projects. |
