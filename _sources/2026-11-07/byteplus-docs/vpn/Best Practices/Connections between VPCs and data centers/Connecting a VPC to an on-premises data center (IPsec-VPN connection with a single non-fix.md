---
title: "Connecting a VPC to an on-premises data center (IPsec-VPN connection with a single non-fixed egress IP)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center"
---

This topic describes the configuration method for VPN Connect when an egress IP address of the on\-premises data center (IDC) gateway is non\-fixed.

> **tip**

> A non\-fixed IP refers to the possibility that the egress IP address of the customer gateway's internet egress may change each time a connection to Volcanic VPN is initiated.

## Background

Using VPN Connect to achieve network connectivity between an IDC and a Virtual Private Cloud (VPC) is a typical cloud migration scenario. This scenario generally requires the IDC to have a fixed static public IP as the egress IP address of the on\-premises gateway.

Currently, a company has an on\-premises  gateway with a non\-fixed static public IP due to its network restrictions. Considering cost, it hopes to use VPN attachment for cloud migration. This article introduces how to configure VPN attachment to achieve network connectivity under this special scenario with a non\-fixed egress IP address. For configuration operations involving multiple non\-fixed egress IPs, see [Building connectivity between VPC and data center via VPN-IPsec (multiple non-fixed egress IPs)](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center-1).

## Prerequisites

* A Virtual Private Cloud (VPC) (named VPC1) and its subnet have been created. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The IP ranges are properly planned, and the subnet of the part of the IDC to be migrated to the cloud does not overlap with the private network subnet of VPC1.

## Related information

The obtained information is shown in the figure below. VPC1, its subnet, and the Elastic Compute Service represent created cloud resources. The VPN gateway and customer gateway are resources to be created in the following operations.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a09166c31553f459f8311a4a4bd135.png)

> **tip**

> The configuration process for VPN Connect with a non\-fixed egress IP at the customer gateway is consistent with the static public IP scenario. However, parameter settings differ during the creation of the customer gateway and IPsec\-VPN connection stages and require special attention.

## Procedure

### Step 1: Create VPN gateway

1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type of the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method for the VPN gateway. |Subscription |
   |Regions |Select the region where the VPN gateway resides. The VPN gateway must reside in the same region as VPC1. |China (Beijing) |
   |Name |Name of the VPN gateway. |VPNGW\-test |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Single tunnel |
   |IP address type |The IP address type used to interconnect the VPN gateway and the client. In single\-tunnel mode, only IPv4 addresses are supported. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. For single\-tunnel VPN gateways, only IPv4 addresses are supported. |IPv4 |
   |**Network Configuration** |||
   |Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |20Mbps |
   |VPC |The VPC where the VPN gateway resides. |VPC1 \| 192.168.1.0/24 |
   |Subnet |Select the subnet where the VPN gateway resides. The subnet must reserve enough IPv4 addresses to deploy the VPN gateway. |Subnet 1\|192.168.1.128/25 |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. Configuring BGP ASN for a VPN gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   |**More information** |||
   |Duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Select whether to enable automatic renewal. |Uncheck |
   |Affiliated Project |The resource belongs to the project fixed as Project\-01, which was selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-01 |

5. Click **Confirm order**, and follow the console guidance to review and accept the legal terms.

6. Click **Buy now** for payment to complete the purchase. Click **Confirm order**, and complete the action as prompted by the interface.

   After VPNGW\-test is created, the system allocates a gateway egress IP of 101.XX.XX.58.

### Step 2: Create customer gateway

