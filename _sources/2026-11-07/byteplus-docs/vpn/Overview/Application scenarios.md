---
title: "Application scenarios"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Application-scenarios"
---

<span id=".5Y2V54us5L2_55SoSVBzZWMgVlBO55qE5bqU55So5Zy65pmv"></span>
## Scenarios with only IPsec\-VPN

<span id=".56eB5pyJ572R57uc5LmL6Ze06L-e5o6l"></span>
### Connect two VPC

By default, Elastic Compute Service (ECS) instances in a Virtual Private Cloud (VPC A) cannot access ECS instances in VPC B. You can connect VPCs A and B by establishing an IPsec\-VPN tunnel between them for secure communication.

VPC A and VPC B can be from different cloud vendors and in different regions, or under the same account or different accounts of the same cloud vendor.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_130ba561ad060c6d6feaee2fc9f0eaab.png) </span>

<span id=".5Y2V5pWw5o2u5Lit5b-D5LiO56eB5pyJ572R57uc5LmL6Ze06L-e5o6l"></span>
### Connect a single data center to a VPC

<span id=".5L2_55SoVlBO572R5YWz77yI5Y2V57q_6Lev6K6_6Zeu77yJ"></span>
#### Use VPN gateway (single\-line access)

In a hybrid cloud scenario, you can associate an IPsec\-VPN connection to a VPN gateway when creating the IPsec\-VPN connection, establishing a secure communication tunnel between the local data center and the VPC. This allows you to seamlessly migrate some business to the cloud to save on\-premises space.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03c52657e7a8e89bf83072d329dc00df.png) </span>

<span id=".5L2_55SoVlBO572R5YWz77yI5aSa57q_6Lev6K6_6Zeu77yJ"></span>
#### Use VPN gateway (multi\-line access)

In a hybrid cloud scenario, you can establish two IPsec\-VPN connections between the data center and the VPC. This ensures secure communication and business continuity even if one tunnel fails.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_147b5d308da2f2b6f18c3a1d46bce909.png) </span>

<span id=".5L2_55So5Lit6L2s6Lev55Sx5Zmo"></span>
#### Use TR

In a hybrid cloud scenario, you can associate an IPsec\-VPN connection to a Transit Router (TR) when creating the IPsec\-VPN connection, and configure flexible routing policies on the TR. This allows you to connect or isolate data centers and VPCs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb33ab7bef3be63cf1600b349cb418aa.png) </span>

<span id=".5aSa5pWw5o2u5Lit5b-D5LiO56eB5pyJ572R57uc5LmL6Ze06L-e5o6l"></span>
### Connect multiple data centers to a VPC

To allow cross\-region data centers to access ECS instances in a VPC, establish multiple IPsec\-VPN tunnels between them and the VPC. This ensures secure, encrypted communication.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ad8875b60290709d68926226462942f.png) </span>

<span id=".5pWw5o2u5Lit5b-D5LiO56eB5pyJ572R57uc5LmL6Ze06auY5Y-v55So6L-e5o6l"></span>
### High availability connection between data centers and VPCs

A TR can associate with multiple IPsec\-VPN connections simultaneously. For a data center hosting critical business, you can establish multiple IPsec\-VPN tunnels to balance loads and ensure business stability.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d473a690c416c8da735ca04672c2451b.png) </span>

<span id=".5Y2V54us5L2_55SoU1NMIFZQTueahOW6lOeUqOWcuuaZrw=="></span>
## Scenarios with only SSL\-VPN

<span id=".5a6i5oi356uv5LiO56eB5pyJ572R57uc5LmL6Ze06L-e5o6l"></span>
### Connection between client and VPC

The SSL\-VPN enables network access between clients and the VPC, allowing different clients to securely and flexibly access the VPC anytime and anywhere over the internet.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c0083cdc8c230d559ac0e33ec3184ce.png) </span>

<span id=".5ZCM5pe25L2_55SoSVBzZWMgVlBO5LiOU1NMIFZQTueahOW6lOeUqOWcuuaZrw=="></span>
## Scenarios with both IPsec\-VPN and SSL\-VPN

<span id=".5a6i5oi356uv5LiO56uZ54K55LmL6Ze06L-e5o6l"></span>
### Connection between client and site

You can use both IPsec\-VPN and SSL\-VPN to connect clients and the data center with the cloud Virtual Private Cloud, enabling access to the Virtual Private Cloud from both clients and office networks.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2e977bb978991ae0438a98257185ba3.png) </span>
