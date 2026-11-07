---
title: "Configuring cross-VPC traffic mirrors"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Cross-VPC-Traffic-Mirrors"
---

Copy the Internet traffic of the current VPC to a traffic monitoring platform deployed in another VPC for auditing, providing clues and evidence for cybersecurity incidents, and enabling timely detection of potential cybersecurity threats.

## Background introduction

An enterprise under the same account and in the same region has two VPCs, each belonging to different departments. VPC\-A is under the R&D department, and VPC\-B is under the security department. The security department (VPC\-B) monitors and audits the Internet traffic of the R&D department (VPC\-A).

* The name of Virtual Private Cloud 1 is VPC\-A, with a CIDR block of 192.168.0.0/16. The name of its subnet is Subnet\-A, with a subnet CIDR block of 192.168.1.0/24

* The name of Virtual Private Cloud 2 is VPC\-B, with a CIDR block of 172.16.0.0/16. The name of its subnet is Subnet\-B, with a subnet CIDR block of 172.16.1.0/24.

* The IP address of ECS\-A is 192.168.1.66, the IP address of ECS\-B is 172.16.1.11, and the IP address of ECS\-C is 172.16.1.22.

* The IP address of the Classic Load Balancer is 172.16.1.88.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22454f7421847238940cd3d6abbc53bf.png)

> **tip**

