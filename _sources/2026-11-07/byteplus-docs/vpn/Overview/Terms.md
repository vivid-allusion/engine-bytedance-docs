---
title: "Terms"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Basic-concepts"
---

<span id=".VlBO572R5YWz"></span>
## VPN gateway

A VPN gateway is a component of the VPN Connect service. It serves as an egress of a VPC and a carrier of the cloud VPN Connect service.

VPN gateways feature IPsec\-VPN and SSL\-VPN connection capabilities, which are suitable for different scenarios.


* IPsec\-VPN can be used on VPN gateways with IPsec\-VPN enabled or VPN gateways with both IPsec\-VPN and SSL\-VPN enabled.

* SSL\-VPN can be used on VPN gateways with SSL\-VPN enabled or VPN gateways with both SSL\-VPN and IPsec\-VPN enabled.


<span id="IPsec VPN"></span>
## IPsec\-VPN

IPsec\-VPN refers to a VPN technology that uses the IPsec (Internet Protocol Security) protocol to achieve remote access. IPsec\-VPN can provide temporary communication tunnels over the internet between a data center and a VPC, or between different VPCs, ensuring connection security by using encrypted channels.

<span id=".55So5oi3572R5YWz"></span>
### Customer gateway

A customer gateway is a component of the VPN Connect service. It is an abstraction of your local gateways, and allows you to register the information of local gateways in the cloud.

<span id=".SVBzZWPov57mjqU="></span>
### IPsec\-VPN connection

An IPsec\-VPN connection is a communication tunnel established between a customer gateway and a VPN gateway. Only after the establishment of an IPsec\-VPN connection can encrypted communication occur between the user side and the VPC.

IPsec\-VPN connections currently support associating the VPN gateway and the TR:


* Associate a VPN gateway: Establish an IPsec\-VPN tunnel between a customer gateway and a VPN gateway, achieving communication between a data center and a VPC or between different VPCs.

* Attach a TR: Establish an IPsec\-VPN tunnel between a customer gateway and a TR, allowing you to configure flexible routing policies on the TR. This ensures precise access between a data center or a VPC and the cloud resources associated with the TR (such as VPCs and Direct Connect Gateways).


<span id=".SUtF562W55Wl"></span>
### IKE policy

An IKE policy defines the encryption, authentication algorithms, and negotiation mode used in the IPsec communication tunnel during the negotiation phase.

<span id=".SVBzZWPnrZbnlaU="></span>
### IPsec policy

IPsec policy specifies the IPsec communication tunnel, encryption, and authentication algorithms used during data transmission.

<span id=".TkFU56m_6LaK"></span>
### NAT traversal

Enabling NAT traversal skips the verification of the UDP port number during IKE negotiation and facilitates the discovery of NAT Gateway devices involved in VPN Connect.

<span id=".6aKE5YWx5Lqr5a-G6ZKl"></span>
### Pre\-shared key

Pre\-shared key refers to the key configured in the cloud VPN attachment, used for IKE negotiation between the VPN devices on both ends. The pre\-shared keys on both sides must match to avoid IKE negotiation failure and inability to establish the communication tunnel.

<span id="PFS"></span>
### PFS

Perfect Forward Secrecy (PFS) is a feature that ensures this critical security property. If PFS is enabled in VPN Connect, the corresponding client must also enable it. After enabling PFS, the key is updated each time an IPsec\-VPN connection is established to secure VPN communication.

<span id="DPD"></span>
### DPD

Dead Peer Detection (DPD) is a feature that detects dead peers. When DPD is enabled, the device from which an IPsec\-VPN connection is established sends DPD packets to detect the status of the IKE process in peer devices (such as data centers or other VPCs). If the device does not receive a response within a specified time, it deems the peer device disconnected and performs subsequent actions based on the settings.

<span id="SSL VPN"></span>
## SSL\-VPN

SSL\-VPN is an OpenVPN\-based network connectivity technology that establishes network connections between an internet client and a VPC. With SSL\-VPN, you can use a client to quickly and securely access VPCs over the internet anytime and anywhere.

<span id=".U1NM5pyN5Yqh56uv"></span>
### **SSL\-VPN server**

An SSL\-VPN server is a service module of SSL\-VPN for encapsulating and decapsulating data packets.

When creating an SSL\-VPN server, you must specify the private CIDR blocks of the service modules for the SSL\-VPN client to access, such as the subnet CIDR block of the VPC, the CIDR block of the data center communicating with the VPC via Direct Connect, and the CIDR block of cloud services such as the Torch Object Storage cloud database. Additionally, you must specify the CIDR block that the SSL client uses to access the SSL server, the encryption algorithm (such as AES\-128\-CBC, AES\-192\-CBC, AES\-256\-CBC, or none), and the authentication algorithm (such as SHA\-1, MD5, or none).

<span id=".U1NM5a6i5oi356uv"></span>
### **SSL\-VPN client**

An SSL\-VPN client is used to initiate SSL\-VPN connections. To achieve this, you need to generate a client certificate based on the configurations of the SSL server, then install the VPN software and load the certificate on the client.

<span id=".56eB5pyJ572R57uc"></span>
## VPC

Unlike a traditional network, a Virtual Private Cloud (VPC) is a customized virtual network environment for isolating, configuring, and managing cloud resources.

<span id=".5Lit6L2s6Lev55Sx5Zmo"></span>
## TR

A Transit Router (TR) is a regional gateway that can connect VPCs or VPN Connect, flexibly realizing private network interconnection and isolation between various cloud resources, as well as interconnection between VPCs and on\-premises data centers. You can achieve precise access from a data center to cloud resources (VPC, Direct Connect Gateway) attached to the TR by associating an IPsec\-VPN connection to the TR. For specific information, refer to Achieving independent interconnection between different VPCs and data centers through Transit Router and VPN Connect.
