---
title: "Basic Introduction"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/General-FAQs"
---

<span id="b65b8b2d"></span>
### Can the cloud firewall protect assets not under BytePlus? 

The cloud firewall only supports the protection of cloud assets under BytePlus accounts and does not support assets not under BytePlus.

<span id="0a80a961"></span>
### Does the cloud firewall support cross\-region usage?


* Please refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/cloud_firewall/Region_and_Availability_Zones) for information on supported regions and availability zones for the cloud firewall.

* The cloud firewall supports cross\-region protection; you only need to purchase one version specification of the firewall to protect public EIP traffic, NAT gateway traffic, and TR transit router traffic in different regions.


<span id="bb0dc27a"></span>
### What is the difference between the cloud firewall and access controls of security groups and network ACLs? 

The cloud firewall, security groups, and network ACLs are independent systems, and only when the policies of all three systems allow it can the relevant network traffic successfully pass through.


| |**Cloud firewall** |**Security group** |**Network ACL** |
|---|---|---|---|
|Definition |BytePlus Cloud Firewall (CFW) is a cloud\-native cloud boundary network security protection product that provides functions such as internet boundary security, VPC boundary security, unified security access control for on\-cloud and off\-cloud, traffic visibility, intrusion prevention, and log auditing. |The security group consists of a series of security group rules used to control the inbound and outbound traffic of network interfaces, and each network interface must be added to a security group. |Network ACLs are used to control the incoming and outgoing traffic of subnets; a subnet supports associating only one network ACL. |
|Protected objects |* Internet boundary<br><br>* VPC boundary<br><br>* NAT boundary |Network interface |Subnet |
|Functional features |* Supports five\-tuple access control<br><br>* Supports geographic location, domain, and address book access control<br><br>* Supports Intrusion Prevention System (IPS)<br><br>* Supports full traffic log auditing |* Supports five\-tuple access control |Supports five\-tuple access control |
|Number of access control policies |* Supports up to 300,000 access control policies<br><br>* The single access control policy can configure up to 100,000 IP address ranges for both access source and access destination |* [The default number of rules supported by a single security group](https://docs.byteplus.com/en/docs/vpc/Security-group-FAQ)<br><br>   * Inbound direction: 200 IPv4 rules, 200 IPv6 rules<br><br>   * Output direction: 200 IPv4 rules, 200 IPv6 rules<br><br>   * If the default quota cannot meet your needs, please go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to apply for a quota increase<br><br>* Each network card of the cloud server can associate with up to 5 security groups |* [Default number of rules supported for a single network ACL created](https://docs.byteplus.com/en/docs/vpc/Network-ACL-FAQ)<br><br>   * Inbound: 20 rules for IPv4, 20 rules for IPv6<br><br>   * Outbound: 20 rules for IPv4, 20 rules for IPv6<br><br>   * Default rules with priority \* do not count towards the rule quota<br><br>   * If the default quota cannot meet the needs, please go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to apply for an increase in quota<br><br>* One subnet only supports associating one network ACL, but one network ACL can associate with multiple subnets |


<span id="56df5589"></span>
### What ranges does the cloud firewall support protection for?


* Internet boundary protection: provides security protection for inbound and outbound traffic between the internet and public EIP.

* VPC boundary protection:

   * Interconnect communication between VPCs

   * Communication between VPC and on\-premises data center (via VPN or dedicated line)

   * Communication between VPC and third\-party cloud platform (via VPN or dedicated line)

* NAT boundary protection, supports precise tracking of traffic to specific private IPs:

   * Protection of private IP assets against outgoing SNAT traffic to the internet

   * Protection of private IP assets against incoming DNAT traffic from the internet


<span id="7cf263de"></span>
### If DDoS protection, web application firewall, cloud firewall, and advanced network threat detection system are deployed simultaneously, how does the business inbound traffic flow? 

If DDoS, web application firewall, cloud firewall, and advanced network threat detection system are deployed simultaneously, the business inbound traffic flow is: DDoS/advanced network threat detection system \-\> cloud firewall \-\> web application firewall (cname access & load balancing access).

&nbsp;
