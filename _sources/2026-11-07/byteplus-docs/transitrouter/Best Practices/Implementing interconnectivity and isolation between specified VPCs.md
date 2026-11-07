---
title: "Implementing interconnectivity and isolation between specified VPCs"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-01"
---

This topic describes how to configure the Transit Router (TR) to meet the networking requirements for interconnectivity and isolation between multiple Virtual Private Clouds (VPCs).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

TR flexibly enables interconnectivity and isolation between multiple VPCs, whether they are in the same region or across different regions. You can implement network isolation by configuring route policies or using multiple TR route tables. This example uses a cross\-region scenario to demonstrate how to use the TR to achieve interconnectivity shown in the diagram below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To achieve interconnectivity and isolation between multiple VPCs in the same region, first complete TR route planning by seeing <a href="https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02">Route planning</a>, and then follow the configuration procedure described in <a href="https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02">Implementing private interconnectivity and isolation between different VPCs (same account, same region)</a>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e96532455ca0ddea271357ba0f56855.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created Elastic Compute Service (ECS) instances in all VPCs. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5pWw5o2u6KeE5YiS"></span>
### Data planning

Before configuration, plan the data parameters for VPCs and TRs in the diagram, as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8503e143d9c851218577429a7273895c.png) </span>


* VPC

   
   |Region |VPC |VPC CIDR block |Subnet name |Subnet availability zone |Subnet |ECS private IP |
   |---|---|---|---|---|---|---|
   |China (Guangzhou) |vpc01 |192.168.0.0/20 |subnet01 |Availability zone A |192.168.0.0/24 |192.168.0.10 |
   ||vpc03 |192.168.32.0/20 |subnet03 |Availability zone A |192.168.32.0/24 |192.168.32.10 |
   |China (Beijing) |vpc02 |192.168.16.0/20 |subnet02 |Availability zone A |192.168.16.0/24 |192.168.16.10 |
   ||vpc04 |192.168.48.0/20 |subnet04 |Availability zone A |192.168.48.0/24 |192.168.48.10 |
   

