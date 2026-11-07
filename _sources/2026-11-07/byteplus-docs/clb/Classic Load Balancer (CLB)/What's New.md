---
title: "What's New"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Whats-New"
---

This topic introduces the feature releases and related documentation updates for each Classic Load Balancer (CLB) version. New features will be gradually released across Regions for you to experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Products or features in beta stage are not yet available to all users. To help users understand the product, documentation for some beta products/features is open to all users, while documentation for others is visible only to users who have the corresponding product capability enabled. To request access to a beta product or feature, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">The availability of regions and areas varies by product or feature. The regions available in the console shall prevail.</div>



<span id="5QilPqb4"></span>
## September 2026


|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Listener |HTTPS listener supports TLS v1.3. |GA |[Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener) |


<span id="f14vhsda"></span>
## August 2025


|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Product rename |The original Load Balancer Cloud Load Balancer has been renamed to Classic Load Balancer. |GA |[What is a Classic Load Balancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) |
|2 |Query optimization |The CLB instance list page supports searching CLB instances by backend server IP address and ID. |GA |[CLB FAQ](https://docs.byteplus.com/en/docs/clb/CLB-instance-faq) |
|3 |Health metrics |Outbound and inbound bandwidth usage is split into two metrics: outbound bandwidth usage and inbound bandwidth usage, and displayed separately. |GA |\-\- |


<span id=".MjAyNOW5tDEy5pyIMDbml6U="></span>
## April 2025


|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Experience optimization |When non\-global IAM users add backend servers to CLB instances, they can select backend servers from different projects. |GA<br><br><div style="text-align: center"><br></div><br> |\- |
|2 ||When adding servers, the maximum quantity per batch increased from 20 to 40. ||\- |
|3 ||Integrate with TLS tag service; deleting is forbidden when health check log projects are BOUND to CLB instances. ||[Health check log overview](https://docs.byteplus.com/en/docs/clb/Health-check-log-01) |
|4 |Access log (7\-Layer) delivery to TLS |Support access log delivery of Layer 7 listeners to Torch Log Service (TLS). ||[Access log delivery to TLS](https://docs.byteplus.com/en/docs/clb/Access-Log-Delivery-to-TLS) |


<span id=".MjAyNOW5tDEy5pyIMDbml6U="></span>
## February 2025


|No. |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Tags |Forwarding rules support tags. Tags are used for marking and categorizing. You can search for and view forwarding rules by tags. |GA |[Add forwarding rule](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule) |
|2 |Deleting the CLB instance |Support one\-click deletion of CLB instances without deleting listeners and backend server groups first. |GA |[Deleting the CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-09) |


<span id="AnpWEmIm"></span>
## November 2024


|**No.**  |**Feature** |**Description** |**Stage** |**Document** |
|---|---|---|---|---|
|1 |Connect to Certificate Center |CLB certificates are connected to the Certificate Center for convenient centralized management. |GA |[Certificate Overview](https://docs.byteplus.com/en/docs/clb/Certificate-management-01) |
|2 |Modification protection |Risk reminders are supported when the modification protection feature is disabled. |GA |[Configure modification protection](https://docs.byteplus.com/en/docs/clb/CLB-instances-07) |
|3 |Deny creation of internet CLB policy |Provide custom policy example for denying IAM user to create internet CLB. |GA |[CLB FAQ](https://docs.byteplus.com/en/docs/clb/CLB-instance-faq) |


<span id="ofLbiqlc"></span>
## October 2024


|**No.**  |**Feature** |**Description** |**Stage** |**Document** |
|---|---|---|---|---|
|1 |IPv4/IPv6 Network Type Conversion |CLB supports free switching between single \- stack IPv4 and dual \- stack IPv4&IPv6. |Beta |[Changing the IP address version](https://docs.byteplus.com/en/docs/clb/Changing-the-IP-address-version) |
|2 |Listen by port range |Supports creating a layer\-4 listener for the listening port range. |Beta |* [Create a TCP Listener](https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener)<br><br>* [Create a UDP Listener](https://docs.byteplus.com/en/docs/clb/Creating-a-UDP-listener) |


<span id="E4K8ATW1"></span>
## May 2024


|**No.**  |**Feature** |**Description** |**Stage** |**Document** |
|---|---|---|---|---|
|1 |Established timeout |HTTP and HTTPS Listener supports custom configuration of established timeout, such as client_header_timeout, client_body_timeout. |GA |* [Creating an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener)<br><br>* [Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener) |
|2 |TLS security policy |HTTPS Listener supports enabling the TLS (Transport Layer Security, TLS) security policy. After enabling, you can choose the TLS security policy as needed, and there are differences in the TLS protocol versions and encryption suites supported by different policies. |GA |[Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener) |
|3 |HTTP2.0 |HTTPS Listener supports enabling HTTP2.0, which is compatible with HTTP1.x. |GA |[Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener) |
|2 |Tag |Listener and server group support tags. Tags are used for marking and classification, and can be searched and viewed according to tags. |GA |* [Creating a Listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener)<br><br>* [Creating a server group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group) |


<span id="g1SJFoxM"></span>
## April 2024


|**No.**  |**Function** |**Description** |**Stage** |
|---|---|---|---|
|1 |Cloud Load Balancer |Classic Load Balancer was released. |GA |


&nbsp;
