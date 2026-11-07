---
title: "Deploying multiple Internet NAT Gateways in a single VPC."
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC"
---

When Elastic Compute Service (ECS) instances in different subnets of a Virtual Private Cloud (VPC) have different internet requirements, multiple NAT Gateways can be used to facilitate granular management of internet traffic. This topic describes how to deploy multiple Internet NAT Gateways within the same VPC.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

A company has three subnets within the same VPC. Subnet A​ is used for product development. Subnets B and C​ are used for product testing. Each subnet has different requirements for internet access. To enable granular management of internet traffic, the company uses two Internet NAT Gateways.

The VPC is named as VPC\-A, and its CIDR block is 172.16.1.0/16.


* The CIDR block of Subnet\-A is 172.16.1.0/24, and the IP address of ECS\-A is 172.16.1.11.

* The CIDR block of Subnet\-B is 172.16.2.0/24, and the IP address of ECS\-B is 172.16.2.22.

* The CIDR block of Subnet\-C is 172.16.3.0/24, and the IP address of ECS\-C is 172.16.3.33.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1700943622a77977cd6e6e0103fae40e.png) </span>


In the diagram above, Internet NAT Gateway\-A shows only one SNAT rule, and Internet NAT Gateway\-B shows only one SNAT rule and one DNAT rule. In practice, you can create multiple SNAT and DNAT rules as needed.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following steps based on the background information before proceeding:


