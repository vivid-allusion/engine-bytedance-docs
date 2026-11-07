---
title: "Security overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Security-overview"
---

BytePlus provides a variety of security products to enhance the security capabilities of your ECS instances. These products help prevent events such as cryptojacking on instances, file\-encrypting ransomware attacks, and intranet breaches via insecure configurations, which could threaten instance data security and disrupt your business operations.

This topic describes how to configure basic security capabilities for ECS instances. For more comprehensive security capabilities, see [Enhancing security of ECS instances](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances).

<span id=".5a6J5YWo6Ziy5oqk57G75Z6L"></span>
## Security capability types

<span id=".5a6e5L6L5YaF6YOo6Ziy5oqk"></span>
### Internal protection for instances

Weak passwords and improperly opened IP addresses and ports are potential security risks for instances. To fundamentally improve instance security, we recommend that you first enhance the internal protection of your instance.


|Protection method |Description |Operation guide |
|---|---|---|
|Password |It is recommended to improve the password complexity such as adding uppercase letters, symbols, and numbers or using a long password. |[Reset login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) |
|Key pair |Compared to "Password", we recommend that you use "Key Pair", which is based on an encryption algorithm and is applicable for scenarios that require higher security. |[Overview of key pair](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview) |
|Security group |The security group is used to control the inbound and outbound network traffic of each network interface of the ECS instance. It is an important isolation mechanism for ensuring network security. The security group feature helps you to control access to or from the ECS instance.<br><br>To ensure resource security within the security group, we recommend that you follow the principle of least privilege and cautiously and precisely allow IP addresses and ports. |* [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview)<br><br>* [Common ports for ECS instances](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances) |


<span id=".5a6e5L6L5aSW6YOo6Ziy5oqk"></span>
### External protection for instance

Internal protection prevents access from unknown sources, but external security issues such as DDoS traffic attacks, anomalous intrusions, and brute force cracking also occur from time to time. You are recommended to select protection methods based on the business situation.


|Protection method |Description |Operation guide |
|---|---|---|
|Security enhancement |If you enable this feature, the system dynamics will be monitored and analyzed in real time. In addition, file monitoring, process monitoring, and alerting for exceptions like unauthorized logins are also enabled, lowering the risk of host intrusion. |[Enabling security enhancement for instance](https://docs.byteplus.com/en/docs/ecs/Security-enhancement) |
