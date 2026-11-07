---
title: "Release notes"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/web-application-firewall-release-notes"
---

This article introduces the feature release and documentation dynamics of various versions of the web application firewall. We welcome you to experience the new features of the product.

<span id="27rSsQur"></span>
## August 2025


|Release time |Function |Description |
|---|---|---|
|2025\-08\-12 |Log management |When the Content\-Encoding type is gzip or deflate, the WAF log will return the response body content in Base64 encoding format; for other Content\-Encoding types, the original content will be returned. |


<span id="2452010c"></span>
## February 2025


|Release time |Function |Description |
|---|---|---|
|2025\-02\-26 |System management \- Instance management |* Adding elastic QPS post\-paid capability based on prepaid instance specifications helps you cope with sudden traffic during peak business periods, avoiding throttling due to exceeding purchased specification QPS.<br><br>* The original time\-limited free features begin to charge, including logging body, smart rate limiting, API smart management, advanced bot protection, and bot behavior mapping. All new users are provided with a free trial period not exceeding 15 days. |


<span id="a238b768"></span>
## January 2025


|Release time |Function |Description |
|---|---|---|
|2025\-01\-07 |Website configuration |Under the CNAME access method, support obtaining the client IP through TOA method (from the option field of TCP). |


<span id="6dc4576b"></span>
## December 2024


|Release time |Function |Description |
|---|---|---|
|2024\-12\-16 |Website configuration |When accessing via CNAME and CLB layer 4 TCP, it supports logging request bodies and response bodies, facilitating monitoring analysis, debugging, and troubleshooting. |
|2024\-12\-16 |Protection strategy |The vulnerability protection policy supports configuring parameters related to high\-frequency scanning and directory traversal, achieving a vulnerability protection effect that better matches your actual scenario. |


<span id="8508e090"></span>
## November 2024


|Release time |Function |Description |
|---|---|---|
|2024\-11\-28 |Protection policy |* Bot protection supports multiple matching conditions to meet more refined condition configurations.<br><br>* Unify the types of handling actions between different strategies. |


<span id="f007a35e"></span>
## October 2024


|Release time |Function |Description |
|---|---|---|
|2024\-10\-22 |Project access |Integration of instances and domain resources with the BytePlus official website project to achieve resource group isolation, helping to improve resource management efficiency and reduce operational risks. |
|2024\-10\-22 |Protection strategy |In advanced conditions, the client IP field supports matching geographic locations, facilitating the setting of statistical conditions based on IP geographic locations. |
|2024\-10\-22 |Security Panorama and Overview |* Supports custom chart layouts to display or hide charts as needed.<br><br>* Supports adding a log service (TLS) dashboard to the overview page for easy access to related logs and protection data. |


<span id="3349bd79"></span>
## September 2024


|Release time |Function |Description |
|---|---|---|
|2024\-09\-26 |Website access |Under the CNAME access method, the origin configuration adds the Server Name Indication (SNI) parameter configuration. |
|2024\-09\-26 |Attack details |Added "Attack Details" module to summarize and display attack detail data for centralized viewing of attack event information. |
|2024\-09\-26 |Log management |Support custom log header fields that record as needed, configuring the headers that need to be counted. |


<span id="4f765fb5"></span>
## August 2024


|Release time |Function |Description |
|---|---|---|
|2024\-08\-30 |Protection strategy |Supplement the execution action description of the protection strategy to help you understand the differences between different execution actions. |
|2024\-08\-30 |Protection strategy |Supports configuration of protection settings for WebSocket traffic. By setting the request path corresponding to the WebSocket protocol, you can distinguish between regular HTTP requests and WebSocket requests, avoiding duplicate traffic statistics. |
|2024\-08\-14 |Website access |On the page where the website access is completed, a new policy configuration navigation has been added to help you quickly enable the relevant policy protection functions. |
|2024\-08\-08 |Website access |Support for DDoS native protection for enterprise edition, adding the EIP of cloud WAF to the DDoS native protection resource package, enhancing security protection capability, |


<span id="4b814ef7"></span>
## July 2024


|Release time |Function |Description |
|---|---|---|
|2024\-07\-30 |Security Panorama and Overview |The page adds a new user guide module to help you quickly access WAF protection. |
|2024\-07\-16 |Website access |Under the CNAME access method, supports shared VPC backhaul. |
|2024\-07\-05 |Security Panorama and Overview |Support custom report export, with filters for time, domain, and report type. |
|2024\-07\-05 |Protection strategy \- Access control |Supports the creation of access control policies based on IP geographical location, including domestic and overseas regions. |


<span id="a51f6d25"></span>
## June 2024


|Release time |Function |Description |
|---|---|---|
|2024\-06\-28 |Protection Policy \- Bot Management |* The Bot hosting rules add the "release" action, and the released traffic is not subject to detection by all rules of the Bot module.<br><br>* Support configuring the Bot behavior map, intelligently tracking and analyzing discovered and confirmed API access behaviors and corresponding traffic based on the domain name dimension, and providing a visual queue chart. |
|2024\-06\-28 |Website access |Support batch import of domain information; domain information under different access methods must be filled out according to different template requirements. |


