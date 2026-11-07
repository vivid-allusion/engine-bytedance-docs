---
title: "Building dual-tunnel VPN interconnection between VPCs (dynamic routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Build-dual-tunnel-VPN-dynamic-routing"
---

By default, Virtual Private Clouds (VPCs) operate in complete logical isolation. To establish network connectivity between two VPCs, you can build communication tunnels between them via VPN Connect. This topic describes how to achieve network connectivity between two VPCs under separate accounts with an IPsec\-VPN connection using dual\-tunnel dynamic routing. Communication between VPCs under the same account does not require switching accounts to log in. All other steps are the same as communication between two VPCs under separate accounts.

> tip

> To connect a VPC to a third\-party VPC through VPN, you can configure the third\-party VPC as a client when configuring a VPN link. For more information on the third\-party VPC configuration, see the vendor's documentation.

## Background

* The VPN link does not support establishing cross\-border connectivity. In the scenario where a network connection is established between VPCs via the IPsec\-VPN connection, the two interconnected VPCs must both belong to regions within China Mainland or both belong to regions outside China Mainland. It is not allowed that one VPC resides in a China Mainland region and the other resides in a region outside China Mainland. For more information, see [Regions](https://docs.byteplus.com/en/docs/vpn/Regions#YocmnS6d).

* If you need to connect one VPC in a China Mainland region with another VPC in a region outside China Mainland, we recommend you use the Cloud Enterprise Network (CEN) service. For details, see [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/6405).

* If you need to connect VPCs across different regions through an IPsec\-VPN connection (where VPCs are either both in China Mainland regions or both in regions outside China Mainland), the network quality of IPsec\-VPN is relatively poor due to the quality of the internet. We recommend using CEN. For procedure, see [Inter-VPC communication across regions within the same account](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) or [Inter-VPC communication across regions and accounts](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).

The existing deployment is illustrated in the diagram below. VPC1, VPC2, ECS1, and ECS2 represent created resources. VPN Gateway 1 and VPN Gateway 2 are resources to be created in the following steps.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_674948f94a1f29f66f27ffda7cdd09ce.png)

**Network planning**

|Account |VPC name |VPC CIDR |VPN gateway |Egress IP address |Customer gateway |
|---|---|---|---|---|---|
|testzh\-01 |VPC1 |10.0.0.0/16 |VPNGW\-01<br><br>BGP ASN: 65500 |**VPNGW\-01**<br><br><br>* Primary tunnel: 180.XX.XX.207<br><br>* Secondary tunnel: 180.XX.XX.208 |* CGW\-01<br><br><br>BGP ASN: 65511<br><br><br>* CGW\-02<br><br><br>BGP ASN: 65511 |
|testzh\-02 |VPC2 |192.168.1.0/24 |VPNGW\-02<br><br>BGP ASN: 65511 |* Primary tunnel: 180.XX.XX.209<br><br>* Secondary tunnel: 180.XX.XX.210 |* CGW\-03<br><br><br>BGP ASN: 65500<br><br><br>* CGW\-04<br><br><br>BGP ASN: 65500 |

|Tunnel |Tunnel CIDR |Local Tunnel IP |Peer Tunnel IP |
|---|---|---|---|
|Primary tunnel |169.254.1.0/30 |169.254.1.1 |169.254.1.2 |
|Secondary tunnel |169.254.2.0/30 |169.254.2.1 |169.254.2.2 |

## Prerequisites

* Two accounts (testzh\-01 and testzh\-02) have been activated and completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923).

* You have obtained the information about testzh\-01 and testzh\-02.

* You have created VPC1 under testzh\-01 and VPC2 under testzh\-02, with non\-overlapping private CIDR blocks between the two VPCs.

## Procedure

### Step 1: Create a VPN gateway

