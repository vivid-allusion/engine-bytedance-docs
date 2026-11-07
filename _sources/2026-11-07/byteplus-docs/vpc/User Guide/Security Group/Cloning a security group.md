---
title: "Cloning a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Cloning-a-security-group"
---

## Scenarios

Compared to creating a new security group from scratch, it is more efficient to clone an existing one with similar traffic requirements and then modify it accordingly.

## Action description

* Cross\-account cloning of security groups is not supported.

* Cross\-region cloning of security groups is not supported.

* When cloning a security group, please delete rules that cannot be cloned (i.e., rules referencing the source or destination **Security Group**) on the cloning page.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click  **··· \> Clone Security Group** on the right side of the target security group.

5. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Enter the name of new Security Group. |sg\-01 |
   |Regions |Fixed to the region of the target security group. |China (Guangzhou) |
   |VPC |Select the new security group's VPC. |vpc01 |
   |Access rules |Delete any rules that are unsupported for cloning or not needed to be cloned. |\- |
   |Related project |Select the new security group's project. |default |
   |Tags |Add tags as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon to add tags to the security group. |* Tag key: sg\-key<br><br>* Tag value: sg\-v1 |

6. Click **Create** to complete the action.

## What to do next

* [Associate Network Interface](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-a-network-interface)

* [Manage security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules)
