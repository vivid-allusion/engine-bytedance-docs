---
title: "Limits"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Limits"
---

This topic details the limits for resources related Virtual Private Cloud (VPC).

For the quota items adjustable in the table below, if the default quotas are insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to request an increase.

<span id=".56eB5pyJ572R57uc"></span>
## VPC


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|vpc |Maximum number of VPCs (including default VPC) creatable per account per region |10 |Yes<br><br> |50 |
|vpc/subnet |Maximum number of subnets creatable per VPC (including the default subnet) |200 |Yes |250 |
|resource_share_recipient_accept |Maximum number of subnets a single account can share |50 |Yes |200 |
|resource_share_account_num |Maximum number of accounts a single subnet can be shared with |50 |Yes |200 |
|vpc/secondary_cidr |Maximum secondary CIDRs addable per VPC |5 |No |\-\- |
|vpc/cidr_v6 |Maximum IPv6 CIDR blocks attachable per VPC |1 |No |\-\- |
|None |Maximum number of custom tags per VPC |50 |No |\-\- |


<span id=".6Lev55Sx6KGo"></span>
## Route Table


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|vpc/route_table |Maximum number of route tables creatable per VPC (including both system\-maintained route tables and custom route tables) |10 |Yes |32 |
|vpc/route_table/route_entry |Maximum custom route entries addable to a single route table |200 |Yes |1,000 |
|None |Maximum route tables associable with a single subnet |1 |No |\-\- |


<span id=".572R5Y2h"></span>
## Network Interface (ENI)


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|eni |Maximum secondary network interfaces creatable per account per region |View in the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=VPC) |Yes |20,000 |
|&nbsp;<br><br>None |Number of primary network interfaces attachable per ECS instance |1 |No |\-\- |
||Maximum number of network interfaces (including 1 primary ENI) attachable to a single ECS instance |The maximum number of network interfaces supported varies by ECS instance type. For specific capacities, see [data in the ENI column of the specification instance list](https://docs.byteplus.com/en/docs/ecs/General-purpose). |No |\-\- |
||Maximum number of custom tags per ENI |50 |No |\-\- |


<span id=".5a6J5YWo57uE"></span>
## Security Group


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|security_group |Maximum number of security groups creatable per account per region (including default security groups) |300 |Yes<br><br> |10,000 |
|security_group/ingress_entry |Maximum inbound rules addable per security group |* 200 IPv4 rules<br><br>* 200 IPv6 rules |Yes |500 |
|security_group/egress_entry |Maximum outbound rules addable per security group |* 200 IPv4 rules<br><br>* 200 IPv6 rules |Yes |500 |
|eni/security_group |Maximum number of Security Groups attachable per Network Interface |5 |Yes |15 |
|vpc/security_group/eni |Network interfaces that can be associated with a single security group |2,000 |No |\-\- |
|vpc/security_group/ip |Maximum private IP addresses (IPv4/IPv6) associable with a single security group |6,000 |No |\-\- |
|None  |Maximum number of Security Group IDs referenceable by a single security group |10 | | |
|None |Maximum custom tags addable to a single security group |50 | | |


<span id=".572R57ucQUNM"></span>
## Network ACL


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|vpc/acl |Maximum number of Network ACLs creatable per VPC |200 |No |\-\- |
|None |Maximum network ACLs attachable per subnet |1 |No |\-\- |
|acl/ingress_entry |Maximum inbound rules supportable per Network ACL |* 20 IPv4 rules<br><br>* 20 IPv6 rules |&nbsp;<br><br>&nbsp;<br><br>Yes |100 |
|acl/egress_entry |Maximum outbound rules supportable per Network ACL |* 20 IPv4 rules<br><br>* 20 IPv6 rules ||100 |


<span id="pJmon1X3"></span>
## High\-Availability Virtual IP Address (HAVIP)


|Quota parameter |Description |Max |Adjustable |Cap |
|---|---|---|---|---|
|havip |Maximum number of HAVIPs creatable per account per region |20 |Yes |30 |
|vpc/havip |Maximum number of HAVIPs creatable within a single VPC |5 |Yes |15 |
|&nbsp;<br><br>None |Maximum HAVIPs attachable per ECS |5 |&nbsp;<br><br>No<br><br> |<div style="text-align: center"><br></div><br><br><br>\-\-<br><br> |
||Maximum number of HAVIPs simultaneously attachable to a single network interface |5 |||
||Maximum number of ECS instances or network interfaces simultaneously attachable to a single HAVIP |10 |||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HAVIP supports unicast only and does not support multicast or broadcast. When configuring high\-availability services using HA software (e.g., Keepalived, Windows Server Failover Cluster), you must set the communication mode to unicast.</div>


<span id="HX6RRU8r"></span>
## Flow log


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|vpc_flowlog |Maximum number of flow logs creatable per account per region |10 |Yes |30 |


<span id="IMwjDkN6"></span>
## Prefix list


|Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|
|prefixlist |Maximum number of prefix lists creatable per account per region |100 |&nbsp;<br><br>No<br><br> |&nbsp;<br><br>\-\-<br><br> |
|prefixlist/maxentry |Maximum prefix list entries addable to a single prefix list |200 |||
|prefixlist/resource |Maximum number of resources associable with a single prefix list |1,000 |||


<span id="yu0wKDSz"></span>
## Traffic mirror


|Resource |Quota parameter |Description |Max |Adjustable |Adjustable limit |
|---|---|---|---|---|---|
|Traffic mirror session |mirror_session |Maximum number of Traffic Mirror Sessions creatable per account per region |10,000 |&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>No<br><br>&nbsp;<br><br> |&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>\-\- |
||mirror_session/mirror_source |Maximum number of mirror sites associable with a single mirror session |1 |||
||None |Maximum number of mirror targets associable with a single mirror session |1 |||
|||Maximum number of filter rules associable with a single mirror session |1 |||
|Traffic mirror filter |mirror_filter |Maximum number of filter rules creatable per account per region |10,000 |||
||mirror_filter/mirror_session |Number of mirror sessions associable with a mirror filter rule |2,000 |||
||mirror_filter/rule |Maximum mirror filter rules per traffic direction under a single Mirror Filter |10 |||
|Mirror site |mirror_source/mirror_session |Maximum number of mirror sessions associable with a single mirror site |3 |||
|Traffic mirror target |mirror_target |Maximum number of traffic mirror targets supportable per account per region |10,000 |||
||mirror_target/mirror_session |Maximum number of mirror sessions associable with a single mirror target |10 |||
||mirror_target/mirror_source |Maximum number of mirror sites associable with a single traffic mirror target |100 |||
