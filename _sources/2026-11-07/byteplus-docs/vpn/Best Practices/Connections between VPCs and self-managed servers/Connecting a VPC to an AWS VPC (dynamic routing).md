---
title: "Connecting a VPC to an AWS VPC (dynamic routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-VPC-to-AWS-VPC-Dynamic-Route"
---

This topic introduces how to establish a private network access tunnel between BytePlus and AWS VPC through the dynamic route feature of the BytePlus VPN Connect.

## Prerequisites

* You have activated your account and completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923). Ensure that the available balance in your account is sufficient to purchase Elastic Compute Service (ECS), VPN Connect, and other related resources.

* A Virtual Private Cloud (VPC) named VPC\-01 (CIDR: 192.168.0.0/16) and its subnet have been created. An ECS instance with an IP address of 192.168.2.88 has been created in one of the subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

* VPC\-02 (CIDR block: 172.31.0.0/16) and a public subnet have been created on AWS. An EC2 instance (if using CentOS, subscribe in Marketplace in advance) has been launched in the public subnet to simulate a business server. The EC2 private IP address is 172.31.16.111. For details, refer to AWS official documentation [Get started with Amazon EC2](https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/EC2_GetStarted.html).

## Limits

* The CIDR blocks between the BytePlus VPC and the AWS VPC being connected must not overlap.

* The dynamic route feature of BytePlus VPN connection must be enabled.

* The ASN of the BytePlus VPN gateway must not be the same as the ASN of the AWS virtual private gateway.

* The tunnel CIDR block of the BytePlus IPsec\-VPN connection must be in the same CIDR block as the ASN VPN connection's IPv4 CIDR block.

## Instructions

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df46d3f6c4dccf6bc99b663d62832a90.png)

|Resource ownership |VPC information |Instance information |Tunnel CIDR |Tunnel IP |ASN |
|---|---|---|---|---|---|
|BytePlus |VPC\-01 (CIDR: 192.168.0.0/16) |ECS IP address: 192.168.2.88 |169.254.1.0/30 |169.254.1.1 |65501 |
|AWS |VPC\-02 (CIDR: 172.31.0.0/16) |EC2 IP address: 172.31.16.111 |169.254.1.0/30 |169.254.1.2 |65502 |

## Procedure

### Step 1: Create a VPN gateway under a VPC

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

5. Click **Buy now** for payment to complete the purchase. After VPNGW\-Volcano is created successfully, the system assigns the gateway egress IP as `180.XX.XX.109`.

### Step 2: Create VPN resources on the AWS side

The following operations need to be performed in the AWS console. The related configurations here are for reference only. For detailed configurations and descriptions, please refer to the official AWS website. Contact AWS support for any questions.