1. Log in to [the VPN gateway console](https://console.byteplus.com/vpn/vpnGateway) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Gateway**.

4. Create a VPN gateway  **(VPNGW\-01)**  for VPC1 based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type of the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method of the VPN gateway. |Subscription |
   |Region |Select the region where the VPN gateway resides. It must be the same region as VPC1. |China (Beijing) |
   |Name |The name of the VPN gateway. |VPNGW\-01 |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Dual\-tunnel |
   |IP address type |The IP address type to interconnect the VPN gateway and client. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. |IPv4 |
   |**Network configuration** |||
   |Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |5Mbps |
   |VPC |The VPC where the VPN gateway resides. |VPC1 \| 10.0.0.0/16 |
   |Primary subnet |Select the primary subnet where the VPN gateway is located. Reserve at least one IPv4 address in the subnet for deploying the VPN gateway.​ |subnet1 \| 10.0.0.0/24 \| Availability Zone A |
   |Secondary subnet |Select the subnet where the VPN gateway resides. Reserve at least one IPv4 address in the subnet for deploying the VPN gateway.​ |subnet2 \| 10.0.1.0/24 \| Availability Zone B |
   |BGP ASN |Set the Autonomous System Number (ASN) of the VPN gateway.<br><br><br>* Valid ranges of BGP ASN: 64512 to 65534 and 4200000000 to 4294967294.<br><br>* The BGP ASN of the VPN gateway must not be the same as that of the customer gateway. |65500 |
   |**More information** |||
   |Purchase duration |The validity period for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. |Disable |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-1 |
   |**Advanced options** |||
   |Tags |Set tags for the VPN gateway. Tags consist of key\-value pairs used for classification and search. This example does not use tags. |\- |

5. After the configuration is completed, click **Confirm order**, and follow the console guidance to review and accept the Legal.

6. Click **Buy now** for payment to complete the purchase.

   After creation, the system assigns egress IP addresses (180.XX.XX.207 and 180.XX.XX.208) to **VPNGW\-01**.

7. Log in to [the VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway) under testzh\-02, repeat steps 2\-7 to create another VPN gateway  **(VPNGW\-02)**  with BGP ASN set to **65511**.

   After creation, the system assigns egress IP addresses (180.XX.XX.209 and 180.XX.XX.210) to **VPNGW\-02**.

### Step 2: Create a customer gateway

1. Log in to [the Customer Gateway console](https://console.byteplus.com/vpn/vpnClient) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create Customer Gateway**.

4. Configure two customer gateways (CGW\-01 and CGW\-02) for **VPNGW\-01** based on the table below, then click **OK**.

   |Parameter |Description |Example 1 |Example 2 |
   |---|---|---|---|
   |Region |Select the region where the customer gateway resides.<br><br>Must be consistent with the regions of VPC1 and VPNGW\-01. |China (Beijing) |China (Beijing) |
   |Name |Set a name for the customer gateway. |CGW\-01 |CGW\-02 |
   |IP address |Enter the static public IP address of the peer VPN gateway. It is the gateway’s egress IP address. |180.XX.XX.209 |180.XX.XX.210 |
   |BGP ASN |Set the ASN for the customer gateway, which must match the ASN of the peer VPN gateway. |65511 |65511 |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |Project\-1 |

5. Log in to [the Customer Gateway console](https://console.byteplus.com/vpn/vpnClient) under testzh\-02, repeat steps 2\-4 to configure two customer gateways (CGW\-03 and CGW\-04) for **VPNGW\-02**, setting **BGP ASN** to **65500, with IP addresses ** 180.XX.XX.207 and 180.XX.XX.208 respectively.

### Step 3: Create an IPsec\-VPN connection

1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect) under testzh\-01.

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
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated. |VPN gateway |
      |VPN gateway |Select VPNGW\-01 created in VPC1. |VPNGW\-01 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Dynamic routing |

   * Tunnel configuration

      |Parameter |Description |Example (Tunnel1) |Example (Tunnel2) |
      |---|---|---|---|
      |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* It must be within `169.254.0.0/16`.<br><br>* Its subnet mask must be `/30`.<br><br>* It must not be within `169.254.255.0/24`. |169.254.1.0/30 |169.254.2.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |169.254.2.1 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |169.254.2.2 |
      |Customer gateway |Select the customer gateway created under VPC1. |CGW\-01 |CGW\-02 |
      |Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. The configuration on both sides must be identical.<br><br>This information is crucial. Keep it secure. |test@123 |test@123 |
      |Confirm key |Enter Pre\-Shared Key again. |test@123 |test@123 |

5. Log in to [the VPN connection console](https://console.byteplus.com/vpn/vpnConnect) under testzh\-02. Repeat steps 1\-3 to configure the IPsec\-VPN connection, and then click **Create**.

   * Basic information

      |Parameter |Description |Example |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |The name of the IPsec\-VPN connection. |IPsecVPN\-02 |
      |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

   * Associate resources

      |Parameter |Description |Example |
      |---|---|---|
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated. |VPN gateway |
      |VPN gateway |Select VPNGW\-02 created under VPC2. |VPNGW\-02 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Dynamic routing |

   * Tunnel configuration

      |Parameter |Description |Example (Tunnel1) |Example (Tunnel2) |
      |---|---|---|---|
      |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* It must be within `169.254.0.0/16`.<br><br>* Its subnet mask must be `/30`.<br><br>* It must not be within `169.254.255.0/24`. |169.254.1.0/30 |169.254.2.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.2 |169.254.2.2 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.1 |169.254.2.1 |
      |Customer gateway |Select the customer gateway created under VPC2. |CGW\-03 |CGW\-04 |
      |Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. The configuration on both sides must be identical.<br><br>This information is crucial. Keep it secure. |test@123 |test@123 |
      |Confirm key |Enter Pre\-Shared Key again. |test@123 |test@123 |

### Step 4: View VPN gateway routes

1. Log in to [the VPN gateway console](https://console.byteplus.com/vpn/vpnGateway) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click the name of the VPN gateway  **(VPNGW\-01)** .

4. Click the **Routing information** tab to view VPN gateway routes.

After the BGP session is established, the VPN gateway  **(VPNGW\-01)**  automatically learns the BGP routes announced by the peer VPN gateway  **(VPNGW\-02)** , and publishes them as system routes into all route tables (system and custom route tables) of **VPNGW\-01**'s host VPC (VPC1). Now, you can proceed to test connectivity.

If no relevant routes are displayed, it means the establishment of the dual\-tunnel VPN link failed. Check your network planning and reconfigure.

## Test connectivity

On the VPN gateway route list page, view the next hop of the route.

* Normally, the next hop of the VPN gateway route is the primary tunnel of the IPsec\-VPN connection.

   Run the `ping` command to verify mutual connectivity between Elastic Compute Service (ECS) instances in VPCs. Successful ping indicates that VPC1 and VPC2 can communicate properly through the primary tunnel of the IPsec\-VPN connection.

* In case of availability zone failure or unavailability of the primary tunnel's internet egress IP, the next hop of the VPN gateway route automatically switches to the secondary tunnel of the IPsec\-VPN connection.

   Run the `ping` command to verify mutual connectivity between ECS instances in VPCs. A successful ping indicates that VPC1 and VPC2 can communicate properly through the secondary tunnel of the IPsec\-VPN connection.

   * In case of failure in one availability zone, mutual connectivity remains between ECS instances in non\-failed availability zones, while ECS instances within the failed availability zone cannot communicate.

   * When the internet egress IP of the primary tunnel is unavailable, mutual connectivity remains normal between ECS instances within the availability zone where the primary and secondary tunnels are located.
