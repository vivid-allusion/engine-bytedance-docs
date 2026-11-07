---
title: "Sharing an Internet NAT Gateway across VPCs via CEN"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-VPCs-to-share-an-Internet-NAT-Gateway-using-CEN"
---

When multiple Virtual Private Clouds (VPCs) require Internet access, you can configure a single Internet NAT Gateway for these VPCs to conserve Elastic IP Address (EIP) resources and reduce enterprise costs. This topic describes how to use Cloud Enterprise Network (CEN) to enable multiple VPCs to share a single NAT Gateway for Internet access.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

A company has its development environment and testing environment deployed in two separate VPCs. The testing environment (VPC\-A) shares the Internet NAT Gateway of the development environment (VPC\-B).


* Testing Environment VPC (VPC\-A): CIDR block: 172.16.0.0/16; Subnet (Subnet\-A) CIDR block: 172.16.1.0/24; ECS (ECS\-A) IP Address: 172.16.1.11.

* Development Environment VPC (VPC\-B): CIDR block: 192.168.0.0/16; Subnet (Subnet\-B) CIDR block: 192.168.1.0/24; ECS (ECS\-B) IP Address: 192.168.1.22.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8ac024e76f52b7d63f91333b1eefdc86.png) </span>


The diagram above illustrates a single SNAT rule (all\-pass mode). In practice, you can create multiple SNAT and DNAT rules as needed.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following steps based on the background information before proceeding:


1. Use the same BytePlus account to create two VPCs in China (Beijing), with their parameters consistent with the background introduction. For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create ECS\-A (172.16.1.11) in Subnet\-A of VPC\-A, and create ECS\-B (192.168.1.22) in Subnet\-B of VPC\-B. Neither ECS should be bound to an EIP. For specific actions, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. Apply for 1 EIP not bound to any cloud resources. This topic uses EIP\-X (180.XX.XX.44). For specific actions, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5LqR5LyB5Lia572R"></span>
### Step 1: Configure CEN

Create a CEN instance, and attach both VPC\-A and VPC\-B to it to enable communication between VPC\-A and VPC\-B.

This topic uses VPC\-A and VPC\-B belonging to the same account and region as an example. For operational steps, see [VPC interconnection (same account and same region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01).

In actual usage, the following situations may exist:


* For multiple VPCs within the same account but in different regions, see [VPC interconnection (same account, cross-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01).

* For multiple VPCs under different accounts but in the same region, see [VPC interconnection (cross-account, same region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region).

* For multiple VPCs under different accounts and in different regions, see [VPC interconnection (cross-account and cross-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).


<span id=".5q2l6aqk5LqM77ya5Yib5bu65YWs572RTkFU572R5YWz"></span>
### Step 2: Create Internet NAT gateway

Through the following steps, you can create an Internet NAT Gateway in all\-pass mode within the VPC\-B.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create NAT gateway** to enter the creation page for an Internet NAT gateway.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Region |Select the region where the Internet NAT gateway is located. |China (Beijing) |
   |Name |Set a name for the Internet NAT gateway. |NAT\-X |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With Pay\-by\-CU, you don't need to specify a specification. Performance scales dynamically based on demand, making it ideal for scenarios with significant traffic fluctuations.</div><br> |Pay\-by\-Specification |
   |Specification |Select the specification of the Internet NAT gateway. |Small |
   |VPC |Select a VPC. |VPC\-B\|192.168.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-B \| 192.168.1.0/24 |
   |Project |Select the project to which the Internet NAT gateway belongs as needed. |default |
   |Configuration mode |When the billing method is **Pay\-as\-you\-go**, select the configuration method for the Internet NAT Gateway.<br><br><br>* Manual configuration: After creation, you must manually associate an EIP and configure SNAT or DNAT entries.<br><br>* Auto\-configure (all\-pass mode): Automatically creates a 0.0.0.0/0 SNAT rule. |Automatic configuration (all\-pass mode) |
   |Gateway mode |Select the mode of the Internet NAT Gateway according to your networking scenario. The mode of an Internet NAT Gateway cannot be changed after creation. Proceed with caution.<br><br><br>* Internet egress is an IPv4 Gateway: Select **Non\-passthrough mode.** <br><br>* Internet egress is an EIP: Select **Pass\-through mode.**  |Pass\-through mode |
   |EIP |When the configuration method is set to **Automatic configuration**, select an EIP from the drop\-down list |EIP\-X |
   |Tags |Add one or more user tags to the Internet NAT gateway as needed. |No tags added |
   

5. Click **Confirm order**.

6. Follow the console guidance to review and accept the legal terms, and click **Buy now** to complete the action.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the creation failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf">Why did the Internet NAT Gateway creation fail</a>.   </div>
   

<span id=".5q2l6aqk5LiJ77ya5omL5Yqo5Y-R5biD6Lev55Sx"></span>
### Step 3: Manually publish the route

You can follow the steps below to publish the route of the above Internet NAT gateway to the Cloud Enterprise Network (CEN).


1. Log in to the [Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the region and project of VPC\-B's route table. This example uses **China (Beijing)**  and **default**. In the left\-side navigation pane, click Route table to access the route table console.

3. In the route table list, click the name of the VPC\-B system route table to navigate to its details page.

4. Select the **Route entry \> Custom route** tab, and click **Publish** on the right side of the route entry where the next hop points to the Internet NAT gateway.

5. Click **Publish** to complete the propagation.

6. Verify whether the route was successfully published.

   1. Log in to the Cloud Enterprise Network console.

   2. Click the target CEN name to navigate to its details page.

   3. On the **Route Table** tab, view whether there is a route entry with the Destination CIDR of 0.0.0.0/0.


<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification


1. Log in to the pre\-prepared ECS instance ECS\-A (172.16.1.11) and execute `ping 8.8.8.8` in the command line.

2. If the `ping` is successful, it indicates that ECS\-A in VPC\-A can access the Internet via the SNAT rule of the Internet NAT Gateway.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>ping</code> fails, see <a href="https://docs.byteplus.com/en/docs/natgateway/SNAT-entry-FAQ#.5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw==">Why cannot Elastic Compute Service instances configured with SNAT entries be accessed over the Internet</a>.   </div>
