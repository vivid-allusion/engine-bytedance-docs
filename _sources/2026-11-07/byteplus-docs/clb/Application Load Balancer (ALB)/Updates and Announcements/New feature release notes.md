---
title: "New feature release notes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Updates-and-announcements"
---

This section provides the latest product release updates for Application Load Balancer (ALB). Stay informed and explore the new features.

### May 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Forwarding rule |The "Redirect to" of the Standard Edition ALB adds a query string configuration option. |GA |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|2 |Server Group |Backend server groups support slow start. Newly added backend server instances can have their weight linearly increased from 0 to the target value by the ALB within a specified duration, enabling smooth distribution of business traffic. |GA |[Configuring the slow start](https://docs.byteplus.com/en/docs/clb/Configuring-the-slow-start) |

### March 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Forwarding rules support Cookie |Forwarding rules of the Standard Edition ALB support Cookie. |Invite\-only Beta |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|2 |Forwarding rules support SourceIP |Forwarding rules of the Standard Edition ALB support SourceIP. |Invite\-only Beta |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|3 |Forwarding rules support cross\-origin |Forwarding rules of the Standard Edition ALB support cross\-origin. |Invite\-only Beta |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|4 |Clone ALB |ALB supports Clone. |GA |[Cloning an ALB instance](https://docs.byteplus.com/en/docs/clb/Cloning_an_ALB_instance) |
|5 |ALB instance |The Standard Edition ALB instance is generally available for commercial use. |GA |\-\- |

### January 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Custom configuration |The maximum allowed length for response header characters has been increased to 256 characters. |GA |[Custom configuration](https://docs.byteplus.com/en/docs/clb/Custom-configurations) |
|2 |Creating a forwarding rule (Standard edition) |ALB now supports domain name rewriting. |GA |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition) |

### November 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Access Log |ALB logs now support recording the servicegroup_name field, allowing you to retrieve the backend server group's name from the logs. |GA |* [Access log delivery to TOS](https://docs.byteplus.com/en/docs/clb/Sending-access-logs-to-TOS)<br><br>* [Access log delivery to TLS](https://docs.byteplus.com/en/docs/clb/Sending-access-logs-to-TLS) |
|2 |IPv6 Internet bandwidth |When creating an ALB instance, IPv6 internet bandwidth can now be added to a Bandwidth Package. |GA |[Creating an ALB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-instance) |

