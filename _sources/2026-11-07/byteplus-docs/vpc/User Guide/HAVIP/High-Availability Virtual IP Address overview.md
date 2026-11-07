---
title: "High-Availability Virtual IP Address overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/HAVIP-overview"
---

<span id=".566A5LuL"></span>
## Introduction​

The High\-Availability Virtual IP Address (HAVIP) is a private IP resource that can be independently held and managed. It can be created or deleted on demand to meet specific business requirements. In active\-standby cluster scenarios, HAVIP is typically combined with high\-availability software (e.g., Keepalived, Windows Server Failover Cluster) to deploy fault\-tolerant primary\-secondary services.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature description


* The HAVIP is a floating IP address, meaning it is not permanently bound to any single ECS instance or network interface.

* It is a private IP address allocated from a subnet and can only be bound to ECS instances or network interfaces within the same subnet.

* A single HAVIP can be bound to up to 10 ECS instances or 10 network interfaces, but it cannot be bound to both ECS instances and network interfaces simultaneously.

* Ten ECSs or ten Network Interfaces bound to a HAVIP announce the same virtual IP address via the Address Resolution Protocol (ARP).


<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

**Support public network high availability services**

Two ECS instances, ECS1 and ECS2, within the same subnet are bound to the same HAVIP. An EIP is associated with this HAVIP to facilitate the setup of a primary\-secondary high\-availability cluster, using Keepalived software, capable of serving Internet traffic. Under normal circumstances, ECS1 operates as the primary instance and provides services to the Internet via the EIP bound to the HAVIP.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eafb23eb31bb8bbe5ac057dddb104064.png) </span>

**Support private network high availability services**

HAVIP is bound to the network interfaces of both ECS1 and ECS2, forming a primary\-secondary high\-availability cluster using Keepalived software to provide highly available private network services for other instances within the VPC. Under normal conditions, ECS1 functions as the primary instance and provides services to ECS3 and other instances within the VPC via the HAVIP address. If ECS1 fails, ECS2 automatically takes over its workload and continues serving ECS3 and other instances in the VPC.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2574d581fa8da12f983f0772d5adefd4.png) </span>

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits

For limits related to the use of the High\-Availability Virtual IP Address, see [Limits](https://docs.byteplus.com/en/docs/vpc/Limits#.572R5Y2h).

<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures

Refer to [building a primary-secondary high-availability cluster using High-Availability Virtual IP Address and Keepalived](https://docs.byteplus.com/en/docs/vpc/Building-high-availability-primary-and-secondary-clusters-using-HAVIP-and-Keepalived).
