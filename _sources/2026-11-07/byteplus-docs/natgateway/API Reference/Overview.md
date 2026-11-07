---
title: "Overview"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/API-Overview"
---

Welcome to use the BytePlus NAT gateway service. This topic introduces the description, syntax, parameters, samples, and other information about open APIs of a NAT gateway. You can call open APIs to manage your cloud resources.

<span id="terms"></span>
## Terms


|Name |Description |
|---|---|
|Region |Internal networks in different Regions are completely isolated. We recommend that you select a Region closer to your business to reduce the network latency and increase the access speed. |
|Availability Zone |An Availability Zone is an isolated physical area that has independent power and networking infrastructure within a specific Region. By default, internal networks between Availability Zones in the same virtual private cloud (VPC) are interconnected. We recommend that you deploy instances requiring low latency in the same Availability Zone, and deploy instances requiring disaster recovery in different Availability Zones of the same Region. |
|BytePlus account |A BytePlus account is an account or a main account. It is an entity to which your resources on BytePlus belongs and is used for resource metering and resource billing. You are required to register a BytePlus account before using BytePlus services. Generally, you can use your username as the login ID of the account.<br><br>The account is the owner of all service resources under it and has full control over these resources. It allows you to buy, renew, unsubscribe from, and upgrade these resources, and contains resource\-related orders and bills. You can use your account to access and perform operations on the service resources under it freely. |
|IAM user |An Identity Access Management (IAM) user is a sub\-account, and it is an authorized entity under a BytePlus account. It is also a kind of resource belonging to the BytePlus account. An IAM user does not own any service resources or support independent metering and billing. It can only be authorized by the BytePlus account to manage various resources under the account, and the resources managed by the IAM user belong to the BytePlus account. The BytePlus account pays for using these resources, and the IAM user has no separate bills.<br><br>After an IAM user is granted permissions by a BytePlus account, you can set a password and an access key for this IAM user. In this way, you can use this IAM user to log on to the console and manage the resource under the BytePlus account s through open APIs. |


<span id="api-authorization"></span>
## API authorization

To ensure the security of your BytePlus account, we recommend that you use the identity credential of an IAM user to call open APIs. When doing so, you must associate the IAM user with the policies of related resources.
