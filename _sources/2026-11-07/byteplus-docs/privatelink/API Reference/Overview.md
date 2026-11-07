---
title: "Overview"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Overview"
---

This topic describes the PrivateLink API from BytePlus. It provides details about the API actions, including requests and responses, parameters, and examples. This allows you to manage cloud resources by making API requests.

When you use an IAM user to call the PrivateLink API, there may be permission limitations that prevent calling some actions. You can contact the BytePlus account user to grant you permissions. For more information, refer to [IAM Overview](https://docs.byteplus.com/en/docs/privatelink/Permission-management-01).

<span id="terms"></span>
## Terms


|Name |Description |
|---|---|
|Region |Regions are completely isolated from each other in different virtual private clouds (VPCs). We recommend you select a Region that is geographically closer to your business in order to reduce network latency and improve access speeds. |
|Availability Zone |Availability Zones refer to a physically distinct location within a Region that is isolated from failures in other Availability Zones, such as power or networking failures. In the same VPC, Availability Zones can interconnect with each other by default. We recommend you deploy instances with low latency requirements in the same Availability Zone, and to deploy instances with disaster recovery requirements across different Availability Zones in the same Region. |
|BytePlus account |The BytePlus account is the entity responsible for resource ownership, resource metering, and resource billing on BytePlus. Before using BytePlus services, first register and generate a BytePlus account, which generally uses a username as the login identifier for the account.<br><br>The BytePlus account is the owner of all service resources under the account. It has full control permissions over all resources under the account and can perform operations such as purchasing, renewing, unsubscribing, and upgrading resources. It also has ownership over resource orders and bills. Service resources can be arbitrarily operated and accessed by their owning BytePlus account. |
|IAM user |An IAM user is an authorized entity under the BytePlus account. It is also a type of resource that belongs to the BytePlus account. The IAM user does not have ownership of any service resources and cannot independently track usage or billing. It can only be authorized by the BytePlus account to administer various resources associated with that account. Any resources managed by the IAM user belong to the BytePlus account (who is responsible for payments), and the IAM user does not have their own separate bills.<br><br>Upon being authorized by the BytePlus account, the IAM user can be assigned a password and an access key pair, enabling them to log into the console and use the API to administer resources associated with the BytePlus account. |
