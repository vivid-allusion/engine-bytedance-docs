---
title: "Building single-tunnel VPN interconnection between VPCs (static routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-virtual-private-clouds"
---

This topic describes how to connect two Virtual Private Clouds (VPCs) under different accounts through IPsec\-VPN using static routing mode to enable network connectivity.

## Background

VPCs are naturally isolated. VPN Connect can build a tunnel between VPCs to enable communication. This topic uses two VPCs from different accounts as an example. For communication between VPCs under the same account, no account switch is required. Other actions remain the same as those in the current topic.

> **tip**

> To connect a VPC to a third\-party VPC through VPN, you can configure the third\-party VPC as a client when configuring VPN Connect. For more information on the third\-party VPC configuration, see the vendor's documentation.

## Prerequisites

* Activate accounts tesezh\-01 and tesezh\-02 and complete real\-name authentication.

* Get account information about tesezh\-01 and tesezh\-02.

* Create VPC1 under tesezh\-01 and VPC2 under tesezh\-02, with non\-overlapping private CIDR blocks between the two VPCs.

## Related information

The existing deployment is illustrated in the diagram below. VPC1, VPC2, and Elastic Compute Services (ECS1 and ECS2) represent created resources. VPN Gateway 1 and VPN Gateway 2 are resources to be created in the following steps.

> **tip**

* > VPN Connect does not support establishing cross\-border connectivity. In the scenario where a network connection is established between VPCs via the IPsec\-VPN connection, the two interconnected VPCs must both belong to regions within China Mainland or both belong to regions outside China Mainland. It is not allowed that one VPC resides in a China Mainland region and the other resides in a region outside China Mainland. For more information, see Regions.

* > If you need to connect one VPC in a China Mainland region with another VPC in a region outside China Mainland, we recommend you use the Cloud Enterprise Network (CEN) service. For details, see [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/6405).

* > If you need to connect VPCs across different regions through an IPsec\-VPN connection (where VPCs are either both in China Mainland regions or both in regions outside China Mainland), the network quality of IPsec\-VPN is relatively poor due to the quality of the internet. We recommend using CEN. For procedure, see [Inter\-VPC communication across regions within the same account](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) or [Inter\-VPC communication across regions and accounts](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8431e8de73cbaca604d0ed878e3ad37e.png)

## Procedure

### Step 1: Create VPN gateway

1. Log in to the VPN Gateway console using tesezh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

6. Log in to the VPN Gateway console using tesezh\-02, and repeat steps 2\-7 to create VPNGW\-02.

   After VPNGW\-02 is created successfully, the system assigns a gateway egress IP of 180.XX.XX.209.

### Step 2: Create customer gateway

1. Log in to the Customer Gateway console using tesezh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create Customer Gateway**.

4. Configure the customer gateway based on the table below, and click Confirm when completed.

   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select the region where the customer gateway resides.<br><br>Must be consistent with the regions of VPC1 and VPNGW\-01. |China (Beijing) |
   |Name |Set a name for the customer gateway. |CGW\-01 |
   |IP address |Enter the static public IP address of the peer VPN gateway. It is the gateway’s egress IP address. |180.XX.XX.209 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Configuring BGP ASN for a customer gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

5. Log in to Account tesezh\-02 and the Customer Gateway console, then refer to Step 2 to Step 4 to create customer gateway CGW\-02. In the parameters, set IP address to 180.XX.XX.207.

   At this point, the relationship between the VPC, VPN gateway, and customer gateway is as shown in the table below.

   |Account |VPC name |VPN gateway |Egress IP address |Customer gateway |
   |---|---|---|---|---|
   |tesezh\-01 |VPC1 |VPNGW\-01 |180.XX.XX.207 |CGW\-01 |
   |tesezh\-02 |VPC2 |VPNGW\-02 |180.XX.XX.209 |CGW\-02 |

### Step 3: Create IPsec\-VPN connection

1. Log in the VPN Connection console using tesezh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Connection**.

4. Configure the IPsec\-VPN connection based on the table below, and click **Create** after completing the configuration.

   * Basic information

      |Parameter |Description |Example |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |The name of the IPsec\-VPN connection. |IPsecVPN\-01 |
      |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

   * Associate resources

      |Parameter |Description |Example |
      |---|---|---|
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Attach the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Attach the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select VPNGW\-01 created under VPC1. |VPNGW\-01 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Static routing |
      |Customer gateway |Select the customer gateway (CGW\-01) created under VPC1. |CGW\-01 |
      |Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. The configuration on both sides must be identical.<br><br>This information is crucial. Keep it secure. |test@123 |
      |Confirm key |Enter the Pre\-Shared Key again. |test@123 |

5. Log in to the VPN Connection console under Account tesezh\-02, repeat steps 2 to 4, create the IPsec\-VPN connection: IPsecVPN\-02, with the Pre\-Shared Key consistent with IPsecVPN\-01, and set all settings to test@123.

   At this point, the relationship between the Virtual Private Cloud (VPC), VPN gateway, customer gateway, and IPsec\-VPN connection is as shown in the table below.

   |Account |VPC name |VPN gateway |Egress IP address |Customer gateway |IPsec\-VPN connection |
   |---|---|---|---|---|---|
   |tesezh\-01 |VPC1 |VPNGW\-01 |180.XX.XX.207 |CGW\-01 |IPsecVPN\-01 |
   |tesezh\-02 |VPC2 |VPNGW\-02 |180.XX.XX.209 |CGW\-02 |IPsecVPN\-02 |

### Step 4: Configure route for on\-premises VPN gateway

1. Log in to the VPN Gateway console using tesezh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click VPNGW\-01, the name of the VPN gateway, in the list.

4. Click the Route information tab. On this tab, click Add route.

5. Configure the routing information according to the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of VPC2. |192.168.1.0/24 |
   |Next Hop type |Fixed as **IPsec\-VPN connection**. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-01 |

6. Click OK to complete the addition of the VPNGW\-01 route entry.

### Step 5: Configure remote route

1. Log in to the VPN Gateway console using tesezh\-02.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click the VPN gateway name: VPNGW\-02 in the list.

4. Click the Route information tab. On this tab, click Add route.

5. Configure the routing information with reference to the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of VPC1 under tesezh\-01. |10.0.0.0/16 |
   |Next Hop type |Fixed as **IPsec\-VPN connection**. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-02 |

6. Click OK to complete the addition of the VPNGW\-02 route entry. This completes all configuration operations for the VPN Connect.

## Test connectivity

1. Log in to ECS1 within VPC1.

2. Execute the `ping` command to ping the private IP of ECS2.

   The result shown below indicates that the IPsec\-VPN connection between VPC1 and VPC2 is successfully established and communication is working normally.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/d6ca3483c8e9468ea237993b5c8da040.png)
