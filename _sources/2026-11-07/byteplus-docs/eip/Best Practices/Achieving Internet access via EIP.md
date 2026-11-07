---
title: "Achieving Internet access via EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Configuring-internet-access"
---

When associating a cloud resource with an Elastic IP Address (EIP), it can communicate with the Internet. This topic describes how to use EIPs in different scenarios.

<span id=".5LqR5YaF6K6_6Zeu5YWs572R"></span>
## Outbound internet access

<span id=".5Y2V5Y-w5LqR5pyN5Yqh5Zmo6K6_6Zeu"></span>
### Single ECS instance access

To enable a single Elastic Compute Service (ECS) instance within a Virtual Private Cloud (VPC) to access the Internet, associate an EIP with the instance. For procedure, see [Associating a cloud resource](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35e708ff72bae2f3e99b7a293b20360e.png) </span>

<span id=".5aSa5Y-w5LqR5pyN5Yqh5Zmo6K6_6Zeu"></span>
### Multiple ECS instances access

If multiple ECS instances within a VPC require Internet access, create an Internet NAT Gateway within the VPC and configure an SNAT entry. The ECS instances in the SNAT entry share the EIP via the NAT Gateway to access the Internet. For procedure, see [Enabling Internet access via SNAT](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c37d1dddb3f6bb406917fcb9d0cfbb75.png) </span>

<span id=".5YWs572R6K6_6Zeu5LqR5YaF"></span>
## Internet access to cloud

<span id=".6K6_6Zeu5Y2V5Y-w5LqR5pyN5Yqh5Zmo"></span>
### Access a single ECS instance

In low\-traffic scenarios, to achieve external access to a single ECS instance within the VPC, you simply associate an EIP to the ECS instance. For procedure, see [Associating a cloud resource](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_969c480798af7d8f9539d20184be0e1f.png) </span>

<span id=".6K6_6Zeu5aSa5Y-w5LqR5pyN5Yqh5Zmo"></span>
### Access multiple ECS instances


* **Use an Internet NAT gateway**

   In scenarios where multiple ECS instances need to provide Internet services and the ECS instances provide different services, you can create an Internet NAT gateway and a DNAT entry within the VPC. The ECS instances in the DNAT entry can share the same EIP to provide Internet services. For procedure, see [Configuring DNAT for Internet service access](https://docs.byteplus.com/en/docs/natgateway/Providing-services-over-the-internet-using-DNAT).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ec5a9ee9e2fa7819e2b9c881a1db7fc.png) </span>


* **Use a Classic Load Balancer**

   In high\-concurrency scenarios with heavy traffic, numerous external users may access the services within the VPC simultaneously. Direct access may cause excessive load. In this case, you can use a Classic Load Balancer with an associated EIP to distribute the load. With Internet access capabilities provided by the EIP, the CLB distributes traffic elastically and evenly across multiple ECS instances, supporting massive external access. For procedure, see [Quick start of Layer-4 CLB](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01) and [Quick start of Layer-7 CLB](https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-01).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_158983b878cba0da842166ef77f3c8bc.png) </span>


* **Use an NLB**

   Network Load Balancer (NLB) is a next\-generation Layer\-4 load balancing service provided by BytePlus. It supports higher\-performance elastic forwarding on Layer\-4, helping you easily handle high\-concurrency workloads (with a single instance supporting up to 100 million concurrent connections and 100 Gbps bandwidth). It can serve as an ingress for IoT services such as the Internet of Things and Internet of Vehicles. After creating an NLB instance, the system automatically creates a service network interface in each Availability Zone. To achieve cluster\-wide internet communication, associate the EIP with the service IP (IPv4 address). For procedure, see [Setting up an IPv4 Network Load Balancer](https://docs.byteplus.com/en/docs/clb/Setting-up-an-IPv4-NLB).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c2139e8762418612365b2ad1425e99d.png) </span>
