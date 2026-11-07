---
title: "What is ArkClaw Enterprise"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/What_is_ArkClaw_Enterprise"
---

<span id="wgdAJgoM"></span>
## ArkClaw Enterprise overview

ArkClaw Enterprise is an enterprise\-grade agent infrastructure launched by BytePlus. Built on ArkClaw, it provides targeted enhancements to meet core requirements such as enterprise authentication, security compliance, skill asset accumulation, team memory, and business automation. This helps enterprises upgrade AI agent capabilities from "personal efficiency improvement tools" to "organization productivity platforms".

ArkClaw Enterprise evolves independently and is continuously updated without being associated with a single application ecosystem. Enterprises can deeply integrate ArkClaw Enterprise with existing IM systems (Feishu, WeCom, and DingTalk), identity systems (OIDC, SAML, AD, and LDAP), as well as networking and business systems. This ensures that agents are seamlessly integrated with employee workflows while remaining within the enterprise IT and security governance framework. It is suitable for large and medium‑sized enterprises that want to apply agent capabilities across all business scenarios while ensuring **centralized management, auditability, and traceability**. The scenarios involve roles such as R&D, product, marketing, HR, finance, legal, risk control, and IT operations.

<span id="q0rbahnj"></span>
## Why choose ArkClaw Enterprise

Open\-source OpenClaw and ArkClaw can significantly improve personnel efficiency. However, they face a series of governance and compliance challenges when used on a large scale within an enterprise. ArkClaw Enterprise provides end\-to\-end solutions for the following six types of issues as a service.


|**Pain point dimension** |**Typical issue** |**Impact on enterprises** |
|---|---|---|
|**Deployment and operation** |Heavy reliance on local environments, complex cross\-platform deployment, and high environment maintenance costs |Low system stability and difficulty in scaling |
|**Resource scheduling** |Concurrent tasks compete for resources due to the lack of enterprise\-grade resource isolation and scheduling |Unpredictable execution efficiency for critical tasks |
|**Security and compliance** |Difficulty in attributing AI operations due to the lack of centralized permission management and audit logs |Data security and compliance checks cannot meet enterprise standards |
|**Asset accumulation** |Skills and configurations are scattered across personal terminals, without centralized management |Employee turnover leads to loss of core knowledge assets |
|**Cost control** |Lack of unified monitoring and optimization for token consumption and high hidden costs |Large model usage costs can spiral as the usage scale grows. |
|**Overall protection** |No systematic security protection system |Difficulty in ensuring enterprise data and business process security |


<span id="QFPybbOM"></span>
## Overall architecture

ArkClaw Enterprise adopts an architecture consisting of three layers: centralized management plane, controlled execution environment, and AI\-native security foundation. It reuses the mature IaaS and PaaS capabilities of BytePlus, such as VPC, security groups, IAM/veIdentity, TLS, APMplus, TOS, and OpenSearch/MySQL/Serverless PG. This reduces the cost of self\-built enterprise infrastructure.


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="U53DErEU"></span>
### Centralized management plane

ArkClaw Enterprise provides a one\\-stop centralized management center for enterprise IT and security administrators. It fully covers user identities, network policies, quota allocation, and operations and maintenance (O&M) monitoring, as well as the full\\-lifecycle management of enterprise assets, including skills, cloud disks, knowledge bases, and AI applications. Through a policy‑driven automated distribution mechanism, it seamlessly synchronizes configurations to various underlying execution environments. This effectively reduces the cost of managing multiple spaces and achieves the principle of one configuration taking effect globally for efficient O&M.

</card>




<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="w0NYkf0n"></span>
### Controlled execution environment

ArkClaw Enterprise provides a highly available environment with resource isolation and network convergence for Agent operation. It supports a flexible deployment architecture. Standard mode achieves logical isolation through spaces and VPCs, which is suitable for mainstream medium\\-sized enterprises. Dedicated mode provides the highest level of isolation by using independent accounts. Dedicated mode meets the strict compliance requirements of large customers. A built\\-in unified access layer integrates authentication, host hardening, security group isolation, and NAT egress control to ensure the security of underlying compute resources.

</card>




<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="EIQY8Bhl"></span>
### AI\\-native security foundation

ArkClaw Enterprise horizontally spans five dimensions: identity, permissions, network, runtime, and auditing. This builds an in\\-depth defense system. It seamlessly integrates with enterprise SSO (OIDC, SAML, and AD are supported) and fine\\-grained RBAC. It provides centralized credential management and private network boundary isolation to ensure core data is not stored locally. Combined with native agent sandbox isolation and end\\-to\\-end security auditing (including DDoS protection, vulnerability scanning, and runtime monitoring), it achieves end\\-to\\-end traceability of operations.

</card>



<span id="zZZ1nKzv"></span>
## Core advantages


<columns>
<columnsItem zoneid="6NTDbmX1">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

Proactive control

When using AI, enterprises often face the dilemma of "banning kills efficiency and allowing breeds risk". ArkClaw Enterprise integrates permission management and resource configuration with governance without affecting employee experience. This achieves a balance between efficiency and risk control.

</card>



</columnsItem>
<columnsItem zoneid="bJ6Z5o0R">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

Global protection

The platform provides multi\\-dimensional security capabilities to achieve prevention before an incident, management during an incident, and traceability after an incident. Identity access, model calls, plugin usage, log auditing, and issue investigation all operate inside one unified security system.

</card>



</columnsItem>
</columns>



<columns>
<columnsItem zoneid="Ug0n5ZLc">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

Value accumulation

Prompts, process experience, skills, and knowledge generated during daily use of AI by employees do not need to be exclusive to individuals. Enterprises can turn these into reusable organizational assets. This reduces duplicate work and facilitates new members in getting started.

</card>



</columnsItem>
<columnsItem zoneid="vjSuPQBb">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

Easier use

Administrators can quickly complete service activation, employee\\-side configuration, and daily management. Employees can use the service through familiar messaging channels (such as Feishu and DingTalk) or the web client. This significantly reduces enterprise O&M costs and the difficulty of using this service.

</card>



</columnsItem>
</columns>