> The traffic monitoring platform deployed on the ECSs in the above diagram needs to support decapsulating VXLAN\-encapsulated data packets. This is because traffic mirroring copies traffic that meets the Mirror Filters from the mirror site, encapsulates it using VXLAN, and forwards it to the Mirror Target. Only after the traffic monitoring platform decapsulates the VXLAN encapsulation can the original traffic data be obtained for monitoring and analysis. For more details, see [Traffic Mirror Overview](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview#.6ZWc5YOP55uu55qE).

## Preparations

Complete the following tasks based on the background information before proceeding:

1. Create two VPCs in China (Beijing) region using your account, keeping the VPC parameters consistent with the [background information above](https://docs.byteplus.com/en/docs/vpc/Cross-VPC-Traffic-Mirrors#.6IOM5pmv5LuL57uN). For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create ECS instances:

   * Create ECS\-A (192.168.1.66) in Subnet\-A of VPC\-A, bind an EIP to it, and add it to the default security group of VPC\-A.

      > tip

      > Traffic mirroring is not supported for the primary or secondary network interfaces of ECSs using first\-generation (except for r1ie, c1ie, g1ie) or third\-generation (e.g., g3i, c3i) instance types. For more details on instance types, see [Instance Type Introduction](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) and [Instance Selection Best Practices](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice).

   * Create ECS\-B (172.16.1.11) and ECS\-C (172.16.1.22) in Subnet\-B of VPC\-B, [Deploy backend services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh) on them, and add them to the default security group of VPC\-B.

3. Configure private network connectivity between VPC\-A and VPC\-B. You can use Cloud Enterprise Network (CEN), Transit Router (TR), or VPN Connect.

   * For CEN, see [private network connectivity within the same account and region](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01) for operation steps.

   * For TR, see [achieving private network connectivity and isolation between different VPCs (same account and region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02) for operation steps.

   * For VPN Connect, see [setting up inter-VPC network connectivity](https://docs.byteplus.com/en/docs/vpn/Connecting-virtual-private-clouds) for operation steps.

## Procedures

### Step 1: Configure CLB

#### Create Classic Load Banlancer (CLB)

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click **Create classic load balancer**.

3. Configure the relevant parameters of the CLB instance according to the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Select a billing method for the CLB instance. |Pay\-as\-you\-go |
   |Region |Select the Region where the CLB instance resides. |China (Beijing) |
   |Availability zone |Select the master and slave availability zone of the CLB instance respectively. |* Primary: Availability Zone A<br><br>* Secondary: Availability Zone B |
   |Name |Enter the name of the CLB instance. |TrafficMirror\-CLB |
   |**Network configuration** |||
   |IP version |Select the private IP address version of CLB instance. |IPv4 |
   |Network type |Select the network type of the CLB instance, which supports both Internet and private networks. |Private |
   |VPC |Select the private network where the CLB instance belongs. |VPC\-B |
   |Subnet |Select the subnet to which the CLB instance belongs. The subnet provides a private deployment environment for the CLB instance. |Subnet\-B \| 172.16.1.0/24 |
   |IPv4 address |Select the allocation method for the CLB instance IPv4 address, supporting both Auto\-assign and Custom\-assign. This topic uses Custom\-assign IP, enter the private IP address of the CLB. |Custom\-assign IP 172.16.1.88 |
   |**Performance** |||
   |Specification |Select the specification of CLB instance. For different specification metrics, see [Product specification](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |Small I |
   |Project |Select the project of CLB instance. |default |

4. Follow the console guidance to review and accept Legal.

5. Click **Buy now** to proceed to the application submission success page.

6. Click **Go to the console** to navigate to the Instances page and view the newly created instance.

#### Configure backend server

1. Click the newly created CLB name TrafficMirror\-CLB.

2. On the **Server Group** tab, click **Add Server Group**.

3. Input the backend server group name TrafficMirror\-group and select the Type of server.

4. Click **Create** to complete the action.

5. Click TrafficMirror\-group, then click **Add Server**.

6. Select the Basic mode (that is, do not enable **Advanced mode**.) Check ECS\-B and ECS\-C, then click **Next step**.

7. Configure ports and weights for ECS\-B and ECS\-C. The port is configured as 4789, and the weight is set to 100.

8. Click **Add** to complete the action.

#### Create listener

Create a listener that listens on UDP port 4789 for Traffic Mirror.

1. On the Listeners tab, click **Add listener**.

2. Refer to the following table to configure the basic **Protocol & Listening** settings.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Listener name |Set the name of Listener. |TrafficMirror\-listener |
   |CLB protocol |Select the protocol type for CLB instance listener. This topic uses the fixed UDP protocol for Traffic Mirror. |UDP |
   |Listening port |This refers to the listening port. The listener distributes requests accessing this port to the backend server group. This topic uses the fixed port 4789 for Traffic Mirror. |4789 |
   |Scheduling algorithm |Specify the rule for forwarding requests accessing TCP port 80 by this listener. |Weighted Round Robin (WRR) |
   |Timeout period |When no requests to access TCP port 80 are received within the timeout period, the CLB instance will automatically release the connection. |900 seconds |

3. Click **Next** to configure **Server Group**. Select the newly created Server Group **TrafficMirror\-group**.

4. Click **Next** and configure **Health check** parameters (use default values as shown).

5. Click **Next**, and review the configuration on the **Configuration review** page to verify accuracy. After confirming there are no errors, click **Add** to complete the actions.

### Step 2: Configure the security group

The default security group of VPC\-A (which is associated with the Network Interface of ECS\-A) allows all outbound traffic by default, so no additional configuration is required.

The default security group of VPC\-B (which is associated with the Network Interfaces of ECS\-B and ECS\-C) does not allow inbound traffic on UDP port 4789, which is required for Traffic Mirror transmission. Therefore, you need to manually add a security group rule to permit this traffic.

1. Log in to the [security group console](https://console.byteplus.com/vpc/securityGroup).

2. In the top menu bar, select the target project and region.

3. Find the default security group of VPC\-B, then click **Configure rule** on the right side.

4. On the **Access rules \> Inbound rule** tab, click **Add rule** to open the Add inbound rule window.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Priority |Set the priority of security group rules, ranging from 1 to 100, where the default value 1 represents the highest precedence.​​ |1 |
   |Strategy |Select a Security Group policy, supporting both allow and deny. |Allow |
   |Protocol type |Select the protocol type; this topic uses the fixed UDP protocol for Traffic Mirror. |UDP |
   |Port range |Enter the port range. This topic uses fixed port 4789 for Traffic Mirror |4789 |
   |Source |Select CIDR and enter the source address for the inbound security group rule. |192.168.1.66/32 |

6. Click **Confirm** to complete the action.

### Step 3: Configure Traffic Mirror

#### Create Traffic Mirror Target

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Target**.

3. Click **Create Mirror Target**.

4. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of Traffic Mirror Target. |Target\-X |
   |Target type |Select the type of Traffic Mirror Target. |CLB |
   |Target Instance​​ |Select the Traffic Mirror Target instance from the dropdown list. |TrafficMirror\-CLB |

5. Click **Create** to complete the action.

#### Create Traffic Mirror Filter

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. Click **Create Mirror Filter**.

4. Enter the Traffic Mirror Filter name, this topic uses Filter\-X.

5. Refer to the table below to configure inbound and outbound rules.

   |Parameter |Description |Outbound rule example |Inbound rule example |
   |---|---|---|---|
   |Priority |The priority of Mirror Filter ranges from 1 to 1000, with a default value of 1 (highest priority). |1 |1 |
   |Strategy |Policy for the Traffic Mirror Filter.<br><br><br>* Allow: When traffic from the mirror site matches this rule, it is copied to the Mirror Target for monitoring and analysis.<br><br>* Deny: When traffic from the mirror site matches this rule, it is not copied, meaning monitoring and analysis for this traffic is rejected. |Allow |Allow |
   |Agreement |Supports ALL, TCP, UDP, ICMP protocols. |ALL |ALL |
   |Source address and port |Set the source address and port for the traffic. |192.168.1.66/32<br><br>ALL |0.0.0.0/0<br><br>ALL |
   |Destination address and port |Set the destination address and port for the traffic. |0.0.0.0/0<br><br>ALL |192.168.1.66/32<br><br>ALL |

6. Click **Create** to complete the action.

#### Create Traffic Mirror Session

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Session**.

3. Click **Create Traffic Mirror Session**.

4. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Name of the Traffic Mirror Session. |Session\-X |
   |Mirror site |Select the mirror site from the dropdown list. This topic uses the primary network interface of ECS\-A. |ECS\-A\-eni\-1 |
   |Mirror Target |Select the Traffic Mirror Target from dropdown list. |Target\-X |
   |Priority |Set the priority of mirror session. |1 |
   |VNI |Set the VNI for Traffic Mirror Session. |1234 |
   |Data packet size |The packet size for Traffic Mirror is configurable as needed. The minimum range is 64 bytes, and the recommended range is 64 to 1450 bytes. If not specified, the default value is 1500 bytes.<br><br>> **tip**<br><br><br>> If the set packet size is ≤ the MTU of the mirror site or \> 1450, some packets may be truncated and the truncated content discarded. To ensure packets are not truncated, it is recommended to set the packet size and the Network Interface's MTU value according to the following relationship:<br><br><br>> The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450.<br> |1000 |
   |Mirror Filter |Select Traffic Mirror Filter from the dropdown list. |Filter\-X |

6. Click **Buy now** to complete the action.

### Step 4: Verification

1. Log in to the ECS\-A and execute the following command to access the Internet.

   `ping 8.8.8.8`

2. Log in to the ECS\-B and execute the following command to capture and print the traffic data replicated from ECS\-A,

   `tcpdump -i eth0 udp and port 4789 -vv -nn`

   Results:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_903fd485985a21dfe493dc99c345f098.png)
