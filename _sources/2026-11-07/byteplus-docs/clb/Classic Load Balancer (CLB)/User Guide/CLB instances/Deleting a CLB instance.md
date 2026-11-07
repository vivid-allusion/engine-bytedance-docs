---
title: "Deleting a CLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-09"
---

## Prerequisites

* Please confirm the original business has been migrated or closed.

* The CLB instance has not enabled modification protection. If enabled, please [Disable](https://docs.byteplus.com/en/docs/clb/CLB-instances-07) first.

* The CLB instance is pay\-as\-you\-go or the subscription has expired. If the subscription CLB has not expired.

* CLB instance is not attached to [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01). If already attached, please see [Removing service resource](https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources#.56e76Zmk5pyN5Yqh6LWE5rqQ).

## Action description

When deleting a CLB instance, its related resource status is as follows:

|Resource |Explanation |
|---|---|
|Listener |Automatically deleted along with the CLB instance. |
|Server group |Automatically deleted along with the CLB instance. |
|Forwarding rules |Automatically deleted along with the CLB instance. |
|Elastic IP Address |* When the CLB is a public CLB and its EIP has joined a Bandwidth Package, the system first removes the EIP from the Bandwidth Package and then releases it; if the EIP has not joined a Bandwidth Package, it is released directly.<br><br>* When the CLB is a private CLB with an associated EIP, the system only detaches it from the EIP without affecting the EIP’s associations with other resources (such as Bandwidth Package). If you need to release this EIP, see [Releasing an EIP](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP). |
|Health check log |Automatically detached from the CLB instance. If you need to delete the health check log, see [Deleting a log topic](https://docs.byteplus.com/en/docs/clb/Creating-a-log-topic#.55u45YWz5pON5L2c). |
|Access Log |Automatically detached from the CLB instance.  |
|Certificate |Automatically detached from the CLB instance. If you need to delete this certificate, see [Deleting a certificate](https://docs.byteplus.com/en/docs/clb/Deleting-the-certificate). |
|Tags |Automatically removed from the CLB instance. If the tag is not added to other resources, it will be deleted automatically; if the tag is still added to other resources and needs to be deleted, see [Deleting a tag](https://docs.byteplus.com/en/docs/clb/Tag-management#.57yW6L6R5qCH562-). |
|Access Control List (ACL) policy |Automatically detached from the CLB instance. If you need to delete the access control list, please see [Deleting an ACL](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups). |
|Web application firewall |Automatically detached from the CLB instance.  |

> Note that:

> Deletion is irreversible. Proceed with caution.

## Procedures

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Delete on the right side of the target CLB instance.

4. After inputting Confirm Delete, click Delete to complete the action.

## Related documents

[DeleteLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer)
