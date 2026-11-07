---
title: "Implementing private interconnectivity and isolation between different VPCs (same account, same region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02"
---

This section describes how to use Transit Router (TR) to connect vpc01 and vpc02 to vpc03 under the same account in the same region. It also explains how to isolate vpc01 from vpc02, as illustrated in the diagram below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_907f79ede9089aafd79bded679c2f4a1.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created three Virtual Private Clouds (VPCs) and their subnets. For procedure, see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure that the VPCs do not contain conflicting subnets. That is, no duplicate or overlapping CIDR blocks exist.   </div>
   

* You have created Elastic Compute Service (ECS) instances in the three VPCs. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".6Lev55Sx6KeE5YiS"></span>
## Route planning

A single TR instance can use the same route table to forward traffic from multiple network instances that share a common destination. Thus, in this example, the TR uses one route table for forwarding from vpc01/vpc02 to vpc03, and a separate route table for the return path from vpc03 to vpc01/vpc02. This design necessitates at least two route tables, as illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_174b27efb6f1438028d5e58fff7e1cc7.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Routes in the VPC route tables illustrated above can be manually configured or automatically synchronized. This example uses automatic publishing.</div>


<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures


1. [Create a TR instance](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02#.5q2l6aqk5LiA77ya5Yib5bu6VFLlrp7kvos=): Create a TR instance to host the TR service.

2. [Create a TR custom route table](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02#.5q2l6aqk5LqM77ya5Yib5bu6VFLoh6rlrprkuYnot6_nlLHooag=): Create a custom route table to receive and forward network traffic along with the TR system route table.

3. [Create an attachment and configure routing](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02#.5q2l6aqk5LiJ77ya5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx): Create three attachments to separately connect the TR instance and three VPCs. On the TR side, configure association forwarding and route learning to control the traffic flow to and from these VPCs. On the VPC side, configure auto publishing to control flow direction.

4. [View TR and VPC routes](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02#.5q2l6aqk5Zub77ya5p-l55yLVFLlkoxWUEPot6_nlLE=): Review that the routes of the TR instance and three VPCs meet expectations.

5. [Validation](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02#.57uT5p6c6aqM6K-B): Run `ping` to verify the connectivity between ECS instances in different VPCs to ensure that the VPCs are connected and isolated as expected.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya5Yib5bu6VFLlrp7kvos="></span>
### Step 1: Create a TR instance


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. In the top menu bar, select the target project and region.

3. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Guangzhou) |
   |Name |The system names it TR\-*XXX* by default. Modify the name as needed for easier identification. |tr01 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br>In this example, the ASN for the TR instance can be anyone within the valid range.<br><br>After being assigned with an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published from it to other network instances. |64512 |
   |Supports multicast |Multicast is a point\-to\-multipoint communication method that allows one server to send packets to multiple clients simultaneously, avoiding the bandwidth waste associated with traditional unicast or broadcast.<br><br>By default, the system disables multicast. To use it, enable multicast on the TR. [Prerequisite](https://docs.byteplus.com/en/docs/transitrouter/Multicast-Overview) |Do not enable |
   |Related project |Select the project to which the TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

4. Click **Create** to complete the creation of the TR instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table (rtb\-sys). The following uses rtb\-sys as an example.</div>


<span id=".5q2l6aqk5LqM77ya5Yib5bu6VFLoh6rlrprkuYnot6_nlLHooag="></span>
### Step 2: Create a TR custom route table


1. Click the name of the target TR instance.

2. In the zone below **Basic information**, select the **Route Table** tab.

3. Click **Create Route Table** to the right of the route table list, and type rtb\-set as the route table name.

4. Click **Create** to complete the creation of the TR route table.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
### Step 3: Create an attachment and configure routing

Create three attachments to connect to vpc01, vpc02, and vpc03 separately by the following steps.


1. In the section below **Basic information**, select the **Intra\-region attachment** tab.

2. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |Example<br><br>(Attach vpc03) |
   |---|---|---|---|---|
   |**Basic information** |||||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |tr01 |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |China (Guangzhou) |China (Guangzhou) |
   |Name |The name for the network instance attachment to be created. |attach\-vpc01 |attach\-vpc02 |attach\-vpc03 |
   |**Network instances** |||||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |vpc03 |
   |**Attachment point configuration** |||||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select an availability zone and subnet, then set this availability zone as the default. |China (Guangzhou) A, subnet01 |Availability Zone A, subnet02 |Availability Zone A, subnet03 |
   

3. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |Example<br><br>(Attach vpc03) |
   |---|---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on rtb\-sys.</div><br> |Enabled, rtb\-sys |Enabled, rtb\-sys |Enabled, rtb\-set |
   |Route learning |After enabling route learning, the TR route table will automatically learn routes from the network instance, and generate entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (rtb\-set) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01. That is, routes pointing to vpc01 are configured in rtb\-set.</div><br> |Enabled, rtb\-set |Enabled, rtb\-set |Enabled, rtb\-sys |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within the selected VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from rtb\-sys to all route tables within vpc01. These synchronized routes are system routes. That is, routes pointing to the TR are configured in the vpc01 route tables.</div><br> |Checked |Checked |Checked |
   

4. Click **Buy now** to complete the action.


<span id=".5q2l6aqk5Zub77ya5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
### Step 4: View TR and VPC routes


1. View the TR route tables (rtb\-sys and rtb\-set) in sequence, and confirm that the route entries listed below exist.

   
   |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |
   |---|---|---|---|---|---|---|
   |rtb\-sys |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
   |rtb\-set |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |
   ||192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |
   

2. View the system routes in the route tables of vpc01, vpc02, and vpc03 in sequence, and confirm that the route entries listed below exist.

   
   |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
   |---|---|---|---|---|
   |vpc01 |192.168.32.0/24 |Available |TR |tr01 |
   |vpc02 |192.168.32.0/24 |Available |TR |tr01 |
   |vpc03 |192.168.0.0/24 |Available |TR |tr01 |
   ||192.168.16.0/24 |Available |TR |tr01 |
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

The following verification steps take a Linux\-based ECS as an example:


1. Remotely log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `ping` command to connect the private IP addresses of respective ECS instances in vpc02 and vpc03, verifying network connectivity.

   * The ECS instances in vpc01 and vpc02 are mutually isolated and cannot ping each other.

   * The ECS instances in vpc01 and vpc03 can communicate and ping each other successfully.

3. Similarly, remotely log in to the ECS instances in vpc02 and vpc03 to verify connectivity between vpc02, vpc03, and another VPC.
