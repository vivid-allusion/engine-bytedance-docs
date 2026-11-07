---
title: "Basic concepts"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-basic-concepts"
---

To effectively use SealSuite, it is essential to understand its core terminology. This document serves as a glossary, defining key concepts across identity, network, and device management, such as Authorization Rules, Application Gateway, IAM, and Device Baselines, to help you grasp the product's architecture and capabilities.

<span id="c81b8a7c"></span>
# General Concepts

<span id="5cbe0950"></span>
## **Authorization Rule**

Whether it's a Virtual Private Network (VPN), Wi\-Fi, Wired network, business systems, cloud services, or internet applications, all resources accessed through SealSuite are granted to users via authorization rules. When an administrator enables a resource for full usage, corporate members are assigned to the default group; when it is switched to restricted usage, it requires defining the scope of authorization rules based on departments, roles, and members and setting the priority among policies to achieve refined access control rules.


---



<span id="ebb6ec90"></span>
# Application Gateway

The function of an application gateway is to authenticate and authorize the forwarding of unauthorized incoming requests, forward resource access for properly authorized requests, and intercept and block denied access requests to prevent them from accessing further.

A zero\-trust application gateway usually achieves this using Layer 7 reverse proxying over the HTTP protocol. This is typically done by resolving the backend application's domain name to the gateway, which intercepts and forwards resource access requests. It features easy operation by users without depending on terminal agents, etc., and is suitable for managing scenarios involving uncontrolled terminal users, such as accessing a school's official website.


---



<span id="8770af22"></span>
# Identity Management

<span id="b756542f"></span>
## **IAM**(Identity and Access Management)

Identity and access management ensures secure access to business resources through authentication and permission management. SealSuite supports integrating various applications, including business systems, cloud services, and internet resources, and enforces authentication by default during application login to enhance security.

Regarding data source integration, SealSuite supports building organizational structures internally and connecting to data sources such as Feishu and DingTalk. Moreover, SealSuite has added a role\-based resource authorization approach on top of departments and employee authorizations to meet the flexible management needs of project teams and individuals belonging to multiple departments. Defining dynamic roles allows for more detailed access control rules that align with specific business scenarios.

<span id="eaf5680a"></span>
## **MFA**(Multi Factor Authentication)

Multi\-factor authentication enhances security by adding a second layer of identity authentication, such as OTP, Short Messaging Service (SMS), or email, following the initial username and password verification. This method effectively helps enterprises identify risks of account misuse or impersonation when employee devices are lost, or usernames and passwords are acquired by attackers.

In SealSuite, administrators can configure a second authentication policy triggered by actions such as VPN connections and app access or triggered by device information risks.


---



<span id="9067a829"></span>
# Network Management

<span id="ca005ed1"></span>
## **Network Verification**

To confirm the identity of users or devices attempting to access the network, SealSuite offers various verification methods. For enterprise members, authentication using 802.1x and Portal protocols is adopted, and VPN, Wi\-Fi, and wired network permissions are assigned based on the authentication status.

<span id="ed916df2"></span>
## **Wi\-Fi Management**

Network access control refers to managing the network access behavior of office devices by dividing VLANs to prevent attacks, such as malicious programs, from spreading laterally within the office network. Through Wi\-Fi Management, companies can allow only authorized and trustworthy devices (such as PCs, mobile phones, etc.) to access the network while blocking other devices.

Based on integrated device management and security capabilities, SealSuite can help enterprises quickly establish security standards for the mobile office. For instance, when office devices lack screen lock passwords or engage in unauthorized Wi\-Fi connections, SealSuite dynamically reduces their network access privileges (VPN, Wi\-Fi, and wired network). After the risk is mitigated, the original permissions of the terminal are automatically restored, enabling the construction of a remote or on\-site integrated dynamic network access.

<span id="adc1a491"></span>
## **Access Control**

Access control is a method that restricts or allows subjects to access objects in a certain way, used to prevent losses caused by illegal user intrusion or accidental operations by legitimate users, ensuring controlled and lawful use of business resources.

In SealSuite, employees are the subjects who access resources (objects), such as the network and cloud applications. Enterprise administrators can customize risk scenarios according to corporate policies and assess trust levels based on member properties, network environment, device properties, and risk status. Then, based on the trust level and security policies, administrators can assign the minimum required access permissions by mapping members, roles, and resources to implement role\-based access control (RBAC).

<span id="f3f95b0b"></span>
## **VPN Node**

By setting VPN node(s) policies, SealSuite achieves refined management of VPN resources. Each node corresponds to a different internal or public IP, control port, data port, and DNS Server. Administrators can customize the name of the VPN server, view connectivity, concurrency, throughput trends of the node, and the online employee accounts at that node. The employee client supports the automatic selection of node paths and the manual switching of nodes.

SealSuite's public cloud services are deployed in the cloud. Therefore, VPN node(s) are deployed as components within the internal corporate network.

<span id="9d7df7f1"></span>
## **RADIUS Gateway**

Remote Authentication Dial\-In User Service (RADIUS) servers provide 3A functionality: Authentication, Authorization, and Accounting. In traditional network management practice, enterprises statically map personnel to work area network permissions through routing devices. SealSuite, however, uses its proprietary RADIUS server to dynamically associate users, roles, and permissions. This allows for granular network permission management based on identity type or real\-time permission changes based on the security posture of the user and their device.

By configuring multiple RADIUS gateways, SealSuite can better meet the needs of enterprises with multiple work areas. SealSuite's public cloud services are deployed in the cloud. Therefore, RADIUS gateways are deployed as components within the internal corporate network.


---



<span id="c19db159"></span>
# Device

<span id="84052db8"></span>
## **Device**

In a digital office environment, companies are responsible for managing a broader range of office equipment. This includes not only corporate\-owned assets but also personal devices used by employees for work\-related tasks. Therefore, comprehensive and accurate device management capabilities can help improve the efficiency of office network access management and provide more convenient IT service support for employees.

SealSuite integrates seamlessly with corporate asset management platforms to enable unified management of company devices and BYOD (Bring Your Own Device). It can collect general information, software lists, login records, and the status of the equipment in real\-time. It also organizes devices based on work area, department, and personnel to facilitate refined device access management.

<span id="f1b06877"></span>
## **Device Baseline**

Device baseline refers to the security practices and compliance checks for corporate office device assets and employee BYOD, including mandatory security configurations such as screen lock passwords, antivirus software installation, connection to insecure Wi\-Fi, and running of non\-compliant apps or processes.

SealSuite provides various detection items for daily office use involving Windows, Mac, Android, iOS, and Linux systems. Administrators can flexibly configure either scheduled scanning strategies or trigger\-based scanning strategies to ensure more comprehensive compliance with device security configurations.


---



<span id="dd56b5c2"></span>
# Related Documentation


* [What is SealSuite？](https://docs.byteplus.com/docs/sealsuite/docs-what-is-sealsuite)

* [Product advantages](https://docs.byteplus.com/docs/sealsuite/docs-product-advantages)

* [User scenarios](https://docs.byteplus.com/docs/sealsuite/docs-user-scenario)
