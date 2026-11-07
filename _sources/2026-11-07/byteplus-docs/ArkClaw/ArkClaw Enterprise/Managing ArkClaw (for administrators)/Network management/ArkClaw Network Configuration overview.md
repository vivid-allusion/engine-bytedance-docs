---
title: "ArkClaw Network Configuration overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview"
---

<span id="Wals3GV4"></span>
## Overview

ArkClaw Enterprise provides flexible network configuration capabilities, enabling connectivity with your enterprise network to meet secure, controlled, and efficient access requirements.


* **Public access to ArkClaw**: Employees can access ArkClaw and interact with AI agents from any internet\-connected environment using the public login link provided by the enterprise. Enterprises can also integrate the ArkClaw access portal into their own domain system, unifying brand identity and portal management. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/custom-domain-overview)

* **Private access to ArkClaw**: After the administrator configures an allowlist for a business account, employees can create an interface endpoint to establish a PrivateLink connection. Through this connection, they can log in to ArkClaw and interact with agents.

* **ArkClaw access to Internet**: Enables ArkClaw to actively access Internet resources through a public network egress. The public network egress, based on a NAT Gateway, provides centralized outbound connectivity and control capabilities.

* **ArkClaw access to internal resources**: Integrates ArkClaw instances with your enterprise IT assets via private network egress. ArkClaw can securely access internal enterprise systems (e.g., CRM, ERP), connect to databases for private data analysis, or retrieve information from internal file servers and knowledge bases. All within the private network. This ensures all data flows exclusively over the private network, meeting compliance requirements such as "Data must remain the region" in finance, government, and other regulated industries.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c2f49fccf7534078acf3f7826a49716.png) </span>

<span id="bZD3naK5"></span>
## Terms


|Term |Description |
|---|---|
|Public network ingress |The network channel for users to access ArkClaw services (e.g., login, Chat UI, Terminal) over the Internet. In addition to the default access address, ArkClaw offers two custom access addresses:<br><br><br>* [Custom enterprise domain](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version): Bind your own registered and ICP\-filed domain to hide platform information, creating a completely enterprise\-branded dedicated login portal.<br><br>* [Custom domain prefix](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-old-version): Add a custom prefix before the platform's fixed domain suffix to obtain a concise, memorable enterprise\-specific access address without needing your own domain. |
|Public network egress |The network channel used by ArkClaw to actively access public resources. The public network egress supports network access policies and Web access policies, providing fine\-grained, reliable access control and security protection.<br><br><br>* Network access policy: Controls Layer\-4 traffic from Claw instances to the public network.<br><br>* Web access policy: Controls Layer\-7 traffic from Claw instances to the public network.<br><br>* Cross\-border acceleration: Provides network acceleration for public network access in cross\-border scenarios. |
|Private network ingress |The network channel for users to access ArkClaw services (e.g., login, Chat UI, Terminal) over the private network.<br><br><br>* [Account allowlist](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-account-allowlist): Controls which business accounts are authorized to access Claw over the private network.<br><br>* [Connection management](https://docs.byteplus.com/en/docs/ArkClaw/Accepting-or-rejecting-a-connection): Administrators can manually accept or reject PrivateLink connections from business accounts.<br><br>* [Custom domain](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-prefix): Administrators can modify the system\-assigned private ingress domain prefix or configure a custom domain. This helps business staff identify and remember it easily. |
|Private network egress |The network channel for ArkClaw to access internal enterprise networks (e.g., business systems, databases, file servers). The private network egress supports network access policies, Web access policies, and DNS access policies, providing fine\-grained, reliable access control and security protection.<br><br><br>* Network access policy: Controls Layer\-4 private network traffic from Claw instances to your enterprise services.<br><br>* Web access policy: Controls Layer\-7 private network traffic from Claw instances to your enterprise services.<br><br>* DNS access policy: Blocks​ a Claw instance from resolving specified domains. |


<span id="U8egXhoo"></span>
## Use limits

Due to limited network configuration resources, the table below lists the limits for large\-scale ArkClaw network configuration in a single region under a single account.


|Quota category ||Limit item |Default maximum |
|---|---|---|---|
|Private network egress |General |Maximum private network egress instances that can be created |1 |
|||Maximum availability zones per private network egress |2 |
|||Maximum IPs occupied by private network egress |6 |
|||Maximum access destinations per private network egress |50 |
|||Security group configurations must be consistent across multiple availability zones |Not applicable |
|||Maximum external DNS server IP addresses |10 |
|||Maximum domains for forwarded resolution |500 |
||Network access policy |Maximum rules per network access policy |100 |
|||Maximum underlying forwarding rules per network access policy |5000 |
|||Maximum source IDs per network access rule |100 |
|||Maximum destination CIDRs per network access rule |20 |
|||Maximum destination ports per network access rule |20 |
||Web access policy |Maximum rules per Web access policy |100 |
|||Maximum listening ports per Web access rule |5 |
|||Maximum source IDs per Web access rule |100 |
|||Maximum domains per Web access rule |500 |
|Public network egress |Network access policy |Maximum rules per network access policy |100 |
|||Maximum source instances per network access policy |100 |
|||Maximum destination IPs per network access policy |20 |
|||Maximum destination ports per network access policy |20 |
||Web access policy |Maximum domains for cross\-border public acceleration |500 |
|||Maximum listening ports per Web access policy |5 |
|||Maximum cross\-border acceleration rules per Web access policy |1 |
|||Maximum rules per web access policy |100 |
|||Maximum sources per Web access rule |100 |
|||Maximum destinations per Web access rule |500 |
|Private network ingress |Maximum bandwidth |Maximum bandwidth per connection per endpoint per availability zone |10 Gbps |


&nbsp;
