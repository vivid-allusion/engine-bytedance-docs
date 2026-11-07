---
title: "Building dual-tunnel VPN interconnection between VPCs (static routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Building-dual-tunnel-VPN-connectivity"
---

This topic describes how to connect two virtual private clouds (VPCs) under different accounts by using the IPsec\-VPN in dual\-tunnel static routing.

## Background

VPCs are naturally isolated. VPN Connect can build a tunnel between VPCs to enable communication. This topic uses two VPCs from different accounts as an example. For communication between VPCs under the same account, no account switch is required. Other actions remain the same as those in the current topic.

> **tip**

> To connect a VPC to a third\-party VPC through VPN, you can configure the third\-party VPC as a client when configuring a VPN Connect. For more information on the third\-party VPC configuration, see the vendor's documentation.

## Prerequisites

* Two accounts (testzh\-01 and testzh\-02) have been activated and completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923).

* You have obtained the information about testzh\-01 and testzh\-02.

* You have created VPC1 under testzh\-01 and VPC2 under testzh\-02, with non\-overlapping private CIDR blocks between the two VPCs.

## Related information

The existing deployment is illustrated in the diagram below. VPC1, VPC2, ECS1, and ECS2 represent created resources. VPN Gateway 1 and VPN Gateway 2 are resources to be created in the following steps.

> **tip**

