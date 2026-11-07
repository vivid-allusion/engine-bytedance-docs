---
title: "Network planning"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Network-planning"
---

<span id="zBvfa3py"></span>
## Background

If the on\-cloud network is not planned in advance, subsequent expansions may encounter difficulties due to unreasonable architecture, leading to challenges in scaling and chaotic operations, which not only increase security risks but also make cost control difficult. Therefore, combining business needs to execute thorough network planning and build a network architecture tailored to the business can easily solve expansion challenges, reduce operational difficulty, and minimize impact on existing business.

<span id="oX3s0sTn"></span>
## Factors to consider

On\-cloud network planning should at least consider the following factors:


|Consideration |Notes |
|---|---|
|Network performance |Network performance directly affects user experience. If the network experiences high latency and lag, it can lead to user loss. |
|Scalability |Whether the business scales up or scales down, it involves a change in resources. Poor scalability and massive resource coupling can easily affect existing services. |
|Security |Whether it is internal or external traffic within the network, it needs to be managed. On one hand, external traffic malice must be prevented from intrusion, and on the other hand, adjustments, upgrades, and other actions of some applications must be prevented from affecting other applications. |
|Network O&M |Whether it is permission restriction management, service upgrades, or issue troubleshooting, O&M management is required. A pre\-planned network architecture can reduce O&M difficulty and thus lower O&M costs. |
|Fee |A pre\-planned network architecture can avoid configuring unnecessary resources. For example, if the CIDR blocks of two VPCs that need to communicate are conflicting, it is necessary to configure a VPC NAT Gateway to handle this. |


<span id="oy6WUSut"></span>
## Planning content

<span id="D0MWAUWw"></span>
### Region and Availability Zone


* **Region**

   The closer users are to the region, the shorter the internet transmission distance and the lower the network latency. Please select the Region closest to the user based on the actual business situation.

* **Availability Zone**

   * Multi\-Availability Zone assurance: Each Availability Zone has independent power supply and network. It is recommended to deploy your business across at least two Availability Zones. Even if one Availability Zone fails, the business can still function normally.

   * Advantages of the same Availability Zone: Private network access within the same Availability Zone does not require cross\-Availability Zone calculations, resulting in lower latency.


<span id="WWQrM4Wf"></span>
### Account and VPC


* **Number of accounts**

   The main account has full permission over resources, and all resource purchases are settled through the main account. You can apply for multiple accounts as needed based on the diversity of your business. Applicable application scenarios are as follows:

   * Different business lines within the same enterprise: Each business line has varying operation models and resource requirements. Independent accounts can achieve resource isolation and precise management.

   * Different subsidiaries: Each subsidiary is relatively independent in terms of finance, operations, and management. Using independent accounts enables clearer resource allocation and fee accounting for each subsidiary.

