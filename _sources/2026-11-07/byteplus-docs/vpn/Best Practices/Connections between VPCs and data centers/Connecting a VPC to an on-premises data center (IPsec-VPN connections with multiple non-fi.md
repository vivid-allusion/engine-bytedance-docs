---
title: "Connecting a VPC to an on-premises data center (IPsec-VPN connections with multiple non-fixed egress IPs)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center-1"
---

This topic describes the configuration method for VPN Connect when an on\-premises data center (IDC) gateway's egress IP is non\-fixed. In this example, the IDC has multiple IPs to connect to the cloud, and all of them are not fixed.

## Background

Currently, an enterprise has two branches (Branch A and Branch B) that need to access the cloud resources at headquarters. Due to network restrictions, the local gateway egress IPs of both branches are non\-fixed static public IPs. Considering cost efficiency, the enterprise hopes to use VPN connections from the IDCs to access the cloud. This topic explains how to configure VPN connections to achieve network connectivity under this special non\-fixed egress IP scenario.

Given the enterprise's current situation, there are two possible solutions. This topic only covers the configuration for **Solution 2**. For actions of Solution 1, see [Building connectivity between VPC and data center via VPN-IPsec (single non-fixed egress IP)](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center).

* **Solution 1**: Configure one IPsec\-VPN connection with the customer gateway IP set as `0.0.0.0`, allowing both branches to access the VPC. However, if both branches initiate connections simultaneously, the later connection will preempt the earlier one, causing the earlier connection to disconnect.

* **Solution 2**: Configure two IPsec\-VPN connections with the customer gateway IP set as `0.0.0.0`, separately enabling both branches to access the VPC. The only difference between the two IPsec connections is the Remote ID (on the VPC side); all other configurations are identical. The two IPsec connections do not interfere with each other, allowing both branches to access cloud VPC resources simultaneously.

   > **warning**

   > The phase 1 authentication algorithm, encryption algorithm, and DH algorithm of the second IPsec connection must match those of the first IPsec connection in this solution.

## Prerequisites

* A Virtual Private Cloud (VPC) (named VPC1) and its subnet have been created. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The CIDR blocks have been properly planned, ensuring no overlap between the parts of IDC A and IDC B to be connected to the cloud and the private CIDR blocks of VPC1.

## Related information

The information obtained is shown below. VPC1, its subnet, and Elastic Compute Service (ECS) are existing cloud resources, while the VPN gateway and customer gateway are resources to be created in the following steps.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c545e7d473662381d6df12ceea2ccf9.png)

> **tip**

> The configuration process for VPN connections with a non\-fixed egress IP address at the customer gateway is the same as for scenarios with a static public IP at the customer gateway, but differences in parameter settings occur during customer gateway creation and IPsec\-VPN connection creation phases and require attention.

## Procedure

### Step 1: Create VPN gateway

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type for the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method of the VPN gateway. |Subscription |
   |Region |Select the region where the VPN gateway resides. The VPN gateway must reside in the same region as VPC1. |China (Beijing) |
   |Name |The name of the VPN gateway. |VPNGW\-test |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Single tunnel |
   |IP address type |The IP address type used to interconnect the VPN gateway and the client. In single\-tunnel mode, only IPv4 addresses are supported. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. For single\-tunnel VPN gateways, only IPv4 addresses are supported. |IPv4 |
   |**Network configuration** |||
   |Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |20Mbps |
   |VPC |The VPC where the VPN gateway resides. |VPC1\|192.168.1.0/24 |
   |Subnet |Select the subnet where the VPN gateway resides. Reserve sufficient IPv4 addresses in the subnet for deploying the VPN gateway.​ |Subnet 1 \| 192.168.1.128/25 |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. Configuring BGP ASN for a VPN gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   |**More information** |||
   |Purchase duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. |Do not select |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-01 that is selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-01 |

5. Click **Confirm order**, and follow the console guidance to review and accept the legal terms.

6. Click **Buy now** for payment to complete the purchase. Click **Confirm order**, and complete the action as prompted by the interface.

   The VPN gateway VPNGW\-test was created successfully, with the system\-assigned gateway egress IP 180.XX.XX.43.

### Step 2: Create customer gateway

1. Log in to the Customer Gateway console.

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click **Create Customer Gateway**, and configure the customer gateway based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select the region where the customer gateway resides. It must match the region of VPC1 and the VPN gateway (VPNGW\-test). |China (Beijing) |
   |Name |Set a name for the customer gateway. |CGW\-test |
   |IP address |Enter the static public IP address of the peer VPN gateway. It is the gateway’s egress IP address. In this scenario, the peer does not have a fixed gateway egress IP address. Therefore `0.0.0.0` is configured. |0.0.0.0 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. User gateway BGP ASN needs to be set only when IPsec connections use dynamic route propagation mode. This operation demonstration uses static route propagation mode, so configuring user gateway BGP ASN is not required. |\-\- |
   |Affiliated project |The project to which the customer gateway belongs. It is fixed as Project\-01 that is selected before entering the creation page. |Project\-01 |

5. After configuration, click **Accept**.

### Step 3: Create IPsec\-VPN connection

#### Create the first IPsec\-VPN connection