1. Log in to the [Customer Gateway console](https://console.byteplus.com/vpn/vpnClient).

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click **Create Customer Gateway**, and configure the customer gateway based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Regions |Select the region where the customer gateway resides. The customer gateway must reside in the same region as the Virtual Private Cloud (VPC1) and the VPN gateway (VPNGW\-test). |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-test |
   |IP Address |Type the static public IP address of the peer VPN gateway, which is the gateway’s egress IP address. In this scenario, the peer does not have a fixed gateway egress IP address, so it must be set to `0.0.0.0`. |0.0.0.0 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Configuring the customer gateway BGP ASN is only required when the IPsec\-VPN connection uses dynamic routing propagation mode. This demonstration uses static routing propagation mode, so no customer gateway BGP ASN configuration is needed. |\-\- |
   |Affiliated Project |The project of the customer gateway, fixed as the Project\-01 selected before entering the creation page. |Project\-01 |

5. After configuration, click **Accept**.

### Step 3: Create IPsec\-VPN connection

1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the target project Project\-01 and Region China (Beijing).

3. Click **Create VPN Connection**, and configure the IPsec\-VPN connection based on the table below.

   * Basic information

      |Parameter |Description |Sample value |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-test |
      |Affiliated Project |The project to which the resource belongs. It is fixed as Project\-02 selected before entering the creation page. |Project\-01 |

   * Associate resources

      |Parameters | |Sample value |
      |---|---|---|
      |Attach type |Select the resource type of the new IPsec\-VPN connection associated. |VPN gateway |
      |VPN gateway |Select the VPN gateway created in the previous phase. |VPNGW\-test |

   * Connection information

      |Parameter |Description |Sample value |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination Routing Mode |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration.<br><br>> **warning**<br><br><br>> In this scenario, the peer does not have a fixed gateway egress IP address, so active negotiation cannot be initiated from the cloud. Here defaults to No and cannot be modified.<br> |No |
      |Routing propagation mode |Select a routing propagation mode. |Static routes |
      |Customer gateway |Select the customer gateway created in the step of [Create customer gateway](https://docs.byteplus.com/en/docs/52/5034#.5q2l6aqk5LiA77ya5Yib5bu6VlBO572R5YWz). |CGW\-test |
      |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>This information is crucial. Keep it secure. |test@00000 |
      |Confirm the key |Type the Pre\-Shared Key again. |test@00000 |

   * Advanced configuration

      > **tip**

      > This section only shows parameters requiring special configuration; other parameters remain at their default values.

      |Parameter ||Description |Sample value |
      |---|---|---|---|
      |IKE Config |Version |IKE key exchange protocol version. In this scenario, the peer does not have a fixed gateway egress IP address. Only ikev1 can be used here. |ikev1 |
      ||Negotiation |Select the negotiation mode for IKE authentication.<br><br>> **warning**<br><br><br>> In this scenario, the peer does not have a fixed gateway egress IP address. Only aggressive can be used here.<br> |aggressive |

5. After completing the configuration, click Create.

### Step 4: Configure route for VPN gateway

1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project Project\-01 and region China (Beijing).

3. Click the VPN gateway name "VPNGW\-test" in the list.

4. Select the Routing information tab, then click Add route.

5. Configure routing according to the following table.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Destination CIDR |Type the private CIDR block of the IDC. |10.0.0.0/16 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the step of [Create IPsec-VPN connection](https://docs.byteplus.com/en/docs/52/5034#.5q2l6aqk5LiJ77ya5Yib5bu6SVBzZWPov57mjqU=). |IPsecVPN\-test |

6. Click OK to complete adding the route entry to the IDC within VPNGW\-test.

> **tip**

> If the VPC where the VPN gateway resides has a custom route table, and the subnets associated with the route table need to access the on\-premises data center (IDC) through the VPN Connect, you must manually add a route entry to the route table. Set the destination CIDR block to the on\-premises IDC CIDR block and the Next Hop type to **VPN gateway**. For procedure, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH).

### Step 5: Configur on\-premises route and initiate connection

1. Download the IPsec configuration file.

   1. Log in to the VPN Connection console, select the IPsec\-VPN connection in China (Beijing) and under Project\-01.

   2. In the IPsec\-VPN connection list, check the IPsec\-VPN connection created in [Create IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center#.5q2l6aqk5LiJ77ya5Yib5bu6SVBzZWPov57mjqU=).

   3. Click Download IPsec Config.

   4. Click Download.

2. Configure on\-premises gateway routing based on the downloaded IPsec configuration file, ensuring identical IPsec settings on both sides. For details, see [File transfer overview](https://docs.byteplus.com/en/docs/vpn/Overview-1).

3. Initiate the connection from the IDC. The scenarios in this article are applicable when the peer has no fixed gateway egress IP address, and a connection cannot be initiated from the VPC. After all configurations are complete, the negotiation request must be initiated from the IDC.

   > **tip**

   > If any IPsec connection disconnects later, the negotiation request must still be initiated from the IDC.