* **VPC CIDR block**

   * Available CIDR block:

      
      |**Comparative Item** |**IPv4** |**IPv6** |
      |---|---|---|
      |Address length |32\-bit |128\-bit |
      |Optional CIDR block |The optional IPv4 CIDR blocks (32\-bit) are as follows:<br><br><br>* **10.0.0.0/8\-** **28** (The VPC can use up to 16,777,213 IP addresses)<br><br>* **172.16.0.0/12\-** **28**  (The VPC can use up to 1,048,573 IP addresses)<br><br>* **192.168.0.0/16\-** **28**  (The VPC can use up to 65,533 IP addresses) |IPv6 CIDR blocks (128\-bit) cannot be selected.<br><br><br>* The IPv6 address of BytePlus is globally unique.<br><br>* The system automatically assigns you an `/56` IPv6 CIDR block.<br><br>* The subnet mask is fixed at /64.<br><br><br><div data-tips="true" data-tips-type="default">Notes</div><br><br><br><div data-tips="true" data-tips-type="default">Dual\-Stack VPC is currently in beta stage. If you need a trial, please contact the account manager.</div><br><br><br><div data-tips="true" data-tips-type="default"></div><br> |
      

   * Suggestions for VPC CIDR block planning

      * Basic CIDR block settings: It is recommended to use `/16` as the primary IPv4 CIDR block for the VPC. When the IPv4 address resources of the primary CIDR block are insufficient, you can extend the available IP address space by [Adding secondary CIDR](https://docs.byteplus.com/en/docs/vpc/Managing-secondary-CIDR-blocks).

      * Principles of CIDR block differentiation

         * Avoid conflicts between networks: Different VPCs, as well as between a VPC and the data center (IDC), should set distinct CIDR blocks to avoid IP address conflicts during subsequent network interconnections.

         * Conflict response policy: If CIDR block conflicts in the VPC cannot be avoided, ensure that the target subnet's CIDR block does not conflict.

* **The number of VPCs**

   
   |Comparative Item |Notes |
   |---|---|
   |Single VPC |In the following scenarios, using a single VPC is recommended:<br><br><br>* Business startup phase: When the business is in its startup phase, with a small scale and simple network architecture, deploying multiple VPCs increases O&M costs. A single VPC can meet the requirements.<br><br>* Low\-security and stable\-type business: For businesses with low security requirements, stable business models, and minimal expansion needs, a single VPC can meet the requirements while reducing management complexity.<br><br>* Budget\-constrained scenarios: When the budget is limited, using a single VPC can avoid potential inter\-VPC communication fees. |
   |Multiple VPCs |The following scenarios recommend using multiple VPCs:<br><br><br>* Large and complex enterprises: Large business scale and complex organizational structure require multiple VPCs to achieve precise management.<br><br>* High security demand scenarios: High security requirements necessitate decoupling individual business from other businesses to avoid mutual impact caused by adjustments to the security policy.<br><br>* Rapidly developing businesses: Business expands rapidly or has high scalability requirements. Multiple VPCs allow flexible adaptation to changes. |
   

* **Subnet CIDR block and quantity**

   * The subnet CIDR block belongs to a subset of the VPC CIDR block.

   * Each subnet reserves 3 system IP addresses: the first, second, and last usable addresses. For example, in the subnet CIDR block 192.168.2.0/24, IP addresses 192.168.2.0, 192.168.2.1, and 192.168.2.255 are reserved for the system.

   * Planning recommendations:

      * Divide subnet CIDR blocks based on application modules or purposes, such as applications and databases.

      * When planning subnet CIDR blocks, ensure sufficient IP capacity to accommodate future requirements, accounting for these reserved addresses.

      * At least two subnets are recommended, distributed across different Availability Zones, to ensure normal disaster recovery.


<span id="I056C0up"></span>
### Security

Both VPC security groups and Network ACLs are free resources. We recommend making full use of these two features to strengthen network security protection and ensure business security.


|Feature |Notes |
|---|---|
|Security Group |Security groups control **Network interface** traffic, suitable for implementing one\-to\-one fine\-grained protection on servers, precisely limiting specific servers' access sources and outbound directions, preventing external malicious probing and internal lateral penetration scenarios. [Learn more](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups) |
|Network ACL |A Network Access Control List controls **Subnet** traffic, making it ideal for implementing unified traffic control policies that enforce coarse\-grained, subnet\-wide restrictions. [Learn more](https://docs.byteplus.com/en/docs/vpc/Network-ACL-use-cases) |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f32762123ccfc557786295e2aa606f8.png) </span>

<span id="ZZqEUPNw"></span>
### Operations and Maintenance

If your network architecture becomes increasingly complex or if you require refined and standardized network O&M management, we recommend leveraging the flow log and traffic mirror features. The former records traffic directions, while the latter captures specific traffic, helping you to clearly understand network conditions and achieve efficient O&M.


|Planning item |Notes |
|---|---|
|Flow Log |Flow logs can analyze the log data of outbound and inbound traffic of network interfaces to help troubleshoot network problems and optimize network architecture. [Learn more](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview) |
|Traffic Mirror |The traffic mirror can copy the specified traffic of the designated network interface to the target server, making it convenient for you to analyze this traffic. [Learn more](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview) |


<span id="WNDvL6zt"></span>
### Internet connection

Whether for accessing the internet, enabling private communication between VPCs, or building a hybrid cloud across cloud and on\-premises, you can refer to [Application scenarios](https://docs.byteplus.com/en/docs/vpc/Application-scenarios) to plan an appropriate network connection.
