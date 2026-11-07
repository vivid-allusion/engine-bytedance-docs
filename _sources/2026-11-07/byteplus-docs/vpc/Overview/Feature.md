---
title: "Feature"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Features-list"
---

## Product features

|Feature |Explanation |Related documents |
|---|---|---|
|Virtual Private Cloud instance |Assign CIDR blocks to VPC to establish isolated network environments. Different VPCs are logically isolated from each other. |[Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) |
|Subnet |Deploying a subnet is equivalent to assigning a range of intra\-VPC IP addresses in an availability zone. These private IP addresses can be assigned to off\-premises resources, such as ECS and Classic Load Balancer (CLB) instances. |[Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet) |
|Route Table |Consisting of a series of routing entries, it specifies the next\-hop resource for traffic in a VPC, which forwards the VPC traffic. |[Route table overview](https://docs.byteplus.com/en/docs/vpc/Route-table-overview) |
|Network interface |A network interface (ENI), specifically a Virtual Elastic Network Interface (vENI), is an ENI mounted on cloud resources such as ECS instances. |[Network interface overview](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview) |
|Security group |A security group acts as a logical container that provides access policies for network interfaces within the same VPC. These network interfaces share identical security requirements and mutual trust relationships. By configuring security group rules, you control inbound and outbound traffic for associated network interfaces. |[Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) |
|Network ACL |Implement subnet\-tier security policies by configuring inbound/outbound rules in network ACLs to control traffic flow.​​ |[Network ACL Overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) |
|Prefix List |A prefix list is a group of CIDR blocks used to simplify the configuration of security group rules and routing table entries.​​ When a prefix list is modified, all associated resources are automatically updated.​​ |[Prefix List Overview](https://docs.byteplus.com/en/docs/vpc/Prefix-list-overview) |
|HaVip |HaVip is an independently assignable private IP resource. In active\-standby cluster scenarios, HaVip is typically combined with high\-availability software (e.g., Keepalived, Windows Server Failover Cluster) to deploy fault\-tolerant primary\-secondary services. |[High-Availability Virtual IP Address Overview](https://docs.byteplus.com/en/docs/vpc/HAVIP-overview) |
|Flow Log |Flow logs collect inbound and outbound traffic data from network interfaces within the Virtual Private Cloud and deliver it to Torch Log Service for storage, retrieval, and analysis. You can leverage flow log analysis to monitor network traffic, troubleshoot connectivity issues, and optimize network architecture. |[Flow log overview](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview) |
|Traffic Mirror |VPC provides the Traffic Mirror feature. Through traffic mirroring, you can on\-demand duplicate traffic from specified network interface(s) and privately forward it to target network interfaces or CLBs for monitoring and analysis. |[Traffic Mirror Overview](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview) |

## Related products

|Service name |Feature Description |
|---|---|
|[Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service) |Services can be deployed on cloud servers within VPCs. |
|[Elastic IP Address](https://docs.byteplus.com/en/docs/eip/What-is-EIP) |You can associate an EIP with ECSs within your VPC to enable internet connectivity. |
|[IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway) |​Enable internet bandwidth allocation for ECSs' IPv6 addresses to establish connectivity with the internet.​​ |
|[Public NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway) |Multiple ECSs within a VPC can access the internet or provide services externally through a shared Internet NAT Gateway.​​ |
|[Classic Load Balancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) |CLB distributes traffic to operating Elastic Compute Service (ECS) instances, giving you secure and stable access to off\-premises services. |
|[Cloud Enterprise Network](https://docs.byteplus.com/en/docs/cen/Product-Overview-01) |CEN enables interconnectivity between multiple VPCs. |
|[Transit Router](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01) |Transit routers enable controlled interconnection and isolation between VPCs.​​ |
|[PrivateLink (PL)](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01) |Private connectivity enables secure and simplified access to services shared across other VPCs from within your VPC. |
|[VPN Connect](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network) |VPN connects utilize encrypted communication over the Internet to enable interconnectivity between multiple VPCs, or between cloud\-based VPCs and on\-premises data centers. |
|[Direct Connect (DC)](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect) |Dedicated connections leverage Direct Connect Connection to enable private network communication between cloud\-based VPCs and on\-premises data centers, unaffected by Internet jitter. |
