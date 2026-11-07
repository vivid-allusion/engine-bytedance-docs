---
title: "Route table overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Route-table-overview"
---

<span id=".566A5LuL"></span>
## Overview

A route table consists of a series of routing entries that direct traffic to the next\-hop cloud resource.

<span id="2WFbXSgI"></span>
## Category


* Categorized by **creation method**:

   
   |Category |Notes |
   |---|---|
   |**System Route Table** |A system route table is automatically created during VPC creation.<br><br><br>* When a subnet is created, it is associated with the system route table by default. After a subnet is disassociated from a custom route table, it is automatically associated with the system route table.<br><br>* The system route table cannot be manually deleted by users; it is removed only when the associated VPC is deleted. |
   |**Custom Route Table** |Manually created by users, who have full operational permissions for this route table. |
   

* Categorized by **associated objects**:

   
   |Category |Notes |
   |---|---|
   |**Subnet route table** |A subnet route table is associated with a subnet to enable resources within the subnet to forward traffic through the subnet route table. The system route table is the subnet route table. Each subnet must be associated with exactly one route table, while each route table can be associated with multiple subnets. |
   |**Gateway route table** |The gateway route table associates with an IPv4 gateway to forward inbound IPv4 internet traffic to a firewall or gateway node for security protection. |
   

   A comparison between subnet route tables and gateway route tables is shown below:

   
   |Comparison item |Subnet route table |Gateway route table |
   |---|---|---|
   |Associated object |Subnet<br><br><br>* One subnet can only be associated with one subnet route table<br><br>* A single subnet route table can be associated with multiple subnets<br><br><br>For operations, see [Attaching/Detaching a subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet) |IPv4 gateway<br><br>An IPv4 gateway can only be associated with one gateway route table<br><br>For actions, see [Attaching/Detaching an IPv4 Gateway](https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway) |
   |Quota limitations |A VPC supports up to 10 subnet route tables by default |Only one can be created per VPC |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Gateway route table is currently in invite\-only Beta stage. If you need a trial, please contact your account manager.   </div>
   

<span id=".6Lev55Sx5p2h55uu"></span>
## Route entry

<span id=".57uE5oiQ"></span>
### Components


* **Parameter description**

   
   |Parameters |Notes |
   |---|---|
   |Destination CIDR block |The CIDR block to which the destination IP address in the packet belongs. |
   |Next Hop type |Quickly filter out next\-hop cloud resources by next\-hop type. For example, NAT Gateway, CEN, VPN Gateway, etc. |
   |Next Hop |The cloud resource that acts as the next hop for traffic (i.e., data packets). |
   