1. Using your BytePlus account, create one VPC in the China (Beijing) region, with configurations matching the parameters described in the [Background](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC#.6IOM5pmv5LuL57uN) section above. For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create ECS\-A (172.16.1.11) in Subnet\-A of VPC\-A. Create ECS\-B (172.16.2.22) in Subnet\-B. Create ECS\-C (172.16.3.33) in Subnet\-C. None of the three ECSs are bound to an Elastic IP Address (EIP). For more information, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. Apply for 3 EIPs not bound to any cloud resources. This topic uses EIP\-A (180.XX.XX.11), EIP\-B (180.XX.XX.22), and EIP\-C (180.XX.XX.33). For procedure, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".6YWN572u6aaW5Liq5YWs572RTkFU572R5YWz"></span>
## Configure the first Internet NAT Gateway

<span id=".5q2l6aqk5LiA77ya5Yib5bu65YWs572RTkFU572R5YWz5bm257uR5a6a5YWs572RSVA="></span>
### Step 1: Create an Internet NAT Gateway and associate an EIP with it


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create NAT Gateway**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Regions |Select the region where the internet NAT Gateway is located. |China (Beijing) |
   |Name |Set a name for the Internet NAT Gateway. |Internet NAT Gateway\-A |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT Gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With Pay\-by\-CU, you don't need to select a specification. Performance scales dynamically based on demand, making it ideal for scenarios with significant traffic fluctuations.</div><br> |Pay\-by\-CU |
   |Specification |Select the specification of the Internet NAT Gateway. |Small |
   |VPC |Select a VPC. |VPC\-A\|172.16.1.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-A \| 172.16.1.0/24 |
   |Project |Select the project to which the Internet NAT Gateway belongs. |default |
   |Configuration mode |Select the configuration method of the Internet NAT Gateway. |Manual configuration |
   |Gateway mode |Select the mode of the Internet NAT Gateway according to your networking scenario. The mode of an Internet NAT Gateway cannot be changed after creation. Proceed with caution.<br><br><br>* Internet egress is an IPv4 Gateway: Select **Non\-passthrough mode.** <br><br>* Internet egress is an EIP: Select **Pass\-through mode.**  |Pass\-through mode |
   |Tags |Add one or more user tags to the Internet NAT Gateway as needed. |No tags added |
   

5. Click **Confirm order**.

6. Follow the console instructions to review and confirm the legal terms. Click **Buy now** to complete the creation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the creation failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf">Why did the Internet NAT Gateway creation fail</a>.   </div>
   

7. In the Internet NAT Gateway list, click **Configure EIP** to the right of the target gateway.

8. Click **Associate EIP**, select the pre\-prepared EIP\-A from the drop\-down menu, and click **OK** to complete the association.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6U05BVOinhOWImQ=="></span>
### Step 2: Create a SNAT rule


1. In the Internet NAT Gateway list, click the name of Internet NAT Gateway\-A.

2. Select the **SNAT rules** tab, then click **Create SNAT rule**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Set the name of the SNAT entry. |SNAT rule\-A |
   |Granularity |Select the granularity of the SNAT entry. |Subnet<br><br>Subnet\-A \| 172.16.1.0/24 |
   |EIP |Select the EIP associated with the Internet NAT Gateway. |180.XX.XX.11\|EIP\-A |
   

4. Click **OK** to complete the action.

5. Log in to the pre\-prepared ECS instance ECS\-A and execute `ping 8.8.8.8` in the command line.

6. If the ping is successful, ECS\-A can access the internet via the SNAT rule of the Internet NAT Gateway.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the ping failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/SNAT-entry-FAQ#.5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw==">Why cannot Elastic Compute Service instances configured with SNAT entries be accessed over the internet</a>.   </div>
   

<span id=".6YWN572u6Z2e6aaW5Liq5YWs572RTkFU572R5YWz"></span>
## Configure an additional Internet NAT Gateway

<span id=".5q2l6aqk5LiA77ya5Yib5bu65YWs572RTkFU572R5YWz5bm257uR5a6a5YWs572RSVA="></span>
### Step 1: Create an Internet NAT Gateway and associate an EIP with it


1. In the Internet NAT Gateway list, click **Create NAT Gateway**.

2. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Regions |Select the region where the internet NAT Gateway is located. |China (Beijing) |
   |Name |Set a name for the Internet NAT Gateway. |Internet NAT Gateway\-B |
   |Specification |Select the specification of the Internet NAT Gateway. |Small |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT Gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Pay\-as\-you\-go (Pay\-by\-CU) is currently in Beta stage and temporarily only supports accounts that have completed <a href="https://docs.byteplus.com/en/docs/6261/64937">Enterprise certification</a> to apply for trial. If you need a trial, please contact your account manager.</div><br> |Pay\-by\-Specification |
   |VPC |Select a VPC. |VPC\-A\|172.16.1.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-B \| 172.16.2.0/24 |
   |Project |Select the project to which the Internet NAT Gateway belongs. |default |
   |Configuration mode |Select the configuration method of the Internet NAT Gateway. |Manual configuration |
   |Tags |Add one or more user tags to the Internet NAT Gateway as needed. |No tags added |
   

3. Click **Confirm order**.

4. Follow the console instructions to review and confirm the legal terms. Click **Buy now** to complete the creation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the creation failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf">Why did the Internet NAT Gateway creation fail</a>.   </div>
   

5. In the Internet NAT Gateway list, click **Configure EIP** to the right of the target Internet NAT Gateway.

6. Click **Associate EIP**, select the prepared EIP\-B from the dropdown menu, and then click **OK** to complete the association.

7. Repeat Step 8 to bind the pre\-prepared EIP\-C.


<span id=".5q2l6aqk5LqM77ya6YWN572u6Lev55Sx"></span>
### Step 2: Configure route

For the first Internet NAT Gateway created in a VPC, the system automatically configures a route in the VPC route table. For additional Internet NAT Gateways, you need to manually configure their routes. You can follow this step to configure a route for an additional Internet NAT Gateway.

**Create a route table**


1. Log in to the [Route Table console](https://console.byteplus.com/vpc/routeTable). 

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**. In the left\-side navigation pane, click Route table to access the route table console.

3. Click **Create Route Table**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Enter the name of custom route table. |route\-X |
   |Virtual Private Cloud (VPC) |Select the VPC for the route table. |VPC\-A |
   

5. Click **Create** to complete configuration.


**Associate a subnet**


1. In the route table list, click **Associate subnet** to the right of the newly created custom route table.

2. Select Subnet\-B, then click **Associate** to complete the association.

3. Repeat Steps 1 and 2 to associate Subnet\-C. At this point, Subnet\-A is associated with the system route table, while Subnet\-B and Subnet\-C are associated with custom route tables.


**Add a route for the Internet NAT Gateway**


1. In the route table list, click the target custom route table name.

2. Select **Route entry \> Custom route** tab, and click **Add route**.

3. Add a custom route with a destination CIDR block of 0.0.0.0/0 and the Internet NAT Gateway\-B as the next hop.

4. Click **Add** to complete configuration.


Here, the route configuration for Internet NAT Gateway\-B is complete. The traffic of ECS instances without EIPs in Subnet\-B and Subnet\-C can be routed to Internet NAT Gateway\-B.

<span id=".5q2l6aqk5LiJ77ya5Yib5bu6U05BVOinhOWImQ=="></span>
### Step 3: Create SNAT rule


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the Internet NAT Gateway list, click the name of Internet NAT Gateway\-B.

4. Select the **SNAT rules** tab, then click **Create SNAT rule**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Set the name of the SNAT entry. |SNAT rule\-B |
   |Granularity |Select the granularity of the SNAT rule. |Subnet<br><br>Subnet\-B \| 172.16.2.0/24 |
   |EIP |Select the EIP associated with the Internet NAT Gateway. |180.XX.XX.22\|EIP\-B |
   

6. Click **OK** to complete the action.

7. Log in to the pre\-prepared ECS instance ECS\-B and execute `ping 8.8.8.8` in the command line.

   If the ping is successful, ECS\-B can access the internet via the SNAT rule of the Internet NAT Gateway.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the ping failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/SNAT-entry-FAQ#.5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw==">My ECS has a SNAT entry configured but is still not reachable from the Internet. Why​</a>.   </div>
   

<span id=".5q2l6aqk5Zub77ya5Yib5bu6RE5BVOinhOWImQ=="></span>
### Step 4: Create DNAT rule


1. In the Internet NAT Gateway list, click the name of Internet NAT Gateway\-B.

2. Select the **DNAT rules** tab, and click **Create DNAT rule**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Enter the name of the DNAT entry. |DNAT rule\-C |
   |Protocol |Select protocol type. Supported protocols include TCP, UDP. |TCP |
   |Private IP |Set the private IP address of the pre\-prepared ECS instance and the port or port range it uses to provide services to the public network. The port range is 1 to 65535. |172.16.3.33<br><br>22 |
   |EIP |Specify the EIP associated with the Internet NAT Gateway and select a port or a port range to receive requests from the internet. The value range is 1–65535. |180.XX.XX.33\|EIP\-C<br><br>80 |
   

4. Click **Create** to complete the action.

5. Open the command line on your local computer and enter `ssh <EIP address set in the DNAT rule> -p <EIP port set in the DNAT rule>`.

   If the login page appears, the pre\-prepared instance ECS\-C can provide remote login service to the internet through the DNAT rule of the Internet NAT Gateway.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you encounter issues during verification, see <a href="https://docs.byteplus.com/en/docs/natgateway/DNAT-entry-FAQ#.5bey6YWN572uRE5BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiiq-WFrOe9keiuv-mXru-8nw==">My ECS has a DNAT entry configured but is still not reachable from the Internet. Why​</a>.   </div>
