---
title: "Application scenarios"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Application-scenarios"
---

## Internet Access

**Cloud access to Internet**

* When a single Elastic Compute Service (ECS) instance in a virtual private cloud (VPC) needs to access the internet using the IPv4 protocol, you can Associate an Elastic IP (EIP) with it. For related operations, see [Binding cloud resources](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP).

* When Elastic Compute Service (ECS) instances in a virtual private cloud (VPC) need to access the internet with the IPv6 protocol, you can enable Internet bandwidth for the ECS instances' IPv6 addresses by configuring an IPv6 gateway. For related operations, see [Enable IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth).

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84df0f36781da9138f7e418a29765d5f.png)

* When multiple Elastic Compute Service (ECS) instances in a Virtual Private Cloud (VPC) need to access the internet through IPv4 protocol, you can create an Internet NAT gateway in the VPC and create an SNAT entry. For related operations, see [Use SNAT entries to access the internet](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT).

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e4aeb673a4b63ca994a519b8a040beb0.png)

**Internet access to cloud**

* When a large number of external users access applications deployed on Elastic Compute Service (ECS) simultaneously, traffic can be distributed to multiple ECS instances through Classic Load Balancer to prevent a single ECS instance from being overloaded and crashing. For relevant operations, see [getting started with layer 4 load balancing](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01) and [getting started with layer 7 load balancing](https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-01).

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93ebdd2fb76b91b8aa40fd8dac0f3ea7.png)

* When multiple Elastic Compute Service (ECS) instances need to provide services to the internet, and the services provided by different ECS instances differ, you can create an Internet NAT gateway in a virtual private cloud (VPC) and configure DNAT entries. For relevant operations, see [using DNAT entries to provide services to the public network](https://docs.byteplus.com/en/docs/natgateway/Providing-services-over-the-internet-using-DNAT).

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91a55582b3b2862ef60157e518ce0f2b.png)

## ​​Private Network Access​​

**Communication within the VPC**

Elastic Compute Service (ECS) within the same VPC can communicate directly over the private network.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ceb80447bb671502aee313fbb6510486.png)

**Interconnection between VPCs**

When data communication is needed between VPCs, you can select either the CEN for full communication or the TR for on\-demand communication.

* To enable mutual connectivity between multiple VPCs, create a Cloud Enterprise Network (CEN) instance and associate the VPCs to it. This establishes direct inter\-VPC communication. For detailed steps, see [Enable private network connectivity via Cloud Enterprise Network](https://docs.byteplus.com/en/docs/cen/Quick-Start).

* If you require on\-demand connectivity between multiple VPCs, you can use a transit router. By leveraging the transit router's routing tables to control traffic between VPCs, you achieve both interconnection and isolation between them. For detailed steps, see [Enable private network connectivity and isolation between different VPCs (same region, same account)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3f69340b3c7159583deeab0eb831e95.png)

**Unidirectional Access**

When a VPC needs to provide services to multiple VPCs, you can create a PrivateLink instance, configure the consumer VPC as an endpoint, and configure the provider VPC's resources as an endpoint service. For detailed steps, see [implementing private access between VPCs the same account](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f31edc95b38ae5f0284b5499f9fa5a79.png)

## Hybrid Cloud

**Internet encryption**

VPN connections encrypt over the Internet to quickly establish a secure IPsec tunnel between a virtual private cloud (VPC) and a data center, achieving communication between them. For details, see [Establishing network connectivity between VPCs and on-premises multi-data centers](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ab255ea7d934e85439fac92f4d3fbfc.png)

**Private network connectivity**

The Direct Connect service is based on DC Connection, enabling a high\-speed channel between the virtual private cloud (VPC) and a data center. Unaffected by internet jitter, it establishes private network connectivity between the VPC and the data center. For details, see [Accessing ECS via Direct Connect from IDCs](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15408c1ff593df949eb232dcf7022983.png)

## Secure

**Service Isolation Deployment**

Private communication between different VPCs is isolated by default. When you have multiple business systems, such as production and test environments, and strict isolation requirements, deploy them in separate VPCs to prevent accidental data access and avoid environment conflicts.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7379bbf18323753a2f4be4b46c4d510e.png)

**Cross-AZ Disaster Recovery**

Subnets have Availability Zone attributes. Each Availability Zone has independent power supply and physical network. It is recommended to deploy businesses in at least two Availability Zones. Even if one Availability Zone fails, the business can still function normally.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2091903c25b2c0b47125b356b49d0543.png)

**Security protection**

Security groups, combined with Network Access Control List (ACL), can provide security protection for your services.

* Security group controls traffic entering and leaving the network interface, enables fine\-grained protection for servers, strictly restricts inbound and outbound traffic origins, prevents external malicious probes, and limits internal lateral infiltration.

* Network Access Control List (ACL) controls traffic entering and leaving the subnet, establishes a unified traffic control policy, and implements coarse\-grained, holistic restrictions on all traffic within the subnet.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_800d99c7dc9dacd6d4207678d866f48c.png)

###