### October 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Extended certificate |When ALB modification protection is enabled, viewing extended certificate configurations is now supported. |GA |* [Configuring multiple certificates for an HTTPS listener (Basic Edition)](https://docs.byteplus.com/en/docs/clb/Configuring-SNI-for-an-HTTPS-listener)<br><br>* [Configuring Multiple certificates for HTTPS listeners (Standard Edition)​](https://docs.byteplus.com/en/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition) |
|2 |Custom configuration |Standard Edition ALB supports appending request header fields containing client certificate owner information and verification results. |GA |[Custom configuration](https://docs.byteplus.com/en/docs/clb/Custom-configurations) |

### **July 2025**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Forwarding rule |In forwarding rules, the forwarding condition can now be set to "Query String". |GA |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/docs/clb/Creating-a-forwarding-rule_Standard-edition) |

### **June 2025**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Forwarding rule |In forwarding rules, the forwarding condition can now be set to "HTTP Request Method". |GA |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|2 |Forwarding rule |In forwarding rules, the forwarding action can now be set to "Return Fixed Response", allowing users to customize the response status code and body. |GA |[Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/docs/clb/Creating-a-forwarding-rule_Standard-edition) |
|3 |Server Group |When adding backend servers, users can now batch\-set the same port and weight for multiple servers. |GA |[Add Server](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5re75Yqg5ZCO56uv5pyN5Yqh5Zmo) |
|4 |Server Group |Users can now configure cross\-zone load balancing at the server group level. |GA |[Create server group](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5Yib5bu65pyN5Yqh5Zmo57uE) |
|5 |Access control |Supports IPv6 address entries. |GA |[Access control](https://docs.byteplus.com/docs/clb/Access-control) |
|6 |Listener |Added support for the iQUIC protocol. |GA |[Create QUIC listener](https://docs.byteplus.com/docs/clb/Creating-a-QUIC-listener) |

### **April 2025**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Tag |The following ALB resources now support tags: Access Controls, Custom Configurations, Health Check Templates. |GA |[Tag management has been extended to additional ALB resources](https://docs.byteplus.com/docs/clb/Using-tags-to-manage-ALB-resources) |
|2 |Project |The following ALB resources now support project\-level management: health check templates |GA |[Project-level management has been extended to additional ALB resources](https://docs.byteplus.com/docs/clb/Using-projects-to-manage-ALB-resources) |
|3 |Health Check |When the health check protocol is HTTP/1.1: If you do not specify a domain name, ALB defaults to using the backend server's private IP address as the target for health checks. |GA |[Health Check](https://docs.byteplus.com/docs/clb/ALB-Health-check) |
|4 |Custom configuration |Custom response headers now support semicolons, enabling you to specify multiple directives or parameters within a single header, such as HSTS. |GA |[Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations) |
|5 |ALB instance |Quota items for ALB instances have been split into Basic Edition and Standard Edition. |GA |[Quotas for Basic and Standard Edition ALB instances](https://docs.byteplus.com/docs/clb/Limits) |
|6 |Forwarding rule |Adjusted usage restrictions for forwarding rules in Basic Edition ALB instances: QPS rate limiting must be used together with the "Forward to" forwarding action. |GA |[Forwarding rules of Basic Edition ALB instance](https://docs.byteplus.com/docs/clb/Creating-a-forwarding-rule) |

### **March 2025**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |ALB instance |When creating an ALB instance, you can now specify the instance version as "Standard Edition". Compared to Basic Edition instances, Standard Edition instances offer richer features and more flexible configuration options. |Invite\-only Beta |[Supports Standard Edition ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance) |
|2 |Server Group |When creating a server group, you can now specify gRPC as the backend communication protocol. The backend communication protocol is used for traffic between the ALB instance and the server group. |GA |[Supports backend communication protocol gRPC](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5Yib5bu65pyN5Yqh5Zmo57uE) |
|3 |Server Group |Starting March 27, 2025, health checks are enabled by default when you create a server group in the console. When the health check feature is enabled, there are some default health check configurations. You can enable or disable health checks as needed and also customize the health check configuration. |GA |[Health check is enabled by default](https://docs.byteplus.com/docs/clb/Managing-server-groups) |

### **September 2024**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Custom configuration |ALB custom configurations now include the ability to `Ignore client exceptions` and force `Forward backend response headers`. |GA |[Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations) |
|2 |The communication protocol between ALB and backend server groups now supports HTTPS |When creating a server group, ALB now supports HTTPS communication with backend server groups. |GA |[Manage server group](https://docs.byteplus.com/docs/clb/Managing-server-groups) |
|3 |Clone ALB instance |ALB provides an instance cloning feature. You can quickly create a new instance with the same configuration as the original by cloning an existing ALB instance. |GA |[Manage instance](https://docs.byteplus.com/docs/clb/Managing-instances) |
|4 |Use limits |Updated documentation on ALB quota limits and allowlist capabilities. You can review ALB quota information and allowlist features here. |GA |[Use limits](https://docs.byteplus.com/docs/clb/Limits) |

### **July 2024**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Tag |The listener now supports tags. |GA |[Create listener](https://docs.byteplus.com/docs/clb/Creating-a-listener) |
|2 |Tag |Server groups now support tags |GA |[Create server group](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5Yib5bu65pyN5Yqh5Zmo57uE) |
|3 |Shared VPC |When creating an instance, allowlisted ALB users can select a VPC shared from another account. If you need a trial, please contact your account manager. |Invite\-only Beta |[Create NLB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance) |
|4 |Shared VPC |When creating a server group, allowlisted ALB users can select a VPC shared from another account. If you need a trial, please contact your account manager. |Invite\-only Beta |[Create server group](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5Yib5bu65pyN5Yqh5Zmo57uE) |
|5 |Custom configuration |Custom configurations now allow the addition of custom request headers. |GA |[Custom request header](https://docs.byteplus.com/docs/clb/Custom-configurations) |
|6 |WAF protection |Integration between ALB and WAF has been enhanced. You can now enable WAF protection for an instance with one click directly within the ALB console. |GA |[WAF protection](https://docs.byteplus.com/docs/clb/WAF-protection) |
|7 |Forwarding rule |Custom forwarding rules can now include multiple server groups, with support for weight distribution across groups and session persistence between groups. |GA |[Custom forwarding rules now support adding multiple server groups](https://docs.byteplus.com/docs/clb/Forwarding-rule-Overview) |

### **June 2024**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Listener |Creation of QUIC listeners is currently available only to users on the allowlist. If you need a trial, please contact your account manager. |Invite\-only Beta |[Create QUIC listener](https://docs.byteplus.com/docs/clb/Creating-a-QUIC-listener) |

### **May 2024**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Log and monitor |Access log delivery to TOS feature is currently available only to users on the allowlist. If you need a trial, please contact your account manager. |Invite\-only Beta |[Access log delivery to TOS](https://docs.byteplus.com/docs/clb/Sending-access-logs-to-TOS) |
|2 |Health Check |ALB has added TCP health check feature. |GA |[TCP health check](https://docs.byteplus.com/en/docs/clb/ALB-Health-check) |
|3 |Custom configuration |For ALB custom response headers (add_header), the always parameter is now supported for configuration. |GA |[Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations) |

### **April 2024**

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Certificates |When adding server certificates or extended certificates, ALB now supports directly selecting certificates from the BytePlus Certificate Center. |GA |\-\- |

### March 2024

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |ALB |ALB was released for the first time. |GA |[What is an Application Load Balancer](https://docs.byteplus.com/en/docs/clb/Introduction) |
