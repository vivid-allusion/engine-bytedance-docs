---
title: "Connecting a VPC to an on-premises data center (IPsec-VPN connection with dynamic routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/connecting-a-vpc-to-multiple-data-centers-bgp-routing"
---

This topic describes how to create IPsec\-VPN tunnels in dynamic route mode between a Virtual Private Cloud (VPC) and multiple on\-premises data centers (IDCs). These tunnels enable flexible hybrid cloud deployment solutions.

## Prerequisites

* The VPC1 and its subnets have been created. For details, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The gateways of IDC1 and IDC2 have static Elastic IP Address (EIP) addresses and support BGP routing protocol.

* The CIDR blocks of IDC1 and IDC2 do not overlap with each other or with the private CIDR block of VPC1.

## Related information

> **tip**

> If two data centers in the same region establish VPN connections with a cloud VPC, the procedure is the same as described here.

The obtained information is shown as below. VPC1, its subnets, Elastic Compute Service (ECS), and GPU ECS are existing cloud resources. The VPN gateway and customer gateway are resources to be created in the following operations.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e531aa8a9d76775f6ae55d90be3aeeeb.png)

## Procedure

### Step 1: Create a VPN gateway

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project: Project\-02 and region: China (Beijing).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

|Parameters |Description |Sample value |
|---|---|---|
|**Basic information** |||
|Billing method |The billing method for the VPN gateway. |Subscription |
|Regions |Select the region where the VPN gateway resides. The VPN gateway must reside in the same region as VPC1. |China (Beijing) |
|Name |Name of the VPN gateway. |VPNGW\-test |
|Tunnel mode |The tunnel mode of the VPN gateway. |Single tunnel |
|**Network Configuration** |||
|Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. |20Mbps |
|Virtual Private Cloud (VPC) |The Virtual Private Cloud (VPC) where the VPN gateway resides. |VPC1 \| 192.168.1.0/24 |
|Subnet |Select the subnet where the VPN gateway resides. The subnet must reserve enough IPv4 addresses to deploy the VPN gateway. |Subnet1\|192.168.1.128/25 |
|BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway.<br><br><br>* Valid ranges of BGP ASN: 64512 to 65534 and 4200000000 to 4294967294.<br><br>* The VPN gateway BGP ASN must not duplicate the customer gateway BGP ASN. |65000 |
|**Function configuration** |||
|IPsec\-VPN capability |Enable VPN connection as needed. After enabling, you can use the IPsec\-VPN feature and can enable SSL connectivity concurrently. |Check |
|SSL\-VPN capability |Enable SSL connection as needed. After enabling, you can use the SSL\-VPN feature and enable IPsec connectivity concurrently. |Disabled |
|**More information** |||
|Duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
|Automatic renewal |Enable automatic renewal as needed. |Disable |
|Affiliated Project |The project to which the resource belongs. It is fixed as the project Project\-02 selected before entering the creation page. Cloud resources cannot be shared between different projects. |Project\-02 |

4. After the configuration is completed, click **Confirm order**, and follow the console guidance to review and accept the Legal.

5. Click **Buy now** for payment to complete the purchase.

   After creating VPN gateway VPNGW\-test successfully, the system allocates the gateway egress IP as 180.XX.XX.91.

### Step 2: Create a customer gateway

1. Log in to the Customer Gateway console.

2. In the top menu bar, select the target project: Project\-02 and region: China (Beijing).

3. Click **Create Customer Gateway**.

4. Configure the customer gateway based on the table below, and click Confirm when completed.

   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select the region where the customer gateway resides. It must match the region of VPC1 and the VPN gateway (VPNGW\-test). |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-01 |
   |IP address |Enter the egress IP address of the peer VPN gateway. |27.XX.XX.42 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Configuring BGP ASN for a customer gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required.<br><br><br>* The valid range for the customer gateway BGP ASN is 1 to 4294967294, excluding 137718, 65535, and 150436.<br><br>* The customer gateway BGP ASN must not duplicate the VPN gateway BGP ASN or any other customer gateway BGP ASN. |64001 |
   |Affiliated project |The project to which the customer gateway belongs. It is fixed as Project\-02 that is selected before entering the creation page. |Project\-02 |

5. Follow steps 2 to 4 to create another customer gateway CGW\-02. Select China (Beijing), set the IP address to 22.XX.XX.8, and set the BGP ASN to 64002.

### Step 3: Create an IPsec\-VPN connection

1. Log in to the VPN Connection console.

2. In the top menu bar, select the target project: Project\-02 and region: China (Beijing).

3. Click **Create VPN Connection**.

4. Configure the IPsec\-VPN connection based on the table below, and click **Create** after completing the configuration.

   * Basic information

      |Parameter |Description |Example |
      |---|---|---|
      |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
      |Name |The name of the IPsec\-VPN connection. |IPsecVPN\-01 |
      |Affiliated project |The project to which the resource belongs. It is fixed as Project\-02 that is selected before entering the creation page. |Project\-02 |

   * Associate resources

      |Parameter |Description |Example |
      |---|---|---|
      |Attach type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
      |VPN gateway |Select the VPN gateway (VPNGW\-test) created under VPC1. |VPNGW\-test |

   * Connection information

      |Parameter |Description |Example |
      |---|---|---|
      |Routing mode |Select a routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Routing propagation mode |Select a routing propagation mode. |Dynamic routing |
      |Customer gateway |Select the customer gateway (CGW\-01). |CGW\-01 |
      |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* It must be within `169.254.0.0/16`.<br><br>* Its subnet mask must be `/30`.<br><br>* It must not be within `169.254.255.0/24`. |169.254.1.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |
      |Pre\-Shared Key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>This information is crucial. Keep it secure. |test@123 |
      |Confirm key |Enter the Pre\-Shared Key again. |test@123 |

5. Repeat steps 2 to 4 to create IPsecVPN\-02, with the connection information parameters as below. Other configurations remain the same as IPsecVPN\-01.

   |Parameter |Description |Example |
   |---|---|---|
   |Customer gateway |Select the customer gateway (CGW\-02). |CGW\-02 |
   |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. |169.254.2.0/30 |
   |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.2.1 |
   |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.2.2 |

### Step 4: Configure routing for on\-premises gateway

After completing the IPsec configuration, you can [download the IPsec-VPN connection configuration](https://docs.byteplus.com/en/docs/vpn/Downloading-IPsec-VPN-connection-configurations) and add the VPN configuration separately on the gateway devices of IDC1 and IDC2. The operation method for different devices is slightly different. Both IDC1 and IDC2 introduced in this document use the Sangfor firewall. Please refer to Configuring the Sangfor firewall for specific operations.

Once the VPN configuration is added and the IPsec\-VPN connection is successfully established, route between VPC1 and IDC1 and IDC2 will be automatically propagated through the BGP route protocol. At this point, local IDC1 and IDC2 can access cloud servers in VPC1 via the IPsec VPN tunnel.
