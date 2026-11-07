---
title: "VPC interconnection (same account, cross-region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01"
---

This topic explains how to use Cloud Enterprise Network (CEN) to establish private network connectivity between same account, cross\-region Virtual Private Cloud (VPC) instances.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5fb6bfec6fdff5eb0a90b823d6c6aa9d.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:


1. Register account A and complete real name verification.

2. Recharge account.

3. Create [one VPC and subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [one Elastic Compute Service (ECS) instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) in China (Beijing) and China (Shanghai), respectively, with the following details:

   * VPC\-A (172.16.0.0/16), Subnet\-A (172.16.1.0/24), ECS\-A.

   * VPC\-B (192.168.0.0/16), Subnet\-B (192.168.1.0/24), ECS\-B.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure the CIDR blocks of the different VPC subnets are non\-overlapping and not identical. If it exists, the CEN automatically learns VPC routes and synchronizing the learned routes to the VPC may cause conflicts, resulting in the corresponding subnets being unable to communicate. In this case, see <a href="https://docs.byteplus.com/en/docs/natgateway/Resolving-address-conflicts-in-multiple-VPCs">Resolving Address Conflicts in Multi\-VPC Communication Scenarios</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following describes only the required parameters and their values. For other parameters not mentioned, retain the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65LqR5LyB5Lia572R"></span>
### Step 1: Create CEN


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click **Create CEN**.

4.  Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Set the name of CEN instance. |CEN\-X |
   |Attaching a network instance |Choose whether to enable the option to attach a network instance under the current account to the CEN instance. |Off |
   

5. Click **Create** to complete configuration.


<span id=".5q2l6aqk5LqM77ya5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 2: Attach Network Instance

You can refer to this procedure to sequentially load VPC\-A and VPC\-B into the CEN.


1. Click the CEN\-X.

2. On the **Network Instances** tab, click **Attach Network Instance**.

3. Configure the relevant information for the network instance to be attached.

   
   |Parameter |Explanation |Sample value for VPC\-A |Sample Value for VPC\-B |
   |---|---|---|---|
   |Account |Select the account to which the network instance to be attached belongs. |My account |My account |
   |Regions |Select the region where the instance to be attached resides. |China (Beijing) |China (Shanghai) |
   |Instance type |Select VPC type. |VPC |VPC |
   |Network Instances |Select the target VPC to be attached. |VPC\-A |VPC\-B |
   

4. Click **Attach** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5Z-f6Ze05bim5a69"></span>
### Step 3: Configure inter\-region bandwidth

You can refer to this operation to create a Bandwidth Package and allocate bandwidth for VPC communication between China (Beijing) and China (Shanghai).


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the left navigation pane, select **Bandwidth Package**.

3. Click **Create bandwidth package**.

4.  configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Billing method |Select the billing method for Bandwidth Package. |Subscription |
   |Name |Type a name for the bandwidth package. |package\-u5cy |
   |Cloud Enterprise Network |Select the target CEN instance to associate with. |CEN\-X |
   |Interoperability area |Select the local and peer regions that need to interconnect. |Chinese mainland \- Chinese mainland |
   |Bandwidth |Set the bandwidth value for the bandwidth package to be created. Valid range: 2 to 10,000. Unit: Mbps. |500 Mbps |
   |Duration |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. |Not selected |
   

5. Click **Confirm order** and consult the console instructions to review and confirm the legal agreements. Click **Buy now**.

6. In the left\-side navigation pane, click **CEN Instances**.

7. Click the CEN\-X.

8. On the **Inter\-region bandwidth** tab, click **Allocate inter\-region bandwidth**. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Bandwidth package |Select the bandwidth package for inter\-region bandwidth allocation. |package\-u5cy |
   |Interconnected regions |Select the local and peer regions that require interconnection. |China (Beijing) \- China (Shanghai) |
   |Bandwidth |Enter the bandwidth between the two regions to be interconnected. The value cannot exceed the allocatable bandwidth of the bandwidth package. |200Mbps |
   

9. Click **Allocate** to complete configuration.


<span id=".5q2l6aqk5Zub77ya5p-l55yL6Lev55Sx"></span>
### Step 4: View routes

View the route table of the CEN and confirm that it has successfully learned the subnet routes of the VPC.

View the VPC's route table to confirm it has successfully received the routes from the CEN.


<Tabs>
<Tab zoneid="tpqFPgn7Kq" title="View CEN route information">
<TabTitle>View CEN route information</TabTitle>

1. Click the CEN\-X.

2. On the **Route Table** tab, confirm the subnet routes automatically learned by the Cloud Enterprise Network (CEN).


</Tab>
<Tab zoneid="TTaIJ7nSFZ" title="View VPC-A route">
<TabTitle>View VPC-A route</TabTitle>

1. Click the name of VPC\-A.

2. Click **Route Table**.

3. Click the name of route table.

4. In the **Route Entry \> System route** tab, you can view the routes synchronized from the CEN to VPC\-A.





</Tab>
<Tab zoneid="JYtZb8IOVQ" title="View VPC-B route">
<TabTitle>View VPC-B route</TabTitle>

1. Click the name of VPC\-B.

2. Click **Route Table**.

3. Click the name of route table.

4. On the **Route Entry \> System Route** tab, you can view the routes synchronized from the CEN to VPC\-B.


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqU77ya5p-l55yLL-aUvumAmuWuieWFqOe7hA=="></span>
### Step 5: View and Release the security group

You can refer to this section to check whether the security groups associated with ECS\-A and ECS\-B allow the required traffic. If not allowed, allow the traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to the default outbound rules added by the security group, traffic for all networks (0.0.0.0/0), all ports, and all protocols are already allowed. Therefore, in this example, only the inbound rules are configured to allow traffic from ECS\-A to ECS\-B and from ECS\-B to ECS\-A.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A or ECS\-B

5. On the **Security Group** tab, you can view the current rule.

6. Click **Configure ** on the right side of the target security group.

7. On the **Inbound rule** tab, click **Add rule**. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |ECS\-A value |ECS\-B value |
   |---|---|---|---|
   |Priority |Priority of Security Group rules. |100 |100 |
   |Policy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, and ICMPv6 protocols. |ALL |ALL |
   |Port range |Limit the port range based on different protocol types. |ALL |ALL |
   |Source |Indicates that the network interfaces in this security group are allowed/denied access from resources at the source address. |192.168.1.0/24 |172.16.1.0/24 |
   

8. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5YWt77ya6aqM6K-B"></span>
### Step 6: Verification


1. Remotely log in to ECS\-A.

2. On the command line, execute `ping <IP address of ECS-B, using 192.168.1.22 as an example>` to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png) </span>

3. Similarly, verify that ECS\-B can access ECS\-A.
