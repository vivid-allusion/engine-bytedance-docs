---
title: "Getting started"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Traffic-Mirror-Quick-start"
---

This topic introduces how to quickly configure and use Traffic Mirror.

## Scenarios

An enterprise has multiple Elastic Compute Services (ECS) within the same Virtual Private Cloud (VPC) that communicate with the Internet. To monitor the Internet traffic of these ECSs in real time, a new ECS is deployed with traffic monitoring software, and the Internet traffic from other ECSs is replicated to this ECS for [Monitoring and analysis](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-analysis-example).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91a3bd0a26cd2d69e85509b4bc952e97.png)

This topic demonstrates a scenario where both the mirror site and Mirror Target belong to the same VPC and the same security group. If your environment differs from this example, you may need to configure the route table's [Route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry), [Security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules), and [Network ACL](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) to ensure the mirror site can privately access the mirror target via UDP protocol on port 4789.

## Before you begin

Create a VPC and two ECSs within it. One server is bound with an EIP. The other is not bound with an Elastica IP Address (EIP). Both are added to the default security group default. The resource names and IP addresses in this topic align with the diagram provided.

> **tip**

> Only the primary and secondary network interfaces of ECSs with the following specifications are supported as mirror sites: g1ie, g3il, g3al, c1ie, c3il, c3al, r1ie, r3il, r3al, i2, i2g, d2, d2c, d2s, hfr2, hfg2, hfc2, g2ine, t2, s2. For more restrictions, see [Limits](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview#.5L2_55So6ZmQ5Yi2).

## Procedure

> **tip**

> The following section only describes essential parameters and their values. For parameters not mentioned, leave them as default.

### Step 1: Create traffic mirror target

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Target**.

3. In the Traffic Mirror Target list, click **Create Mirror Target**.

4. Configure parameters based on the table below.

   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Enter the name of Traffic Mirror Target. |Target\-X |
   |Target type |Select the type of Traffic Mirror Target. |Network Interface |
   |Target Instance |Select the traffic mirror target instance from the dropdown list. This topic uses the primary network interface of ECS\-TrafficMirrorTarget. |ECS\-TrafficMirrorTarget\-eni\-1 |

5. Click **Create** to complete the operation.

### Step 2: Create traffic mirror filter

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. In the traffic mirror filter list, click **Create Mirror Filter**.

4. Enter the Traffic Mirror Filter name, this topic uses Filter\-X.

5. See the table below to configure inbound and outbound rules.

   |Parameter |Description |Inbound rule example |Outbound rule example |
   |---|---|---|---|
   |Priority |The priority of Mirror Filter ranges from 1 to 1000, with a default value of 1 (highest priority). |1 |1 |
   |Policy |Policy for the Traffic Mirror Filter.<br><br><br>* Allow: When traffic from the mirror site matches this rule, it is copied to the Mirror Target for monitoring and analysis.<br><br>* Deny: When traffic from the mirror site matches this rule, it is not copied, meaning monitoring and analysis for this traffic is rejected. |Allow |Allow |
   |Protocol |Supports ALL, TCP, UDP, ICMP protocols. |ALL |ALL |
   |Source address and port |Set the source address and port for the traffic. |0.0.0.0/0<br><br>ALL |192.168.1.2/32<br><br>ALL |
   |Destination address and port |Set the destination address and port for the traffic. |192.168.1.2/32<br><br>ALL |0.0.0.0/0<br><br>ALL |

6. Click **Create** to complete the operation.

### Step 3: Create traffic mirror session

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Session**.

3. In the Traffic Mirror Session list, click **Create Traffic Mirror Session**.

4. Configure parameters based on the table below.

   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Name of the traffic mirror session. |Session\-X |
   |Mirror site |Select the mirror site from the dropdown list. This topic uses the primary network interface of ECS\-TrafficMirrorSource. |ECS\-TrafficMirrorSource\-eni\-1 |
   |Traffic Mirror Target |Select the Traffic Mirror Target from dropdown list. |Target\-X |
   |Priority |Set the priority of mirror session. |1 |
   |VNI |Set the VNI for the mirror session. |1234 |
   |Packet size |The packet size for Traffic Mirror is configurable as needed. The minimum range is 64 bytes, and the recommended range is 64 to 1450 bytes. If not specified, the default value is 1500 bytes.<br><br>> **tip**<br><br><br>> If the set packet size is < the MTU of the mirror site or \> 1450, some packets may be truncated and the truncated content discarded. To ensure packets are not truncated, it is recommended to set the packet size and the [Network interface's MTU](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface) value according to the following relationship:<br><br><br>> The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450.<br> |1000 |
   |Traffic Mirror Filter |Select Traffic Mirror Filter from the dropdown list. |Filter\-X |
   |Session management status |Start traffic mirror session.<br><br><br>* **Start**: The mirror session starts replicating traffic, and the corresponding billing item takes effect immediately and starts charging.<br><br>* **Stop**: The mirror session does not replicate traffic, and the corresponding billing item does not take effect and is not billed. To enable it later, see [Starting the Traffic Mirror](https://docs.byteplus.com/en/docs/vpc/Starting-Stoping-a-traffic-mirror-session). |Enable |

5. Click **Buy now** to complete the operation.

## Verification

1. Log in to the ECS\-TrafficMirrorSource and execute the following command to access the Internet.

   `ping 8.8.8.8`

2. Log in to the ECS\-TrafficMirrorTarget and execute the following command to capture and print the traffic data replicated from ECS\-TrafficMirrorSource.

   `tcpdump -i eth0 udp and port 4789 -vv -nn`

   The results are shown in the figure below, indicating that the traffic data has been successfully mirrored to the traffic mirror target's ECS.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7444169dcfe2c57f837dafefc6466db1.png)

   The mirrored traffic data can subsequently be analyzed; for operations, see [Traffic Mirror analysis example](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-analysis-example).