* Transit Router

   The route planning is illustrated above. For details, see [TR Route configuration planning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example only covers required parameters. Leave other parameters at their default values.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
#### Step 1: Configure a TR instance in China (Guangzhou)


1. Create a TR instance.

   Create a TR instance (named tr01) in China (Guangzhou). For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it to forward traffic from the inter\-region attachment. The following uses tr01's system route table (named <strong>tr01\-rtb\-sys</strong>) as an example.   </div>
   

2. Create a TR custom route table.

   Create two custom route tables for tr01 (**tr01\-rtb\-set1** and **tr01\-rtb\-set2**) to forward traffic from respective attachments (**attach\-vpc01** and **attach\-vpc03**). For procedure, see [Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03).

3. Create a VPC attachment.

   Create two attachments for tr01 to connect vpc01 and vpc03 separately. For procedure, see [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).

   * **Basic configuration**

      
      |Parameter |Description |Example<br><br>(attach\-vpc01) |Example<br><br>(attach\-vpc03) |
      |---|---|---|---|
      |Name |Type the name for the attachment. |attach\-vpc01 |attach\-vpc03 |
      |AZs and Subnets |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This example uses a single availability zone, so only one subnet is selected. We recommend using multiple availability zones for greater reliability in actual scenarios.</div><br> |Availability zone A A, subnet01 |Availability zone A, subnet03 |
      

   * **Route configuration**

      
      |Parameter |Description |Example<br><br>(attach\-vpc01) |Example<br><br>(attach\-vpc03) |
      |---|---|---|---|
      |Association forwarding |Enable association forwarding for both attach\-vpc01 and attach\-vpc03, and specify the route table that the TR uses to forward traffic from attach\-vpc01 and attach\-vpc03. |Enabled, tr01\-rtb\-set1 |Enabled, tr01\-rtb\-set2 |
      |Route learning |Enable route learning for both attach\-vpc01 and attach\-vpc03 to allow the specified TR route tables to automatically learn respective subnet routes of vpc01 and vpc03. |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-sys |
      |Auto Publish Route |Enable Auto Publish Route for both attach\-vpc01 and attach\-vpc03, automatically propagating routes in TR route tables (tr01\-rtb\-set1 and tr01\-rtb\-set2) associated with forwarding to respective VPCs (vpc01 and vpc03). |Check |Check |
      

4. View TR and VPC routes

   * The custom route tables (tr01\-rtb\-set1 and tr01\-rtb\-set2) contain no entries, while the routes in tr01\-rtb\-sys are listed below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |
      |---|---|---|---|---|---|
      |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
      |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |
      

   * In this example, since the vpc01 route table learns routes from the tr01\-rtb\-set1, and the vpc03 route table learns from tr01\-rtb\-set2, routes in the vpc01 and vpc03 route tables are unchanged.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
#### Step 2: Configure a TR instance in China (Beijing)


1. Create a TR instance.

   Create a TR instance (named tr02) in China (Beijing). For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the TR instance is created, the system automatically creates a system route table (to forward traffic from <strong>attach\-Inter\-region</strong>). Record the name of this system route table (tr02\-rtb\-sys). The following uses tr02\-rtb\-sys as an example.   </div>
   

2. Create a TR custom route table.

   Create two custom route tables for tr02 (tr02\-rtb\-set1 and tr02\-rtb\-set2) to forward traffic from respective attachments (**attach\-vpc02** and **attach\-vpc04**). For procedure, see [Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03).

3. Create a network instance attachment.

   Create two attachments for tr02 to connect vpc02 and vpc04 separately. For procedure, see [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).

   * **Basic configuration**

      
      |Parameter |Description |Example<br><br>(attach\-vpc02) |Example<br><br>(attach\-vpc04) |
      |---|---|---|---|
      |Name |Type the name for the attachment. |attach\-vpc02 |attach\-vpc04 |
      |AZs and Subnets |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This example uses a single availability zone, so only one subnet is selected. We recommend using multiple availability zones for greater reliability in actual scenarios.</div><br> |Availability zone A, subnet02 |Availability zone A, subnet04 |
      

   * **Route configuration**

      
      |Parameter |Description |Example<br><br>(attach\-vpc02) |Example<br><br>(attach\-vpc04) |
      |---|---|---|---|
      |Association forwarding |Enable association forwarding for both attach\-vpc02 and attach\-vpc04, and specify the route table that tr02 uses to forward traffic from attach\-vpc02 and attach\-vpc04. |Enabled, tr02\-rtb\-set1 |Enabled, tr02\-rtb\-set2 |
      |Route learning |Enable route learning for both attach\-vpc02 and attach\-vpc04 to allow the specified TR route tables to automatically learn respective subnet routes of vpc02 and vpc04. |Enabled, tr02\-rtb\-sys |Enabled, tr02\-rtb\-sys |
      |Auto Publish Route |Enable Auto Publish Route for both attach\-vpc02 and attach\-vpc04, automatically propagating routes in TR route tables (tr02\-rtb\-set1 and tr02\-rtb\-set2) associated with forwarding to respective VPCs (vpc02 and vpc04). |Check |Check |
      

4. View TR and VPC routes

   * The custom route tables (tr02\-rtb\-set1 and tr02\-rtb\-set2) contain no entries, while the routes in tr02\-rtb\-sys are listed below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |
      |---|---|---|---|---|---|
      |192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |
      |192.168.48.0/24 |attach\-vpc04 |Available |Route learning |VPC |vpc04 |
      

   * In this example, since the vpc02 route table learns routes from the tr02\-rtb\-set1, and the vpc04 route table learns from tr02\-rtb\-set2, entries in the vpc02 and vpc04 route tables are unchanged.


<span id=".5q2l6aqk5LiJ77ya6YWN572u6Leo5Zyw5Z-f5bim5a69"></span>
#### Step 3: Configure inter\-region bandwidth


1. Create a bandwidth package.

   Create a bandwidth package (named trbp01) to provide bandwidth resources for the inter\-region attachment. For procedure, see [Creating a TR bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01#.5pON5L2c5q2l6aqk).

2. Create an inter\-region attachment.

   Create an inter\-region attachment to link the TR instance in China (Guangzhou) and the TR instance in China (Beijing). For procedure, see [Creating an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-01#.5pON5L2c5q2l6aqk).

   This example uses the TR instance in China (Guangzhou), tr01, as Local TR to create an inter\-region attachment. Specific parameters are shown in the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |Type the name for the inter\-region attachment. |attach\-Inter\-region |
   |Bandwidth package |Add to the created bandwidth package (trbp01) and allocate bandwidth. |Checked, trbp01, 2 Mbps |
   |Local associated route table |Enable association forwarding, and specify that the local TR instance (tr01) uses tr01\-rtb\-sys to forward traffic from the inter\-region attachment. |Enabled, tr01\-rtb\-sys |
   |Remote TR association forwarding |Enable association forwarding, and specify the peer TR instance (tr02) uses tr02\-rtb\-sys to forward traffic from the inter\-region attachment. |Enabled, tr02\-rtb\-sys |
   |Local TR route learning |Enable route learning to allow the specified TR route table to automatically learn routes from the peer TR route table (tr02\-rtb\-sys) associated with forwarding. |tr01\-rtb\-set2 |
   |Remote TR route learning |Enable route learning to allow the specified TR route table to automatically learn routes from the local TR route table (tr01\-rtb\-sys) associated with forwarding. |tr02\-rtb\-set1 |
   

3. Configure a TR route pointing to the inter\-region attachment.

   Add the static route pointing to the inter\-region attachment to respective custom route tables (tr01\-rtb\-set1 and tr02\-rtb\-set2). Specific routes are listed in the table below. For procedure, see [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx).

   * **Route table (tr01\-rtb\-set1)** 

      
      |Parameter |Route name |Destination CIDR |Black hole routing |Next Hop type |Next Hop |
      |---|---|---|---|---|---|
      |1 |Routing traffic to vpc02 |192.168.16.0/20 |No |Inter\-region attachment |attach\-Inter\-region |
      

   * **Route table (tr02\-rtb\-set2)** 

      
      |Parameter |Route name |Destination CIDR |Black hole routing |Next Hop type |Next Hop |
      |---|---|---|---|---|---|
      |1 |Forwarding traffic to vpc03 |192.168.32.0/20 |No |Inter\-region attachment |attach\-Inter\-region |
      

4. View TR and VPC routes

   * The routes in tr01\-rtb\-set1 and tr01\-rtb\-set2 are listed in the following table.

      
      |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |
      |---|---|---|---|---|---|---|
      |tr01\-rtb\-set1 |192.168.16.0/20 |attach\-Inter\-region |Available |Static |TR |tr02 |
      |tr01\-rtb\-set2 |192.168.16.0/20 |attach\-Inter\-region |Available |Route learning |TR |tr02 |
      ||192.168.48.0/20 |attach\-Inter\-region |Available |Route learning |TR |tr02 |
      

   * The routes in tr02\-rtb\-set1 and tr02\-rtb\-set2 are listed in the following table.

      
      |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |
      |---|---|---|---|---|---|---|
      |tr02\-rtb\-set1 |192.168.0.0/20 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
      ||192.168.32.0/20 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
      |tr02\-rtb\-set2 |192.168.32.0/20 |attach\-Inter\-region |Available |Static |TR |tr01 |
      

   * In this example, the VPC route tables learn routes from respective tr route tables: vpc01 from tr01\-rtb\-set1, vpc03 from tr01\-rtb\-set2, vpc02 from tr02\-rtb\-set1, and vpc04 from tr02\-rtb\-set2. The routes in each VPC route table are listed in the following table.

      
      |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
      |---|---|---|---|---|
      |vpc01 |192.168.16.0/20 |Available |TR |tr01 |
      ||192.168.0.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      |vpc03 |192.168.48.0/20 |Available |TR |tr01 |
      ||192.168.16.0/20 |Available |TR |tr01 |
      ||192.168.32.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      |vpc02 |192.168.32.0/20 |Available |TR |tr02 |
      ||192.168.0.0/20 |Available |TR |tr02 |
      ||192.168.16.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      |vpc04 |192.168.32.0/20 |Available |TR |tr02 |
      ||192.168.48.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      


<span id=".5q2l6aqk5Zub77ya6YWN572uVlBD6Ieq5a6a5LmJ6Lev55Sx77yI5Y-v6YCJ77yJ"></span>
#### Step 4: Configure a VPC custom route (optional)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In this example, this step is not required since Auto Publish Route is enabled when creating the attachment in Step 1 and Step 2.</div>


* <div data-tips="true" data-tips-type="warning">If you do not enable Auto Publish Route at creation, follow the steps below to configure a custom route for respective VPCs.</div>


1. Click the instance name in the **Name/ID** column.

2. In the **Associated resources** section, click the digit to the right of **VPC resource \> Route Table**.

3. Click the target route table name.

4. In the section below Basic information, select the **Route Entry \> Custom route** tab.

5. Click **Add route**, and configure the route based on the table below.

   * Route configuration for vpc01

      
      |No. |Destination CIDR |Next Hop type |Next Hop |
      |---|---|---|---|
      |1 |192.168.16.0/20 |TR |tr01 |
      

   * Route configuration for vpc02

      
      |No. |Destination CIDR |Next Hop type |Next Hop |
      |---|---|---|---|
      |1 |192.168.0.0/20 |TR |tr02 |
      |2 |192.168.32.0/20 |TR |tr02 |
      

   * Route configuration for vpc03

      
      |No. |Destination CIDR |Next Hop type |Next Hop |
      |---|---|---|---|
      |1 |192.168.16.0/20 |TR |tr01 |
      |2 |192.168.48.0/20 |TR |tr01 |
      

   * Route configuration for vpc04

      
      |No. |Destination CIDR |Next Hop type |Next Hop |
      |---|---|---|---|
      |1 |192.168.32.0/20 |TR |tr02 |
      

6. Click **Create** to complete configuration.

7. Review the custom routes in each VPC route table as shown in the table below.

   
   |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
   |---|---|---|---|---|
   |vpc01 |192.168.16.0/20 |Available |TR |tr01 |
   |vpc02 |192.168.32.0/20 |Available |TR |tr02 |
   ||192.168.0.0/20 |Available |TR |tr02 |
   |vpc03 |192.168.48.0/20 |Available |TR |tr01 |
   ||192.168.16.0/20 |Available |TR |tr01 |
   |vpc04 |192.168.32.0/20 |Available |TR |tr02 |
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect to respective servers in vpc02, vpc03 and vpc04, verifying that vpc01 communicates with vpc02, but not with vpc03 or vpc04.

3. Similarly, log in to respective ECS instances in vpc02, vpc03 and vpc04, and execute the `ping` command to connect other ECS instances, verifying interconnectivity and isolation between VPCs.

   * vpc02 communicates with vpc01 and vpc03, but not with vpc04.

   * vpc03 communicates with vpc02 and vpc04, but not with vpc01.

   * vpc04 communicates with vpc03, but not with vpc01 or vpc02.
