---
title: "Implementing private interconnectivity and isolation between different VPCs (same account, cross-region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03"
---

This section describes how to use Transit Routers (TRs) for cross\-region VPC interconnectivity under the same account. Specifically, it covers connecting two VPCs (vpc01 and vpc02) in one region to another VPC (vpc03) in a different region. After the connection is complete, vpc01 and vpc02 can both communicate with vpc03 via the TR. However, vpc01 and vpc02 cannot communicate with each other, as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63a751358b708861afc272af284b2dfe.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created three Virtual Private Clouds (VPCs) and their subnets. For procedure, see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure that neither VPC contains conflicting subnets. That is, no duplicate or overlapping CIDR blocks exist.   </div>
   

* You have created Elastic Compute Service (ECS) instances in the three VPCs. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".6Lev55Sx6KeE5YiS"></span>
## Routing planning

In a single TR instance, multiple network instances with the identical access destination can use the same TR route table to forward traffic.


* Within China (Guangzhou): Since both vpc01 and vpc02 only need to access vpc03, their traffic can share a single TR route table. However, the inter\-region attachment requires access to distinct destinations (both vpc01 and vpc02). Therefore, a separate TR route table is required to handle this traffic.

* Within China (Beijing): vpc03 and the inter\-region attachment require access to the same destinations (both vpc01 and vpc02). So only one TR route table is required.


In summary, at least three TR route tables are required to enable connectivity and isolation between different VPCs. The following figure illustrates the specific route planning.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95708d4bd257af5c5d1119e7d6e03f16.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Routes in the VPC route tables illustrated above can be manually configured or automatically synchronized. This example uses auto publishing. </div>


<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures


