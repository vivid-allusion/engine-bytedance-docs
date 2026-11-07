---
title: "Version Features"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Version_Features"
---

Before purchasing a cloud firewall, you need to choose the suitable version of cloud firewall based on business protection needs, features of different firewall versions, cost factors, and other considerations. This article introduces the features supported by different versions of cloud firewall.

<span id="259b673f"></span>
## Product Feature Comparison


|**Function classification** |**Function Description** |**Pro version** |**Enterprise Edition** |**Flagship version** |**Pay\-as\-you\-go version** |
|---|---|---|---|---|---|
|Firewall switch |The internet perimeter firewall protects the inbound and outbound traffic between the internet and public IPs. |✅ |✅ |✅ |✅ |
||VPC border firewall, traffic between VPCs, between VPC and on\-premises data centers (VPN or dedicated line), and between VPC and third\-party clouds (VPN or dedicated line gateway). |❌ |✅ |✅ |❌ |
||NAT boundary firewall protects the inbound and outbound traffic between NAT gateway private IP assets and the internet. |✅ |✅ |✅ |✅ |
|Access Control |Internet border access control policy configuration, supporting access control for in\-bound and out\-bound traffic of public EIP assets, reducing the exposure of public assets to lower intrusion risks, and effectively intercepting unauthorized access from the internal network to the public network. |✅ |✅ |✅ |✅ |
||VPC boundary access control policy configuration supports access control of traffic between private network VPCs, between VPCs and local data centers (VPN or dedicated line), and between VPCs and third\-party clouds (VPN or dedicated line gateway), ensuring business isolation and effectively intercepting unauthorized access between internal networks. |❌ |✅ |✅ |❌ |
||NAT boundary firewall policy configuration supports access control on the traffic of NAT gateway private IP accessing the public network, effectively intercepting unauthorized access from the internal network to the public network. |✅ |✅ |✅ |✅ |
||Host boundary firewall policy configuration supports access control for inbound and outbound traffic between ECS instances (east\-west), restricting unauthorized access between ECS instances. |✅ |✅ |✅ |✅ |
||Address book configuration supports specifying multiple IP addresses, ports, and domain addresses as a single address book. When configuring, you only need to reference the address book to achieve batch configuration of multiple IP addresses, ports, and domain addresses. |✅ |✅ |✅ |✅ |
||Domain blocklist strategy configuration, supports interception of outbound malicious domain access for VPC without the need to change DNS or deploy proxies, strategy is ready to use out of the box. |✅ |✅ |✅ |❌ |
|Security Panorama and Overview |Provides an overview of the defense capabilities of the cloud firewall, displaying recent traffic statistics, security protection overview, resource usage overview, and other data. |✅ |✅ |✅ |✅ |
|Protection Analysis |The proactive outreach page displays real\-time outreach data for assets, helping you promptly identify suspicious assets. |✅ |✅ |✅ |✅ |
||Asset exposure analysis detects in real time the IP addresses, ports, and other information exposed to the public network. |✅ |✅ |✅ |✅ |
||The cloud firewall's VPC intervisit analysis shows you the traffic information between the VPC private networks, helping you to obtain VPC network traffic information in real\-time and timely discover and troubleshoot abnormal traffic. |❌ |✅ |✅ |❌ |
||Displays all outbound and inbound traffic data that the current firewall has intercepted. |✅ |✅ |✅ |✅ |
|Log management |Supports access control logs, traffic session log audits, and provides retrieval analysis, monitoring alerts, data visualization and other functions based on BytePlus log service. |✅ |✅ |✅ |✅ |
|Warning notification |When the resource usage of the cloud firewall, such as traffic bandwidth, log storage, and access control policy count, is insufficient, an alert notification is sent. |✅ |✅ |✅ |✅ |
|Operation and maintenance tools |Provides backup and rollback functions for access control policies, allowing you to roll back the policies to a specified time point according to business needs, effectively improving policy migration and operation efficiency. |✅ |✅ |✅ |✅ |
||Cloud firewall provides policy verification query function. When encountering network anomalies, you can quickly confirm whether the traffic is allowed or blocked by the firewall policy by entering the network quintuplet information (source IP, destination IP, protocol, source port, destination port), facilitating troubleshooting. |✅ |✅ |✅ |✅ |


<span id="e883bcf8"></span>
## Product Performance Comparison


|**Product performance parameters** |**Advanced version** |**Enterprise Edition** |**Flagship version** |**Pay\-as\-you\-go version** |
|---|---|---|---|---|
|The number of public IPs supported by the firewall for protection |The default value is set at 1,000. |The default value is set at 2,000. |The default setting is 5,000 |The default setting is 1,000. |
|Internet boundary traffic processing capability |* Traffic bandwidth: default 20 Mbps, expandable up to 2,000 Mbps |* Traffic bandwidth: default 50 Mbps, expandable to 10,000 Mbps |* Traffic bandwidth: default 200 Mbps, expandable to 20,000 Mbps |* Traffic bandwidth: supports a maximum of 10,000 Mbps; if larger bandwidth is needed, please submit an [order](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001280) for processing. |
|VPC boundary firewall number |Not supported |The default is 2, expandable up to 200 |The default setting is 5, with options to expand to 200. |Supports up to 5 |
|VPC boundary traffic handling capacity |Not supported |* Bandwidth: the default is 200 Mbps, scalable up to 5,000 Mbps. |* Traffic bandwidth: default 2,000 Mbps, expandable to 80,000 Mbps |* Traffic bandwidth: maximum support of 10,000Mbps. For larger traffic handling bandwidth, please submit an [order ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001280) for processing. |
|NAT border firewall count |The default is not included, scalable up to 20. |Default 1, expandable to 100 |The default setting is 2, with expandability up to 200. |A maximum of 10 can be supported. |
|NAT boundary traffic processing capability |* Traffic bandwidth: not included by default, expandable to 1,000Mbps |* Traffic bandwidth: default 10 Mbps, expandable up to 5,000 Mbps |* Traffic bandwidth: default 20 Mbps, scalable up to 10,000 Mbps |* Traffic bandwidth: up to 10,000 Mbps supported; for larger traffic handling bandwidth, please submit a [ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001280) for processing. |
|Number of access control policies |The default is 4,000, expandable to 100,000. |The default is 10,000, expandable to 200,000 |The default value is set at 20,000, extendable to 300,000. |The default value is set at 10,000. |
|Number of domain blocking policies |Default does not include, expandable to 10,000 |Default is not included, extendable to 20,000. |By default, it does not include, expandable to 50,000 |Not supported |
