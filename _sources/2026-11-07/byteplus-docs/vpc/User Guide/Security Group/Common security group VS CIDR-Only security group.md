---
title: "Common security group VS CIDR-Only security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Common-security-group-VS-CIDR-Only-security-group"
---

This topic compares common security groups and CIDR\-Only security groups across four aspects: IP capacity, intra\-group communication, support for referencing other security groups, and default rules. This comparison helps you more accurately select the security group type suited to your business scenario.

<span id="KuUi837u"></span>
## IP capacity


|Category |Explanation |
|---|---|
|Common Security Group |Up to 6000 private IP addresses (including both IPv4 and IPv6 addresses) can be associated |
|CIDR\-Only Security Group |The number of associated private IPs is unlimited<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Limited by ENI count. A single security group can be associated with a maximum of 15,000 ENIs by default. If the default quota does not meet your needs, please contact your account manager.</div><br> |


<span id="TmP3rFSS"></span>
## **Intra\-group communication**


|Category |Explanation |
|---|---|
|Common Security Group |Intra\-group communication is allowed by default<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">An inbound rule with itself as the source ensures communication between ENIs within the group. If deleted, private communication within the group is broken.</div><br> |
|CIDR\-Only Security Group |Intra\-group communication is isolated by default |


<span id="7ZuBpADh"></span>
## **Supports referencing security groups**


|Category |Explanation |
|---|---|
|Common Security Group |Rules can reference other security groups. All IP addresses within the referenced group serve as the source or destination IP. |
|CIDR\-Only Security Group |Rules cannot reference other security groups. |


<span id="H96Ap6Uk"></span>
## Default rule


|Category |Direction |Priority |Strategy |Agreement |Port range |Source/destination address |Description |
|---|---|---|---|---|---|---|---|
|Common Security Group |Inbound |1 |Allow |ALL |ALL |This security group |Allow ECSs within the same security group to communicate with each other |
||Outbound<br><br> |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow all IPv4 traffic |
|||100 |Allow |ALL |ALL |::/0 |Allow all IPv6 traffic |
|CIDR\-Only Security Group |Inbound |\- |\- |\- |\- |\- |\- |
||Outbound<br><br> |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow all IPv4 traffic |
|||100 |Allow |ALL |ALL |::/0 |Allow all IPv6 traffic |
