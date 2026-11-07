---
title: "Deleting a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-security-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can delete security groups that are no longer in use.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The security group is not associated with any network interfaces. If associated, first [Disassociate](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-a-network-interface#.6Kej6Zmk5YWz6IGU572R5Y2h).

* Ensure the security group is not referenced as an IP address in the **Source** field of any other security group's inbound rules. If in use, first [Delete security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

* The security group is not managed. If it is managed, the security group will be automatically deleted when its associated managed service (such as NAT gateway's managed security group) is deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

   * Delete a single security group:

      1. Click **Delete** on the right side of the target security group.

      2. Click **Delete** to complete the action.

   * Delete multiple security groups:

      1. On the left, select multiple security groups to be deleted.

      2. Click **Delete Multiple**, then click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteSecurityGroup](https://docs.byteplus.com/en/docs/vpc/DeleteSecurityGroup)
