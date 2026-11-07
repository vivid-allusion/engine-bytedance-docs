---
title: "User scenarios"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-user-scenario"
---

As enterprises adopt mobile offices and multi\-cloud services, they face new security and management challenges. SealSuite is a comprehensive security platform designed to address these needs. This document outlines key user scenarios, including remote access, network access control, and zero\-trust implementation, detailing how SealSuite's solutions help you build a secure and efficient modern office environment.

<span id="9bc097d3"></span>
# Scenario one: Remote access to the office network

With the increasing demand for remote working, "working anytime and from any device" has become the norm. Employees need to be able to access the internal office network and business systems from locations outside the office.

<span id="85dc8eb2"></span>
## Solution

SealSuite offers a VPN module alongside office security features like MFA Authentication, baseline checks, and virus eradication. These tools help enterprises create a secure, stable, and seamless borderless office environment. They ensure the safe publication of internal network data and enable encrypted transmission of business data.

The VPN module utilizes a multi\-node infrastructure and supports both TCP and UDP protocols. Employees can easily activate it with one click to automatically connect to the most accessible network node by default. Enterprise administrators can set up different network resources for nodes based on business needs, enabling identity\-based, fine\-grained authorization of these resources. The decentralized deployment mode of the VPN, without a central control node, eliminates performance bottlenecks. This allows for faster deployment speeds and smooth scalability with business growth while avoiding complex hardware configurations in the office.

In response to security needs for teleworking, SealSuite enables enterprises to centrally manage access points and provide endpoint security through scanning items. Simultaneously, it can be integrated with VPN permission management, account connection status, notification alerts, and other methods to achieve more flexible and efficient security processing. Administrators can tailor the enterprise's dynamic access control policies to securely manage access to internal business resources and minimize risk exposure.

Due to the decreased efficiency in IT support caused by remote working and increased geographical distances, SealSuite has enhanced the client's IT capabilities. This includes improvements in network diagnosis, DNS reset, service center, and features like one\-click feedback and one\-click oncall to bolster the company's ability to troubleshoot IT issues.

<span id="ba35047f"></span>
## Impact of adoption


* **From a management perspective.** 

   * Enterprises can swiftly address teleworking needs and reduce hardware expenses.

   * Enterprises can consolidate their business backends and ensure the security of their operations.

   * Enterprises benefit from high stability and availability, which helps reduce IT operation and maintenance costs.

* **From an employee perspective**

   * Employees can connect to VPN with one click, enabling efficient work anywhere, anytime.

   * Employees can still maintain a smooth work experience in weak network environments.

   * Employees can conveniently handle work through their mobile phones.


<span id="75acaa62"></span>
# Scenario two: Network access control

Currently, corporate office networks lack adequate visibility. There is not only a shortage of awareness regarding internal and external threats but also a deficiency in centralized management. Administrators must configure Staff Wi\-Fi and Guest Wi\-Fi separately.

<span id="1a3b2adf"></span>
## Solution

SealSuite, featuring its standalone RADIUS gateway expansion capability, supports both wired and wireless access authentication and offers centralized policy management and administration functions.

For staff networks, SealSuite offers authentication schemes based on 802.1X authentication protocol and Portal authentication protocol, effectively mitigating the risk of lateral threat proliferation commonly seen in traditional LAN access scenarios. In addition, it supports permission control based on dynamic VLAN, capable of adjusting the network permission of employees in real time, reducing risk exposure, and providing dynamic control from a business security perspective.

SealSuite provides continuous monitoring of device security configurations, enabling ongoing insights into device and behavioral risk events of members. It also timely restricts network permissions during business access, thereby enhancing data security for the target business. At the same time, SealSuite client\-side features an integrated product architecture that incorporates both virus detection and sensitive data detection, eliminating the need for additional third\-party antivirus software or desktop management software. This results in more comprehensive detection and more efficient operations and maintenance.

<span id="2862384e"></span>
## Impact of adoption


* **From a management perspective.** 

   * Based on the identity of employees, companies can finely control their access to the network and can revoke the permissions of former employees with just one click.

   * By monitoring employee behavior and equipment risk events, companies can implement dynamic access control, bolster office network security, and accurately trace risks back to specific individuals.

   * Enterprises can more conveniently manage IT by accessing connection information for networked devices and personnel.

   * Enterprises can enhance the efficiency of password governance and mitigate the effects of password breaches.

* **From an employee perspective**

   * Employees can access the office network with a single click without the need to manage accounts or passwords.

   * Employees do not have to select a Wi\-Fi network, which helps prevent accidental connections to malicious Wi\-Fi networks.

   * Employees can perform self\-repairs on network faults.


<span id="b83db64b"></span>
# Scenario three: Access control rules

New companies often start without established employee MFA authentication management, necessitating building these systems from the ground up. In contrast, larger enterprises face the challenge of having their employee identity systems scattered across various platforms, such as Instant Messaging (IM) and Lightweight Directory Access Protocol (LDAP), which can lead to information silos within each business system. This dispersed identity and access management leads to inadequate security and low management efficiency.

<span id="ec6e5f20"></span>
## Solution

SealSuite focuses on identity\-centric management within a boundaryless office environment. It enables enterprises to refine their dynamic authorization model for accessing business resources. This includes VPN, Wi\-Fi, wired networks, and other network resources, as well as intranet business systems and internet resources. The result is a unified management system with tiered protection.

To bolster the security of business access, SealSuite implements MFA Authentication and a thorough device security configuration for each access event. When the risk events in the access environment do not match the requirements, access will be either downgraded or denied, ensuring business security through dynamic access control rules.

