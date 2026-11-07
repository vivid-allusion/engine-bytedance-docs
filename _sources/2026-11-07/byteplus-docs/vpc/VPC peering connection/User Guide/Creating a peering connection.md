---
title: "Creating a peering connection"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-peering-connection"
---

## Action notes

* After creating a peering connection, the requester VPC initiates a connection request to the accepter VPC.

* Within the same account:​ The system automatically accepts the peering connection. Across different accounts:​ The accepter must manually accept the request.

> **tip**

> The CIDR blocks of the two VPCs must not overlap.

## Procedures

1. Log in to the [Peering Connection console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/peerConnection).

2. In the top menu bar, select the target region and project.

3. Click **Create peering connection**.

4. Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |Name |Enter the name of peering connection instance. |Peering\-X |
   |Requester VPC instance |Select the requester VPC. |VPC\-Source |
   |Acceptor account type |Select the acceptor account type.<br><br><br>* **Same account**: The accepter VPC and the requester VPC belong to the same account.<br><br>* **Cross\-account**: The accepter VPC and the requester VPC belong to different accounts. |Cross\-account |
   |Acceptor root user UID |If you select cross\-region, enter the root user ID​. |210005XXXX |
   |Acceptor region type |Select the acceptor region type. Currently, only same region is supported. The accepter VPC and the requester VPC are in the same region. |Same region |
   |Acceptor VPC instance |Select the acceptor VPC. |VPC\-Destination |
   |Project |Select a project​ for the peering connection. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to the Peering Connection as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources More information is available in [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |peerConnection:v1 |

5. Click **Create** to complete the action.
