---
title: "Limits"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Limits"
---

Before using Direct Connect, you need to understand the following limits.

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits

The table below describes the default quotas for resources related to Direct Connect (DC) on the BytePlus platform. If the default quota of adjustable items does not meet your needs, you can go to BytePlus Quota Center to increase the corresponding quota. For specific actions, see [Quota Overview](https://docs.byteplus.com/en/docs/resourcemanagement/Quota_Overview).


|Topic |Quota parameter |Description |Default quota |Increaseable |Adjustable quota limit |
|---|---|---|---|---|---|
|DC Connection |directconnect |The number of DC Connections that you can create under a single account in a single region. |4 |Increasable |50 |
|DC Gateway |directconnectgateway |The number of DC Gateways that you can create under a single account in a single region. |10 |Increasable |20 |
||\- |The number of Cloud Enterprise Networks (CENs) that you can mount for a single DC Gateway.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Whether loading to a CEN under the same account or to a CEN under another account via cross\-account authorization, you can load a single DC Gateway to only one CEN.</div><br> |1 |No |\- |
|Virtual Interface |directconnect/virtual_interface |The number of DC virtual interfaces that you can associate with a single DC Connection. |5 |Self\-service upgrade is currently not supported. If needed, please contact your account manager. |\- |
||directconnectgateway/virtual_interface |The number of DC virtual interfaces that you can associate with a single DC Gateway. |8 |Increasable |16 |
|Route entry |directconnectgateway/static_route |The number of custom static route entries that a single DC Gateway can send to the on\-premises data center. |50 entries |Self\-service upgrade is currently not supported. If needed, please contact your account manager. |\- |
||directconnectgateway/bgp/bgp_route |The number of BGP route entries that a single BGP session can receive from the on\-premises data center. |100 |Increasable |200 |
||directconnectgateway/tr_route |The number of route entries that a single DC Gateway can receive from the CEN, TR, or Edge Interconnect (EIC). |100 |Increasable |1,000 |
|QoS policy |directconnect_qos |The number of QoS policies that you can create under a single account in a single region. |10 |Increasable |20 |
||\- |The number of advanced flow queues that you can add to a single QoS policy. |1 |No |\- |
||\- |The number of standard flow queues that you can add to a single QoS policy. |2 |Increasable |4 |
||directconnect_qos/rule |The number of flow classification rules that you can add under a single traffic queue. |5 |Increasable |10 |
|Health check |directconnect_healthcheck |The number of health check instances that you can create under a single account in a single region. |1 |Increasable |2 |
||directconnect_healthcheck/probe |The number of probes that you can add to a single health check instance. |4 |Increasable |10 |
|Failure drill |\- |The number of failure drill tasks that you can create under a single account in a single region. |20 |Increasable |\- |
||\- |The number of drill objects that you can add to a single drill task. |16 |Increasable |\- |


<span id=".54mp55CG5LiT57q_6ZmQ5Yi2"></span>
## Direct Connect connection limits


* Before establishing a DC Connection, you need to plan the overall network between the data center and the VPC to avoid subnet overlap.

* Do not use 100.64.0.0/10 for the data center. This subnet is occupied by cloud services in the VPC.

* BytePlus only provides free optical modules of 1 Gbps and 10 Gbps with a data transmission distance of 10 kilometers. If you need to use optical modules with the following specifications, you must prepare them yourself.

   * Optical modules of 1 Gbps and 10 Gbps with data transmission distances over 10 kilometers.

   * Optical modules of 40 Gbps, 100 Gbps, and 400 Gbps.


<span id=".6Lev55Sx5p2h55uu6ZmQ5Yi2"></span>
## Route entry limits


* Each Direct Connect Gateway supports up to 50 static route entries by default. Configuring more than 50 static route entries will fail.

* The system does not accept default routes (0.0.0.0/0) published from the data center, including both static and BGP routes.

* Each DC Gateway can have up to 8 BGP Peers by default and learn up to 100 BGP routes from each Peer. Excess BGP routes will be discarded.

* You cannot configure the following IPv4 subnet routes:

   `127.0.0.0/8`, `224.0.0.0/4`, `240.0.0.0/4`, and `255.255.255.255`.

* You cannot configure the following IPv6 subnet routes:

   * Within subnets of `::1/128`, `FF00::/8`, and `FE80::/10`.

   * Equivalent to the `FE80::/9` subnet.


<span id=".SVDpmZDliLY="></span>
## IP limits

When using DC Connections to enable network interconnection between your data center and VPC, avoid using `100.96.0.32`\-`100.96.0.39` as destination IP addresses. Otherwise, the network may become unreachable.

<span id=".5YaX5L2Z57q_6Lev6ZmQ5Yi2"></span>
## Redundancy limits


* Direct Connect redundancy supports two redundancy modes: active\-standby and load\-balancing. Choose the mode that fits your business scenario.

* For redundancy scenarios, we recommend connecting different DC Connections to different switches to improve business disaster recovery.

* **BytePlus** ** **  ** only guarantees service availability for multiple DC Connections to different access points. For multiple DC Connections to the same access point and a single DC Connection to the same access point, ** **BytePlus** ** will not guarantee service availability**. For details, see[ the Service availability commitment of Direct Connect SLA](https://docs.byteplus.com/en/docs/directconnect/BytePlus-Direct-Connect-Service-Level-Agreement-Template).


<span id=".5LiT57q_5pa95bel6ZmQ5Yi2"></span>
## Construction limits


* Before visiting the BytePlus access point data center, the construction party needs to download the approved Letter of Authorization (LOA) in advance. This document is required for construction within the BytePlus data center.

* The construction party must strictly adhere to the approved time slot specified in the LOA to enter the BytePlus access point data center for construction. Otherwise, entry will be denied.

* Only pre\-authorized engineers listed in the approved LOA can enter the BytePlus access point data center for construction. Unregistered personnel will be denied entry without exception.

* When entering the BytePlus access point data center for construction, adhere to the regulations introduced by the data center operator and BytePlus engineers to ensure smooth completion of the work.


<span id=".5YW25LuW6ZmQ5Yi2"></span>
## Other limits

The maximum acceptable AS\-Path length for Direct Connect is 30.
