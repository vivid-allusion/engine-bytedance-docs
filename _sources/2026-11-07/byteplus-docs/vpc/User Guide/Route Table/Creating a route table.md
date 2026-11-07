---
title: "Creating a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table"
---

## Scenarios

When the system route table cannot meet your business requirements, you can create custom route tables to flexibly manage the network traffic.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click **Create Route Table**.

5. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Enter the name of custom route table. |route\-1 |
   |VPC |Select the VPC for the route table. |vpc01 |
   |Associated Resource Type |Select the type of associated resource. Supports subnet and gateway:<br><br><br>* Subnet: Resources within the subnet forward traffic through the route table.<br><br>* Gateway: Forward incoming Internet traffic to the firewall or gateway node for security protection. |Subnet |
   |Route entry |* After selecting a VPC, the system automatically adds the following system route entries:<br><br>   * A route entry with the destination CIDR block 100.64.0.0/10, which is used for communication between cloud resources within the VPC.<br><br>   * A route entry with the destination CIDR block matching the subnet's CIDR block, which is used for communication between subnets.<br><br>* Click  **+Add route** to add multiple route entries as required. For parameter details and limits of route entries, see [Adding a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry). |\- |
   |Related project |Select a route table entry. [Learn more](https://docs.byteplus.com/en/docs/vpc/Managing-projects) |default |
   |Tags |Add one or more custom tags to the route table as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon, select or enter the tag key and tag value to add tags to the route table. |* Tag key: route\-key<br><br>* Tag value: route\-v1 |

6. Click **Create** to complete the action.

## What to do next

* [Add route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry)

* Associated resources:

   * Subnet route table: [Associate Subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet#.5YWz6IGU5a2Q572R)

   * Gateway route table: [Associate IPv4 Gateway](https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway)

## Related documents

[CreateRouteTable](https://docs.byteplus.com/en/docs/vpc/CreateRouteTable)