1. Create a customer gateway.

   Log in to the [VPN console](https://console.aws.amazon.com/vpc/) using your AWS account to create a customer gateway.

   The customer gateway on the AWS side refers to the BytePlus VPN gateway; creating an AWS customer gateway is effectively registering the BytePlus VPN gateway information with AWS. After creation, the customer gateway ID is: **cgw\-s01kd\*\*\*\*3m**.

   |Parameter |Description |Example |
   |---|---|---|
   |Name tag |Enter the name of the customer gateway. |Volcano\-Gateway |
   |BGP ASN |The Border Gateway Protocol (BGP) Autonomous System Number (ASN) of the customer gateway, i.e., the BGP ASN of the VPN gateway. |65501 |
   |IP address |The static Internet\-routable IP address of the customer gateway device. It is the egress IP address of the VPN gateway. |180.XX.XX.109 |

2. Create a virtual private gateway.

   The virtual private gateway on the AWS side serves as the egress gateway for the AWS VPC. After creation, the virtual private gateway ID is: **vgw\-e2fje\*\*\*\*f9**.

   |Parameter |Description |Example |
   |---|---|---|
   |Name tag |The name of the virtual private gateway. |AWS\-toVolcano |
   |Autonomous System Number (ASN) |The ASN of the virtual private gateway on the AWS side. |65502 |

3. Associate the virtual private gateway with the VPC.

   After creating the virtual private gateway, associate it with the VPC you need to communicate with. Select the created Virtual Private Gateway Volcano\-Gateway, then proceed to select Actions \> Attach to VPC. From Available VPCs, select the VPC to connect to (in this example, VPC\-02).

4. Create VPN Connect.

   The VPN Connect links the customer gateway and the virtual private gateway.

   > **tip**

   > As the VPN connection does not support dual tunnel mode, only one tunnel needs to be configured on the AWS side.

   |Parameter |Description |Example |
   |---|---|---|
   |Name tag |The name of the VPN Connect. |AWS\-connection |
   |Target gateway type |Select the target gateway type. In this example, select Virtual private gateway. |Virtual private gateway |
   |Virtual private gateway |Select the ID of the created virtual private gateway (AWS\-toVolcano). |vgw\-e2fje\*\*\*\*f9 |
   |Customer gateway |Select the customer gateway. |Existing |
   |Customer gateway ID |Select the ID of the created customer gateway (Volcano\-Gateway). |cgw\-s01kd\*\*\*\*3m |
   |Route options |Select the route type of the VPN Connect. In this example, select Dynamic routing. |Dynamic (requires BGP) |
   |Local IPv4 Network CIDR |The CIDR block on the cloud side that is allowed to be accessed through the VPN Connect. |192.168.0.0/16 |
   |Remote IPv4 Network CIDR |The CIDR block on the AWS side that is allowed to be accessed through the VPN Connect. |172.31.0.0/16 |
   |IPv4 for tunnel inside IP version (Tunnel IPv4 CIDR) |The tunnel CIDR block of the VPN Connect. |169.254.1.0/30 |
   |IKE versions |IKE version. |ikev2 |
   |Pre\-shared key (PSK) |Pre\-Shared Key. |test@123 |

5. Download the configuration file.

   After the VPN connection configuration is completed, download the configuration file to create an IPsec\-VPN connection. Ensure the AWS side VPN connection matches the BytePlus side IPsec\-VPN connection in IKE Config, DPD, IPsec Config, and others. For detailed steps, see the AWS guide: [Download config file](https://docs.aws.amazon.com/zh_cn/vpn/latest/s2svpn/SetUpVPNConnections.html#vpn-download-config).

   In the config file, the Virtual Private Gateway under Outside IP Addresses is the AWS\-side external IP address. In this example, it is `3.XX.XX.32`.

6. Configure route.

   Enable route propagation for the virtual private gateway in the route table associated with the VPC.

### Step 3: Create a customer gateway

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create Customer Gateway**.

4. Configure the customer gateway based on the table below, and click Confirm when completed.

   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select the region where the customer gateway is located. |China (Beijing) |
   |Name |Set a name for the customer gateway. |AWS\-Gateway |
   |IP address |Enter the public IP address of the peer VPN gateway. This is the external IP address on the AWS side. |3.XX.XX.32 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway, which is the BGP ASN of the AWS virtual private gateway.<br><br><br>* The valid range for the customer gateway BGP ASN is: 1 to 4294967294. The values 137718, 65535, and 150436 are unavailable.<br><br>* The customer gateway BGP ASN must not duplicate the VPN gateway BGP ASN. |65502 |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |

### Step 4: Create an IPsec\-VPN connection

1. Log in to the VPN gateway console.

2. In the top menu bar, select the target project (Project\-1) and region (China (Beijing)).

3. Click **Create VPN Connection**.

4. Configure the IPsec\-VPN connection based on the table below, and click **Create** after completing the configuration. DPD, IKE Config, and IPsec Config must match the VPN connection settings on the AWS side.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
   |Name |The name of the IPsec\-VPN connection. |Volcano\-connection |
   |Affiliated project |The project to which the resource belongs. It is fixed as Project\-1 that is selected before entering the creation page. |Project\-1 |
   |**Associate resource** |||
   |Attach type |Select the resource type of the new IPsec\-VPN connection associated. |VPN gateway |
   |VPN gateway |Select VPNGW\-Volcano created in [Step 1: Create VPN gateway in VPC](https://docs.byteplus.com/en/docs/52/80548#.5q2l6aqk5LiA77ya5Zyo54Gr5bGx5byV5pOO5L6nVlBD5LiL5Yib5bu6VlBO572R5YWz). |VPNGW\-Volcano |
   |**Connection information** |||
   |Routing mode |Select a routing mode. |Destination routing |
   |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
   |Route propagation mode |Select a routing propagation mode. |Dynamic routing |
   |Customer gateway |Select the customer gateway created in [Step 3: Create customer gateway](https://docs.byteplus.com/en/docs/vpn/Connecting-a-VPC-to-AWS-VPC-Dynamic-Route#.5q2l6aqk5LiJ77ya5Zyo54Gr5bGx5byV5pOO5L6n5Yib5bu655So5oi3572R5YWz). |AWS\-Gateway |
   |Tunnel CIDR |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* It must be within `169.254.0.0/16`.<br><br>* Its subnet mask must be `/30`.<br><br>* It must not be within `169.254.255.0/24`. |169.254.1.0/30 |
   |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. It must be in the same CIDR block as the peer tunnel IP.​ |169.254.1.1 |
   |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. It must be in the same CIDR block as the local tunnel IP.​ |169.254.1.2 |
   |Pre\-shared key |Enter the key for IKE negotiation between the two VPN devices. See the configuration file downloaded in the AWS guide. Keep it consistent with the **Pre\-Shared Key** in the file.​ |test@123 |
   |Confirm key |Enter Pre\-Shared Key again. |test@123 |

## Test connectivity

After the configuration is complete, the IPsec\-VPN connection between the VPC and the AWS VPC is successfully established, and the network connectivity must be tested.

1. Log in to the ECS under VPC01 (IP address is 192.168.2.88). For specific actions, refer to Log in to ECS.

2. In the ECS instance, execute the command ping 172.31.16.111 (172.31.16.111 is the IP address of the EC2 instance under the AWS interconnected VPC). If a normal response is received from AWS EC2, it indicates that the communication is normal, and the network between VPC01 and AWS VPC02 is connected.
