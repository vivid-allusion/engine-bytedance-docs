---
title: "New feature release notes"
product: "Direct Connect"
product_code: "directconnect"
section: "Document"
source: "https://docs.byteplus.com/en/docs/directconnect/What-is-New"
---

This topic describes feature release updates for Direct Connect (DC) versions. New features will roll out across regions gradually. Explore them now.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Beta products or features are not yet available to all users. To better understand the product, some companion documents for Beta products or features are available to all users. Meanwhile, some companion documents for Beta products or features are only visible to users who have enabled product capabilities. If you need a trial of Beta products or features, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">The availability of regions and areas varies by product or feature. The regions available in the console shall prevail.</div>



<span id="epvdZymQ"></span>
## July 2026


|<div style="text-align: center"><br>No.</div><br> |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |<div style="text-align: center"><br>Status</div><br> |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|
|1 |DC Connection |DC Connections with MACsec functionality are now available for application. |<div style="text-align: center"><br>GA</div><br> |[Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) |
|2 |DC Connection |Optimized the onboarding process for DC Connections. |<div style="text-align: center"><br>GA</div><br> |[Direct Connect access process](https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-access-procedure) |
|3 |Global Direct Exchange Gateway |Global Direct Exchange Gateway (DXGW) launched for the first time. |<div style="text-align: center"><br>Beta</div><br> |[Global Direct Exchange Gateway overview](https://docs.byteplus.com/en/docs/directconnect/Direct_Exchange_Gateway_overview) |


<span id="5y4WsgpG"></span>
## November 2025


|<div style="text-align: center"><br>No.</div><br> |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |<div style="text-align: center"><br>Status</div><br> |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|
|1 |DC Connection |Bare fiber DC connections may face link stability risks due to environmental factors, with potential downtime lasting hours or days. Be aware and fully assess your business situation to deploy disaster recovery. |<div style="text-align: center"><br>GA</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Preparation-for-access">Preparations before access</a></div><br> |


<span id="yj9byvAp"></span>
## October 2025


|<div style="text-align: center"><br>No.</div><br> |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |<div style="text-align: center"><br>Status</div><br> |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|
|1 |Cross\-account authorization for Edge Interconnect |The DC Gateway supports attaching Edge Interconnect (EIC) for efficient and stable private network communication between edge nodes. |<div style="text-align: center"><br>Beta</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/6407/1847916">Cross\-account authorization for Edge Interconnect</a></div><br> |
|2 |Add disabled CIDR blocks for Virtual Interface |The Virtual Interface adds the following disabled CIDR blocks for interconnect IPs.<br><br><br>* IPv4: `169.254.0.0/16`.<br><br>* IPv6: `FC01:A9FE::0/64`, `FE80:0:0:0:A9FE::/80`. |<div style="text-align: center"><br>GA</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1">Creating a Virtual Interface</a></div><br> |


<span id="yj9byvAp"></span>
## October 10, 2025


|<div style="text-align: center"><br>No.</div><br> |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |<div style="text-align: center"><br>Region</div><br> |Stage |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|---|
|1 |DC health check |China (Guangzhou) region supports Health Check feature. |<div style="text-align: center"><br>China (Guangzhou)</div><br> |<div style="text-align: center"><br>GA</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Direct_Connect_health_check_overview">Direct Connect Health Check overview</a></div><br> |
|2 |Outbound traffic package |An outbound traffic package is a prepaid traffic package provided by DC. After purchase, it automatically offsets the outbound traffic fee generated by your DC gateway, offering a more cost\-effective solution compared to Pay\-as\-you\-go. |<div style="text-align: center"><br>All</div><br> ||<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Outbound_Traffic_Package_overview">Outbound Traffic Package overview</a></div><br> |
|3 |QoS Policy feature becomes GA |DC supports QoS Policy. After attaching a DC Connection to a QoS Policy, outbound traffic can be scheduled according to the related QoS Policy. |||<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview">QoS Policy overview</a></div><br> |
|4 |DC Connection metric monitoring |Support monitoring average bandwidth rate and average packet loss rate of QoS traffic queues; support monitoring bandwidth rate limiting for Virtual Interface. |||<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Viewing-the-indicator-monitoring-data">Viewing monitoring data</a></div><br> |
|5 |Apply for a DC Connection LOA |If the DC Connection access location is outside China, there is no need to fill in the Field Engineer information. |||<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1">Creating a Direct Connect Connection</a></div><br> |
|6 |Line detection supports BFD detection \- echo packet mode |BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. ||<div style="text-align: center"><br>Beta</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Detection methods</a></div><br> |


<span id="LTDeotuq"></span>
## September 30, 2025


|No. |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |Region |<div style="text-align: center"><br>Stage</div><br> |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|---|
|1 |Virtual Interface interconnect IP restriction |The following restrictions apply to Virtual Interface interconnect IP segments:<br><br><br>* IPv4 interconnect IP cannot use the segment: `169.254.0.0/16`.<br><br>* IPv6 interconnect IP cannot use the segments: `FC01:A9FE::0/64`, `FE80:0:0:0:A9FE::/80`. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |<div style="text-align: center"><br><a href="https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1">Creating a Virtual Interface</a></div><br> |


<span id="1u0QMyMg"></span>
## July 24, 2025


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |DC Connection supports 400Gbps optical port specifications |Dedicated Line **Classic** mode’s Beijing\-Langfang\-C access point supports 400Gbps optical ports and user\-to\-cloud interconnection. |<div style="text-align: center"><br>China (Beijing)</div><br> |<div style="text-align: center"><br>Beta</div><br> |[Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) |
|2 |DC health check |When you transmit business data between cloud/on\-premises BytePlus and the third\-party cloud via a DC Connection, and any significant network fluctuations or unstable transmission links occur, you can use the DC health check to identify and detect network issues. |China (Beijing), Asia Pacific (Johor) |<div style="text-align: center"><br>GA</div><br> |[Direct Connect Health Check overview](https://docs.byteplus.com/en/docs/directconnect/Direct_Connect_health_check_overview) |


<span id="ws1t6K69"></span>
## June 4, 2025


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Custom ASN feature of the DC Gateway moves to GA |DC Gateway supports custom ASN, allowing you to set the ASN according to your needs. This applies when the DC Gateway is connected to multiple Cloud Enterprise Networks (CENs). |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |[Creating a Direct Connect Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1) |


<span id=".MjAyNOW5tDEy5pyIMDbml6U="></span>
## February 12, 2025


|<div style="text-align: center"><br>No.</div><br> |<div style="text-align: center"><br>Feature</div><br> |<div style="text-align: center"><br>Description</div><br> |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |<div style="text-align: center"><br>Documentation</div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>1</div><br> |Dedicated Line supports high reliability mode |The access point mode of the DC Connection supports Classic mode and high reliability mode. |<div style="text-align: center"><br>All</div><br> |GA |[Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) |


<span id=".MjAyNOW5tDEy5pyIMDbml6U="></span>
## December 06, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Supports QoS policy |Direct Connect supports QoS policies. After linking the DC Connection with a QoS policy, traffic outbound to the cloud can be queued and scheduled according to the related QoS policy. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>Beta</div><br> |[QoS Policy overview](https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview) |
|2 |Direct Connect alarm policy adds Direct Connect status |Create CloudMonitor alarm policies to monitor the status of DC Connections. It is recommended to monitor only DC Connections in the Enabled status to avoid false alarms caused by incomplete construction of some connections. ||<div style="text-align: center"><br>GA</div><br> |[Creating a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) |


<span id=".MjAyNOW5tDA55pyIMjTml6U="></span>
## September 24, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |DC Gateway supports project management |The DC Gateway integrates with the project. You can manage DC Gateway resources by project and categorize and perform accounting through projects. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |[Project management](https://docs.byteplus.com/en/docs/directconnect/Project-management) |
|2 |DC Gateway supports custom ASN |The DC Gateway supports custom ASN, allowing the ASN to be customized according to actual needs. This applies to scenarios where the DC Gateway is connected to multiple Cloud Enterprise Networks (CENs). ||<div style="text-align: center"><br>Beta</div><br> |[Creating a DC Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1) |


<span id=".MjAyNOW5tDA55pyIMjDml6U="></span>
## September 20, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Shared Line beta to GA |The Shared Line feature officially becomes GA. Shared Line operators can create shared lines for tenants, allowing tenants to use the shared lines created by operators directly. To become a Shared Line operator, you must first submit an application to BytePlus. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |* [Line operator guide](https://docs.byteplus.com/en/docs/directconnect/Operator-operation-guide)<br><br>* [Tenant guide](https://docs.byteplus.com/en/docs/directconnect/Tenant-operation-guide) |


<span id=".MjAyNOW5tDA35pyIMTnml6U="></span>
## July 19, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |New inbound bandwidth speed limit for Virtual Interface |The bandwidth rate limiting for the Virtual Interface has changed from outbound\-only to bidirectional rate limiting. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |[Creating a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface) |
|2 |Provide self\-service documentation for troubleshooting Direct Connect faults |Add documentation for common issues and self\-troubleshooting solutions of new DC Connections. |||[Direct Connect troubleshooting guide​​](https://docs.byteplus.com/en/docs/directconnect/Troubleshooting-and-solutions-for-Direct-Connect-issues) |


<span id=".MjAyNOW5tDA15pyIMjnml6U="></span>
## May 29, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Supports Shared Virtual Interface capability |DC Connection supports creating Shared Virtual Interfaces for other accounts to use, enabling multiple accounts to share one physical connection. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>Beta</div><br> |[Creating a Shared Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Create-shared-Direct-Connect-Virtual-Interface) |
|2 |The port fee is displayed on the physical port order page |Product optimization supports displaying the port resource occupancy fee price on the DC Connection order page. ||<div style="text-align: center"><br>GA</div><br> |Not applicable |


<span id=".MjAyNOW5tDA05pyIMTLml6U="></span>
## April 12, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Modify DC Connection bandwidth |Supports modifying the bandwidth of a DC Connection, allowing bandwidth adjustment anytime after creation. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |[Modifying bandwidth for a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Modify-dedicated-line-bandwidth) |
|2 |Provide on\-premises switch configuration examples |Provide on\-premises data center's switch configuration examples as a reference for your setup approach. ||<div style="text-align: center"><br>GA</div><br> |* [Configuration examples for on-premises data centers in static routing](https://docs.byteplus.com/en/docs/directconnect/Configuration_examples_for_on-premises_data_centers_in_static_routing)<br><br>* [Configuration examples for on-premises data centers with BGP](https://docs.byteplus.com/en/docs/directconnect/Configuration_examples_for_on-premises_data_centers_with_BGP) |
|3 |Identity and Access Management (IAM) documentation optimization |Optimize and organize access control documentation, supplement common custom access policies for the DC product. ||<div style="text-align: center"><br>GA</div><br> |[IAM overview](https://docs.byteplus.com/en/docs/directconnect/Identity-and-access-management) |


<span id=".MjAyNOW5tDAx5pyIMTnml6U="></span>
## January 19, 2024


|No. |Feature |Description |<div style="text-align: center"><br>Region</div><br> |<div style="text-align: center"><br>Stage</div><br> |Documentation |
|---|---|---|---|---|---|
|1 |Event alert |Direct Connect supports configuring event monitoring alarm rules. |<div style="text-align: center"><br>All</div><br> |<div style="text-align: center"><br>GA</div><br> |[Configuring event monitoring](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts) |


<span id=".MjAyM-W5tDA55pyIMTPml6U="></span>
##
