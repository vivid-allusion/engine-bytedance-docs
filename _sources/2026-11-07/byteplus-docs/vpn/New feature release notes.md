---
title: "New feature release notes"
product: "Virtual Private Network"
product_code: "vpn"
section: "Document"
source: "https://docs.byteplus.com/en/docs/vpn/What-is-New"
---

This topic introduces feature updates for VPN Connect in each version. New features will be gradually available in all regions. Welcome to explore them.

> **tip**

> Products or features in Invite\-only Beta stage are not yet available to all users. To better understand the product, some companion documents for Invite\-only Beta products or features are available to all users. Meanwhile, some companion documents for Invite\-only Beta products or features are only visible to users who have enabled product capabilities. To request access to an Invite\-only Beta product or feature, please contact your account manager.

## September 2026

|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |DPD method for IPsec\-VPN connection |Dead Peer Detection (DPD) can be configured in periodic or on\-demand mode. |GA |[Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |
|2 |VPN gateway feature upgrade |A protocol type can be selected when creating a VPN gateway (IPsec VPN gateway or SSL VPN gateway).​ |GA |[Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2) |

## July 2026

|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |SSL\-VPN feature upgrade |The DNS server IP addresses can be customized. |Invite\-only Beta |[Creating an SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server-1) |
|||Two\-factor authentication is supported. |GA ||

## March 2026

|No. |Feature |Description |<br>Stage<br> |Documentation |
|---|---|---|---|---|
|1 |SSL\-VPN logs |Logs of the SSL\-VPN server can be viewed through the log service. You can troubleshoot VPN Connect issues based on the logs.​ |<br>Invite\-only Beta<br> |[Viewing VPN Connect logs](https://docs.byteplus.com/en/docs/vpn/Viewing-IPsec-VPN-connection-logs) |

## November 2025

|No. |Feature |Description |<br>Stage<br> |Documentation |
|---|---|---|---|---|
|1 |IPv6 protocol for IPsec\-VPN connection |IPv6 communication links are supported in dual\-tunnel mode for IPsec\-VPN connections. |<br>Invite\-only Beta<br> |[Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |

## October 10, 2025

|No. |Feature |Description |<br>Region<br> |<br>Stage<br> |Documentation |
|---|---|---|---|---|---|
|1 |Dual\-tunnel mode for IPsec\-VPN connection |Two encrypted tunnels are supported in primary/secondary mode. When the primary tunnel fails, traffic can be switched to the secondary tunnel for normal transmission. The two encrypted tunnels are deployed in different availability zones. This enables disaster recovery at the availability zone level.​ |<br>All<br> |<br>Invite\-only Beta<br> |[Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |
|2 |Client certificate reuse |When this feature is enabled, a certificate created by the SSL\-VPN server supports multiple clients connecting simultaneously.​ ||<br>GA<br> |[Creating an SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-client-certificate) |

## July 22, 2025

|No. |Feature |Description |<br>Region<br> |<br>Stage<br> |Documentation |
|---|---|---|---|---|---|
|1 |Alerts and monitoring |Disconnection data is monitored, and alerts are reported.​ |All |GA |* [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1)<br><br>* [Configuring health check](https://docs.byteplus.com/en/docs/vpn/Configure-health-check) |
|2 |VPN gateway |The specification of 3Gbps is supported. ||Invite\-only Beta |* [Billing for VPN gateway](https://docs.byteplus.com/en/docs/vpn/VPN-gateway-billing)<br><br>* [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |
|3 |Health check |VPN health check supports checking the source IP. ||GA |* [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1)<br><br>* [Configuring health check](https://docs.byteplus.com/en/docs/vpn/Configure-health-check) |
|4 |Optimization |Health check editing is optimized.​ ||GA |[Configuring health check](https://docs.byteplus.com/en/docs/vpn/Configure-health-check) |

## June 4, 2025

|No. |Feature |Description |<br>Region<br> |<br>Stage<br> |Documentation |
|---|---|---|---|---|---|
|1 |Invite\-only Beta to GA |BGP dynamic routing and 300/400M bandwidth for the VPN gateway are now generally available.​ |All |GA |* [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2)<br><br>* [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |
|2 |Console optimization |TR\- IPsec does not support health checks. ||GA |[Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) |

## April 1, 2025

|No. |Feature |Description |<br>Region<br> |<br>Stage<br> |Documentation |
|---|---|---|---|---|---|
|1 |Console optimization |The link opening behavior on the console is optimized. Project display is unified as the owning project.​ |All |GA |* [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2)<br><br>* [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1) |

## February 12, 2025

|No. |Feature |Description |<br>Region<br> |<br>Stage<br> |Documentation |
|---|---|---|---|---|---|
|1 |Tag resource governance |Customer Gateway, IPsec\-VPN Connection, SSL\-VPN Server, and SSL Client Certificate are integrated with the platform Tag system.​ |All |<br>GA<br> |* [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1)<br><br>* [Tag management](https://docs.byteplus.com/en/docs/vpn/Tag-management) |
|2 |VPN gateway |A single VPC supports multiple VPN gateways. ||<br>GA<br> |* [Limits](https://docs.byteplus.com/en/docs/vpn/Limits)<br><br>* [Quota management](https://docs.byteplus.com/en/docs/vpn/Quota-management)<br><br>* [VPN gateway FAQs](https://docs.byteplus.com/en/docs/vpn/VPN-gateway-FAQs) |

##
