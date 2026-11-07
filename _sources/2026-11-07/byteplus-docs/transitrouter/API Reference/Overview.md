---
title: "Overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Overview"
---

This topic describes the Transit Router (TR) API, including the request syntax, parameters, and examples. You can make API requests to manage cloud resources.

You can call relevant APIs using the Software Development Kit (SDK). For more information, refer to [SDK overview](https://docs.byteplus.com/en/docs/transitrouter/Transit-Router-SDK-overview).

When you use an IAM user to call the Transit Router API, there may be permission restrictions that prevent you from calling certain interfaces. You can contact the root user to add authorization for you. For more information on authorization, refer to [Identity and Access Management (IAM)](https://docs.byteplus.com/en/docs/transitrouter/Permission-management-01).

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Name |Description |
|---|---|
|Regions |The internal networks of different Regions are isolated. A Region closer to your business is recommended because the network latency can be kept low, and access speed can be faster. |
|Primary account<br><br> |An account or a primary account is a principal that owns resources, by which resources are measured, and against which resources are billed. Before you use cloud services, you must sign up for an account. The username of the account is usually used as the login identifier of it.<br><br>An account is the owner of all the service resources under itself. It has full access to all the resources. You can use it to purchase, renew, unsubscribe, and upgrade those resources. It also owns the purchase orders and bills of those resources. Service resources can be accessed and manipulated by accounts they belong to. |
|Subaccount<br><br> |A subaccount, or an Identity and Access Management (IAM) account, is an authorized entity of the primary account and also a resource belonging to the primary account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |
