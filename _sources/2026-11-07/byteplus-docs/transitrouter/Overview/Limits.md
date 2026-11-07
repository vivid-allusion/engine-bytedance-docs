---
title: "Limits"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04"
---

This topic describes the default quantity limits for resources related to Transit Router (TR).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The TR IPv6 and multicast features are in the beta stage. If you need a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="tip">The conversion factor between Gbps and Mbps is 1,000, i.e. 20 Gbps = 20,000 Mbps.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Network resource |Limit description |
|---|---|
|TR instance |Instance types that do not support the TR service: General\-purpose g1, Compute\-optimized c1, Memory\-optimized r1, Local SSD i1, Big Data Storage d1s, GPU Accelerated g1t, GPU Accelerated g1tl, Local SSD EBM ebmi2, General\-purpose EBM ebmg2i, General\-purpose EBM ebmg2a, High Frequency Compute\-optimized EBM ebmhfc2i, and Security Enhanced EBM ebmg2t (beta). [Learn more](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) |
||The maximum bandwidth per availability zone is 20 Gbps for a single TR instance by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can check the maximum bandwidth on the TR instance details page. If it is insufficient, contact your account manager.</div><br> |
||The CIDR blocks of an on\-premises data center connected via TR must not be `169.254.255.0/24` or `FE80::/56` . |
|Network instance attachment |The maximum bandwidth per availability zone is 10 Gbps for a single attachment by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can check the maximum bandwidth on the attachment details page. If it is insufficient, contact your account manager.</div><br> |
||A single VPC supports up to 5 attachments by default. |
||A single VPC allows up to 5 attachments to enable route synchronization concurrently. |
|TR bandwidth package |The maximum bandwidth is 10 Gbps for a single bandwidth package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To modify quota, please contact your account manager.</div><br> |
|TR route table |Each TR route table supports learning up to 16 routes that share a destination CIDR block from separate DC Gateways, forming equal\-cost multi\-path routing (ECMP). |
|Route policy |Within the same route policy, a single policy entry can contain multiple types of match conditions, and each condition can have multiple values. |
||A single TR route table supports associating a maximum of one inbound and one outbound route policy at the same time. |
||Entries in an inbound route policy do not support match conditions for target instance type and ID.  |
||If you change the action of an inbound route policy from Deny to Allow and this change causes the number of routes to exceed the TR's quota, any additional routes beyond the quota limit will not take effect. Moreover, these routes will not become effective automatically even after the quota is sufficient. |
|Forwarding policy |Priority values of policy entries cannot be duplicated within the same forwarding policy. |
|Traffic marking policy |This feature currently only supports inter\-region attachments. |
||A single inter\-region attachment supports only one traffic marking policy. |
|Traffic queue policy |This feature currently only supports inter\-region attachments. |
||A single inter\-region attachment supports only one traffic queue policy. |
|Multicast |You can add a maximum of 10 network interfaces when adding multicast source or members. |
||The maximum bandwidth is 10 Gbps for a single multicast group.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum bandwidth here refers to the aggregate bandwidth of the TR's inbound traffic from the multicast source plus its outbound traffic to all multicast members.</div><br> |
|Flow log |The TR flow log feature is unavailable in regions where the Torch Log Service (TLS) is unsupported, as its operation requires integration with TLS. For regions where TLS is available, see [Select an endpoint](https://docs.byteplus.com/en/docs/tls/endpoint). |
||Only inter\-region attachments support flow logs.  Within the same TR instance, only one flow log can be configured per TR attachment. |
||Exceeding quotas for log projects and log topics in TLS may cause inability to create TR flow logs. For quota details, see [Apply for resource quota](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota). |


<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The adjustable quota items are listed in the table below. If the default quota is insufficient, see <a href="https://console.byteplus.com/quota/productList">Create quota adjustment request</a> to increase quota.</div>



|Network resource |Quota parameter |Description |Maximum |Adjustable |Adjustable quota limit |
|---|---|---|---|---|---|
|TR instance |tr |The maximum number of TR instances that you can create under a single account in a single region<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Shared TR instances do not count toward the TR instances that a shared user  can create.</div><br> |5 |Yes |10 |
||tr/share_to_account_number |The maximum number of shared users that you can share a single TR instance with |10 |Yes |50 |
||tr/accept_shared_tr_number |The maximum number of shared TR instances that you can accept under a single account in a single region |10 |Yes |50 |
|Network instance attachment |tr/vpc_attachment |The maximum number of VPC attachments (including cross\-account attachments within this account) that you can create for a single TR instance |200 |Yes |1,000 |
||vpc_associate_tr_quota |The maximum number of TR instances to which you can attach the same VPC |5 |No |\-\- |
||tr/vpn_attachment |The maximum number of VPN attachments that you can create for a single TR instance |10 |Yes |50 |
||tr/dcgw_attachment |The maximum number of DC Gateway attachments that you can create for a single TR instance |10 |Yes |16 |
||tr/inter_region_peer_attachment |The maximum number of inter\-region attachments that you can create for a single TR instance |10 |No |\-\- |
|TR route table |tr/route_table/routeentry |The maximum number of routes (including IPv4 and IPv6) that you can add to a single TR route table |2,000 |No |\-\- |
||tr/route_table |The maximum number of TR route tables (including the TR system route table) that you can create for a single TR instance |20 |No |\-\- |
|TR bandwidth package |trbandwidthpackage |The maximum number of bandwidth packages that you can create in a single account across all regions |10 |Yes |100 |
|Route policy |tr/route_policy_table |The maximum number of route policies that you can create for a single TR instance |40 |No |\-\- |
||tr/route_policy_table/route_policy_entry |The maximum number of entries that you can add to a single route policy |20 |Yes |100 |
|Forwarding policy |tr/forward_policy_table |The maximum number of forwarding policies that you can create for a single TR instance |5 |Yes |20 |
||tr/forward_policy_table/forward_policy_entry |The maximum number of entries that you can add to a single forwarding policy |10 |Yes |100 |
|Traffic marking policy |tr/traffic_qos_marking_policy |The maximum number of traffic marking policies that you can create for a single TR instance |10 |No |\-\- |
||tr/traffic_qos_marking_policy/traffic_qos_marking_entry |The maximum number of marking rules that you can add to a single traffic marking policy |100 |Yes |500 |
|Traffic queue policy |tr/traffic_qos_queue_policy |The maximum number of traffic queue policies that you can create for a single TR instance |10 |No |\-\- |
||tr/traffic_qos_queue_policy/traffic_qos_queue_entry |The maximum number of queues (excluding the default queue) that you can add to a single traffic queue policy |64 |No |\-\- |
|Multicast |tr/multicast_domain |The maximum number of multicast domains that you can create for a single TR instance |20 |No |\-\- |
||tr/multicast_source_and_member |Total number of multicast sources and members per TR instance |2,000 |Yes |10,000 |
||tr/multicast_domain/subnet |The maximum number of subnets per multicast domain |10 |Yes |50 |
||tr/multicast_group/multicast_member |The maximum number of sources per multicast group |100 |No |\-\- |
||tr/multicast_group/multicast_source |The maximum number of members per multicast group |100 |No |\-\- |
