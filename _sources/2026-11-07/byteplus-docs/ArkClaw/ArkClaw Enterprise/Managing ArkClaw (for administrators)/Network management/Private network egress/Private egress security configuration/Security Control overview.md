---
title: "Security Control overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Private-egress-security-overview"
---

<span id="aevzCx1j"></span>
## Overview

Security Controls for Private Network Egress provide granular access control for traffic from Claw instances to enterprise internal services. This feature enhances security across three dimensions: IP/port (Layer 4), domain (Layer 7), and DNS resolution.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_42c216f65b5b5ac9cb06d2c48907aa47.png) </span>


|Component |**Description** |Target |
|---|---|---|
|Network Access Policy |A Layer 4 policy for the private network egress. It controls (Allows/Denies) a Claw instance's access to specific target IPs and ports. |Layer 4 traffic |
|Web Access Policy |A Layer 7 policy for the private network egress. It controls (Allows/Denies) a Claw instance's access to specific target domains. |Layer 7 traffic |
|DNS Access Policy |A DNS access policy for the private network egress. It blocks DNS resolution for specified domains from Claw instances. |DNS traffic |


<span id="JEHqtlQw"></span>
## How it works

**Network access policy (Layer 4)** 

When a request passes through the network access policy, rules are matched in descending priority order. If a rule is matched, the corresponding action (Allow or Block) is applied. If no rule is matched, the system default rule applies and allows the request.

**Web access policy (Layer 7)** 

When a request passes through the Web access policy, rules are matched in descending priority order. If a rule is matched, the corresponding action (Allow or Block) is applied. If no rule is matched, the system default rule applies and allows the request.

**DNS access policy**

When a DNS resolution request passes through the policy, resolution is denied if the domain matches a block rule. If no rule is matched, resolution proceeds normally.

<span id="zFG8Soem"></span>
## Quota limits


|**Quota** |Default maximum |
|---|---|
|Maximum rules per network access policy |100 |
|Maximum source IDs per network access rule |100 |
|Maximum destination CIDRs per network access rule |20 |
|Maximum destination ports per network access rule |20 |
|Maximum rules per Web access policy |100 |
|Maximum listening ports per Web access rule |5 |
|Maximum source IDs per Web access rule |100 |
|Maximum domains per Web access rule |500 |