<span id="e70ce270"></span>
## May 2024


|Release time |Function |Description |
|---|---|---|
|2024\-05\-28 |Website access |New ALB instance access capability.<br><br><br>* If your protected domain name has been connected to the ALB instance, the protection rules will take effect according to the domain name.<br><br>* If your protected domain name has not yet been connected to the ALB instance, WAF will create a default protection site and name it according to the ALB ID. |
|2024\-05\-28 |Website access |In scenarios where multiple ALB instances are accessed under the same protection domain, it supports configuring the protection mode for a single ALB instance. |
|2024\-05\-28 |Website access |Interface optimization upgrade, supporting the filtering of protection website lists by access type. |
|2024\-05\-15 |Protection policy \- Access control |Supports the association of the Blocklist and Allowlist domain groups, and batch configuration of access control rules. |
|2024\-05\-15 |Protection Strategy \- API Protection |The default action for API route protection has been changed to "no check". |


<span id="994d1410"></span>
## April 2024


|Release time |Function |Description |
|---|---|---|
|2024\-04\-07 |Protection policy \- API protection |* The API interface supports traffic\-based automatic discovery features.<br><br>* Increase sensitive information label. |
|2024\-04\-07 |Protection strategy \- Bot management |* Add frequency limiting protection.<br><br>* Add field\-based duplicate statistics protection.<br><br>* Add JS challenges, proof of work, and discard disposal actions.<br><br>* Support detection and protection based on dynamic tokens. |
|2024\-04\-07 |System management \- Certificate management |Support hosting HTTPS certificates through the Certificate Center. |


<span id="5ebddf13"></span>
## March 2024


|Release time |Function |Description |
|---|---|---|
|2024\-03\-07 |Website access |Load balancing layer 4 TCP access supports IPv6 access. |
|2024\-03\-07 |Website access |Optimize website list search, filter, and sorting functions. |


<span id="2f0e9322"></span>
## January 2024


|Release time |Functional |Description |
|---|---|---|
|2024\-01\-31 |All |Open API release, including website access, protection policy configuration, IP address group management, and certificate management. |
|2024\-01\-31 |Website access |Supports Layer 4 TCP access from the load balancer. |


<span id="32eff747"></span>
## November 2023


|Release time |Function |Description |
|---|---|---|
|2023\-11\-04 |Website access |Unified access method, supporting CNAME access, load balancing access, and application load balancing access methods within the same WAF instance. |
|2023\-11\-04 |Website access |In CNAME access method, supports configuring TLS version and corresponding encryption suite. |
|2023\-11\-04 |System Management \- Instance Management |When the traffic QPS exceeds the specifications of the purchased package, the traffic is normally forwarded through the WAF but is not subjected to protection detection. |
|2023\-11\-30 |Security Panorama and Overview |The overview topology displays the access method and origin information, with origin information showing the public IP address or VPC and internal IP addresses. |
|2023\-11\-30 |Website access |In the CNAME access method, add configurations for long connection consumption, timeout, and other parameters. |
|2023\-11\-30 |Protection strategy \- Access control |Geographical access control policy, updates geographical location database information, covering all public IP addresses. |


<span id="046d403e"></span>
## October 2023


|Release time |Function |Description |
|---|---|---|
|2023\-10\-14 |Website access |The cloud WAF instance supports IPv6 access and source return. |


<span id="4b201fb4"></span>
## September 2023


|Release time |Function |Description |
|---|---|---|
|2023\-09\-28 |Security Panorama and Overview |Increase security time and details of attack requests.<br><br><br>* Display aggregated security events based on attacks.<br><br>* Show attack request information for security protection modules.<br><br>* Support the display of policy rule update times. |
|2023\-09\-28 |System Management \- IP address group |* Supports adding IP address group<br><br>* Supports access control policy referencing IP address group |


<span id="90637662"></span>
## August 2023


|Release time |Function |Description |Related documents |
|---|---|---|---|
|2023\-08\-21 |Protection Strategy \- Vulnerability Protection |* New secondary directory added for protection types, with the ability to view specific vulnerability protection rules under each secondary directory.<br><br>* Optimized the display effect of the existing protection level interface, supporting the viewing of rule details corresponding to different protection levels.<br><br>* Added custom protection rules based on managed rules, supporting the on\-demand activation of vulnerability detection rules. |[Configure protection strategy](https://docs.byteplus.com/en/docs/waf/docs-configuring-vulnerability-protection-policies) |
|2023\-08\-21 |Block management |* Supports centralized viewing of IP information that triggered WAF protection rules, including the number of attacks, facilitating unified management.<br><br>* Supports adding IPs from the blocklist to the allowlist or blocklist as needed based on the scenario, without the need for subsequent detection and verification. After successful addition, WAF automatically generates an access allowlist or blocklist rule. |[View the banned IP list](https://docs.byteplus.com/en/docs/waf/View_the_blocked_IP_list) |
