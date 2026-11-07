---
title: "Creating a Network ACL"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-network-ACL"
---

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click **Create Network ACL**.

5. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Name of the Network Access Control List. |acl\-01 |
   |VPC |Select the VPC to which the Network Access Control List belongs. |vpc\-01 |
   |Project |Select the project to which the Network Access Control List belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |Default |
   |Tags |Add one or more custom tags to the Network ACL as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the Add icon, select or enter the tag key and tag value to add tags to the Network Access Control List. |* Tag key: acl\-key<br><br>* Tag value: acl\-v1 |

6. Click **Create** to complete the action.

## What to do next

After creating the Network ACL, you can [Adding an Acl rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules?lang=en) and [Associating a subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-subnet-with-a-network-ACL?lang=en) in sequence.

## Related documents

[CreateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/CreateNetworkAcl)
