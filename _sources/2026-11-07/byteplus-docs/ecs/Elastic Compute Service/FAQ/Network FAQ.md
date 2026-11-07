---
title: "Network FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Network-FAQs"
---


|Category |Question |
|---|---|
|VPC |* [Which CIDR blocks are supported by VPC? How many available IP addresses are there in each CIDR block?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.56eB5pyJ572R57uc5pSv5oyB5L2_55So5ZOq5Lqb572R5q6177yIQ0lEUu-8ie-8n-WQhOe9keauteacieWkmuWwkeWPr-eUqElQ77yf)<br><br>* [How does a VPC ensure the security of ECS instances?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.56eB5pyJ572R57uc5aaC5L2V5L-d6K-B5LqR5pyN5Yqh5Zmo55qE5a6J5YWo77yf)<br><br>* [Can I change the VPC for an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5LqR5pyN5Yqh5Zmo5piv5ZCm5pSv5oyB5YiH5o2i56eB5pyJ572R57uc77yf)<br><br>* [Can different VPCs communicate with each other?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5LiN5ZCM56eB5pyJ572R57uc5LmL6Ze06IO95ZCm5LqS6YCa77yf) |
|Network interface |* [How do I distinguish the primary network interface and the secondary network interface?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5Yy65YiG5Li7572R5Y2h5ZKM6L6F5Yqp572R5Y2h77yf)<br><br>* [Is there a limit on the number of network interfaces mounted to an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5LqR5pyN5Yqh5Zmo5oyC6L29572R5Y2h5pyJ5pWw6YeP6ZmQ5Yi25ZCX77yf)<br><br>* [Must the ECS instance and the secondary network interface to be mounted belong to the same VPC?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5LqR5pyN5Yqh5Zmo5LiO5ZKM5b6F5oyC6L296L6F5Yqp572R5Y2h5b-F6aG75bGe5LqO5ZCM5LiA56eB5pyJ572R57uc5ZCX77yf)<br><br>* [Why is the network of a secondary network interface unreachable after I mount the secondary network interface to an instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5oyC6L296L6F5Yqp572R5Y2h5ZCO77yM6L6F5Yqp572R5Y2h572R57uc5LiN6YCa77yf)<br><br>* [Why does access to the public network fail after I mount a secondary network interface to a Windows ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.V2luZG93c-S6keacjeWKoeWZqOaMgui9vei-heWKqee9keWNoeWQju-8jOiuv-mXruWFrOe9keWksei0pe-8nw==)<br><br>* [Can I change the EIP and private IP address of a network interface?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5q-P5byg572R5Y2h55qE5YWs572RSVDlkoznp4HnvZFJUOaYr-WQpuaUr-aMgeabtOaNou-8nw==)<br><br>* [Can I unmount the primary network interface?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Li7572R5Y2h5piv5ZCm5Y-v5Lul5Y246L2977yf)<br><br>* [What should I do if I fail to unmount a network interface?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Y246L29572R5Y2h5aSx6LSl77yM6KaB5oCO5LmI5aSE55CG77yf)<br><br>* [Why is an incorrect IP address displayed on a Windows instance after I mount, uninstall, or disable a network interface and perform other operations?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.V2luZG93c-WunuS-i-e9keWNoei_m-ihjOaMgui9veOAgeWNuOi9veOAgeemgeeUqOetieaTjeS9nOWQju-8jElQ5Zyw5Z2A5pi-56S66ZSZ6K-v77yf) |
|Security group |* [How do I plan security groups appropriately?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5ZCI55CG6KeE5YiS5a6J5YWo57uE77yf)<br><br>* [How do I open a port?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5pS-6YCa56uv5Y-j77yf)<br><br>* [What are the common ports for ECS instances?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#oMnwf9pD)<br><br>* [How do I open port 25?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs?TagIDs=2,70,69,87#.5aaC5L2V5pS-6YCaMjXlj7fnq6_lj6PvvJ8=)<br><br>* [What should I do if specific ports cannot be accessed?/What are the high-risk ports?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5peg5rOV6K6_6Zeu5YWs5pyJ5LqR5p-Q5Lqb56uv5Y-j5pe25oCO5LmI5Yqe77yf)<br><br>* [How to view which ports are opened on an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yLRUNT5a6e5L6L5pS-6YCa5LqG5ZOq5Lqb56uv5Y-j77yf)<br><br>* [How do I change the security groups for an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5Li65LqR5pyN5Yqh5Zmo5pu05o2i5a6J5YWo57uE77yf)<br><br>* [What are the differences between a security group and the Windows Firewall?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5a6J5YWo57uE5LiOV2luZG93c-mYsueBq-WimeacieS7gOS5iOWMuuWIq--8nw==)<br><br>* [Why is a Windows instance with an associated EIP still unable to communicate with the public network even after the security group rules are configured to allow traffic?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.57uR5a6a5YWs572RSVDnmoRXaW5kb3dz5a6e5L6L5Li65LuA5LmI5pS-6YCa5LqG5a6J5YWo57uE77yM5L6d54S25peg5rOV5LiO5YWs572R5LqS6YCa77yf)<br><br>* [How can I see whether ports enabled in a security group take effect?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5Yik5pat5a6J5YWo57uE5byA5pS-55qE56uv5Y-j5piv5ZCm55Sf5pWI77yf)<br><br>* [Why can't I access services deployed on an ECS instance after I configure the security group for the instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo6YWN572u5LqG5a6J5YWo57uE77yM5YW26YOo572y55qE5pyN5Yqh6L-Y5piv5peg5rOV6KKr6K6_6Zeu77yf) |
|EIP |* [How to view the IP address of an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qESVDlnLDlnYDvvJ8=)<br><br>* [How can I view the price of an EIP instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yL5YWs572RSVDlrp7kvovnmoTku7fmoLzvvJ8=)<br><br>* [How do I view the EIP bandwidth of an instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qE5YWs572RSVDluKblrr3vvJ8=)<br><br>* [How do I modify the configuration of the EIP associated with an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5L-u5pS55LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a55qE5YWs572RSVDphY3nva7vvJ8=)<br><br>* [How do I change the EIP of an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5pu05o2i5LqR5pyN5Yqh5Zmo55qE5YWs572RSVDvvJ8=)<br><br>* [What changes will occur to the bandwidth when a pay-as-you-go EIP is added to a shared bandwidth package? What is the range of the bandwidth upper limit for a shared bandwidth package?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5oyJ6YeP6K6h6LS55YWs572RSVDliqDlhaXliLDlhbHkuqvluKblrr3ljIXlkI7vvIzluKblrr3kvJrmnInku4DkuYjlj5jljJbvvJ_lhbHkuqvluKblrr3ljIXnmoTluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8=)<br><br>* [Why does an ECS instance remain unable to connect to the Internet after being associated with an EIP?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a5YWs572RSVDku43nhLbml6Dms5Xov57mjqXkupLogZTnvZHvvJ8=)<br><br>* [Why is the access latency of an ECS instance high?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo572R57uc6K6_6Zeu5bu26L-f6auY77yf) |


<span id=".56eB5pyJ572R57uc"></span>
## Virtual Private Cloud

<span id=".56eB5pyJ572R57uc5pSv5oyB5L2_55So5ZOq5Lqb572R5q6177yIQ0lEUu-8ie-8n-WQhOe9keauteacieWkmuWwkeWPr-eUqElQ77yf"></span>
### Which CIDR blocks are supported by Virtual Private Cloud (VPC)? How many available IP addresses are there in each CIDR block?

VPC supports two deployment modes: IPv4 single\-stack and dual\-stack (IPv4 & IPv6). ECS instances within a VPC can communicate via IPv4 (32\-bit address length) or IPv6 (128\-bit address length) addresses, with IPv4 and IPv6 being mutually independent.


* The following table describes the IPv4 CIDR blocks supported by VPC and the number of available IP addresses in each CIDR block.

   
   |**CIDR block** |**Number of IP addresses in the VPC (excluding IP addresses reserved by the system)**  |
   |---|---|
   |10.0.0.0/8~24 |16777213 |
   |172.16.0.0/12~24 |1048573 |
   |192.168.0.0/16~24 |65533 |
   |172.31.0.0/16 (reserved for the default VPC) |65533 |
   

* Since IPv6 addresses on the BytePlus platform are globally unique, the IPv6 CIDR blocks are automatically assigned by the system to avoid conflicts. The subnet mask of a VPC CIDR block is fixed at /56, and that of each subnet CIDR block is fixed at `/64`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Dual\-Stack VPC is currently in beta. If you need a trial, contact your account manager.</div>


<span id=".56eB5pyJ572R57uc5aaC5L2V5L-d6K-B5LqR5pyN5Yqh5Zmo55qE5a6J5YWo77yf"></span>
### How does a VPC ensure the security of ECS instances?


* A VPC is a logically isolated network environment. Direct communication is not possible between different VPCs, nor between a VPC and the public network. Other products are required for the communication.

* The network interface of an ECS instance must be associated with a [security group](https://docs.byteplus.com/en/docs/ecs/Security-group-overview) of the VPC. The security group controls the inbound and outbound traffic of the network interface. By default, all traffic is denied. You need to configure specific rules to allow traffic.

* You can configure [network access control lists (ACLs)](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) for subnets in a VPC based on your needs to control the traffic of the subnets.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To facilitate user experience, the system automatically adds specific rules to security groups and network ACLs to allow traffic. You can modify the rules based on your needs.</div>


<span id=".5LqR5pyN5Yqh5Zmo5piv5ZCm5pSv5oyB5YiH5o2i56eB5pyJ572R57uc77yf"></span>
### Can I change the VPC for an ECS instance?

Yes, you can. For more information, see [Changing VPC or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance).

<span id=".5LiN5ZCM56eB5pyJ572R57uc5LmL6Ze06IO95ZCm5LqS6YCa77yf"></span>
### Can different VPCs communicate with each other?

By default, different VPCs are fully isolated from one another. However, interconnection between them can be achieved using specific products.


|Product |Description |Same account, same region |Cross\-account, same region |Same account, cross\-region |Cross\-account, cross\-region |
|---|---|---|---|---|---|
|Cloud Enterprise Network (CEN) |Complete private network interconnection among multiple VPCs is achieved on the cloud. |Supported. For more information, see [Same account, same region VPC interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01). |Supported. For more information, see [Cross-account, same-region VPC interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region). |Supported. For more information, see [Same account, cross-region VPC interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01). |Supported. For more information, see [Cross-account, cross-region VPC interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts). |
|Transit Router (TR) |Flexibly define connectivity and isolation between multiple VPCs. |Supported. For more information, see [Implementing private connectivity and segmentation between VPCs (same account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02). |Supported. For more information, see [Implementing private connectivity and segmentation between VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04). |Supported. For more information, see [Implementing private connectivity and segmentation between VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03). ||
|PrivateLink |Resources within a VPC can securely and easily access services shared by other VPCs. |Supported. For more information, see [Implementing private access between VPCs within the same account](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02). |Supported. For more information, see [Implementing private access between VPCs across accounts](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03). |Native support is not available, but cross\-region access can be achieved by using other products. ||
|VPN connection |Complete interconnection between two VPCs is achieved. |Supported. For more information, see [Establishing network connectivity between VPCs](https://docs.byteplus.com/en/docs/vpn/Connecting-virtual-private-clouds). ||||


<span id=".572R5Y2h"></span>
## Network interface

<span id=".5aaC5L2V5Yy65YiG5Li7572R5Y2h5ZKM6L6F5Yqp572R5Y2h77yf"></span>
### How do I distinguish the primary network interface and the secondary network interface?


* Primary network interface: When you create an ECS instance, the primary network interface is created by default along with the ECS instance. You cannot unmount the primary network interface from the ECS instance.

* Secondary network interface: A network interface that can be independently created, flexibly mounted, and unmounted.


To distinguish between the primary network interface and the secondary network interface of an ECS instance, perform the following steps:


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select a target region.

3. In the left\-side navigation pane, click "Instances".

4. Click the name of the target ECS instance.

5. Select the "Network Interface" tab. You can distinguish between the primary network interface and the secondary network interface from the "Type" column in the list.


<span id=".5LqR5pyN5Yqh5Zmo5oyC6L29572R5Y2h5pyJ5pWw6YeP6ZmQ5Yi25ZCX77yf"></span>
### Is there a limit on the number of network interfaces mounted to an ECS instance?

There is a limit on the number of network interfaces mounted to an ECS instance. The limit varies based on the ECS instance type. For more information, see [Instance type list](https://docs.byteplus.com/en/docs/ecs/General-purpose).

<span id=".5LqR5pyN5Yqh5Zmo5LiO5ZKM5b6F5oyC6L296L6F5Yqp572R5Y2h5b-F6aG75bGe5LqO5ZCM5LiA56eB5pyJ572R57uc5ZCX77yf"></span>
### Must the ECS instance and the secondary network interface to be mounted belong to the same VPC?

They must belong to the same VPC. However, you can mount secondary network interfaces from different subnets to an ECS instance to segment traffic.

<span id=".5oyC6L296L6F5Yqp572R5Y2h5ZCO77yM6L6F5Yqp572R5Y2h572R57uc5LiN6YCa77yf"></span>
### Why is the network of a secondary network interface unreachable after I mount the secondary network interface to an instance?

Possible causes are as follows:


|Cause |Description |
|---|---|
|Images fail to recognize secondary network interfaces. |After you mount a secondary network interface to an ECS instance, some images cannot automatically recognize the private IP address of the secondary network interface or add the corresponding routes. For more information, see [Configuring secondary network interfaces for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances). |
|The security group does not allow the relevant traffic. |The security group associated with the secondary network interface may not allow the outbound and inbound traffic required. Check whether it allows the outbound and inbound traffic required. For more information, see [Managing security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).<br><br>> If you configure a firewall within the ECS instance, you must also configure traffic ports for the firewall. |
|The network ACL does not allow traffic. |The network ACL associated with the subnet where the secondary network interface is located may not allow the relevant traffic. Check whether it allows the outbound and inbound traffic you need. For more information, see [Network ACL overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) and [Modifying network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules). |


<span id=".V2luZG93c-S6keacjeWKoeWZqOaMgui9vei-heWKqee9keWNoeWQju-8jOiuv-mXruWFrOe9keWksei0pe-8nw=="></span>
### Why does access to the public network fail after I mount a secondary network interface to a Windows ECS instance?

After you mount a secondary network interface to a Windows ECS instance, the image automatically detects the secondary network interface and adds routes. However, the automatically added routes for the secondary network interface are equivalent to those of the primary network interface, which may result in public network\-bound data transfer being routed to a network interface that does not have an associated Elastic IP address (EIP). Therefore, you need to manually specify the forwarding policy. For more information, see [Modify network interface routes for a Windows instance](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).

<span id=".5q-P5byg572R5Y2h55qE5YWs572RSVDlkoznp4HnvZFJUOaYr-WQpuaUr-aMgeabtOaNou-8nw=="></span>
### Can I change the EIP and private IP address of a network interface?


* For information about how to change the EIP of a network interface, see [Associating/Disassociating EIPs](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP).

* You can change the secondary private IP addresses of a network interface (including secondary private IPv4 address and private IPv6 address) by releasing or adding private IP addresses. For more information, see [Assigning/Reclaiming IPv4 addresses](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address) and [Assigning/Reclaiming IPv6 addresses](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv6-address).

* You cannot change the primary private IPv4 address of a secondary network interface. However, you can change the primary private IPv4 address of the primary network interface by [changing the VPC](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance).


<span id=".5Li7572R5Y2h5piv5ZCm5Y-v5Lul5Y246L2977yf"></span>
### Can I unmount the primary network interface?

No, you cannot. The lifecycle of the primary network interface is consistent with that of the ECS instance. You cannot unmount the primary network interface.

<span id=".5Y246L29572R5Y2h5aSx6LSl77yM6KaB5oCO5LmI5aSE55CG77yf"></span>
### What should I do if I fail to unmount a network interface?

Go to the [ECS console](https://console.byteplus.com/ecs/instance) and click "Support \> Create ticket" in the top menu bar to obtain support.

<span id=".V2luZG93c-WunuS-i-e9keWNoei_m-ihjOaMgui9veOAgeWNuOi9veOAgeemgeeUqOetieaTjeS9nOWQju-8jElQ5Zyw5Z2A5pi-56S66ZSZ6K-v77yf"></span>
### Why is an incorrect IP address displayed on a Windows instance after I mount, uninstall, or disable a network interface and perform other operations?

You can try to restart the instance. If the issue persists, execute `ipconfig /release` and `ipconfig /renew` commands within the instance to refresh the IP address.

<span id=".5a6J5YWo57uE"></span>
## Security group

<span id=".5aaC5L2V5ZCI55CG6KeE5YiS5a6J5YWo57uE77yf"></span>
### How do I plan security groups appropriately?

Proper security group planning simplifies business traffic management and enhances security. For the planning principles and examples, see [Planning security groups](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups).

<span id=".5aaC5L2V5pS-6YCa56uv5Y-j77yf"></span>
### How do I open a port?

You can add rules to the security group associated with the network interface of an ECS instance to allow traffic through the specified port. For more information, see [Adding security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

<span id="oMnwf9pD"></span>
### What are the common ports for ECS instances?

For more information, see [Common ports for ECS instances](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances).

<span id=".5aaC5L2V5pS-6YCaMjXlj7fnq6_lj6PvvJ8="></span>
### How do I open port 25?

Port 25 is a [high-risk port](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances). BytePlus blocks this port by default. Even if you open port 25 by specifying a security group rule, the port remains unavailable. Therefore, we recommend that you use other non\-high risk ports.

When port 25 is required for business purposes, submit a ticket to apply for its use. Only enterprise users are eligible to do so.

<span id=".5peg5rOV6K6_6Zeu5YWs5pyJ5LqR5p-Q5Lqb56uv5Y-j5pe25oCO5LmI5Yqe77yf"></span>
### What do I do if I fail to access specific ports on the public cloud?

**Issue phenomenon:**  Access to specific ports on the public cloud fails in some regions and with some line operators, while access to other ports is normal.

**Issue analysis:**  Some line operators identify the ports listed in the following table as high\-risk and block them by default.


|Agreement |Port |
|---|---|
|TCP |42 135 137 138 139 444 445 593 1025 1068 1434 3127 3128 3129 3130 4444 4789 5554 5800 5900 9996 |
|UDP |135 139 1026 1027 1028 1068 1433 1434 4789 5554 9996 |


**Solution:**  We recommend that you change sensitive ports to other non\-high risk ports for business use.

<span id=".5aaC5L2V5p-l55yLRUNT5a6e5L6L5pS-6YCa5LqG5ZOq5Lqb56uv5Y-j77yf"></span>
### How to view which ports are opened on an ECS instance?

To view the ports opened on each network interface of an ECS instance, perform the following operations:


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select a target region.

3. In the left\-side navigation pane, click "Instances".

4. Click the name of the target ECS instance.

5. In the upper left corner on the "Security Group" tab, select the target network interface (the primary network interface or a secondary network interface).

6. Select the "Inbound" or "Outbound" tab based on your needs to view the ports opened in the "Port range" column of the security group rules.


<span id=".5aaC5L2V5Li65LqR5pyN5Yqh5Zmo5pu05o2i5a6J5YWo57uE77yf"></span>
### How do I change the security groups for an ECS instance?

To change the security groups for an ECS instance, you are essentially changing the security groups for the network interfaces mounted to the ECS instance. For more information, see [Changing security groups](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups).

<span id=".5a6J5YWo57uE5LiOV2luZG93c-mYsueBq-WimeacieS7gOS5iOWMuuWIq--8nw=="></span>
### What are the differences between a security group and the Windows Firewall?


1. They belong to different entities. A security group is a feature of VPC, and each network interface of an ECS instance must be associated with a security group. The Windows Firewall is part of the Windows operating system.

2. Traffic path for Windows instances:

   * Outbound: Traffic first passes through the Windows Firewall, and then through the security group, before accessing other cloud services or the public network.

   * Inbound: Traffic from other cloud services or the public network first passes through the security group, and then through the Windows Firewall, before accessing applications on the Windows system.

3. Their usage scenarios are different.

   * A security group is mainly used to control inbound and outbound traffic for a set of network interfaces. It enables quick setup of traffic control systems between ECS instances, and between ECS instances and the public network.

   * The Windows Firewall is primarily used to control traffic for applications running on the Windows system.


<span id=".57uR5a6a5YWs572RSVDnmoRXaW5kb3dz5a6e5L6L5Li65LuA5LmI5pS-6YCa5LqG5a6J5YWo57uE77yM5L6d54S25peg5rOV5LiO5YWs572R5LqS6YCa77yf"></span>
### Why is a Windows instance with an associated EIP still unable to communicate with the public network even after the security group rules are configured to allow traffic?

Possible causes are as follows:


* You have enabled the Windows Firewall. You can disable the Windows Firewall or configure rules to allow traffic. For more information, see [Configuring firewall of Windows ECS instance](https://docs.byteplus.com/en/docs/ecs/Security-FAQs).

* The subnet to which this instance belongs is associated with a network Access Control List (ACL). You can either [disassociate the subnet from the network ACL](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-subnet-with-a-network-ACL#.6Kej6Zmk5YWz6IGU5a2Q572R) or configure network ACL rules to allow traffic. For more information, see [Managing network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules).


<span id=".5aaC5L2V5Yik5pat5a6J5YWo57uE5byA5pS-55qE56uv5Y-j5piv5ZCm55Sf5pWI77yf"></span>
### How can I see whether ports enabled in a security group take effect?

After you open a port by configuring the security groups associated with an ECS instance, you can use any of the following methods to verify whether the port of the ECS instance is reachable.


<Tabs>
<Tab zoneid="za02MNEj8o" title="Method 1: telnet command">
<TabTitle>Method 1: telnet command</TabTitle>

On a terminal within the CIDR block allowed by the security group, execute the following command in the command line:

telnet <IP address of the ECS instance\> <allowed port\>


* If the port is not allowed, the request will persist until the operation times out.

* If the port is allowed but no service is deployed on it, a connection refused message will be returned.

* If the port is allowed and a service is deployed on it, a connection success message will be returned.


</Tab>
<Tab zoneid="LdFhZcNKX4" title="Method 2: nc command">
<TabTitle>Method 2: nc command</TabTitle>

On a terminal within the CIDR block allowed by the security group, execute the following command in the command line:

nc \-zv <IP address of the ECS instance\> <allowed port\>


* If the port is not allowed, the request will persist until the operation times out.

* If the port is allowed but no service is deployed on it, a connection refused message will be returned.

* If the port is allowed and a service is deployed on it, a connection success message will be returned.


</Tab>
</Tabs>


<span id=".5Li65LuA5LmI5LqR5pyN5Yqh5Zmo6YWN572u5LqG5a6J5YWo57uE77yM5YW26YOo572y55qE5pyN5Yqh6L-Y5piv5peg5rOV6KKr6K6_6Zeu77yf"></span>
### Why can't I access services deployed on an ECS instance after I configure the security group for the instance?

Possible causes are as follows:


|Cause |Description |
|---|---|
|Network ACL restrictions |If network ACLs are created, check whether the network ACL associated with the subnet of the ECS instance restricts access traffic. [Learn more](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) |
|Firewall restrictions of the operating system |Check whether the firewall of the ECS instance's operating system restricts access traffic. For more information, see [Configuring firewall for ECS instance running CentOS 7](https://developer.volcengine.com/articles/7270815826700140600), [Configuring firewall for ECS instance running Windows](https://docs.byteplus.com/en/docs/ecs/Security-FAQs), and [Configuring firewall for ECS instance running Ubuntu](https://docs.byteplus.com/en/docs/ecs/Security-FAQs). |
|Abnormal status of the ECS instance |Check whether the status of the ECS instance is abnormal, such as being unstarted, shut down due to arrears, or shut down upon expiration. [Learn more](https://docs.byteplus.com/en/docs/ecs/Instance-lifecycle) |
|Services not started |Check whether the services deployed on the ECS instances are started. |
|Public network exceptions |If services are provided to public network terminals, resolve the issue by performing the following checks:<br><br><br>* If an EIP is associated with the ECS instance to provide services to the public network, check whether the EIP is shut down due to arrears or expiration. [Learn more](https://docs.byteplus.com/en/docs/ecs/EIP-overview)<br><br>* If services are provided to the public network using the DNAT rules of a public network NAT gateway, check whether the DNAT rule configuration is correct. [Learn more](https://docs.byteplus.com/en/docs/natgateway/Providing-services-over-the-internet-using-DNAT)<br><br>* If services are provided to the public network using CLB, check whether the CLB configuration is correct. [Learn more](https://docs.byteplus.com/en/docs/clb/Getting-Started) |
|Cloud Firewall restrictions |If Cloud Firewall is enabled, verify whether it is restricting data transmission. [Learn more](https://docs.byteplus.com/en/docs/cloud_firewall/What-is-BytePlus-Cloud-Firewall) |


<span id=".5YWs572RSVA="></span>
## EIP

<span id=".5aaC5L2V5p-l55yL5a6e5L6L55qESVDlnLDlnYDvvJ8="></span>
### How to view the IP address of an ECS instance?

You can view the EIP associated with an instance on the instance list page or details page. For more information, see [View created instances and instance configuration information](https://docs.byteplus.com/en/docs/ecs/What-to-do-next#.5p-l55yL5bey6LSt5Lmw5a6e5L6L5Y-K5YW26YWN572u5L-h5oGv).

<span id=".5aaC5L2V5p-l55yL5YWs572RSVDlrp7kvovnmoTku7fmoLzvvJ8="></span>
### How can I view the price of an EIP instance?

You can view the price of an EIP instance on the [price calculator](https://www.byteplus.com/en/pricing?product=EIP&tab=2) page. The price calculator provides reference prices. The specific fees shall be subject to the actual order results in the [EIP console](https://console.byteplus.com/eip/eips).

<span id=".5aaC5L2V5p-l55yL5a6e5L6L55qE5YWs572RSVDluKblrr3vvJ8="></span>
### How do I view the EIP bandwidth of an instance?

To view the bandwidth upper limit of the EIP associated with an instance, perform the following operations:

> Elastic IP addresses with different bandwidth specifications have different minimum bandwidth limits. Please refer to [Fee Description](https://docs.byteplus.com/en/docs/eip/Subscription#.6LS555So6K-05piO) for details.



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project.

4. In the list of instances, click the EIP of the target instance.

5. View the bandwidth upper limit in the "Current configuration" section of the EIP details page.


<span id=".5aaC5L2V5L-u5pS55LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a55qE5YWs572RSVDphY3nva7vvJ8="></span>
### How do I modify the configuration of the EIP associated with an ECS instance?

You can modify the configuration of the EIP associated with an ECS instance based on your needs. For more information, see [Changing EIP configuration](https://docs.byteplus.com/en/docs/ecs/Changing_EIP_configuration).

<span id=".5aaC5L2V5pu05o2i5LqR5pyN5Yqh5Zmo55qE5YWs572RSVDvvJ8="></span>
### How do I change the EIP of an ECS instance?

To change the EIP associated with the primary private IPv4 address of the primary network interface of an ECS instance, you first [apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP), then [disassociate](https://docs.byteplus.com/en/docs/ecs/Disassociating-an-EIP) the current EIP from the ECS instance, and finally [associate](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP) the new EIP with the ECS instance.

For information about how to change the EIP associated with either the secondary private IPv4 address of an ECS instance's primary network interface or the ECS instance's secondary network interface, see [Associating/Disassociating an EIP](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP).

<span id=".5oyJ6YeP6K6h6LS55YWs572RSVDliqDlhaXliLDlhbHkuqvluKblrr3ljIXlkI7vvIzluKblrr3kvJrmnInku4DkuYjlj5jljJbvvJ_lhbHkuqvluKblrr3ljIXnmoTluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8="></span>
### What changes will occur to the bandwidth when a pay\-as\-you\-go EIP is added to a shared bandwidth package? What is the range of the bandwidth upper limit for a shared bandwidth package?

After an EIP is added to a shared bandwidth package, its original bandwidth upper limit becomes invalid, and it shares the bandwidth upper limit of the shared bandwidth package.

The bandwidth upper limit for a shared bandwidth package ranges from 2 to 5,000 Mbps.

<span id=".5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a5YWs572RSVDku43nhLbml6Dms5Xov57mjqXkupLogZTnvZHvvJ8="></span>
### Why does an ECS instance remain unable to connect to the Internet after being associated with an EIP?

An ECS instance is associated with an Elastic IP (EIP) when the EIP is associated with the primary private IPv4 address of the instance’s primary network interface. If the instance fails to access the Internet, the possible causes are described in the following table:


|Cause |Description |
|---|---|
|The security group does not allow the relevant traffic. |The security group associated with the primary network interface may not allow the outbound and inbound traffic required. Check whether it allows the outbound and inbound traffic required. For more information, see [Managing security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).<br><br>> If you configure a firewall within the ECS instance, you must also configure traffic ports for the firewall. |
|The network ACL does not allow traffic. |The network ACL associated with the subnet where the primary network interface resides may not allow the relevant traffic. Check whether it allows the inbound and outbound traffic you need. For more information, see [Network ACL overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) and [Modifying network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules). |
|Abnormal status of the EIP |The EIP status may be abnormal, such as being shut down upon expiration or due to arrears. |


<span id=".5Li65LuA5LmI5LqR5pyN5Yqh5Zmo572R57uc6K6_6Zeu5bu26L-f6auY77yf"></span>
### Why is the access latency of an ECS instance high?

Possible causes are as follows:


|Cause |Description |
|---|---|
|Access to domain names outside the Chinese mainland |ECS instances in the Chinese mainland may experience high network latency or unstable connection when accessing domain names outside the Chinese mainland. |
|Bandwidth limit |The latency is related to your network environment, computer performance, and remote connection settings. We recommend that you troubleshoot the issue from the following aspects:<br><br><br>* Switch to a better\-performing network and close other applications or devices that consume large amounts of network resources to reduce network bandwidth usage pressure.<br><br>* Adjust remote connection settings: Higher resolution and color depth increase the amount of data transmitted and latency. We recommend that you lower the display settings of the remote desktop, such as resolution and color depth.<br><br>* Identify if bandwidth rate limiting exists by [viewing monitoring data](https://docs.byteplus.com/en/docs/eip/Viewing-monitoring-data). You can [increase the bandwidth upper limit](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth) or [add to a shared bandwidth package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package) to improve bandwidth utilization. |
|Shared ECS instance limits |In the non\-binding CPU scheduling mode of [Shared instances](https://docs.byteplus.com/en/docs/ecs/Shared), each vCPU is randomly assigned to any idle CPU hyper\-thread. vCPUs from different instances may compete for physical CPU resources, leading to unstable fluctuations in computing performance under high load. We recommend that you use General\-purpose [g3al instances](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNhbA==) to resolve this issue. |
