---
title: "VPC interconnection (cross-account and cross-region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts"
---

This topic explains how to use Cloud Enterprise Network (CEN) to establish private network connectivity between cross\-account, cross\-region Virtual Private Cloud (VPC) instances.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a695af281887aef3f52694cc54dea9fc.png)

## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:

1. Register Account A, Account B, and complete real name verification.

2. Recharge account.

3. Use Account A in China (Beijing) and Account B in China (Shanghai) to [create one VPC and subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), and [create ECSs](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). Details are as follows:

   * Account A: VPC\-A (172.16.0.0/16), Subnet\-A (172.16.1.0/24), ECS\-A.

   * Account B: VPC\-B (192.168.0.0/16), Subnet\-B (192.168.1.0/24), ECS\-B.

> **tip**

> Ensure the CIDR blocks of the different VPC subnets are non\-overlapping and not identical. If it exists, the CEN automatically learns VPC routes and synchronizing the learned routes to the VPC may cause conflicts, resulting in the corresponding subnets being unable to communicate. In this case, see [Resolving Address Conflicts in Multi\-VPC Communication Scenarios](https://docs.byteplus.com/en/docs/natgateway/Resolving-address-conflicts-in-multiple-VPCs).

## Procedures

> **tip**

> The following describes only the required parameters and their values. For other parameters not mentioned, retain the default values.

### Step 1: Create CEN

1. Log in to the CEN consoleCEN console with Account A.

2. In the top navigation bar, select the target project.

3. Click **Create CEN**.

4. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Enter the name of CEN instance. |CEN\-X |
   |Attaching a network instance |Choose whether to enable the option to attach a network instance under the current account to the CEN instance. |Off |

5. Click **Create** to complete the action.

### Step 2: Add cross\-account CEN authorization

You can follow this procedure to authorize Account A from Account B, allowing CEN\-X to attach VPC\-B.

1. Log in to the VPC consoleVPC console using Account B.

2. On the top menu bar, select China (Shanghai).

3. Click the VPC\-B.

4. In the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**.

5. Enter the ID of Account A and the ID of the CEN instance "CEN\-X".

6. Click **Authorize** to complete the action.

### Step 3: Attach Network Instance

You can perform the following operations to attach VPC\-A and VPC\-B to the CEN in sequence.

1. Log in to the Cloud Enterprise Network consoleCloud Enterprise Network console with Account A.

2. Click **CEN\-X**.

3. On the **Network Instances** tab, click **Attach Network Instance**.

4. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Example value A |Example value B |
   |---|---|---|---|
   |Account |Select the account to which the network instance belongs.<br><br><br>* This Account: the Account to which the CEN belongs.<br><br>* Cross\-Account: Enter the peer account ID. |My account |Cross\-account 21000\*\*\*\* |
   |Regions |Select the region where the network instance resides. |China (Beijing) |China (Shanghai) |
   |Instance type |Supports instance type selection. |VPC |VPC |
   |Network Instances |Select a network instance. |VPC\-A |VPC\-B |

5. Click **Attach** to complete the action.

### Step 4: Configure inter\-region bandwidth

You can refer to this operation to create a Bandwidth Package and allocate bandwidth for VPC communication between China (Beijing) and China (Shanghai).

1. Log in to the CEN consoleCEN console with Account A.

2. In the left navigation tree, select **Bandwidth Package**.

3. Click **Create bandwidth package**. Configure the relevant parameters according to the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Billing method |Select the billing method for Bandwidth Package. |Subscription |
   |Name |Type a name for the bandwidth package. |package\-u5cy |
   |Cloud Enterprise Network |Select a CEN instance. |CEN\-X |
   |Interoperability area |Select the local and peer regions that need to interconnect. |Chinese mainland \- Chinese mainland |
   |Bandwidth |Set the bandwidth value for the bandwidth package. Valid range: 2 to 10,000. Unit: Mbps. |500 Mbps |
   |Duration |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. When automatic renewal is enabled, the system will automatically renew the instance upon expiration if your account has sufficient balance. The default renewal cycle is 1 month with unlimited renewals. |Not selected |

4. Click **Confirm order**. Follow the console guidance to review and accept Legal. Click **Buy now**.

5. In the left\-side navigation pane, click **CEN Instances**.

6. Click the CEN\-X.

7. On the **Inter\-region bandwidth** tab, click **Allocate inter\-region bandwidth**. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Bandwidth package |Select the bandwidth package for inter\-region bandwidth allocation. |package\-u5cy |
   |Interconnected regions |Select the local and peer regions that require interconnection. |China (Beijing) \- China (Shanghai) |
   |Bandwidth |Enter the bandwidth between the two regions to be interconnected. The value cannot exceed the allocatable bandwidth of the bandwidth package. |200Mbps |

7. Click **Allocate** to complete the action.

### Step 5: View route

View the route table of the CEN and confirm that it has successfully learned the subnet routes of the VPC.

View the VPC's route table to confirm it has successfully received the routes from the CEN.

**View CEN route information**

1. Click the CEN\-X.

2. On the **Route Table** tab, confirm the subnet routes automatically learned by the Cloud Enterprise Network (CEN).

**View VPC-A route**

1. Click the name of VPC\-A.

2. Click **Route Table**.

3. Click the name of VPC\-A's route table.

4. In the **Route Entry \> System route** tab, you can view the routes synchronized from the CEN to VPC\-A.

**View VPC-B route**

1. Log in to the VPC consoleVPC console using Account B.

2. Click the name of VPC\-B.

3. Click **Route Table**.

4. Click the name of VPC\-B's route table.

5. On the **Route Entry \> System Route** tab, you can view the routes synchronized from the CEN to VPC\-B.

### Step 6: View/Configure security group

You can refer to this section to check whether the security groups associated with ECS\-A and ECS\-B allow the required traffic. If not allowed, allow the traffic.

> **tip**

> Due to the default outbound rules added by the security group, traffic for all networks (0.0.0.0/0), all ports, and all protocols are already allowed. Therefore, in this example, only the inbound rules are configured to allow traffic from ECS\-A to ECS\-B and from ECS\-B to ECS\-A.

1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A or ECS\-B

5. In the **Security Group** tab, click **Configure** on the right side of the target security group.

6. On the **Inbound rule** tab, click **Add rule**. Configure relevant parameters based on the table below.

   |Parameter |Explanation |ECS\-A value |ECS\-B value |
   |---|---|---|---|
   |Priority |Priority of Security Group rules. |100 |100 |
   |Policy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, and ICMPv6 protocols. |ALL |ALL |
   |Port range |Limit the port range based on different protocol types. |ALL |ALL |
   |Source |Indicates that the network interfaces in this security group are allowed/denied access from resources at the source address. |192.168.1.0/24 |172.16.1.0/24 |

7. Click **Confirm** to complete the action.

### Step 7: Verification

1. Remotely log in to ECS\-A.

2. On the command line, execute `ping <IP address of ECS-B, using 192.168.1.22 as an example>` to test network connectivity.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png)

3. Similarly, verify that ECS\-B can access ECS\-A.
