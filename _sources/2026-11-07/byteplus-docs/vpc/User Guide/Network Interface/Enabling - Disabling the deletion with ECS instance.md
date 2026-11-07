---
title: "Enabling/Disabling the deletion with ECS instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After attaching a secondary network interface to an Elastic Compute Service (ECS) instance, you can enable or disable the Deleted with ECS instance feature based on your usage scenario.

<span id=".5byA5ZCvL-WFs-mXremaj-S6keacjeWKoeWZqOWunuS-i-WIoOmZpA=="></span>
## Enable/Disable deletion with ECS instance

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The secondary network interface is attached to the ECS. If unattached, see [Attaching a secondary network interface](https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface#.5oyC6L296L6F5Yqp572R5Y2h).

<span id=".5pON5L2c6K-05piO"></span>
### Action description


* The primary network interface has Removal with ECS Instances enabled by default, and it cannot be disabled.

* The secondary network interface has Deleted with ECS instance disabled by default.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click the name of the target secondary network interface.

   * Enable: Turn on the switch for deletion along with the Elastic Compute Service (ECS) instance

   * Disable: Turn off the switch for deletion along with the Elastic Compute Service (ECS) instance


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes)
