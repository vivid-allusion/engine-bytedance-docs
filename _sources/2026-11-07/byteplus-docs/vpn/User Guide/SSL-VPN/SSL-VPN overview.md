---
title: "SSL-VPN overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/SSL-VPN-overview"
---

SSL\-VPN is developed based on OpenVPN architecture. It enables network interconnection between the Virtual Private Clouds (VPC) and the SSL\-VPN client. You can use SSL\-VPN with simple and flexible configurations. By loading a certificate into an SSL\-VPN client and initiating a connection, you can connect the SSL\-VPN client to the VPC anytime, anywhere.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2ed23329f1b100f8c7dd464b9d6e41a.png) </span>

<span id=".57uE5oiQ6YOo5YiG"></span>
### Compositions


* **VPN gateway**

   A VPN gateway is created based on a VPC and serves as an egress gateway for the VPC. SSL\-VPN can be used on VPN gateways with only SSL\-VPN enabled or VPN gateways with both SSL\-VPN and IPsec\-VPN enabled.

* **SSL server**

   The SSL server is used to specify information such as the private network CIDR block that the SSL\-VPN client needs to access, the CIDR block used by the SSL\-VPN client when accessing the SSL server, the protocol (TCP, UDP), the encryption algorithm (AES\-128\-CBC, AES\-192\-CBC, AES\-256\-CBC, or None), and the authentication algorithm (SHA1, MD5, or None).

* **SSL VPN client certificate**

   You can generate an SSL\-VPN client certificate based on the configurations of an SSL server. After downloading and installing VPN software such as OpenVPN and loading the client certificate on an SSL\-VPN client, you can initiate an SSL\-VPN connection.


<span id="j3v3Brkg"></span>
## Use process

For detailed configuration, see [SSL VPN quick start](https://docs.byteplus.com/en/docs/vpn/Quick-start-1).
