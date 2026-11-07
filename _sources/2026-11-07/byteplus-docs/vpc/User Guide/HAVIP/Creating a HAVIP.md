---
title: "Creating a HAVIP"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-HAVIP"
---

## Prerequisites

Virtual Private Cloud (VPC) and its subnet have been created. If not, [create a VPC and its subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

## Instruction

* During the creation of a HAVIP, specifying a project is not supported. Its project ownership is automatically inherited from the subnet it belongs to and cannot be individually moved into or out of a project. When a subnet is moved into or out of a project, the HAVIP will be moved along with it.

* A single account can create up to 20 HaVips per region.

* A maximum of 5 HAVIPs can be created within a single VPC.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **HaVip**.

3. In the top menu bar, select the target project and region.

4. Click **Create HaVip**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of HaVip. |havip\-01 |
   |VPC |Select a VPC. |vpc\-01 \| 192.168.0.0/16 |
   |Subnet<br><br> |Select the subnet for the HaVip and assign a private IP address for it.<br><br><br>* Custom\-assign IP: Manually assign an available IP address from the subnet.<br><br>* Auto\-assign: The system automatically assigns an available IP address from the subnet.<br><br><br>> **tip**<br><br><br>> The HaVip can only be bound to ECS or network interface under this subnet.<br> |subnet\-01 \| 192.168.21.0/24, Auto\-assign IP<br><br> |
   |Tags<br><br> |Add one or more custom tags to the HaVip as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon, select or enter the tag key and tag value to add tags to the HAVIP. |* Tag key: havip\-key<br><br>* Tag value: havip\-v1<br><br><br> |

6. Click **Create** to complete the action.

## Related documents

[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip)
