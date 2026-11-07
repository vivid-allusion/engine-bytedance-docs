---
title: "Deleting a Virtual Private Cloud"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-VPC"
---

## Scenarios

You may use this procedure to delete unused VPCs.

## Prerequisites

|Prerequisites |Explanation |
|---|---|
|The VPC has no custom route table |If present, first [Delete custom route table](https://docs.byteplus.com/en/docs/vpc/Deleting-a-route-table). |
|The VPC has no custom Security Group |If any, first [Delete custom security groups](https://docs.byteplus.com/en/docs/vpc/Deleting-a-security-group). |
|The VPC has no Network ACL |If any, first [Delete Network ACLs](https://docs.byteplus.com/en/docs/vpc/Deleting-a-network-ACL). |
|The VPC has no network interface |If present, Delete network interface. |
|The VPC has no high availability virtual IP |If any, first [Delete high-availability virtual IPs](https://docs.byteplus.com/en/docs/vpc/Deleting-a-HAVIP). |
|The VPC has no IPv6 Gateway |If present, first [Delete IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/Deleting_an_IPv6_gateway_instance). |
|The VPC is not attached to the Cloud Enterprise Network (CEN) |If attached, first [Detach network instance](https://docs.byteplus.com/en/docs/cen/Network-instances-02). |
|The VPC is not attached to a Transit Router |If attached, delete network instance attachment. |
|The VPC is not authorized for cross\-account CEN access |If already authorized, first [Remove cross-account authorization](https://docs.byteplus.com/en/docs/vpc/Managing-CEN-cross-account-authorization#.6Kej6Zmk6Leo6LSm5Y-35o6I5p2D). |
|The VPC has no subnet |If present, First [Delete subnet](https://docs.byteplus.com/en/docs/vpc/Deleting-a-subnet). |

> **tip**

> The IPv6 gateway is currently in beta stage. If you need a trial, please contact your account manager.

## Action description

When deleting a VPC, its system route table and default security group are automatically deleted along with it.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click **Delete** on the right side of the target VPC.

   * If you receive a "Temporarily Unable to Delete VPC" notification: This indicates unmet prerequisites for deletion. Follow the provided instructions to remove associated resources before retrying VPC deletion.

   * Can be deleted: Click **Delete** to complete the action.

## Related documents

[DeleteVpc](https://docs.byteplus.com/en/docs/vpc/DeleteVpc)
