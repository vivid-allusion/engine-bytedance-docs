---
title: "EIP Cross-Region Disaster Recovery"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/EIP-Cross-Region-Disaster-Recovery"
---

## Background

To ensure business stability, you can configure Internet egress points in multiple regions for your business resources. If the Internet egress in the current region fails, you can use the backup region's Internet egress to achieve cross\-region disaster recovery.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15e93b321d3cd1b9a0f40df9b3875f44.png)

> **tip**

> This topic uses Cloud Enterprise Network (CEN) as an example. The same applies to Transit Router (TR).

The following diagram illustrates a sample configuration:

|Region |Resource type |Resource name |CIDR block/IP address |Remark |
|---|---|---|---|---|
|Region A |Virtual Private Cloud (VPC) |VPC\-A |172.16.0.0/16 |\-\- |
||Subnet |Subnet\-A | 172.16.1.0/24 |Located in Availability Zone A |
||Elastic Compute Service |ECS\-A |172.16.1.11 |Not bound to EIP |
|Region B |Virtual Private Cloud (VPC) |VPC\-B |192.168.0.0/16 |\-\- |
||Subnet |Subnet\-B | 192.168.1.0/24 |Located in Availability Zone A |
||Elastic Compute Service |ECS\-B |192.168.1.22 |Associate an EIP in Region B. |

## Preparations

* The feature to bind EIPs to IP Address\-type resources is currently in private testing. Please contact your account manager to request access.

* In region A:

   1. Create a VPC with parameters consistent with the Background description above.

   2. Create an ECS\-A (172.16.1.11) without an EIP in Subnet\-A of VPC\-A.

* In region B:

   1. Create a VPC with parameters consistent with the Background description above.

   2. Create an ECS\-B (192.168.1.22) without an EIP in Subnet\-B of VPC\-B.

For operations on creating VPC and ECS, consult [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

## Procedures

### Step 1: Establish connectivity between VPC\-A and VPC\-B

Establish private network connectivity between VPC\-A and VPC\-B. For operations, consult [VPC connectivity (same account across regions)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) and [VPC connectivity (cross-account and cross-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).

### Step 2: Configure IPv4 Gateway

#### (1) Create IPv4 Gateway

Create an IPv4 Gateway in **Region A** and **Region B** respectively.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left navigation pane, select **IPv4 Gateway**.

   3. In the top menu bar, select your target Region.

   4. Click **Create IPv4 Gateway**.

   5. Enter the name of the IPv4 Gateway (such as IPv4Gateway\-A, Ipv4Gateway\-B).

   6. Click **Create** to complete the action.

#### (2) Associate and activate VPC

Associate the IPv4 gateway in **Region A** with VPC\-A, and the IPv4 gateway in **Region B** with VPC\-B.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left navigation pane, select **IPv4 Gateway**.

   3. In the top menu bar, select your target Region.

   4. Click **Associate and activate VPC** to the right of the target IPv4 Gateway.

   5. Select the VPC and subnet route table from dropdown.

   6. Click **Associate** to complete the action.

   After association, a route entry with the destination CIDR 0.0.0.0/0 and the next hop pointing to the IPv4 gateway will be created in the subnet route table.

#### (3) Create gateway route table

Create a gateway route table in **Region A**.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Route Table**.

   3. In the top menu bar, select the target project and region.

   4. Click **Create Route Table**.

   5. Configure relevant parameters based on the table below.

      |Parameter |Description |Sample value |
      |---|---|---|
      |Name |Enter the name of gateway route table. |Route\-Gateway |
      |VPC |Select the VPC for the route table. |VPC\-A |
      |Associated Resource Type |Subnet and gateway are currently supported. This topic uses the gateway. |Gateway |
      |Route entry |After selecting a VPC, the system automatically adds the following system route entries:<br><br><br>   * Route entries with the destination CIDR blocks 100.64.0.0/10 and fd00:64::/32 (if the VPC has IPv6 enabled).<br><br>   * A route entry whose destination CIDR matches the subnet's CIDR block.<br><br>   * A route entry synchronized (or propagated) by the CEN.<br><br>* Click  **+Add Entry** to add multiple route entries as needed. For parameter details and limits of route entries, see [Adding a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry). |\- |

   6. Click **Create** to complete the action.

#### (4) Associate IPv4 Gateway with gateway route table

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Route Table**.

   3. In the top menu bar, select the target project and region.

   4. Click **Associate IPv4 Gateway** on the right side of the target gateway route table.

   5. Select the IPv4 Gateway in region A, then click **Associate** to complete the action.

### Step 3: Associate EIP across regions

#### (1) Apply for EIP

Apply for an EIP in region A.

   1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

   2. In the top menu bar, select the region and project.

   3. Click **Apply for EIP**.

   4. Configure relevant parameters based on the table below.

      |Parameter |Description |Sample value |
      |---|---|---|
      |Billing method |Select a billing method for the EIP. Pay\-as\-you\-go and Subscription are supported. |Pay\-as\-you\-go |
      |Regions |Select a region for the EIP. |Region A |
      |Name |Type in a name for the EIP. |eip\-A |
      |Security protection |Select the protection type for the EIP. |default |
      |ISP |Select an ISP for the EIP. BGP (multi\-ISP) is recommended. |BGP (multi\-ISP) |
      |Metering method |When the billing method is **Pay\-as\-you\-go**, you can choose between two billing modes: **Pay\-by\-bandwidth** or **Pay\-by\-data\-transfer**. |Pay\-by\-data\-transfer |
      |Bandwidth Package |If the billing method is **Pay\-as\-you\-go**, check Add EIP to Bandwidth Package as needed. |No |
      |Bandwidth cap |Set the maximum bandwidth for the EIP. |1 Mbps |
      |Quantity |Type the number of EIPs applied. |1 |
      |Related project |Select the project to which the EIP belongs. |default |
      |Tags |Add one or more custom tags to the EIP as needed. |No tags added |

   5. Follow the console guidance to review and accept Legal.

   6. Click **Agree and buy** to complete the action.

#### (2) Associate IP address

Associate the EIP from **Region A** to the ECS in Region B.

   1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

   2. In the top menu bar, select the region and project.

   3. Click **Associate** next to the target EIP.

   4. Configure relevant parameters based on the table below.

      |Parameter |Description |Sample value |
      |---|---|---|
      |Instance type |Select an IP address. |IP Address |
      |Project |Select the project to which VPC\-B belongs. |default |
      |VPC |Select VPC\-B. |VPC\-B |
      |IP Address |Enter the primary private IP address of the primary ENI for ECS\-B. |192.168.1.22 |

   5. Click **Associate** to complete the action.

## Verification

1. **Verify Internet**

   1. Remotely log in to ECS\-B.

   2. Run the `ping 114.114.114.114` command.

   3. A successful ping indicates that the ECS is connected to the Internet.

2. **Verify cross\-region disaster recovery**

   1. Dissociate the EIP in region B from ECS\-B. Refer to [Disassociating a cloud resource](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP) for the procedure.

   2. Run the `ping 114.114.114.114` command.

   3. A successful ping result indicates that the server in Region B can communicate with the Internet through the EIP of Region A.