1. [Configure a TR instance in China (Guangzhou)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03#.5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L): Create the instance and attachments that connect to vpc01 and vpc02 respectively.

   1. **Create a TR instance**: Create a TR instance in China (Guangzhou).

   2. **Create a TR custom route table**: Create a custom route table for the TR instance to receive and forward network traffic along with the TR system route table.

   3. **Create a network instance attachment and configure routing**: Create two network instance attachments on the TR instance to connect the two VPCs in this region. On the TR side, configure association forwarding and route learning to control the traffic flow to and from these VPCs. On the VPC side, configure auto publishing to control flow direction.

   4. **View TR and VPC routes**: Check that the routes of the TR instance and two VPCs in the same region meet expectations.

2. [Configure a TR instance in China (Beijing)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03#.5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L): Create a TR instance and create an attachment for vpc03.

   1. **Create a TR instance**: Create a TR instance in China (Beijing).

   2. **Create an attachment and configure routing**: Create an attachment on the TR instance to connect the VPC in this region. On the TR side, configure association forwarding and route learning to control the traffic flow to and from the VPC. On the VPC side, configure auto publishing to control flow direction.

   3. **View TR and VPC routes**: Check that the routes of the TR instance and two VPCs in the same region meet expectations.

3. [Configure inter-region bandwidth](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03#.5q2l6aqk5LiJ77ya6YWN572u6Leo5Zyw5Z-f5bim5a69): Create an inter\-region attachment to connect TR instances between regions.

   1. **Create a bandwidth package**: Create a bandwidth package to provide bandwidth resources for the inter\-region attachment.

   2. **Create an inter\-region attachment and configure routing**: Create an inter\-region attachment to connect the TR instances in the two regions above. Allocate bandwidth for the attachment. Configure association forwarding and route learning to implement route propagation between the two TR instances.

   3. **View TR and VPC routes**: Check that the routes of two TR instances and three VPCs in two regions meet expectations.

4. [Verification](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03#.57uT5p6c6aqM6K-B): Run `ping` to verify the connectivity between ECS instances in different VPCs to ensure that the VPCs are connected and isolated as expected.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 1: Configure a TR instance in China (Guangzhou)

<span id=".5LiA44CB5Yib5bu6VFLlrp7kvos="></span>
#### I. Create a TR instance


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. In the top menu bar, select the target project and region.

3. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Guangzhou) |
   |Name |Type in a name for the TR instance. |tr01 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br>In this example, TR instances in different regions should be assigned different ASNs.<br><br>After being assigned an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published to other network instances. |64512 |
   |Multicast |Specify whether to enable multicast for the TR. [Prerequisite](https://docs.byteplus.com/en/docs/transitrouter/Multicast-Overview) |Do not enable |
   |Related project |Select the project to which the TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

4. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table: rtb\-sys. The following uses tr01\-rtb\-sys as an example.   </div>
   

<span id=".5LqM44CB5Yib5bu6VFLoh6rlrprkuYnot6_nlLHooag="></span>
#### II. Create a TR custom route table


1. Click the name of the created TR instance.

2. In the zone below **Basic information**, select the **Route Table** tab.

3. Click **Create** to the right of the Route Table List, and type in tr01\-rtb\-set as the route table name.

4. Click **Create** to complete the creation of the TR route table.


<span id=".5LiJ44CB5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
#### Ⅲ. Create a network instance attachment and configure routing

Create two network instance attachments to connect to vpc01 and vpc02 separately by the following steps.


1. In the section below **Basic information**, select the **Intra\-region attachment** tab.

2. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |**Basic information** ||||
   |Transit Router |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |tr01 |
   |Regions |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |China (Guangzhou) |
   |Name |The name for the network instance attachment to be created. |attach\-vpc01 |attach\-vpc02 |
   |**Network instances** ||||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |
   |**Attachment point configuration** ||||
   |AZs and Subnets |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |China (Guangzhou) A, subnet01 |Availability Zone A, subnet02 |
   

3. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. The TR forwards traffic from vpc01 based on tr01\-rtb\-sys.</div><br> |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-sys |
   |Route learning |The selected TR route table automatically learns the routes of the network instance and generates routes whose next hop is the corresponding network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (tr01\-rtb\-set) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01.</div><br> |Enabled, tr01\-rtb\-set |Enabled, tr01\-rtb\-set |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the TR route table associated with this network instance attachment to all route tables within the VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from tr01\-rtb\-sys to all route tables within vpc01. These synchronized routes are system routes.</div><br> |Check |Check |
   

4. Click **Buy now** to complete the action.


<span id=".5Zub44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### IV. View TR and VPC routes


1. View routes of TR route tables (tr01\-rtb\-sys and tr01\-rtb\-set) in sequence.

   * Currently, no routes exist in tr01\-rtb\-sys.

   * The routes in tr01\-rtb\-set are listed in the following table.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |network instance |
      |---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |
      |192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |
      

2. View routes of the vpc01 and vpc02 route tables in sequence to confirm no changes.

   Since the routes in tr01\-rtb\-sys are automatically published to the vpc01 and vpc02 route tables, routes in the vpc01 and vpc02 route tables are unchanged.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 2: Configure a TR instance in China (Beijing)

<span id=".5LiA44CB5Yib5bu6VFLlrp7kvos="></span>
#### I. Create a TR instance


1. Back to the TR Instances page, and select the target project and region in the top menu bar.

2. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Beijing) |
   |Name |Type in a name for the TR instance. |tr02 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br><br>* When networking within the same region, you can assign any ASN from the specified range for the TR instance.<br><br>* When networking across regions, you must assign different ASNs for TR instances in different regions.<br><br>* When connecting on\-premises data centers via a TR and a Direct Connect (DC), the ASNs for the TR and the DC Gateway must be unique.<br><br>* When connecting a single TR instance to multiple DC Gateways to access different data centers, the ASNs for these DC Gateways must also be unique.<br><br><br>After being assigned an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published from it to other network instances. |64513 |
   |Multicast |Specify whether to enable multicast for the TR. [Prerequisite](https://docs.byteplus.com/en/docs/transitrouter/Multicast-Overview) |Do not enable |
   |Related project |Select the project to which the TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

3. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table: rtb\-sys. The following uses tr02\-rtb\-sys as an example.   </div>
   

<span id=".5LqM44CB5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
#### Ⅱ. Create an attachment and configure routing


1. Click the name of the created TR instance.

2. In the section below **Basic information**, select the **Intra\-region attachment** tab.

3. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc03) |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr02 |
   |Region |Defaults to the same region as the TR instance. No manual configuration is required. |China (Beijing) |
   |Name |The name for the network instance attachment to be created. |attach\-vpc03 |
   |**Network instances** |||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |
   |VPC |Select the VPC instance to be connected. |vpc03 |
   |**Attachment point configuration** |||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability Zone A, subnet03 |
   

4. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc03) |
   |---|---|---|
   |Association forwarding |The TR forwards traffic from vpc03 based on the route table (tr02\-rtb\-sys) associated with this network instance attachment.<br><br>At this point, the TR route table contains no routes and only has specified traffic forwarding sources. To actually enable traffic forwarding, configure destinations for the TR route table via route learning or static routes. |Enabled, tr02\-rtb\-sys |
   |Route learning |The selected TR route table (tr02\-rtb\-sys) automatically learns the routes of vpc03, and generates entries with the destination as vpc03 subnets and the next hop as attach\-vpc03. |Enabled, tr02\-rtb\-sys |
   |Auto Publish Route |After enabling auto publishing, the system automatically synchronizes the routes from tr02\-rtb\-sys to all route tables within vpc03. These synchronized routes are system routes. |Check |
   

5. Click **Buy now** to complete the action.


<span id=".5LiJ44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### Ⅲ. View TR and VPC routes


1. View routes in tr02\-rtb\-sys, as shown in the table below.

   
   |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |
   |---|---|---|---|---|---|
   |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
   

2. View the routes in the vpc03 route table to confirm no changes.

   Since the routes in tr02\-rtb\-sys are automatically published to the vpc03 route table and this TR route table contains no routes whose Next Hop is not vpc03, routes in the vpc03 route table are unchanged.


<span id=".5q2l6aqk5LiJ77ya6YWN572u6Leo5Zyw5Z-f5bim5a69"></span>
### Step 3: Configure inter\-region bandwidth

<span id=".5LiA44CB5Yib5bu65bim5a695YyF"></span>
#### I. Create a bandwidth package


1. In the left\-side navigation pane, select **Bandwidth Package**.

2. Click **Create bandwidth package**, and configure the bandwidth package based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method for the bandwidth package to be created. Default: Subscription. |Subscription |
   |Name |Type the name for the bandwidth package to be created. |trbp01 |
   |**Bandwidth configuration** |||
   |Interoperability area |The bandwidth package requires interoperable local and peer areas. |China Mainland \- China Mainland |
   |Bandwidth |Specify a bandwidth cap for the bandwidth package. Valid range: 2 to 10,000. Unit: Mbps. |2Mbps |
   |Duration |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. |Not selected |
   |**More information** |||
   |Project |Specify the project to which the bandwidth package belongs. |default |
   

3. In the right\-side Configuration details section, follow the console guidance to review and accept the Legal.

4. Click **Submit order** to complete the action.


<span id=".5LqM44CB5Yib5bu66Leo5Zyw5Z-f6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
#### II. Create an inter\-region attachment and configure routing


1. In the top menu bar, select the target project and region. The following example is a default project in China (Guangzhou).

2. In the left\-side navigation pane, select **Transit Router** and click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click **Create inter\-region attachment** and configure basic information based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |
   |Name |The name for the inter\-region attachment to be created. |attach\-Inter\-region |
   |**Network instances** |||
   |Attachment type |Inter\-region attachments only support TR instances. |Transit Router |
   |Peer region |Regions that require cross\-region connectivity. |China (Beijing) |
   |Instance |Select the TR instance in the peer region based on the project. |tr02 |
   |Bandwidth package |Specify whether to allocate bandwidth for the inter\-region attachment. If **Add Bandwidth Package** is checked, select the bandwidth package based on the project and set bandwidth size. |Checked, trbp01, 2 Mbps |
   

5. Configure route information for the inter\-region attachment based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Local associated route table |The TR forwards traffic from this inter\-region attachment based on the associated route table (tr01\-rtb\-sys).<br><br>Next, you need to configure the destination for this TR route table. |Enabled, tr01\-rtb\-set |
   |Remote TR association forwarding |The TR forwards traffic from this inter\-region attachment based on the associated route table (tr02\-rtb\-sys).<br><br>Next, you need to configure the destination for this TR route table. |Enabled, tr02\-rtb\-sys |
   |Local TR route learning |Enabling Local TR route learning means the specified Local TR route table will automatically learn the routes of Remote TR, and generate entries with the next hop setting as the inter\-region attachment. |Enabled, tr01\-rtb\-sys |
   |Remote TR route learning |Enabling Remote TR route learning means the specified Remote TR route table will automatically learn the routes of Local TR, and generate entries with the next hop setting as the inter\-region attachment. |Enabled, tr02\-rtb\-sys |
   

6. Click **Create** to complete the action.


<span id=".5LiJ44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### Ⅲ. View TR and VPC routes


1. View routes in TR route tables (tr01\-rtb\-sys and tr02\-rtb\-sys) in sequence, as shown in the table below.

   
   |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |
   |---|---|---|---|---|---|---|
   |tr01\-rtb\-sys |192.168.32.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr02 |
   |tr02\-rtb\-sys |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
   ||192.168.0.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
   ||192.168.16.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
   

2. View routes in the vpc01, vpc02 and vpc03 route tables in sequence, as shown in the table below.

   
   |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
   |---|---|---|---|---|
   |vpc01 |192.168.32.0/24 |Available |TR |tr01 |
   ||192.168.0.0/24 |Available |InnerSubnet |System default |
   ||100.64.0.0/10 |Available |System |System default |
   |vpc02 |192.168.32.0/24 |Available |TR |tr01 |
   ||192.168.16.0/24 |Available |InnerSubnet |System default |
   ||100.64.0.0/10 |Available |System |System default |
   |vpc03 |192.168.0.0/24 |Available |TR |tr02 |
   ||192.168.16.0/24 |Available |TR |tr02 |
   ||192.168.32.0/24 |Available |InnerSubnet |System default |
   ||100.64.0.0/10 |Available |System |System default |
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

The following verification steps take a Linux\-based ECS as an example:


1. Remotely log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `ping` command to connect the private IP addresses of respective ECS instances in vpc02 and vpc03, verifying network connectivity.

   * The ECS instances in vpc01 and vpc02 are mutually isolated and cannot ping each other.

   * The ECS instances in vpc01 and vpc03 can mutually communicate and can ping successfully.

3. Similarly, remotely log in to the ECS instances in vpc02 and vpc03 to verify connectivity between vpc02, vpc03, and another VPC.
