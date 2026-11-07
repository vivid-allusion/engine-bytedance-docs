---
title: "New feature release notes"
product: "Transit Router"
product_code: "transitrouter"
section: "Document"
source: "https://docs.byteplus.com/en/docs/transitrouter/Whats-New-01"
---

This topic introduces feature updates for Transit Router (TR) in each version. New features will be gradually available in all regions. We welcome you to explore them.

> **tip**

* > Invite\-only Beta products or features are not yet available to all users. To better understand the product, some companion documents for Invite\-only Beta products or features are available to all users. Meanwhile, some companion documents for Invite\-only Beta products or features are only visible to users who have enabled product capabilities. To request access to an Invite\-only Beta product or feature, please contact your account manager.

* > Available regions may vary by product or feature. The regions available in the console shall prevail.

## September 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Local Peer Attachment |Supports connectivity between two TR instances in the same region, enabling intercommunication between the two TR\-connected networks. |Beta |[Creating a local peer attachment](https://docs.byteplus.com/docs/transitrouter/Creating_a_local_peer_attachment) |
|2 |Editing support for traffic queue and traffic marking policies |Now supports editing existing traffic queue policies and traffic marking policies. |GA |* [Managing a traffic marking entry](https://docs.byteplus.com/en/docs/transitrouter/Managing-entries-of-qos-marking-policy)<br><br>* [Managing a queue](https://docs.byteplus.com/en/docs/transitrouter/Managing-queues-of-a-qos-queue-policy) |

## July 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Cross\-border bandwidth package |China Telecom Cross\-border Bandwidth Package is released from Invite\-only Beta to GA. |GA |[Create bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01) |
|2 | Network instance attachment |Cross\-account network instance attachments now can be forcibly deleted, bypassing resource dependency restrictions. |GA |[Deleting an intra-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-03) |
|3 |Monitoring enhancement |Supports viewing more monitoring data for bandwidth packages. |GA |[Viewing the monitoring data](https://docs.byteplus.com/en/docs/6979/2533601) |

## May 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Billing |Cross\-region traffic now supports pay\-as\-you\-go billing, integrated with Cloud Data Transfer (CDT) for unified billing. |GA |[Route overview](https://docs.byteplus.com/en/docs/cen/Route-entries-01)<br><br> |

## April 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |VPC\-granular route learning is released from Invite\-only Beta to GA. |TR now supports learning routes of the VPC CIDR block, reducing the number of routes in the TR and simplifying route complexity. |GA |[Managing route learning](https://docs.byteplus.com/docs/transitrouter/Route-tables-06) |
|2 |Fee payer configuration is released from Invite\-only Beta to GA. |Shared TR now supports configuring a fee payer, with connection fees and traffic processing fees charged to the account you specify. |GA |[Configuring a fee payer](https://docs.byteplus.com/en/docs/transitrouter/Configuring_a_fee_payer) |
|3 |Prefix List is released from Invite\-only Beta to GA. |Transit Router supports prefix lists when creating static routes and routing policies, improving routing configuration efficiency. |GA |* [Manage a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05)<br><br>* [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) |

## March 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |QoS management |TR now supports modifying bandwidth percentages for traffic queues. |GA |[Modifying bandwidth allocation](https://docs.byteplus.com/en/docs/transitrouter/Managing-queues-of-a-qos-queue-policy) |
|2 |Prefix List |Transit Router supports prefix lists when creating static routes and routing policies to improve routing configuration efficiency. |Invite\-only Beta |* [Manage a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05)<br><br>* [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) |

## February 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Billing |TR now supports selecting the TR owner account as the fee payer for cross\-account network instance attachments, covering both attachment fees and traffic processing fees. This feature is currently available only in China (Shanghai). |Invite\-only Beta |[Configuring a fee payer](https://docs.byteplus.com/en/docs/transitrouter/Configuring_a_fee_payer) |

## January 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Route learning |TR now supports route learning at the VPC granularity (i.e., the destination CIDR block is the VPC CIDR), reducing the number of routes and simplifying route complexity. |Invite\-only Beta |[Managing route learning](https://docs.byteplus.com/docs/transitrouter/Route-tables-06) |
|2 |Cross\-account management |The cross\-account capability is provided by TR through the resource sharing platform and is generally available. |GA |[Features](https://docs.byteplus.com/docs/transitrouter/Features) |
|3 |Inter\-region attachment |TR now supports changing the bandwidth package associated with an inter\-region attachment. |GA |* [Modifying bandwidth for an inter-region attachment](https://docs.byteplus.com/docs/transitrouter/Inter-region-peering-attachments-03)<br><br>* [Transit Router FAQs](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instance-faq) |

## November 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Optimization |TR's cross\-border bandwidth packages now default to China Telecom. |GA |[Create bandwidth package](https://docs.byteplus.com/docs/transitrouter/TR-bandwidth-packages-01) |
|2 |Availability zone launch |TR now supports Asia Pacific (Jakarta) Availability Zone C. |GA |\-\- |
|3 |Route learning |TR now supports route learning at the VPC granularity (i.e., the destination CIDR block is the VPC CIDR), and supports publishing routes with VPC CIDR as the destination CIDR to the DC Gateway. This reduces the number of routes and simplifying route complexity. |Invite\-only Beta |[Creating a VPC attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-vpc) |
|4 |Cross\-account sharing |Inter\-region attachments now support establishing connections across accounts, enabling connectivity between two TRs in different accounts and regions. |Invite\-only Beta |* [Cross-account Management overview](https://docs.byteplus.com/docs/transitrouter/Cross-account-Sharing-overview)<br><br>* [Accepting a cross-account peering attachment](https://docs.byteplus.com/docs/transitrouter/Accepting_a_cross-account_peering_attachment)<br><br>* [Rejecting a cross-account peering attachment](https://docs.byteplus.com/docs/transitrouter/Rejecting_a_cross-account_peering_attachment) |
|5 |Flow Log |TR now supports cross\-region flow logs, allowing users to directly monitor the traffic of cross\-region services. |GA |[Flow Log overview](https://docs.byteplus.com/docs/transitrouter/Flow-log-overview) |

## October 14, 2025

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Cross\-account resource sharing |TR supports resource sharing, allowing TR instances in the same region under my account—including VPC, Direct Connect, and VPN network instances—to connect and share access with other accounts or enterprise organizations. |All |GA |* [Cross-account Sharing overview](https://docs.byteplus.com/docs/transitrouter/Cross-account-Sharing-overview)<br><br>* [Cross-account Transit Router sharing​​](https://docs.byteplus.com/docs/transitrouter/Cross-account-Transit-Router-sharing) |
|2 |Intelligent Assistant |The TR connects to BytePlus Intelligent Assistant, supporting AI interactions on the console page to quickly obtain relevant information. ||GA |\-\- |

## August 1, 2025

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Monitoring feature |TR now displays monitoring metrics for rate limiting and packet loss. |All |GA |[Viewing the monitoring data](https://docs.byteplus.com/docs/transitrouter/Monitoring-01) |
|2 ||TR now supports monitoring capability at the availability zone level. ||GA |[Viewing the monitoring data](https://docs.byteplus.com/docs/transitrouter/Monitoring-01) |
|3 |Route policy |Fuzzy match is supported for matching route prefix of route policies. ||GA |* [Route Policy overview](https://docs.byteplus.com/docs/transitrouter/Overview-of-routing-policy)<br><br>* [Creating a route policy](https://docs.byteplus.com/docs/transitrouter/Creating-a-routing-policy) |
|4 |Cross\-region traffic analysis |Network Advisor (NA) is now integrated, enabling the TR service with cross\-region traffic analysis capabilities. ||GA |[Cross Region Traffic](https://docs.byteplus.com/docs/transitrouter/Managing-traffic-analysis) |

## June 4, 2025

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Cross\-region connectivity |TR is now available in China Mainland regions. |All |GA |[Areas and Regions](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05) |

## April 1, 2025

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Forwarding policy |TR now supports forwarding policy configuration based on source\-destination IP pairs. |All |GA |* [Forwarding Policy overview](https://docs.byteplus.com/docs/transitrouter/Overview-of-forwarding-policy)<br><br>* [Creating a forwarding policy](https://docs.byteplus.com/docs/transitrouter/Creating-a-forwarding-policy) |
|2 |IPv6 |TR now supports IPv6 route learning and propagation. ||Invite\-only Beta |* [Instance sharing overview](https://docs.byteplus.com/docs/transitrouter/Instance-sharing-01)<br><br>* [Creating a VPC attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-vpc)<br><br>* [Enabling or disabling IPv6](https://docs.byteplus.com/docs/transitrouter/Enabling-Disabling-the-IPv6) |
|3 |Optimization |Editing of VPC attachment points is now enhanced to support simultaneous modification of attachment points and IPv6 toggles. ||Invite\-only Beta |[Editting an attachment point](https://docs.byteplus.com/docs/transitrouter/Attachments-02) |
|4 |Bandwidth Package |Pay\-by\-95th\-peak is now supported for TR bandwidth packages. | |Invite\-only Beta |[Billing for VPN gateway](https://docs.byteplus.com/en/docs/transitrouter/Billing-rules) |

## January 22, 2025

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Optimization |TR now provides a bandwidth package renewal page. |All |GA |[Expiration](https://docs.byteplus.com/docs/transitrouter/Expiration) |

## December 6, 2024

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Route policy |The input field in route policy configuration now supports over 200 route entries, automatically recognizing entries separated by either English (;) or Chinese (；) semicolons. |All |GA |[Creating a route policy](https://docs.byteplus.com/docs/transitrouter/Creating-a-routing-policy) |
|2 |Invite\-only Beta to GA |Custom ASN is generally available. ||GA |[Creating a Transit Router instance](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instances-01) |
|3 |Optimization |When attaching a DC Gateway, filter can be performed by projects. ||GA |[Creating a DC Gateway attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-dc) |
|4 ||The status of low\-priority inactive routes is now optimized from "Conflicted" to "Not Effective." ||GA |[Route table overview](https://docs.byteplus.com/docs/transitrouter/Route-tables-01#.6Lev55Sx5LyY5YWI57qn) |
|5 |QoS management |TR now supports QoS rate limiting for different traffic configurations in cross\-region interconnection scenarios. ||Invite\-only Beta |* [Deleting a Transit Router instance](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instances-04)<br><br>* [Deleting an inter-region attachment](https://docs.byteplus.com/docs/transitrouter/Inter-region-peering-attachments-04)<br><br>* [QoS management](https://docs.byteplus.com/docs/transitrouter/Qos-overview) |

## September 10, 2024

|Serial number |Feature |Description |Region |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Route learning support for VPN attachments |TR now supports automatic route learning and propagation for IPsec\-VPN connections. |All |Invite\-only Beta |* [Creating a VPN attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-vpn)<br><br>* [Enabling or disabling auto publishing](https://docs.byteplus.com/docs/transitrouter/Attachments-04)<br><br>* [Route table overview](https://docs.byteplus.com/docs/transitrouter/Route-tables-01)<br><br>* [Implementing interconnectivity between independent VPCs and a data center](https://docs.byteplus.com/docs/transitrouter/Best-Practices-02)<br><br>* [Route FAQs](https://docs.byteplus.com/docs/transitrouter/Routing-faq) |

## May 29, 2024

|**No.**  |**Feature** |**Description** |**Region** |**Stage** |**Documentation** |
|---|---|---|---|---|---|
|1 |Intra\-attachment |VPC attachment supports setting default Available Zone. |All |GA |[Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) |
|2 |Forwarding policy |TR supports forwarding policy, selects different route tables based on the source address of the business data packet for forwarding, enriches the route ability, and increases network flexibility. ||GA |[Forwarding Policy](https://docs.byteplus.com/en/docs/transitrouter/Forwarding-Policy) |
|3 |Routing policy |TR supports routing policy, which can control the propagation scope and AsPath attribute of different routes, and supports customers to perform more flexible and fine\-grained route control. ||GA |[Routing Policy](https://docs.byteplus.com/en/docs/transitrouter/Routing-Policy) |
|4 |Monitoring |Configure metric meaning and support preset alarm templates. ||GA |[Configuring an alert policy](https://docs.byteplus.com/en/docs/transitrouter/Configuring-an-alert-policy) |

## April 12, 2024

|**No.**  |**Feature** |**Description** |**Region** |**Stage** |
|---|---|---|---|---|
|1 |Transit Router |Transit Router was released. |All |GA |

##
