---
title: "Assigning/Reclaiming IPv6 addresses"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv6-address"
---

This topic describes how to assign IPv6 addresses to or reclaim IPv6 addresses of network interfaces associated with ECS instances.

<span id=".5YiG6YWNSVB2NuWcsOWdgA=="></span>
## Assign IPv6 addresses

<span id=".5pON5L2c6K-05piO"></span>
### Usage notes


* When you create an instance, you can assign IPv6 addresses to the primary network interface only. For more information, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* For the maximum number of private IPv6 addresses that can be assigned to the primary network interface or a secondary network interface associated with an ECS instance, check the private IP quota per network interface for [each ECS instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target ECS instance.

4. On the Instances page, click the name of the target ECS instance.

5. On the "Network Interface" tab, click the name of the target network interface.

6. On the "IP address management" tab, click the "Add Secondary Private IP" button.

7. For the "Private IPv6 Address" parameter, use the dropdown to select automatic assignment or manual assignment.

   * Auto\-assign: The system automatically assigns an unused IPv6 address from the IPv6 CIDR block of the subnet to which the network interface belongs.

   * Custom\-assign: You need to manually enter an unused IPv6 address from the IPv6 CIDR block of the subnet to which the network interface belongs.

8. Click "OK" to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
### Subsequent operations


* If some ECS images cannot identify the newly assigned IPv6 address of the network interface, log in to the ECS instance to configure this address. After this, you can use the newly assigned IPv6 address for instance communication. For details, refer to [Configuring private IPv6 addresses for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances).

* After you assign new IPv6 addresses to network interfaces associated with ECS instances, the instances can only communicate within the same private network. For the instance access to Internet, [enable the IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth) first.


<span id=".5Zue5pS2SVB2NuWcsOWdgA=="></span>
## Reclaim IPv6 addresses


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target ECS instance.

4. On the Instances page, click the name of the target ECS instance.

5. On the "Network Interface" tab, click the name of the target network interface.

6. On the "IP address management" tab, click the "Release" button to the right of the target IP address.

7. Click "OK" to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses): Assigns secondary private IPv6 addresses to the specified network interface (primary network interface or secondary network interface).

* [UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses): Reclaims secondary private IPv6 addresses for the specified network interface.
