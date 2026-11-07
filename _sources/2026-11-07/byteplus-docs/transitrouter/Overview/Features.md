---
title: "Features"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Features"
---

With its robust capabilities for cross\-account networking, cross\-region connectivity, and advanced routing, the Transit Router (TR) provides flexibility to meet your diverse architectural needs.


|Category |Feature |Capabilities |
|---|---|---|
|Instance management |TR instance |The foundation of the TR service. Receives traffic from the network instance and forwards it according to the route table associated with forwarding. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) |
|Cross\-account management |Cross\-account network instance attachment (attach VPC, VPN, or DC Gateway) |With the resource sharing feature, share a TR instance under my account with any other account or enterprise organization. This enables mutual access between TR instances within my account and another account's network instance (such as VPC, VPN, and DC Gateway) via the TR. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Cross-account-Sharing-overview) |
||Cross\-account peering attachment (attach inter\-region TR) |Create a connection directly using the peer account ID and TR instance ID. No need to share your local TR instance. The connection is established after peer TR authorization. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Cross-account-Sharing-overview) |
|Intra\-region management |VPC attachment |The connection is established between a TR instance and a VPC within the same region. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) |
||VPN attachment |The connection is established between a TR instance and an IPsec\-VPN connection within the same region. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpn) |
||DC Gateway attachment<br><br> |The connection is established between a TR instance and a DC Gateway within the same region. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc)<br><br> |
|Inter\-region management |Bandwidth package |Provide bandwidth resources for cross\-region communication scenarios. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01) |
||Inter\-region attachment |The connection is established between two TR instances in separate regions, enabling private network interconnectivity across regions. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-01) |
|Route management |Custom route table |Use multiple TR route tables to implement network isolation. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03) |
||Association forwarding |Specify the route table to forward TR traffic. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07) |
||Route learning |TR automatically learns routes from network instances, simplifying its route configuration. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06) |
||Static routes |Supports adding custom routes to flexibly control traffic direction. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05) |
||Auto Publish Route |Publish TR routes to network instances, simplifying the route configuration for the network instances. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Attachments-04) |
||Route policy |Filter routes in both inbound and outbound directions of a TR to change route propagation and path selection outcomes. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Overview-of-routing-policy) |
||Forwarding policy |Forward traffic from different CIDR blocks of the same network instance through separate TR route tables, achieving source address–based routing. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Overview-of-forwarding-policy) |
|Monitoring and maintenance |Monitor TR resources |Support real\-time monitoring of various metrics for TR instances, attachments, inter\-region attachments, and bandwidth packages. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Monitoring-01) |
||Preset alarm template |Quickly set alarm strategies by preset alarm templates, improving configuration efficiency. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Configuring-an-alert-policy) |
||Cross\-region traffic analysis |Use the cross\-region traffic analysis feature provided by Network Advisor to understand service situations and quickly locate issues. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Managing-traffic-analysis) |
||Flow log |Periodically collects inbound and outbound traffic flowing through an inter\-region attachment. Generates log records and delivers them to Torch Log Service (TLS). You can then search and analyze these traffic logs in TLS, which facilitates business analysis and fault diagnosis. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Flow-log-overview) |
||QoS management |Tag and schedule traffic by traffic marking and traffic queues to optimize bandwidth utilization. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Qos-overview) |
|Account and resource management |Access control |BytePlus’s permission management system. It offers a free service to control access permissions for different identities on cloud resources, enabling decentralized resource management, improving efficiency, and reducing the risk of information leakage. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Permission-management-01) |
||Project management |A resource management method. It allows you to group cloud resources used by different businesses or projects, helping maintain resource independence and data security. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Projects) |
||Tag management |Used to identify resources. Add different tags to cloud resources of various types and purposes. Enables you to tag and categorize resources, and quickly find your target cloud resources with specific characteristics. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags) |
