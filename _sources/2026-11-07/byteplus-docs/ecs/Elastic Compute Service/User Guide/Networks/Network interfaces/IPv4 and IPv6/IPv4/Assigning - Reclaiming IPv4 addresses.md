---
title: "Assigning/Reclaiming IPv4 addresses"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address"
---

This topic describes how to assign private IPv4 addresses to or reclaim private IPv4 addresses of network interfaces associated with ECS instances.

<span id="e4MNjRgV"></span>
## Assign IPv4 addresses

<span id="hIGBOGXK"></span>
### Usage notes


* When you create an instance, you can assign IPv4 addresses to the primary network interface only. For more information, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* For the maximum number of secondary private IPv4 addresses that can be assigned to the primary network interface or a secondary network interface associated with an ECS instance, check the private IP quota per network interface for [each ECS instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).


<span id="HFJL8OHK"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target ECS instance.

4. On the Instances page, click the name of the target ECS instance.

5. On the "Network Interface" tab, click the name of the target network interface.

6. On the "IP address management" tab, click the "Add Secondary Private IP" button.

7. For the "Secondary Private IPv4 Address" parameter, use the dropdown to select automatic assignment or manual assignment.

   * Auto\-assign: The system automatically assigns an unused IPv4 address from the IPv4 CIDR block of the subnet to which the network interface belongs.

   * Custom\-assign: You need to manually enter an unused IPv4 address from the IPv4 CIDR block of the subnet to which the network interface belongs.

8. Click "Add" to complete the operation.


<span id="cQTHfDhd"></span>
### Subsequent operation


* If the ECS image cannot identify the newly assigned IPv4 address of the network interface, log in to the ECS instance to [configure this address](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances). After this, you can use the newly assigned IPv4 address for instance communication.

* You can associate EIPs with the newly assigned secondary private IPv4 addresses of a network interface. This allows the interface to have multiple associated EIPs to effectively avoid service disruption caused by EIP blocking. For detailed operations, refer to [Binding or unbinding an EIP](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP).


<span id="kVrWG3Hk"></span>
## Reclaim IPv4 addresses


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Images".

3. In the top menu bar, select the project and region of the target ECS instance.

4. On the Instances page, click the name of the target ECS instance.

5. On the "Network Interface" tab, click the name of the target network interface.

6. On the "IP address management" tab, click the "Release" button to the right of the target IP address.

7. Click "Release" to complete the operation.


<span id="YaNnxTY7"></span>
## Related documents


* [AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses): Assigns secondary private IPv4 addresses to one specified network interface (primary network interface or secondary network interface).

* [UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses): Reclaims secondary private IPv4 addresses for one specified network interface.