Unlike traditional security measures that compromise the office experience, SealSuite enhances resource connectivity, leverages Single Sign\-on and corporate portals, maximizes security assessments through a unified platform and utilizes real\-time results to effectively balance security with efficiency, ultimately providing a secure, convenient, and efficient "password\-less" office experience.

<span id="5d98ad9b"></span>
## Impact of adoption


* **From a management perspective.** 

   * Administrators can swiftly access the company's business systems and efficiently manage permissions for those systems.

   * Administrators can manage permissions for network and cloud applications throughout the entire identity lifecycle of employees.

   * Administrators can fulfill the requirements for account security.

* **From an employee perspective**

   * Employees can enjoy a seamless and efficient "password\-less" office environment with the one\-click Single Sign\-on system.

   * Employees do not need to remember multiple sets of usernames and passwords.

   * Employees can swiftly apply for application permissions without concern over whom to consult.


<span id="3ee3178a"></span>
# Scenario four: Implementing zero trust architecture in office networks

Employees and ecosystem partners may have excessive trust when accessing the office network, leading to unrecognized risks such as device security risks, personnel misconduct, and unpatched software vulnerabilities. To address these issues, the zero trust principle mandates the achievement of the following objectives:


* Identity: Ongoing assessment of behavioral status.

* Device: Ongoing monitoring of risk status.

* Enterprise applications: Implement access control based on the principle of least privilege.


<span id="c9d19fac"></span>
## Solution

The fundamental principle of zero trust revolves around continuous evaluation and maintaining a permanent stance of non\-trust. SealSuite uses dynamic access control technology to enable limited access to applications, interfaces, and data based on logical identities in an untrusted network environment, helping enterprises implement zero\-trust security within their office networks.

During the member's access process, SealSuite services are not involved in the data forwarding process. Instead, they are solely responsible for verifying the identity of users and terminals, making permission policy decisions, and distributing these policies to the VPN gateway and RADIUS gateway for implementation. By default, SealSuite does not expose any business ports externally except for the Portal. By activating the Business Stealth feature, members can only access the SealSuite Portal normally through a specific entry link after completing multi\-factor authentication and client logon. Without proper credentials, no business port of the SealSuite platform can be accessed, which significantly reduces the risk of external attacks.

The SealSuite client consistently gathers the security setup information from members' access devices and conducts real\-time matching checks by the security baselines established by the administrator. Based on the assessment results, we dynamically adjust members' internet and app access control rules, incorporating dynamic VLAN capabilities to achieve precise, dynamic access control within the corporate network.

SealSuite's main feature is its lightweight nature, supplementing the zero trust categories of multi\-source trust assessment and continual monitoring while preserving as much of the existing corporate network structure as possible. This approach effectively prevents the high\-performance load and single point of risk common in traditional solutions, ultimately enabling businesses to develop a seamless and efficient zero\-trust security access solution for internal and Internet use.

<span id="f9c72f85"></span>
## Impact of adoption


* **From a management perspective.** 

   * Avoid business systems being directly exposed to the internet.

   * SealSuite grants employees ACL policy based on the principles of "just\-in\-time" and "least privilege" and continually performs identity assessments to prevent the lateral movement of malicious activities.

   * The access policy primarily depends on users' identities, devices, and applications without being limited by location or IP.

   * It aids in thoroughly understanding the trusted status of identities, networks, and devices, thereby creating a comprehensive assessment of connections.

   * It streamlines the management of security incidents and reduces operational costs through its orchestration capabilities.

* **From an employee perspective**

   * It maintains a consistent access experience anytime, anywhere, whether in the office area, residence, or public space.


<span id="4639dd89"></span>
# Scenario Five: Accessing business resources across multiple clouds

As businesses continue to grow, an increasing number of companies are recognizing the need to access operations across multiple clouds and data centers. The traditional internal network access solution requires employees to log in again. When accessing business resources spread across multiple nodes, it decreases business efficiency and employee experience.

<span id="6957ee67"></span>
## Solution

SealSuite supports multi\-environment deployment with various delivery options such as integrated MMC, RADIUS extension nodes, VPN extension nodes, etc., ensuring high availability of components and meeting the access requirements of users across multiple locations. For example, in the global expansion of the gaming industry, a company might set up a SealSuite server node at its headquarters for centralized management to meet access mode and operational requirements. Additionally, the company can expand its resources by setting up individual VPN nodes in each region of access. Based on the service offerings in each business region, each SealSuite VPN node provides independent business publications, ensuring an optimal access experience for local employees and partners.

SealSuite offers advantages over other solutions, including lower construction costs and simpler plans that eliminate the need to purchase additional hardware or reconfigure network architecture.

<span id="74cb269c"></span>
## Impact of adoption


* **From a management perspective.** 

   * Meeting requirements: Various delivery forms can meet the needs for high availability of components and multi\-location user access.

   * Flexible deployment: Server nodes can be deployed at corporate headquarters based on business requirements, and VPN nodes can be deployed in various locations.

   * Guaranteed experience: Each VPN node can provide independent service publishing to ensure the access experience of employees and partners.

   * Low cost and simple scheme: SealSuite has low construction costs without the need for additional hardware purchases and network architecture reconfigurations.

* **From an employee perspective**

   * Convenient access: Various delivery forms and deployment methods are available to meet employees' access needs in multiple locations, providing the optimal access experience.

   * Efficient resource utilization: The VPN node can expand resources and improve the utilization of network resources.

   * Easy to use: The SealSuite solution is simple and convenient to use.


<span id="e6d1645a"></span>
# Related Documentation


* [What is SealSuite？](https://docs.byteplus.com/docs/sealsuite/docs-what-is-sealsuite)

* [Basic concepts](https://docs.byteplus.com/docs/sealsuite/docs-basic-concepts)

* [Product advantages](https://docs.byteplus.com/docs/sealsuite/docs-product-advantages)
