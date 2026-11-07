---
title: "Overview"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Overview"
---

This topic introduces the Fasttrack OpenAPI, including its description, syntax, argument explanation, and examples. You can call OpenAPI to manage your cloud resources.

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Name |tip  |
|---|---|
|Region  |The internal networks of different Regions are isolated. A Region closer to your business is recommended because the network latency can be kept low, and access speed can be faster. |
|AZ |An Availability Zone refers to a physical area in the same Region that is isolated in electricity power and network. Internal networks of different Availability Zones in the same Virtual Private Cloud (VPC) are interconnected. It is recommended to deploy instances with low\-latency requirements in the same Availability Zone, and instances with disaster recovery needs in different Availability Zones in the same Region. |
|Root user |On BytePlus, an account or a primary account is a principal that owns resources, by which resources are measured, and against which resources are billed. Before you use BytePlus services, you must create a BytePlus account. In most cases, a username is used as the login identity of an account.<br><br>An account is the owner of all service resources under its name and has full control permissions on the resources. The account can purchase, renew, unsubscribe, and upgrade resources. It is the entity that orders and is billed for resources. Service resources can be accessed and operated by the account they belong to. |
|Sub\-account |An IAM user is an authorized sub\-account under a BytePlus account. It is a resource that belongs to the BytePlus account. An IAM user does not own any service resources and is not independently billed. An IAM user is only authorized by the primary account to manage the resources of the primary account. Resources managed by an IAM user are owned and paid for by the primary account.<br><br>When an authorized IAM user is granted a password and an Access Key, the user can log on to the authorized consoles and call open APIs to manage the resources of the account. |


<span id=".QVBJ5o6I5p2D"></span>
## API authorization

To ensure the security of an account, we recommend that you use IAM users as identity credentials when calling APIs. If you use IAM user credentials to call APIs, you must associate related resource policies with IAM users. For more information, refer to [Policy Management](https://docs.byteplus.com/en/docs/6257/65058).