* **System route**

   * **Default system route entry**

      Default system route entries are automatically included in **every route table** of a VPC. When subnets are added or deleted, the system automatically updates all route tables.

      
      |Destination CIDR |Next Hop type |Next Hop |Notes |
      |---|---|---|---|
      |100.64.0.0/10 |System |System default |Used to access public cloud services. |
      |fd00:64::/32 |System |System default |Used to access public cloud services. |
      |CIDR block of the subnet (including IPv4 and IPv6) |InnerSubnet |System default |\-\- |
      

   * **Synced** ** system route entry**

      Synchronized system route entries are routes that a VPC route table learns from [Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/cen/Product-Overview-01), [Transit Router](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01), and [VPN Gateway](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network). When a route is synchronized to any route table in the VPC, the following process occurs:

      1. The system checks whether the destination CIDR block of the route falls within the range of any VPC subnet CIDR block. If it does, the route is discarded; If it does not, the process continues.

      2. The system then checks whether an identical route (with the same target and destination) already exists. If an identical route is found, the route is discarded. If no identical route exists, the route is added to the route table.

      Route entry description:

      
      |Destination CIDR |Next Hop type |Next Hop |Notes |
      |---|---|---|---|
      |Destination CIDR of CEN routes |Cloud Enterprise Network (CEN) |CEN instances |After a VPC is attached to CEN, CEN synchronizes its routes to the VPC route table in real time. [Learn more](https://docs.byteplus.com/en/docs/cen/Route-entries-01) |
      |Destination CIDR Block for TR route tables |TR |TR instance |When automatic route synchronization is enabled for a VPC\-type connection in the transit router, the transit router dynamically syncs routes from its routing table to the VPC's route table in real\-time. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01) |
      |Destination CIDR Block for VPN Gateway Routes |VPN Gateway |VPN gateway instance |After configuring BGP routing on the VPN gateway, routes are synchronized in real\-time to the route table of its associated VPC. [Learn more](https://docs.byteplus.com/en/docs/vpn/Overview)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The BGP routing of VPN gateway in Beta stage. If you need a trial, please contact your account manager.</div><br> |
      

&nbsp;

* **Custom route**

   These route entries can be manually deleted by users. Route entries are added either manually by users or automatically by the system when certain services (e.g., Internet NAT gateways) are created.

* **Propagated route entries**

   Propagated routes are routes that a VPC route table learns from [Global Direct Exchange Gateway (DXGW)](https://docs.byteplus.com/en/docs/directconnect/Direct_Exchange_Gateway_overview). Every route table in a VPC fully receives all synchronized propagated routes. Route entry description:

   
   |Destination CIDR |Next Hop type |Next Hop |Notes |
   |---|---|---|---|
   |Destination CIDR of DXGW routes |Global Direct Exchange Gateway |DXGW instance |After an DXGW instance is associated with a VPC, the system automatically synchronizes the routes of the DXGW to all subnet route tables of the VPC as propagated routes.<br><br><div data-tips="true" data-tips-type="tip">The Global Direct Exchange Gateway BGP routing feature is in invite\-only beta stage. If you need a trial, please contact your account manager.</div><br> |
   


<span id="cyzkWjyf"></span>
### Matching description

When a VPC route table performs a route lookup for traffic, it matches against all route entries in the route table. The matching follows the **Longest mask match principle**, meaning that the longer the mask of the destination CIDR block of a route entry, the higher its priority. For example, for IPv4, a route entry with a destination CIDR of /32 has the longest mask and the highest priority.

If multiple route entries have the same destination CIDR block, they are matched in the following priority order:


1. Default system route entries, synchronized system route entries, and custom route entries. If none match, proceed to the next step.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Among default system route entries, synchronized system route entries, and custom route entries, any two entries have different destination CIDR blocks.   </div>
   

2. Match propagated routes. If multiple propagated routes have the same destination CIDR block, they are further matched by the following priority:

   1. Routes learned from the DXGW Gateway. If none match, proceed to the next step.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">A VPC can be associated with only one DXGW.      </div>
      

   2. Match routes learned from Cloud WAN. If there are multiple routes with the same destination CIDR block from different Cloud WAN instances, the route from the Cloud WAN instance with the smaller instance ID is selected.


<div data-tips="true" data-tips-type="default">Notes</div>


<div data-tips="true" data-tips-type="default">Two special cases:</div>



* <div data-tips="true" data-tips-type="default">Case 1: the Elastic IP address has a higher priority than the route entries in the route table. For example, if an ECS bound with an EIP also has SNAT rules configured on the NAT Gateway, when it accesses the internet, traffic is forwarded via the EIP rather than the NAT Gateway.</div>


* <div data-tips="true" data-tips-type="default">Case 2: When a VPC route table receives traffic from CEN, it only matches the routes that have been published from this route table to CEN. The matching follows the longest mask match principle.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Use limits


* Quota limitations

   For the quota items adjustable in the table below, if the default quotas are insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to request an increase.

   
   |Category |Limit item |Maximum |Adjustable |
   |---|---|---|---|
   |Subnet route table |Maximum number of route tables creatable per VPC (including both system\-maintained route tables and custom route tables) |10 |Yes |
   ||Maximum custom route entries addable to a single route table |200 |Yes |
   ||Maximum route tables associable with a single subnet |1 |No |
   |Gateway route table |Maximum number of route tables creatable per VPC |1 |No |
   ||The number of IPv4 gateways that can be associated with a single gateway route table |1 |No |
   

* Feature limitations

   Route tables do not support configuring or synchronizing routes for multicast CIDR blocks. The multicast CIDR blocks are as follows:

   * IPv4：224.0.0.0 ~ 239.255.255.255

   * IPv6：FF00::/8


<span id=".5L2_55So5rWB56iL"></span>
## Usage process

The typical process for using custom route tables is as follows:


1. [Create custom route table](https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table)

2. [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry)

3. Subnet vs. Gateway Route Tables:

   * Subnet route table: [Associate Subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet#.5YWz6IGU5a2Q572R)

   * Gateway route table: [Associate IPv4 Gateway](https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway)


<span id=".5bqU55So56S65L6L"></span>
## Example Use Cases

See [Route table use cases](https://docs.byteplus.com/en/docs/vpc/Route-table-use-cases).
