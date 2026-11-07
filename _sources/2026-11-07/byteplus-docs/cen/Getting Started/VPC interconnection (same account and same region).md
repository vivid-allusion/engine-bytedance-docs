---
title: "VPC interconnection (same account and same region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01"
---

This topic explains how to use Cloud Enterprise Network (CEN) to establish private network connectivity between same account, same region Virtual Private Cloud (VPC) instances.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7333187f83c6040bd1f31f76784190b7.png) </span>

&nbsp;

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:


1. Register account A and complete real name verification.

2. Recharge account.

3. In China (Beijing) region, [Create 2 VPCs with their subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Create 2 ECSs](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). The required information is as follows:

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
   |Name |Enter the name of CEN instance. |CEN\-X |
   |Attaching a network instance |Choose whether to enable the option to attach a network instance under the current account to the CEN instance. |Off |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5LqM77ya5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 2: Attach Network Instance

You can perform the following operations to attach VPC\-A and VPC\-B to the CEN in sequence.


1. Click the CEN\-X.

2. On the **Network Instances** tab, click **Attach Network Instance**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |Sample value |
   |---|---|---|---|
   |Account |Select account. |My account |My account |
   |Regions |Select region. |China (Beijing) |China (Beijing) |
   |Instance type |Select the instance type. |VPC |VPC |
   |Network Instances |Select the target VPC to be attached. |VPC\-A |VPC\-B |
   

4. Click **Attach** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5p-l55yL6Lev55Sx"></span>
### Step 3: View route

View the route table of the CEN and confirm that it has successfully learned the subnet routes of the VPC.

Check the VPC's route table to confirm it has successfully received the routes synchronized from the CEN.


<Tabs>
<Tab zoneid="XmI8i5SrCa" title="View CEN route information">
<TabTitle>View CEN route information</TabTitle>

1. Click the CEN\-X.

2. On the **Route Table** tab, confirm the subnet routes automatically learned by the Cloud Enterprise Network (CEN).


</Tab>
<Tab zoneid="td8jCxTNRW" title="View VPC-A route">
<TabTitle>View VPC-A route</TabTitle>

1. Click the name of VPC\-A.

2. Click **Route Table**.

3. Click the name of VPC\-A's route table.

4. In the **Route Entry \> System route** tab, you can view the routes synchronized from the CEN to VPC\-A.


</Tab>
<Tab zoneid="Zq3yjZpKv8" title="View VPC-B route">
<TabTitle>View VPC-B route</TabTitle>

1. Click the name of VPC\-B.

2. Click **Route Table**.

3. Click the name of VPC\-B's route table.

4. On the **Route Entry \> System Route** tab, you can view the routes synchronized from the CEN to VPC\-B.


</Tab>
</Tabs>


<span id=".5q2l6aqk5Zub77ya5p-l55yLL-aUvumAmuWuieWFqOe7hA=="></span>
### Step 4: View all security groups

You can refer to this section to check whether the security groups associated with ECS\-A and ECS\-B allow the required traffic. If not allowed, allow the traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to the default outbound rules added by the security group, traffic for all networks (0.0.0.0/0), all ports, and all protocols are already allowed. Therefore, in this example, only the inbound rules are configured to allow traffic from ECS\-A to ECS\-B and from ECS\-B to ECS\-A.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top navigation bar, select the target region. This topic uses China (Beijing).

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A or ECS\-B

5. On the **Security Group** tab, you can view the current rule.

6. Click **Configure** on the right side of the target security group.

7. On the **Inbound rule** tab, click **Add rule**.

8. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |ECS\-A value |ECS\-B value |
   |---|---|---|---|
   |Priority |Priority of Security Group rules. |100 |100 |
   |Policy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, and ICMPv6 protocols. |ALL |ALL |
   |Port range |Limit the port range based on different protocol types. |ALL |ALL |
   |Source |Indicates that the network interfaces in this security group are allowed/denied access from resources at the source address. |192.168.1.0/24 |172.16.1.0/24 |
   

9. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5LqU77ya6aqM6K-B"></span>
### Step 5: Verification


1. Remotely log in to ECS\-A.

2. On the command line, execute `ping <IP address of ECS-B, using 192.168.1.22 as an example>` to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png) </span>

3. Similarly, verify that ECS\-B can access ECS\-A.
