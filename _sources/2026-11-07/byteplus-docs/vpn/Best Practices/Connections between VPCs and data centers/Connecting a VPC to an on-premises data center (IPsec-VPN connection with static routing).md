---
title: "Connecting a VPC to an on-premises data center (IPsec-VPN connection with static routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers"
---

This topic introduces how to establish IPsec\-VPN communication tunnels in static routing mode between a Virtual Private Cloud (VPC) and multiple on\-premises data centers (IDC) using the IPsec\-VPN connection feature. These tunnels enable flexible hybrid cloud deployment solutions.

## Prerequisites

* Create VPC1 and its subnet. For proceduer, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The gateways of on\-premises IDC1 and IDC2 both have static Elastic IP Addresses (EIPs).

* The CIDR blocks of on\-premises IDC1 and IDC2 do not overlap with each other or with the private CIDR block of VPC1.

## Related information

> **tip**

> If two IDCs in the same region establish VPN connections with the cloud VPC, the operations are the same as described here.

The obtained information is shown below. VPC1 and its subnet, as well as ECS cloud servers and GPU cloud servers, are created cloud resources. The VPN gateway and customer gateway are resources to be created in subsequent operations.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26c94b51c793dbdf3572e0a8dbe62f37.png)

## Procedure

### Step 1: Create a VPN gateway

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project Project\-02 and target region China (Beijing).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type of the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method for the VPN gateway. |Subscription |
   |Name |Name of the VPN gateway. |VPNGW\-test |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Single tunnel |
   |IP address type |The IP address type used to interconnect the VPN gateway and the client. In single\-tunnel mode, only IPv4 addresses are supported. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. For single\-tunnel VPN gateways, only IPv4 addresses are supported. |IPv4 |
   |**Network Configuration** |||
   |Maximum bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |20Mbps |
   |VPC |The VPC where the VPN gateway resides. |VPC1 \| 192.168.1.0/24 |
   |Subnet |Select the subnet where the VPN gateway resides. Reserve enough IPv4 addresses in the subnet for deploying the VPN gateway. |Subnet1\|192.168.1.128/25 |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. Configuring BGP ASN for a VPN gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   |**More information** |||
   |Duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Enable automatic renewal as needed. |Disable |
   |Affiliated Project |The resource’s project is fixed to the project Project\-02 selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-02 |

5. Click **Confirm order**, and follow the console guidance to review and accept the legal terms.

6. Click Buy now to complete your purchase. Click Confirm order and follow the interface prompts to finish.

   After successfully creating the VPN gateway VPNGW\-test, the system assigns the gateway egress IP as 180.XX.XX.91.

### Step 2: Create a customer gateway

1. Log in to the Customer Gateway console.

2. In the top menu bar, select the target project Project\-02 and target region China (Beijing).

3. Click **Create Customer Gateway**.

4. Configure the customer gateway based on the table below, and click Confirm when completed.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Regions |Select the region where the customer gateway resides. The customer gateway must reside in the same region as the Virtual Private Cloud (VPC1) and the VPN gateway (VPNGW\-test). |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-01 |
   |IP Address |Type the static public IP address of the peer VPN gateway, which is the gateway’s egress IP address. |27.XX.XX.42 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Configuring BGP ASN for a customer gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   |Affiliated Project |The customer gateway's project is fixed to the project Project\-02 selected before entering the creation page. |Project\-02 |

5. Follow steps 2 to 4 to create another customer gateway CGW\-02, select region China (Beijing), and set the IP address to 22.XX.XX.8.

### Step 3: Create an IPsec\-VPN connection

1. Log in to the VPN Connection console.

2. In the top menu bar, select the target project Project\-02 and region China (Beijing).

3. Click **Create VPN Connection**.

4. Configure the IPsec\-VPN connection based on the table below, and click **Create** after completing the configuration.

   * Basic information

      |Parameter |Description |Sample value |
      |---|---|---|
      |Regions |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-01 |
      |Affiliated Project |The project of the resource. Fixed as Project\-02 selected before entering the creation page. |Project\-02 |

   * Associate resources

      |Parameter |Description |Sample value |
      |---|---|---|
      |Attach type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select VPNGW\-test created under VPC1. |VPNGW\-test |

   * Connection information

      |Parameter |Description |Sample value |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination Routing Mode |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Routing propagation mode |Select a routing propagation mode. |Static routes |
      |Customer gateway |Select the customer gateway CGW\-01. |CGW\-01 |
      |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>This information is crucial. Keep it secure. |test@123 |
      |Confirm the key |Type the Pre\-Shared Key again. |test@123 |

5. Repeat steps 2 to 4 to create IPsecVPN\-02. Select the region China (Beijing), choose VPN gateway VPNGW\-test, and set the pre\-shared key to **test@321**.

### Step 4: Configure VPN gateway routing

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project (Project\-02) and target region (China (Beijing)).

3. Click the VPN gateway name VPNGW\-test in the list to enter the details page.

4. Select the Routing information tab, then click Add route.

5. Configure the route according to the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Destination CIDR |Enter the private network segment of local IDC1. |192.168.2.0/24 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select IPsecVPN\-01. |IPsecVPN\-01 |

6. Click Confirm to add the route entry for Local IDC1 in VPNGW\-test.

7. Click Add route again, then configure route parameters according to the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Destination CIDR |Enter the private network segment of local IDC2. |192.168.3.0/24 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select IPsecVPN\-02. |IPsecVPN\-02 |

8. Click OK to add the Data Center 2 route entry for VPNGW\-test.

### Step 5: Configuring the local gateway route

The configuration method for IPsec\-VPN varies slightly among different gateway devices. Both IDC1 and IDC2 introduced here use Sangfor firewalls. Configure IDC gateway routes separately. For details, refer to [Configuring Sangfor firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall).

After completing route configuration, the VPN connection setup is finished. At this point, local IDC1 and IDC2 can connect through the IPsec tunnel to access cloud servers in VPC1.
