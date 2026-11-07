---
title: "Application Scenarios"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/fyniF4"
---

This document introduces the application scenarios of BytePlus PrivateZone.

<span id="access-ecs-hosts-using-custom-ecs-hostnames"></span>
## Access ECS hosts using custom ECS hostnames

When creating an ECS instance, you can customize the ECS hostname to clearly describe its purpose. After enabling the hostname record management feature of BytePlus PrivateZone, you can access ECS hosts using custom ECS hostnames.

For example, if you create a domain name `private.zone` and generate a hostname record based on the hostname `ecs-game-app-huabei1` under this domain, you can then access the corresponding ECS using `ecs-game-app-huabei1.private.zone`.

<span id="avoid-requests-across-availability-zones"></span>
## Avoid requests across availability zones

For resources distributed across different availability zones, BytePlus PrivateZone can return IP addresses or domain names you specify according to your configuration, thereby avoiding cross\-availability zone requests.

<span id="load-balancing"></span>
## Load balancing

BytePlus PrivateZone can return IP addresses you specify when responding to a proportional number of DNS queries, according to your load balancing configuration. When a domain name corresponds to multiple servers, BytePlus PrivateZone can distribute user requests to different servers proportionally.

<span id="implement-dns-resolution-between-vpc-and-on-premise-idc-third-party-cloud-services"></span>
## Implement DNS resolution between VPC and on\-premise IDC/third\-party cloud services

In hybrid cloud scenarios, your BytePlus cloud resources are typically connected to on\-premise IDC/third\-party cloud services through Direct Connect or VPN. If your services need to use resources from both BytePlus VPC and on\-premise IDC, your services may need to meet the following DNS resolution requirements:


* VPC users access resources in on\-premise IDC/third\-party cloud services using domain names

* Users in on\-premise IDC/third\-party cloud services access resources in VPC using domain names


To meet these requirements, you can use BytePlus PrivateZone to:


* Forward DNS queries from VPC to on\-premise IDC/third\-party cloud services.

* Forward DNS queries from on\-premise IDC/third\-party cloud services to VPC.
