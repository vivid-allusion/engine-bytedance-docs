---
title: "Creating an SSL-VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server"
---

This topic describes how to create an SSL\-VPN server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The VPN gateway has been created, and SSL connection capability on the VPN gateway is enabled. For procedure, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the[ SSL VPN Server console](https://console.byteplus.com/vpn/sslServer).

2. In the top menu bar, select the target region and project to which the resource belongs.

3. Click **Create SSL Server** and configure the SSL server parameters according to the table below.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |Name |Set the name of the SSL server. |Server\-test |
   |VPN gateway |Select a VPN gateway to which the SSL server you want to create is associated. |VPNGW\-SSL |
   |Local Subnet |In SSL\-VPN, Local Subnet refers to the CIDR blocks that can be accessed by clients over an SSL\-VPN connection. A local subnet can be a CIDR block of a VPC subnet, a CIDR block of a data center interconnected with the VPC via Direct Connect, or a CIDR block of a cloud service such as TOS or a cloud database.<br><br><br>* Local Network mask range: `/8` to `/32`.<br><br>* The local subnet must not conflict with the remote CIDR. |10.0.0.0/24 |
   |Client cidr |In SSL\-VPN, Client IP pool refers to the CIDR blocks assigned by an SSL server to client devices for communication. It is not the local CIDR blocks of client devices. When a client connects through an SSL\-VPN connection, the VPN gateway will assign an IP address from the specified client IP pool for client use.<br><br><br>* The client IP pool cannot conflict with the local subnet.<br><br>* The client IP pool must not conflict with the VPN gateway route.<br><br>* The client IP pool must not conflict with route entries in the VPN gateway's default route table.<br><br>* The client IP pool must not overlap with `100.64.0.0/10`, `169.254.0.0/16`, `127.0.0.0/8`, `224.0.0.0/4`, or `240.0.0.0/4` CIDR blocks.<br><br>* The available IP count in the remote CIDR must be at least four times the SSL Max Connections value configured when creating the VPN gateway. For example, if the SSL Max Connections is set to 10, the remote CIDR must contain more than 40 available IP addresses. |192.168.2.0/24 |
   |Agreement |Select the protocol for the SSL\-VPN connection. Currently supported protocols are TCP and UDP. |TCP |
   |Encryption algorithm |Select the encryption algorithm for the SSL\-VPN connection. Supported options are AES\-128\-CBC, AES\-192\-CBC, AES\-256\-CBC, or no encryption. |AES\-128\-CBC |
   |Authentication algorithm |Select the authentication algorithm for the SSL\-VPN connection. Supported algorithms include SHA1, MD5, and no encryption. |SHA1 |
   |Data compression |Select whether to compress data transmission. |No |
   |Port |The port used by the SSL\-VPN server. Port value range: 1~65535. Unsupported ports: 22, 68, 179, 323, 500, 4500. |1194 |
   |Affiliated Project |Select the project to which the new SSL server belongs. |default |
   

4. After configuration, click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create an SSL-VPN client and download certificate](https://docs.byteplus.com/en/docs/vpn/Creating-and-downloading-an-SSL-client-certificate)

* [Configure a client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1)
