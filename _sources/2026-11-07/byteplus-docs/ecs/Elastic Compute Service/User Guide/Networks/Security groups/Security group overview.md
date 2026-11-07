---
title: "Security group overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Security-group-overview"
---

<span id=".566A5LuL"></span>
## Description

Security groups are designed based on the allowlist principle to control the outbound and inbound traffic for network interfaces of ECS instances. You can add security group rules to allow the required traffic for network interfaces based on your business requirements.

For example, if an ECS instance provides services externally over port 80, its associated security group must include an inbound rule allowing traffic over port 80. This ensures that external traffic can access the services provided by that ECS instance as expected.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the security of ECS instances, we recommend that you follow the principle of least privilege and cautiously and precisely allow IP addresses and ports for security groups associated with ECS instances.</div>


* <div data-tips="true" data-tips-type="tip">For ease of use, the system adds some rules to security groups by default to allow traffic. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Security-group-overview#.5YiG57G7">security group classification</a>.</div>



<span id=".5YiG57G7"></span>
## Category

Security groups are classified based on creation method, as shown in the following table:


|Category |Description |
|---|---|
|Default security group |Created automatically by the system when you create a VPC. Default security groups are automatically deleted when you delete the VPC. You cannot delete default security groups manually. For ease of use, some rules are added to default security groups by default (**you can modify them manually**) to allow traffic:<br><br><br>* Outbound: Allows all traffic. Therefore, you can access resources at any address.<br><br>* Inbound: Allows ICMP and TCP traffic on ports 22, 3389, 80, 443 from all network segments (`0.0.0.0/0`, which means any address). Traffic is also allowed when other network interfaces in the same security group access the network interface. |
|Custom security group |Created manually by users. For ease of use, some rules are added by default (**you can modify them manually**) to allow traffic:<br><br><br>* Outbound: Allows all traffic. Therefore, you can access resources at any address.<br><br>* Inbound: Allows traffic when other network interfaces in the same security group access this network interface. |
|Managed security group |When you create a cloud service that requires a security group, such as a NAT gateway or VPN gateway, the system automatically creates a managed security group. The created security group is managed by cloud service. You can only view the managed security group whose lifecycle is tied to the cloud service. |


<span id=".5a6J5YWo57uE6KeE5YiZ"></span>
## Security group rules


* Security groups are stateful. Therefore, response traffic is automatically allowed (TCP connections time out after 900 seconds, and ICMP connections time out after 30 seconds). Specifically, when a network interface initiates access, only outbound rules need to allow the traffic; when a network interface is accessed, only inbound rules need to allow the traffic.

* Changes to security group rules take effect immediately. The changed rules can control both established long\-lived connections and new connections.

* A rule with the source address set to the security group itself (such as default) allows network interfaces within the group to be accessed by other interfaces in the same security group. If you delete such rule, network interfaces within the security group will fail to communicate over the private network.


<span id=".57uE5oiQ"></span>
### Composition

When you add rules to security groups to allow traffic, the rules include the key parameters as described below:


|Parameter​ |Description |
|---|---|
|Inbound/Outbound |The direction of traffic.<br><br><br>* Inbound: Inbound traffic to the network interface (traffic from external sources to access the ECS instance).<br><br>* Outbound: Outbound traffic from the network interface (traffic from the ECS instance to access external sources). |
|Priority |The priority of security group rules. When traffic matches security group rules, priorities are compared first. If priorities are the same, rule policies are then compared.<br><br><br>* Priorities can be the same.<br><br>* The valid value is from 1 to 100, with the highest priority of 1. |
|Policy |The policy of traffic. When priorities are equal, deny policy takes precedence over allow policy.<br><br><br>* Allow policy: Allows traffic.<br><br>* Deny policy: Blocks traffic. This policy applies when you allow traffic for large CIDR ranges but block traffic from specified IP addresses within these ranges. |
|Protocol type |ALL, TCP, UDP, ICMP, and ICMPv6 are supported. |
|Port range |Restricts port ranges based on protocol types.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Ports 25, 135, 139, 444, 445, 5800, and 5900 are marked as high\-risk by some internet service providers. Even if these ports are allowed in the security group, restricted users will still be unable to access them. Therefore, we recommend that you use other non\-high\-risk ports.</div><br> |
|Source address/Destination address |* Source address: This parameter is only configured for inbound direction. This indicates resources at the source address can access the ECS instance.<br><br>* Destination address: This parameter is only configured for outbound direction. This indicates the ECS instance can access resources at the destination address. |


The following table shows an example: Allow resources in the 12.156.XX.XX/28 range to access network interfaces within the security group via TCP on port 80.


|Inbound/Outbound |Priority |Policy |Protocol type |Port range |Source address |
|---|---|---|---|---|---|
|Inbound |1 |Allow |TCP |80 |12.156.XX.XX/28 |


<span id=".5Yy56YWN6K-05piO"></span>
### Matching description

When you associate one or more security groups with a network interface:


* If no rule exists in any security group, all inbound and outbound traffic of the network interface is denied.

* If the security group contains one or more rules, the traffic matching process for the network interface is as follows: (inbound traffic of the network interface is used as an example here; the same applies to outbound traffic).

   1. **Priority\-based sorting**: All inbound rules from all associated security groups are aggregated and sorted by priority from highest to lowest.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The smaller the priority value, the higher its priority.</div>


* <div data-tips="true" data-tips-type="tip">For rules with equal priority​​, deny policies take precedence over allow policies.</div>


   2. **Matching**: Traffic checks against rules from top to bottom. If matched with a rule, the traffic then is allowed or denied based on the rule policy, and the matching process stops. If not matched, the traffic is denied.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

For more information on security group limits, refer to [Limits](https://docs.byteplus.com/en/docs/vpc/Limits#.5a6J5YWo57uE).

<span id=".5L2_55So5rWB56iL"></span>
## Use procedure


1. [Create security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group)

2. [Associate network interfaces](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-a-network-interface#.5YWz6IGU572R5Y2h)

3. [Add security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules)


For more information, refer to [Security group](https://docs.byteplus.com/en/docs/vpc/Security-Group).

<span id=".5a6e6Le15bu66K6u"></span>
## Usage suggestions


* To plan security groups, refer to [How to make a security group plan](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups).

* To apply security groups, refer to [Security group use cases](https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases).

* After the security group allows the IP address and port, confirm whether the firewall of the ECS instance also allows the corresponding traffic. If the firewall does not allow the traffic, the traffic will still be denied. For details, refer to [How to Configure Linux Instance Firewall?](https://developer.volcengine.com/articles/7270815826700140600) and [How to Configure Windows ECS Firewall?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5aaC5L2V6YWN572uLXdpbmRvd3Mt5LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf).

* We recommend that you operate with caution when allowing access to commonly used service ports, such as SSH (22), Redis (6379), MemCache (11211), MySQL (3306), SMB (445), RDP (3389), and SQL Server (1433). For more information on commonly used ports of ECS instances, refer to [Commonly used ports of ECS instances](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances).
