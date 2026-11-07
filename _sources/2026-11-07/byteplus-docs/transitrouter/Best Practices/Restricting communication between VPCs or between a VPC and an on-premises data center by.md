---
title: "Restricting communication between VPCs or between a VPC and an on-premises data center by route policies"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Realize-network-isolation-between-VPCs-or-IDC-CIDR-blocks-by-Routing-Policy"
---

This topic describes how to restrict communication between Virtual Private Clouds (VPCs) or between a VPC and an on\-premises data center by route policies.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

With route policies, you can restrict communication between VPCs or CIDR blocks. This achieves network isolation and simplifies route configuration of the Transit Router (TR). This example demonstrates how to configure route policies so that vpc01 cannot communicate with vpc02, vpc01 can only access CIDR block 1 in the data center, and vpc02 can only access CIDR block 2 in the data center. Specific network architecture is shown in the diagram below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also use multiple TR route tables to achieve network isolation. For configuration details, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-01">Implementing interconnectivity and isolation between specified VPCs</a> or <a href="https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02">Implementing interconnectivity between independent VPCs and a data center</a>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c53a00d44f3d359d05768413e28d78ff.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Ensure the Direct Connect (DC) Connection and related resources for your on\-premises data center accessing BytePlus are ready. For detailed steps, see the first three steps in [Direct Connect Quick start](https://docs.byteplus.com/en/docs/directconnect/Quick-start).

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5YWo5LqS6YCa5Z-656GA57uE572R"></span>
### Step 1: Configure a basic network with global interconnection


1. Follow the procedure in [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) to create a TR instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system automatically creates a system route table (named rtb\-sys) for your TR instance. The following uses rtb\-sys as an example.   </div>
   

2. Follow the procedure in [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) to connect vpc01 and vpc02 to the TR instance. The route configuration is described in the table below.

   
   |Parameter |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |
   |---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on rtb\-sys.</div><br> |Enable, rtb\-sys |Enable, rtb\-sys |
   |Route learning |After enabling route learning, the TR route table automatically learns routes of the network instance, and generates entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (rtb\-sys) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01. That is, routes pointing to vpc01 are configured in rtb\-sys.</div><br> |Enable, rtb\-sys |Enable, rtb\-sys |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within the selected VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from rtb\-sys to all route tables within vpc01. These synchronized routes are system routes. That is, routes pointing to the TR are configured in the vpc01 route tables.</div><br> |Check |Check |
   

3. Follow the procedure in [Creating a DC Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc) to connect the DC Gateway to the TR instance. The route configuration is described in the table below.

   
   |Parameter |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |
   |---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on rtb\-sys.</div><br> |Enable, rtb\-sys |Enable, rtb\-sys |
   |Route learning |After enabling route learning, the TR route table will automatically learn routes of the network instance, and generate entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (rtb\-sys) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01. That is, routes pointing to vpc01 are configured in rtb\-sys.</div><br> |Enable, rtb\-sys |Enable, rtb\-sys |
   

4. Log in to the Elastic Compute Service (ECS) instance in the VPC, and execute the `ping` command to verify global interconnection between vpc01, vpc02, and the two on\-premises CIDR blocks.


<span id=".5q2l6aqk5LqM77ya5Yib5bu66Lev55Sx562W55Wl"></span>
### Step 2: Create a route policy


1. Follow the procedure in [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) to create an **outbound** route policy. The configuration of the policy entries is described in the table below.

   
   |Priority |Match conditions |Policy action |Description |
   |---|---|---|---|
   |1 |Source instance ID = VPC instance ID (vpc01)<br><br>Destination instance ID = VPC instance ID (vpc02) |Deny |Deny synchronizing routes from vpc01 to vpc02 so that vpc02 cannot access vpc01 |
   |2 |Source instance ID = VPC instance ID (vpc02)<br><br>Destination instance ID = VPC instance ID (vpc01) |Deny |Deny synchronizing routes from vpc02 to vpc01 so that vpc01 cannot access vpc02 |
   |3 |Route prefix = On\-premises CIDR block 2<br><br>Destination instance ID = VPC instance ID (vpc01) |Deny |Deny synchronizing routes from the on\-premises CIDR block 2 to vpc01, so that vpc01 cannot access this on\-premises CIDR block. |
   |4 |Route prefix = On\-premises CIDR block 1<br><br>Source instance ID = VPC instance ID (vpc02) |Deny |Deny synchronizing routes from on\-premises CIDR block 1 to vpc02, so that vpc02 cannot access the CIDR block 1 of the on\-premises data center. |
   

2. Associate the route policy to rtb\-sys based on [Associate route policy to TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table).


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to verify connectivity with vpc02, on\-premises CIDR block 1, and on\-premises CIDR block 2 in sequence.

   If vpc02 and the on\-premises CIDR block 2 are unreachable and the on\-premises CIDR block 1 is reachable, the expected isolation is met.

3. Similarly, log in to the ECS instance in vpc02 and execute the `ping` command to verify network isolation.
