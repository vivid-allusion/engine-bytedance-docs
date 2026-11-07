---
title: "VPC interconnection (cross-account, same region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region"
---

You can follow this topic to achieve private network connectivity across accounts within the same region by using Cloud Enterprise Network (CEN).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74e84a21051755becb6f02eabf0a6787.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:


1. Register Account A, Account B, and complete real name verification.

2. Recharge account.

3. Use Account A and Account B to Creating 1 VPC and subnet in China (Beijing), and Creating one Elastic Compute Service (ECS), as follows:

   * Account A: VPC\-A (172.16.0.0/16), Subnet\-A (172.16.1.0/24), ECS\-A.

   * Account B: VPC\-B (192.168.0.0/16), Subnet\-B (192.168.1.0/24), ECS\-B.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure the CIDR blocks of the different VPC subnets are non\-overlapping and not identical. If it exists, the CEN automatically learns VPC routes and synchronizing the learned routes to the VPC may cause conflicts, resulting in the corresponding subnets being unable to communicate. In this case, see <a href="https://docs.byteplus.com/en/docs/natgateway/Resolving-address-conflicts-in-multiple-VPCs">Resolving Address Conflicts in Multi\-VPC Communication Scenarios</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following describes only the required parameters and their values. For other parameters not mentioned, retain the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65LqR5LyB5Lia572R"></span>
### Step 1: Create CEN


1. Log in to the CEN consoleCEN console with Account A.

2. In the top navigation bar, select the target project.

3. Click **Create CEN**.

4.  Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Set the name of CEN instance. |CEN\-X |
   |Attaching a network instance |Choose whether to enable the option to attach a network instance under the current account to the CEN instance. |Off |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5LqM77ya5re75Yqg6Leo6LSm5Y-35LqR5LyB5Lia572R5o6I5p2D"></span>
### Step 2: Add cross\-account CEN authorization

You can follow this procedure to authorize Account A from Account B, allowing CEN\-X to attach VPC\-B.


1. Log in to the VPC consoleVPC console using Account B.

2. On the top menu bar, select the Region China (Beijing).

3. Click the VPC\-B.

4. In the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**.

5. Enter the ID of Account A and the ID of the CEN instance "CEN\-X".

6. Click **Authorize** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 3: Attach Network Instance

You can refer to this action to sequentially load VPC\-A and VPC\-B into the CEN.


1. Log in to the Cloud Enterprise Network consoleCloud Enterprise Network console with Account A.

2. Click on the CEN Instance name CEN\-X.

3. On the **Network Instances** tab, click **Attach Network Instance**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |Sample value |
   |---|---|---|---|
   |Account |Select the account to which the network instance belongs.<br><br><br>* This Account: the Account to which the CEN belongs.<br><br>* Cross\-Account: Enter the peer account ID. |My account |Cross\-account 21000\*\*\*\* |
   |Regions |Select the region where the network instance resides. |China (Beijing) |China (Beijing) |
   |Instance type |Supports instance type selection. |VPC |VPC |
   |Network Instances |Select a network instance. |VPC\-A |VPC\-B |
   

5. Click **Attach** to complete the action.


<span id=".5q2l6aqk5Zub77ya5p-l55yL6Lev55Sx"></span>
### Step 4: View route

View the route table of the CEN and confirm that it has successfully learned the subnet routes of the VPC.

View the VPC's route table to confirm it has successfully received the routes from the CEN.


<Tabs>
<Tab zoneid="kZZ2qRQ6Jw" title="View CEN route information">
<TabTitle>View CEN route information</TabTitle>

1. Click the CEN\-X.

2. On the **Route Table** tab, confirm the subnet routes automatically learned by the Cloud Enterprise Network (CEN).


</Tab>
<Tab zoneid="XnM1n7kQg3" title="View VPC-A route">
<TabTitle>View VPC-A route</TabTitle>

1. Click the name of VPC\-A.

2. Click **Route Table**.

3. Click the name of route table.

4. In the **Route Entry \> System route** tab, you can view the routes synchronized from the CEN to VPC\-A.


</Tab>
<Tab zoneid="wHtZhWfYVj" title="View VPC-B route">
<TabTitle>View VPC-B route</TabTitle>

1. Log in to the VPC consoleVPC console using Account B.

2. Click the name of VPC\-B.

3. Click **Route Table**.

4. Click the name of route table.

5. On the **Route Entry \> System Route** tab, you can view the routes synchronized from the CEN to VPC\-B.


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqU77ya5p-l55yLL-aUvumAmuWuieWFqOe7hA=="></span>
### Step 5: View and Release security group

You can refer to this section to check whether the security groups associated with ECS\-A and ECS\-B allow the required traffic. If not allowed, allow the traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to the default outbound rules added by the security group, traffic for all networks (0.0.0.0/0), all ports, and all protocols are already allowed. Therefore, in this example, only the inbound rules are configured to allow traffic from ECS\-A to ECS\-B and from ECS\-B to ECS\-A.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A or ECS\-B

5. On the **Security Group** tab, you can view the current rule.

6. Click **Configure** on the right side of the target security group.

7. On the **Inbound rule** tab, click **Add rule**. Configure the relevant parameters according to the table below.

   
   |Parameter |Explanation |ECS\-A value |ECS\-B value |
   |---|---|---|---|
   |Priority |Priority of Security Group rules. |100 |100 |
   |Strategy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |Allow |
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
