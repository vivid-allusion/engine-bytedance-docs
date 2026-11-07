---
title: "VPC overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/VPC-overview"
---

<span id="4rvUqXY8"></span>
## Description

A Virtual Private Cloud (VPC) provides an isolated and self\-configurable virtual network environment for cloud resources. You can customize CIDR blocks, security groups, route policies, and other network settings in your VPCs. This helps you manage cloud resources in a simple, efficient, and secure manner.

<span id="4KFQpCCN"></span>
## Product architecture


|Feature ||Description |
|---|---|---|
|Key components of VPC |VPC CIDR block |The VPC CIDR block defines the IP addresses that can be used by resources within the VPC.<br><br><br>* The optional IPv4 CIDR blocks (32\-bit) are as follows:<br><br>   * **10.0.0.0/8–24** (Excluding IP addresses​ reserved for the system, the maximum number of IP addresses available for resources in the VPC is 16,777,213.)<br><br>   * **172.16.0.0/12–24** (Excluding IP addresses​ reserved for the system, the maximum number of IP addresses available for resources in the VPC is 1,048,573.)<br><br>   * **192.168.0.0/16\-24** (Excluding IP addresses​ reserved for the system, the maximum number of IP addresses available for resources in the VPC is 65,533.)<br><br>   * 172.31.0.0/16 (dedicated for the default VPC. Excluding IP addresses​ reserved for the system, the maximum number of IP addresses available for resources in the VPC is 65,533.)<br><br>* IPv6 CIDR blocks (128\-bit) cannot be selected.<br><br>   * The IPv6 address of BytePlus is globally unique.<br><br>   * The system automatically assigns you an `/56` IPv6 CIDR block.<br><br>   * The subnet mask is fixed at /64. |
||Subnet |A subnet is a segment of a VPC CIDR block allocated within a specific availability zone, providing private IP addresses for resources such as ECS instances and Classic Load Balancers. |
||[Route table](https://docs.byteplus.com/en/docs/vpc/Route-table-overview) |A route table consists of a series of route entries that specify the next\-hop cloud resource for VPC traffic. Each subnet must, and can only, be associated with one route table. This way, traffic from resources within the subnet is forwarded based on the route table. A single route table can be associated with multiple subnets. Traffic from resources within the subnets is forwarded based on the route table. |
||[Network interface](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview) |A network interface is a virtual network interface. In the VPC, a network interface is a network interface mounted on cloud resources like ECS or Classic Load Balancer. It serves as an essential component for enabling network communication. |
|VPC security |[Security group](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) |Security groups are designed based on the allowlist principle to control the outbound and inbound traffic for network interfaces of ECS instances. You can add security group rules to allow the required traffic for network interfaces based on your business requirements.<br><br>For example, if an ECS instance provides services externally over port 80, its associated security group must include an inbound rule allowing traffic over port 80. This ensures that external traffic can access the services provided by that ECS instance as expected. |
||[Network Access Control List (ACL)](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) |A network ACL is used to control outbound and inbound traffic for a subnet. Only one network ACL can be associated with each subnet. Network ACLs are designed based on the allowlist principle: traffic is permitted only if explicitly allowed by the allowlist. |
|VPC operations |[Flow log](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview) |After the flow log aggregates and processes the log data of outbound and inbound traffic for network interfaces as needed, it delivers the data to the Torch Log Service (TLS) for storage and search analysis. You can analyze flow logs to monitor network traffic, troubleshoot network issues, and optimize network architecture. |
||[Traffic mirroring](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview) |You can use traffic mirroring to replicate the traffic of a network interface according to the specified conditions, and forward the replicated traffic over a VPC to the target service for monitoring and analysis. |
|Access the Internet ||To meet the Internet access needs of resources in a VPC, you can combine the following products based on your business requirements:<br><br><br>* [Elastic IP (EIP)](https://docs.byteplus.com/en/docs/eip/What-is-EIP): By associating a single ECS with an EIP, it can communicate with the IPv4 internet.<br><br>* [NAT gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway): Multiple ECS instances can share the same EIP to communicate with the internet.<br><br>* [Cloud Load Balancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01): Internet traffic can be distributed across multiple backend servers associated with a Cloud Load Balancer instance for processing.<br><br>* [IPv6 gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway): Enable IPv6 internet bandwidth for an ECS with an IPv6 address to communicate with the IPv6 internet. |
|Access other VPCs ||To meet the demand for communication between VPCs, you can select the following products as needed:<br><br><br>* [Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/cen/Product-Overview-01): Enables full communication between multiple VPCs.<br><br>* [Transit Router (TR)](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01): Enables on\-demand communication between multiple VPCs.<br><br>* [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01): Allows a single VPC to provide services for multiple VPCs. |
|Access data center (IDC) ||To meet the needs of building a hybrid cloud, you can select the following products as needed:<br><br><br>* [Direct Connect](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect): High speed, private network interconnection, long construction period, high fee.<br><br>* [Virtual Private Network (VPN) connection](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network): Internet encryption, instant use, low fee. |


<span id="xbwT1Qi7"></span>
##