1. Log in to the VPN Connection console.

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click **Create VPN Connection**, and configure the IPsec\-VPN connection based on the table below.

   * Basic information

      |Parameter |Description |Example |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |The name of the IPsec\-VPN connection. |IPsecVPN\-test\-A |
      |Affiliated project |The project to which the resource belongs. It is fixed as Project\-01 that is selected before entering the creation page. |Project\-01 |

   * Associate resources

      |Parameter |Description |Example |
      |---|---|---|
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated. |VPN gateway |
      |VPN gateway |Select the VPN gateway created in the previous [Create VPN gateway](https://docs.byteplus.com/en/docs/52/5033#.5q2l6aqk5LiA77ya5Yib5bu6VlBO572R5YWz) phase. |VPNGW\-test |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration.<br><br>> **warning**<br><br><br>> In this scenario, the peer does not have a fixed gateway egress IP address, so active negotiation cannot be initiated from the cloud. It defaults to No and cannot be modified.<br> |No |
      |Route propagation mode |Select a routing propagation mode. |Static routing |
      |Customer gateway |Select the customer gateway created in the previous [Create customer gateway](https://docs.byteplus.com/en/docs/52/5033#.5q2l6aqk5LqM77ya5Yib5bu655So5oi3572R5YWz) phase. |CGW\-test |
      |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>This information is crucial. Keep it secure. |test@00000 |
      |Confirm key |Enter Pre\-Shared Key again. |test@00000 |

   * Advanced configuration

      > **tip**

      > This section only covers parameters requiring special configuration; keep all other parameters at default values.

      |Parameter ||Description |Example |
      |---|---|---|---|
      |IKE Config |Version |The version of the IKE protocol. In this scenario, the peer does not have a fixed gateway egress IP address. Only **ikev1** can be used here. |ikev1 |
      ||Negotiation mode |Select the IKE authentication negotiation mode.<br><br>> **warning**<br><br><br>> In this scenario, the peer does not have a fixed gateway egress IP address. Only "aggressive" can be used here.<br> |aggressive |
      ||Remote ID |The peer identifier of the IPsec\-VPN connection. It is used for Phase 1 negotiation. |10.XX.XX.1 |

5. After completing the configuration, click Create.

#### Create a second IPsec\-VPN connection

Follow steps 1 to 5 in **creating the first IPsec\-VPN connection** to create the second one. Except for the IPsec\-VPN connection name and Remote ID, all other settings match the first connection and are not repeated here.

> **warning**

> The **authentication algorithm**, **encryption algorithm**, and **DH algorithm** in the first phase IKE configuration of the second IPsec\-VPN connection must be the same as those in the first connection.

|Parameter ||Description |Example |
|---|---|---|---|
|Name ||The name of the IPsec\-VPN connection. |IPsecVPN\-test\-B |
|IKE Config |Remote ID |The peer identifier of the IPsec\-VPN connection. It is used for Phase 1 negotiation. |10.XX.XX.2 |

> **tip**

> The Remote ID `10.XX.XX.2` here can be any IP address except the first Remote ID `10.XX.XX.1`, used only to distinguish between the two IPsec connection tunnels.

### Step 4: Configure route for VPN gateway

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click the VPN gateway name "VPNGW\-test" in the list.

4. Select the Routing information tab, then click Add route.

5. Configure the route according to the following table.

   |Parameter |Description | |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of the on\-premises IDC. |10.1.0.0/16 |
   |Next Hop type |Fixed as **IPsec\-VPN connection**. |IPsec\-VPN connection |
   |Next Hop |Select the first IPsec\-VPN connection created in the [Create IPsec-VPN connection](https://docs.byteplus.com/en/docs/52/5033#.5q2l6aqk5LiJ77ya5Yib5bu6SVBzZWPov57mjqU=) phase. |IPsecVPN\-test\-A |

6. Click OK to complete adding the route entry to the IDC within VPNGW\-test.

7. Add the following routes using the same method.

   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of the on\-premises IDC. |10.2.0.0/16 |
   |Next Hop type |Fixed as **IPsec\-VPN connection**. |IPsec\-VPN connection |
   |Next Hop |Select the second IPsec\-VPN connection created in the [Create IPsec-VPN connection](https://docs.byteplus.com/en/docs/52/5033#.5q2l6aqk5LiJ77ya5Yib5bu6SVBzZWPov57mjqU=) phase. |IPsecVPN\-test\-B |

> **tip**

> If the VPC where the VPN gateway resides has a custom route table, and the subnets associated with the route table need to access the on\-premises data center (IDC) through the VPN Connect, you must manually add a route entry to the route table. Set the destination CIDR block to the on\-premises IDC CIDR block and the next hop type to **VPN gateway**. For procedure, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH).

### Step 5: Configure on\-premises route and initiate connection

1. Download the configuration files for IPsecVPN\-test\-A and IPsecVPN\-test\-B respectively.

   1. Log in to the VPN Connection console, select the IPsec\-VPN connection in China (Beijing) under Project\-01.

   2. In the IPsec connection list, select the IPsec connection created in [Create IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center-1#.5q2l6aqk5LiJ77ya5Yib5bu6SVBzZWPov57mjqU=).

   3. Click Download IPsec Config.

   4. Click Download.

2. Configure route for on\-premises gateway

   Configure the on\-premises gateway routing at IDCs A and B, following the downloaded IPsecVPN\-test\-A and IPsecVPN\-test\-B configuration files. Ensure the IPsec configurations match on both sides. For detailed configuration, see [File transfer overiew](https://docs.byteplus.com/en/docs/vpn/Overview-1).

3. Initiate connections from IDC A and IDC B respectively.

   * Initiate connections simultaneously: both IPsec\-VPN connections succeed.

   * Initiate connections sequentially: both IPsec\-VPN connections succeed.

   > **tip**

   > The scenarios in this topic are applicable when the peer has no fixed gateway egress IP address, and a connection cannot be initiated from the VPC. After all configurations are complete, the negotiation request must be initiated from the IDC. Similarly, if an existing IPsec\-VPN connection disconnects, the negotiation request still needs to be initiated from the IDC.
