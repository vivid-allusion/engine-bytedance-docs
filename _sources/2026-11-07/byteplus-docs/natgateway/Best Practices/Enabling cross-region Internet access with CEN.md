---
title: "Enabling cross-region Internet access with CEN"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Enabling_cross-region_Internet_access_with_CEN"
---

When enterprise servers access services in other regions, internet requests may experience latency as they traverse multiple ISP networks. To mitigate this, Cloud Enterprise Network (CEN) can be used to allow enterprise servers to access through the nearest BytePlus point of presence. Requests are then routed through its accelerated network to the region closest to the target service before being transmitted over the internet. This reduces the number of ISP network hops and achieves internet acceleration.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcf24d3a756bc53d29172f503ceca308.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

This topic uses the scenario of resources in Region A accessing services in Region B as an example. Before you begin, complete the following preparations:


1. If Region A and Region B are not in the [same region](https://docs.byteplus.com/en/docs/cen/Product-Overview-05), you need to [submit a cross-border application](https://docs.byteplus.com/en/docs/6405/79179), which must be approved by the line operator.

2. [Create one VPC and subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) in each Region A and Region B. [Create an ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) instance in the VPC of Region A, with the following information:

   * VPC\-A (172.16.0.0/16), Subnet\-A (172.16.1.0/24), ECS\-A.

   * VPC\-B (192.168.0.0/16), Subnet\-B (192.168.1.0/24).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure the CIDR blocks of the different VPC subnets are non\-overlapping and not identical. If overlapping exists, it will cause route conflicts in the CEN, preventing these subnets from communicating with each other. For example, if the CIDR blocks of Subnet\-A and Subnet\-B in the diagram overlap or are identical, they will be unable to communicate. In this case, the ECS in Subnet\-A will not be able to access the internet through the Internet NAT gateway created in Subnet\-B. For details, see <a href="https://docs.byteplus.com/en/docs/cen/Route-entries-01#.5Yay56qB5Y-K5Yy56YWN6K-05piO">Route overview</a>.   </div>
   

3. [Apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP) in region B.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5pCt5bu65Z-656GA546v5aKD"></span>
### Step 1: Set up the basic environment


|Resources requiring cross\-border internet acceleration |Description |
|---|---|
|On\-premises IDC and VPC\-A |To achieve connectivity between VPC\-A and your on\-premises IDC, follow the steps in [Direct Connect Quick start](https://docs.byteplus.com/en/docs/directconnect/Quick-start). |
|VPC\-A only |You need to [create CEN](https://docs.byteplus.com/en/docs/cen/CEN-instances-01) and [install VPC-A](https://docs.byteplus.com/en/docs/cen/Network-instances-01). |


<span id=".5q2l6aqk5LqM77ya5Yqg6L29VlBD"></span>
### Step 2: Install VPC


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top menu bar, select the target project.

3. Click the target CEN instance name.

4. On the **Network Instances** tab, click **Attach Network Instance**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example Value |
   |---|---|---|
   |Account |Select the account. |My account |
   |Region |Select the region. |Region B |
   |Instance type |Select the instance type. |Virtual Private Cloud (VPC) |
   |Network Instances |Select the target VPC to be attached. |VPC\-B |
   

6. Click **Attach** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5Z-f6Ze05bim5a69"></span>
### Step 3: Configure inter\-region bandwidth

You can follow the steps below to create a bandwidth package and allocate bandwidth between Region A and Region B.


1. Log in to the [Bandwidth Package console](https://console.byteplus.com/cen/cenBandwidthPackage).

2. Click **Create Bandwidth Package**. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Select the billing method for the bandwidth package. |Subscription |
   |Name |Type a name for the bandwidth package. |package\-x |
   |CEN |Select the target CEN instance to associate with. |CEN\-X |
   |Interoperability area |Select the local and peer regions that need to interconnect. |Chinese mainland \- Asia Pacific |
   |Bandwidth |Set the bandwidth value for the bandwidth package to be created. Valid range: 2 to 10,000. Unit: Mbps. |500 Mbps |
   |Duration |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. |Not selected |
   

3. Click **Confirm order** and consult the console instructions to review and confirm the legal agreements. Click **Buy now**.

4. In the left\-side navigation pane, click **CEN Instances**.

5. Click the target CEN instance name.

6. On the **Inter\-region bandwidth** tab, click **Allocate inter\-region bandwidth**. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example Value |
   |---|---|---|
   |Bandwidth package |Select the bandwidth package for inter\-region bandwidth allocation. |package\-x |
   |Interconnected regions |Select the local and peer regions that require interconnection. |Region A – Region B |
   |Bandwidth |Enter the bandwidth between the two regions to be interconnected. The value cannot exceed the allocatable bandwidth of the bandwidth package. |200Mbps |
   

7. Click **Create** to complete configuration.


<span id=".5q2l6aqk5Zub77ya5p-l55yLL-aUvumAmuWuieWFqOe7hA=="></span>
### Step 4: View or allow security groups

You can refer to this section to check whether the security group associated with Elastic Compute Service (ECS) instance A allows outbound traffic to overseas services. If not allowed, allow the traffic.


1. Log in to [the ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A.

5. On the **Security Group** tab, you can view the current rule.

6. Click **Configure** on the right side of the target security group.

7. On the **Outbound rule** tab, click **Add rule**. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example Value |
   |---|---|---|
   |Priority |Priority of security group rules |100 |
   |Strategy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, and ICMPv6 protocols. |ALL |
   |Port range |Limit the port range based on different protocol types. |ALL |
   |Destination address |Indicates that network interfaces in this security group are allowed/denied to actively access resources at the destination address. |0.0.0.0/0 |
   

8. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5LqU77ya6YWN572u5YWs572RTkFU572R5YWz"></span>
### Step 5: Configure an Internet NAT gateway

You can refer to this section to create an internet NAT gateway in all\-pass mode within VPC\-B.


1. Log in to the [Internet NAT gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the target region and project. In this example, select **Region B** and **default**.

3. Click **Create NAT Gateway**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Region |Select the region where the internet NAT gateway is located. |Region B |
   |Name |Set a name for the Internet NAT gateway. |NAT\-X |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With Pay\-by\-CU, you don't need to specify a specification. Performance scales dynamically based on demand, making it ideal for scenarios with significant traffic fluctuations.</div><br> |Pay\-by\-Specification |
   |Specification |Select the specification of the Internet NAT gateway. |Small |
   |Virtual Private Cloud (VPC) |Select a VPC. |VPC\-B\|192.168.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-B \| 192.168.1.0/24 |
   |Project |Select the project to which the internet NAT gateway belongs as needed. |default |
   |Configuration mode |When the billing method is **Pay\-as\-you\-go**, select the configuration method for the Internet NAT Gateway.<br><br><br>* Manual configuration: After creation, you must manually associate an EIP and configure SNAT or DNAT entries.<br><br>* Auto\-configure (all\-pass mode): Automatically creates a 0.0.0.0/0 SNAT rule. |Automatic configuration (all\-pass mode) |
   |Gateway mode |Select the mode of the Internet NAT Gateway based on your networking scenario. The mode of an Internet NAT Gateway cannot be changed after creation, so proceed with caution.<br><br><br>* Internet egress is an IPv4 Gateway: Select **Non\-passthrough mode.** <br><br>* Internet egress is an EIP: Select **Pass\-through mode.**  |Pass\-through mode |
   |EIP |When the configuration method is set to **Automatic configuration**, select a prepared EIP from the drop\-down list |EIP\-X |
   |Tags |Add one or more user tags to the Internet NAT gateway as needed. |No tags added |
   

5. Click **Confirm order**.

6. Follow the console guidance to review and accept Legal, and click **Buy now** to complete the operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the creation failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf">Why did the Internet NAT Gateway creation fail</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Services outside the mainland can also access resources in your on\-premises IDC or mainland VPCs via the DNAT rules of the NAT gateway. This topic does not configure DNAT rules. If required, see <a href="https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules#.5Yib5bu6RE5BVOinhOWImQ==">Create a DNAT rule</a>.   </div>
   


<span id=".5q2l6aqk5YWt77ya5Y-R5biD5YWs572RTkFU572R5YWz6Lev55Sx"></span>
### Step 6: Publish the Internet NAT gateway route

You can follow the steps below to publish the route of the above Internet NAT gateway to the Cloud Enterprise Network (CEN).


1. Log in to the [Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the region and project of VPC\-B's route table. In this example, they are **Region B** and **default**.

3. In the route table list, click the name of VPC\-B's system route table.

4. On the **Route Entry \> Custom route** tab, click **Publish** to the right of the route entry whose next hop points to the Internet NAT gateway.

5. Click **Publish** to complete the publication.

6. Verify whether the route was successfully published.

   1. Log in to the Cloud Enterprise Network console.

   2. Click the target CEN name.

   3. On the **Route Table** tab, view whether there is a route entry with the Destination CIDR Block of 0.0.0.0/0.


<span id=".5q2l6aqk5LiD77ya6aqM6K-B"></span>
### Step 7: Verification

<span id=".6aqM6K-B5LqR5LiKVlBD"></span>
#### Validate VPC Connectivity


1. Remotely log in to ECS\-A.

2. Run command `ping 8.8.8.8` to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9330212f3d9e5d8153020d3d39f9d44.png) </span>

   A successful `ping` response confirms that ECS\-A in VPC\-A can access the internet through the Internet NAT gateway in Region B.


<span id=".6aqM6K-B5pys5ZywSURD"></span>
#### Validate on\-premises data center


1. Remotely log in to server A.

2. Run command `ping 8.8.8.8` to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eafd836d96150c993b663b3e4b505a21.png) </span>

   A successful `ping` indicates that servers in the on\-premises IDC can access the internet through the internet NAT gateway in Region B.
