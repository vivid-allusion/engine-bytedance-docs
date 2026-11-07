---
title: "Access control in VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/VPC-access-control"
---

Virtual Private Cloud (VPC) provides multiple security access control features to protect network security across multiple dimensions. This topic introduces access control for subnets, network interfaces, and load balancers within a VPC.

<span id=".5a2Q572R77yI572R57ucQUNM77yJ"></span>
## Subnet (Network ACL)

Subnets enforce network access control through network access control lists (ACLs). By configuring inbound and outbound network ACL entries, you can control inbound and outbound traffic to and from the subnets.

For example, add an inbound rule to the Network ACL associated with a subnet to deny the IP address 12.XX.XX.89 from accessing ECS instances within the subnet.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ff86fcc48cec5e0de9bdb50ccf640da.png) </span>

<span id=".572R5Y2h77yI5a6J5YWo57uE77yJ"></span>
## Network Interface (Security Group)

Network interfaces implement access control through security groups. Configure access rules to define access policies for network interfaces within the same VPC that require identical security protection and are mutually trusted.

For example, add an inbound rule to the security group of an Elastic Compute Service (ECS) instance's primary network interface.This rule allows SSH remote connections to a Linux ECS instance through port 22 from a specific IP address (e.g., 12.XX.XX.89).

&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc97a5eac88afbd8b01b8c4a613e2e04.png) </span>

<span id=".6LSf6L295Z2H6KGh77yI6buR55m95ZCN5Y2V77yJ"></span>
## Classic Load Balancer (CLB) (denylist and allowlist)

Classic Load Balancer (CLB) provides listener\-level access control. Listeners support allowlist and denylist methods. Select one of these methods based on your scenario to control IP access to backend services. For more information, see [CLB Access Control](https://docs.byteplus.com/en/docs/clb/Access-control-list-01).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fe78275dfe038532c29d2a02b269991.png) </span>
