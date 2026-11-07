---
title: "Manage security groups"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Manage_security_groups"
---

Security groupis used to control the inbound and outbound traffic of each network interface card on cloud servers within the cluster, to divide security domains in the cloud, and is an important network security isolation method provided by Volcano Engine. This document describes how to add security groups and security group rules.

<span id="543a1379"></span>
## Context

When creating an E\-MapReduce cluster, you can use an existing security group or create a new Security group, to control the outbound and inbound network traffic for all ECS instances under a specific Security group. You can divide ECS instances by function and place them in different Security group, and configure different access control policies for each Security group according to different requirements.

<span id="3749ac22"></span>
## Important notes


* When adding Security group rules, you must restrict the range of IP addresses allowed for access. Do not use 0.0.0.0/0 to avoid attacks.

* To avoid security risks caused by allowing unnecessary IP addresses and ports, you should strictly follow the principle of least privilege, allow IP addresses and ports as precisely as possible, and be cautious when allowing traffic to protect the security of cloud servers.

* It is prohibited to use enterprise security groups created on ECS.

* When configuring EMR cluster security group rules, you must ensure internal network connectivity among all ECS instances within the cluster; otherwise, EMR cluster big data services will be affected.

* For user convenience, the system has added some rules to the default security group to allow traffic. Please modify them with caution.


<span id="ad3c1873"></span>
## Create security groups

For details on creating a new security group, see [Create security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

<span id="3bbb066b"></span>
## Modify cluster security group configuration

Currently, EMR on ECS supports modifying the security group configuration for Hadoop clusters and custom clusters. After logging in to the EMR on ECS console, you can modify the security group configuration for the corresponding cluster on the Cluster overview page of the cluster.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9f79c85370a4720bd5e373647b3273e~tplv-goo7wpa0wc-image.image) </span>

<span id="7fa9e5db"></span>
## FAQs


1. **What are the categories of security groups? What traffic allowance rules are included in the default security group?** 


Security groups are categorized based on how they are created, as shown in the following table:


|Category |Note |
|---|---|
|Default security group |Automatically created by the system when a private network is created. Deleted along with the private network; manual deletion is not supported. For user convenience, some rules are added by default (manual modification is supported) to allow traffic:<br><br><br>* Outbound direction: Allow all traffic, that is, resources can access any address.<br><br>* Inbound direction: Allow ICMP and TCP ports 22, 3389, 80, and 443 from the entire network segment (0.0.0.0/0, that is, any address), and allow traffic from other network interfaces within the same security group. |
|Custom security group |Manually created by the user. For user convenience, some rules are added by default (manual modification is supported) to allow traffic:<br><br><br>* Outbound direction: Allow all traffic, that is, resources can access any address.<br><br>* Inbound direction: Allow traffic from other network interfaces within the same security group. |
|Managed security group |Automatically created by the system when a cloud service requiring a security group (such as NAT gateway or VPN gateway) is created. The cloud service manages the security group; users can only view it. Its lifecycle follows that of the cloud service. EMR prohibits the use of enterprise security groups. |



2. **When creating an EMR cluster and selecting a security group, the following prompt appears: "Please use another security group or refer to security group management to modify security group rules, ensuring that cloud servers within the security group can communicate with each other." How should this be handled?** 


Select another security group or modify the rules of the selected security group. It is recommended to adjust the rules according to the default traffic rules.


* Outbound direction: Allow all traffic, that is, resources can access any address.

* Inbound direction: Allow ICMP and TCP ports 22, 3389, 80, and 443 from the entire network segment (0.0.0.0/0, that is, any address), and allow traffic from other network interfaces within the same security group.
