---
title: "SSL-VPN quick start"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Quick-start-1"
---

SSL\-VPN enables remote client access to a Virtual Private Cloud (VPC) by establishing a secure encrypted tunnel between the client and the VPC. This allows users to securely access services deployed in the VPC from their on\-premises networks.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Due to business development, a company expected to access purchased services in its VPC (VPC2) from the on\-premises client. After comprehensive consideration, the company chose the SSL\-VPN connection feature for its simple operation and flexible use. Its SSL VPN client could intercommunicate with its VPC anytime anywhere by just loading a certificate into the SSL VPN client and initiating a connection. Taking this scenario as an example, this section describes how to configure Linux, Mac, and Windows clients to establish an encrypted tunnel via SSL\-VPN connection.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da8d07426be72eb2c1802b71bff1199a.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have activated a cloud account and completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923) before purchasing VPN\-related resources.

* You have created VPC2 and its subnets in China (Beijing). For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have ensured the security group rules used by Elastic Compute Service (ECS) instances in VPC2 allow clients to access resources within VPC2. For procedures, see [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) and [Adding a security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* The client must have normal internet access.

* The CIDR block for an SSL VPN client configured on an SSL VPN server must not conflict with the VPN gateway route.

* The CIDR block for an SSL VPN client configured on an SSL VPN server must not overlap with that of the SSL VPN server to be accessed.

* The CIDR block for an SSL VPN client configured on an SSL VPN server must not conflict with route entries in the route table of the subnet associated with the VPN gateway.

* The CIDR block for an SSL VPN client configured on an SSL VPN server must not overlap with `100.64.0.0/10`, `169.254.0.0/16`, or `127.0.0.0/8`.


<span id=".5pON5L2c5rWB56iL"></span>
## Procedure


1. [Create a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-1): Create a VPN gateway necessary for an SSL\-VPN connection on VPC2 and enable SSL connection.

2. [Create an SSL VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server): Create an SSL VPN server and specify the private CIDR block to be accessed and the CIDR block to be used by the client.

3. [Create an SSL VPN client and download certificate](https://docs.byteplus.com/en/docs/vpn/Creating-and-downloading-an-SSL-client-certificate): Create an SSL VPN client and download the client certificate.

4. [Configure the client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client): Download the corresponding VPN software and load the client certificate downloaded in the previous step.

5. [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1): Initiate a connection from the client to verify connectivity.
