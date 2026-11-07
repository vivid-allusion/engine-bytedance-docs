---
title: "Testing connectivity"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1"
---

This topic describes how to test SSL\-VPN connectivity after completing all configurations.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


* Test from the client: initiate an SSL\-VPN connection from the client. After the connection succeeds, access the Elastic Compute Service (ECS) in the VPC of the local CIDR block configured on the SSL\-VPN server using the client. Access indicates that the server and client communicate properly through SSL\-VPN.

* Test from the server: Use an ECS in the VPC of the local CIDR block configured when you `create SSL VPN server` to `ping` the IP of the TUN interface assigned by SSL\-VPN in the client. A successful ping means the server and client communicate properly through SSL\-VPN.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0eeda75fd245615b521e22872a138cfc.png) </span>