* > The VPN Connect does not support establishing cross\-border connectivity. In the scenario where a network connection is established between VPCs via the IPsec\-VPN connection, the two interconnected VPCs must both belong to regions within China Mainland or both belong to regions outside China Mainland. It is not allowed that one VPC resides in a China Mainland region and the other resides in a region outside China Mainland. For more information, see [Regions](https://docs.byteplus.com/en/docs/vpn/Regions#YocmnS6d).

* > If you need to connect one VPC in a China Mainland region with another VPC in a region outside China Mainland, we recommend you use the Cloud Enterprise Network (CEN) service. For details, see [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/6405).

* > If you need to connect VPCs across different regions through an IPsec\-VPN connection (where VPCs are either both in China Mainland regions or both in regions outside China Mainland), the network quality of IPsec\-VPN is relatively poor due to the quality of the internet. We recommend using CEN. For procedure, see [Inter\-VPC communication across regions within the same account](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) or [Inter\-VPC communication across regions and accounts](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_930d753a6582b7fec87b792c60486649.png)

## Procedure

### Step 1: Create a VPN gateway

1. Log in to [the VPN gateway console](https://console.byteplus.com/vpn/vpnGateway) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Gateway**.

4. Configure VPN gateway parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type of the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method of the VPN gateway. |Subscription |
   |Region |Select the region where the VPN gateway is located. Keep it consistent with the region of VPC1.​ |China (Beijing) |
   |Name |The name of the VPN gateway. |VPNGW\-01 |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Dual\-tunnel |
   |IP address type |The IP address type to interconnect the VPN gateway and client. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. |IPv4 |
   |**Network configuration** |||
   |Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |5Mbps |
   |VPC |The VPC where the VPN gateway resides. |VPC1 \| 10.0.0.0/16 |
   |Primary subnet |Select the primary subnet where the VPN gateway is located. Reserve at least one IPv4 address in the subnet for deploying the VPN gateway.​ |subnet1 \| 10.0.0.0/24 \| Availability Zone A |
   |Secondary subnet |Select the subnet where the VPN gateway resides. Reserve at least one IPv4 address in the subnet for deploying the VPN gateway.​ |subnet2 \| 10.0.1.0/24 \| Availability Zone B |
   |**More information** |||
   |Purchase duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. |Disable |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-1 |
   |**Advanced options** |||
   |Tags |Set tags for the VPN gateway. Tags consist of key\-value pairs used for classification and search. This example does not use tags. |\- |

5. After the configuration is completed, click **Confirm order**, and follow the console guidance to review and accept the legal terms.

6. Click **Buy now** for payment to complete the purchase.

   After VPN gateway VPNGW\-01 is successfully created, the system assigns gateway egress IPs as 180.XX.XX.207 and 180.XX.XX.208

7. Log in to account testzh\-02 and open the [VPN gateway console](https://console.byteplus.com/vpn/vpnGateway), then follow steps 2 to 7 to create VPN gateway VPNGW\-02.

   After VPN gateway VPNGW\-02 is successfully created, the system assigns gateway egress IPs as 180.XX.XX.209 and 180.XX.XX.210

### Step 2: Create a customer gateway

1. Log in to [the Customer Gateway console](https://console.byteplus.com/vpn/vpnClient) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create Customer Gateway**.

4. To configure two customer gateways, see the table below. After completion, click **OK**.

   |Parameter |Description |Example 1 |Example 2 |
   |---|---|---|---|
   |Region |Select the region where the customer gateway resides.<br><br>Must be consistent with the regions of VPC1 and VPNGW\-01. |China (Beijing) |China (Beijing) |
   |Name |Set a name for the customer gateway. |CGW\-01 |CGW\-02 |
   |IP address |Enter the static public IP address of the peer VPN gateway. It is the gateway’s egress IP address. |180.XX.XX.209 |180.XX.XX.210 |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |Project\-1 |

5. Log in to the account testzh\-02 and open the [Customer Gateway console](https://console.byteplus.com/vpn/vpnClient). Following steps 2 to 4, create customer gateways CGW\-03 and CGW\-04, setting the **IP Address** parameters to 180.XX.XX.207 and 180.XX.XX.208.

   At this point, the relationship between the VPC, VPN gateway, and customer gateway is as shown in the table below.

   |Account |VPC name |VPN gateway |Egress IP address |Customer gateway |
   |---|---|---|---|---|
   |testzh\-01 |VPC1 |VPNGW\-01 |* Primary: 180.XX.XX.207<br><br>* Secondary: 180.XX.XX.208 |* CGW\-01<br><br>* CGW\-02 |
   |testzh\-02 |VPC2 |VPNGW\-02 |* Primary: 180.XX.XX.209<br><br>* Secondary: 180.XX.XX.210 |* CGW\-03<br><br>* CGW\-04 |

### Step 3: Create an IPsec\-VPN connection

1. Log in to [the VPN connection console](https://console.byteplus.com/vpn/vpnConnect) under testzh\-01.

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
      |Attach type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection with a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select VPNGW\-01 created under VPC1. |VPNGW\-01 |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select a routing propagation mode. |Static routing |

   * Tunnel configuration

      |Parameter |Description |Example (Tunnel1) |Example (Tunnel2) |
      |---|---|---|---|
      |Customer gateway |Select the customer gateway (CGW\-01) created under VPC1. |CGW\-01 |CGW\-02 |
      |Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. The configuration on both sides must be identical.<br><br>This information is crucial. Keep it secure. |test@123 |test@123 |
      |Confirm key |Enter Pre\-Shared Key again. |test@123 |test@123 |

5. Log in to the [IPsec-VPN connection console](https://console.byteplus.com/vpn/vpnConnect) under account testzh\-02, repeat steps 2 to 4 to create the IPsec\-VPN connection IPsecVPN\-02; set the Pre\-Shared Key consistent with IPsecVPN\-01 as test@123.

   At this point, the relationships among the VPC, VPN gateway, customer gateway, and IPsec\-VPN connection are shown in the table below:

   |Account |VPC name |VPN gateway |Egress IP address |Customer gateway |IPsec\-VPN connection |
   |---|---|---|---|---|---|
   |testzh\-01 |VPC1 |VPNGW\-01 |* Main: 180.XX.XX.207<br><br>* Secondary: 180.XX.XX.208 |* CGW\-01<br><br>* CGW\-02 |IPsecVPN\-01 |
   |testzh\-02 |VPC2 |VPNGW\-02 |* Primary: 180.XX.XX.209<br><br>* Secondary: 180.XX.XX.210 |* CGW\-03<br><br>* CGW\-04 |IPsecVPN\-02 |

### Step 4: Configure route for local VPN gateway

1. Log in to [the VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway) under testzh\-01.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click VPNGW\-01, the name of the VPN gateway, in the list.

4. Click the **Routing information** tab. On this tab, click **Add route**.

5. Configure the route details as shown in the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of VPC2. |192.168.1.0/24 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-01 |

6. Click **OK** to complete the addition of the VPNGW\-01 route entry.

### Step 5: Configure remote route

1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway) under account testzh\-02.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click the VPN gateway name VPNGW\-02 in the list.

4. Click the **Routing information** tab. On this tab, click **Add route**.

5. Configure the route details as shown in the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of VPC1 under testzh\-01. |10.0.0.0/16 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-02 |

6. Click **OK** to complete the addition of the VPNGW\-02 route entry. All VPN Connect configurations are now complete.

## Test connectivity

On the VPN gateway route list page, view the next hop of the route.

* Normally, the next hop of the VPN gateway route is the primary tunnel of the IPsec\-VPN connection.

   Run the `ping` command to verify mutual connectivity between Elastic Compute Service (ECS) instances in VPCs. Successful ping indicates that VPC1 and VPC2 can communicate properly through the primary tunnel of the IPsec\-VPN connection.

* In case of availability zone failure or unavailability of the primary tunnel's internet egress IP, the next hop of the VPN gateway route automatically switches to the secondary tunnel of the IPsec\-VPN connection.

   Run the `ping` command to verify mutual connectivity between ECS instances in VPCs. Successful ping indicates that VPC1 and VPC2 can communicate properly through the secondary tunnel of the IPsec\-VPN connection.

   * In case of failure in one availability zone, mutual connectivity remains between ECS instances in non\-failed availability zones, while ECS instances within the failed availability zone cannot communicate.

   * When the internet egress IP of the primary tunnel is unavailable, mutual connectivity remains normal between ECS instances within the availability zone where the primary and secondary tunnels are located.
