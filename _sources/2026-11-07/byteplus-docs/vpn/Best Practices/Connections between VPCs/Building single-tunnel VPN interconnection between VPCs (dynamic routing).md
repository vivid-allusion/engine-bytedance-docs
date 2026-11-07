---
title: "Building single-tunnel VPN interconnection between VPCs (dynamic routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/connecting_vpcs_bgp_routing"
---

This topic describes how to achieve network connectivity between two Virtual Private Clouds (VPCs) under different accounts through an IPsec\-VPN connection using dynamic routing mode.

## Background

VPCs are naturally isolated. VPN Connect can build a tunnel between VPCs to enable communication. This topic uses two VPCs from different accounts as an example. For communication between VPCs under the same account, no account switch is required. Other actions remain the same as those in the current topic.

> **tip**

> To connect a VPC to a third\-party VPC through VPN, you can configure the third\-party VPC as a client when configuring a VPN link. For more information on the third\-party VPC configuration, see the vendor's documentation.

## Prerequisites

* The peer gateway must support the BGP routing protocol.

* You have activated accounts tesezh\-01 and tesezh\-02 and completed real\-name authentication.

* Get account information about tesezh\-01 and tesezh\-02.

* Create VPC1 under tesezh\-01 and VPC2 under tesezh\-02, with non\-overlapping private CIDR blocks between the two VPCs.

## Related information

The existing deployment is illustrated in the diagram below. VPC1, VPC2, ECS1, and ECS2 represent created resources. VPN Gateway 1 and VPN Gateway 2 are resources to be created in the following steps.

> **tip**

* > The VPN link does not support establishing cross\-border connectivity. In the scenario where a network connection is established between VPCs via the IPsec\-VPN connection, the two interconnected VPCs must both belong to regions within China Mainland or both belong to regions outside China Mainland. It is not allowed that one VPC resides in a China Mainland region and the other resides in a region outside China Mainland. For more information, see [Regions](https://docs.byteplus.com/en/docs/vpn/Regions).

* > If you need to connect one VPC in a China Mainland region with another VPC in a region outside China Mainland, we recommend you use the Cloud Enterprise Network (CEN) service. For details, see [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/6405).

* > If you need to connect VPCs across different regions through an IPsec\-VPN connection (where VPCs are either both in China Mainland regions or both in regions outside China Mainland), the network quality of IPsec\-VPN is relatively poor due to the quality of the internet. We recommend using CEN. For procedure, see [VPC interconnection (same account, cross\-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) or [VPC interconnection (cross\-account and cross\-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8495c5af3054fff4bff3f2c2044862df.png)

## Procedure

### Step 1: Create VPN gateway

1. Log in to the VPN Gateway console using tesezh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

5. Click **Buy now** for payment to complete the purchase.

6. Log in to the VPN Gateway console using the tesezh\-02 account, and follow steps 2 to 7 to create VPN gateway VPNGW\-02, with a BGP ASN of 6000.

   After VPN gateway VPNGW\-02 is successfully created, the system assigns the gateway egress IP as 180.XX.XX.209.

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
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway.<br><br><br>* The valid range of the BGP ASN is 1 to 4294967294 for the customer gateway. The values 137718, 65535, and 150436 are not available.​<br><br>* The BGP ASN of the customer gateway must not be the same as that of the VPN gateway. |6000 |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

5. Log in to the Customer Gateway console under the account tesezh\-02, follow Step 2 to Step 4 to create the customer gateway CGW\-02, and configure the IP address as 180.XX.XX.207 and the BGP ASN as 65500.

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
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select the VPN gateway (VPNGW\-01) created under VPC1. |VPNGW\-01 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Dynamic routing |
      |Customer gateway |Select the customer gateway (CGW\-01) created under VPC1. |CGW\-01 |
      |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* It must be within `169.254.0.0/16`.<br><br>* Its subnet mask must be `/30`.<br><br>* It must not be within `169.254.255.0/24`. |169.254.1.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |
      |Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. The configuration on both sides must be identical.<br><br>This information is crucial. Keep it secure. |test@123 |
      |Confirm key |Enter Pre\-Shared Key again. |test@123 |

5. Log in to the VPN Connection console under Account tesezh\-02, repeat steps 2 to 4, create the IPsec\-VPN connection: IPsecVPN\-02, with the Pre\-Shared Key consistent with IPsecVPN\-01, all settings to test@123.

   * Basic information

      |Parameter |Description |Example |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |The name of the IPsec\-VPN connection. |IPsecVPN\-02 |
      |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

   * Associate resources

      |Parameter |Description |Example |
      |---|---|---|
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select the VPN gateway (VPNGW\-01) created under VPC1. |VPNGW\-02 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Dynamic routing |
      |Customer gateway |Select the customer gateway (CGW\-01) created under VPC1. |CGW\-02 |
      |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. The tunnel CIDR block of IPsecVPN\-02 must be the same as that of IPsecVPN\-01.​ |169.254.1.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. The local tunnel IP of IPsecVPN\-02 is the remote tunnel IP of IPsecVPN\-01. |169.254.1.2 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. The peer tunnel IP of IPsecVPN\-02 is the local tunnel IP of IPsecVPN\-01. |169.254.1.1 |
      |Pre\-shared key |Enter the key used for IKE negotiation between VPN devices on both sides. IPsecVPN\-02 must use the same Pre\-Shared Key as IPsecVPN\-01. |test@123 |
      |Confirm key |Enter Pre\-Shared Key again. |test@123 |

   At this point, the relationship between the Virtual Private Cloud (VPC), VPN gateway, customer gateway, and IPsec\-VPN connection is as shown in the table below.

   |Account |VPC name |VPN gateway |Egress IP address |Customer gateway |IPsec\-VPN connection |
   |---|---|---|---|---|---|
   |tesezh\-01 |VPC1 |VPNGW\-01 |180.XX.XX.207 |CGW\-01 |IPsecVPN\-01 |
   |tesezh\-02 |VPC2 |VPNGW\-02 |180.XX.XX.209 |CGW\-02 |IPsecVPN\-02 |

## Test connectivity

1. Log in to the Elastic Compute Service (ECS1) within VPC1.

2. Run the `ping` command to ping the private IP address of ECS2.

   The result shown below indicates that the IPsec\-VPN connection between VPC1 and VPC2 is successfully established and communication is normal.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/d6ca3483c8e9468ea237993b5c8da040.png)
