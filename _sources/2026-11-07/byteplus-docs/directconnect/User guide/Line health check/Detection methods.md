---
title: "Detection methods"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Detection_methods"
---

In a redundant\-link scenario, you can configure the appropriate health check mechanism based on the route type configured when creating the Direct Connect (DC) Virtual Interface. It enables periodical detection on the line to determine whether to converge routes based on the detection results. Different detection methods vary in different route types. BGP routing supports Bidirectional Forwarding Detection (BFD), and static routing supports BFD and Network Quality Analyzer (NQA). This section describes how to configure a detection method in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background


* **BFD**: Bidirectional Forwarding Detection (BFD) is a universal, standardized mechanism that provides fast, media\- and protocol\-independent failure detection. It is commonly used to monitor link connectivity in IP networks, enabling rapid detection of communication failures between devices. This facilitates timely failover, ensuring business continuity.

* **NQA**: Network Quality Analyzer (NQA) is a real\-time network performance probing and statistical technology. It analyzes link status, network performance, services, and service quality by sending probe packets, and provides parameters indicating current performance, such as delay, jitter, TCP connection time, and FTP transfer time. With NQA analysis results, you can promptly understand the network’s performance, diagnose faults, and locate issues.



|Detection method |Detection direction |Device requirements |Detection mechanism |Limits |
|---|---|---|---|---|
|BFD control packet |Bidirectional |BFD capability is required at both ends of the communication link. |Establish a BFD session between two systems, and periodically send BFD packets over that session. If one system fails to receive BFD packets within the negotiated detection timeout, it declares a failure on the bidirectional channel. |* Virtual Interfaces that use either of route types (**BGP** and **Static**) support enabling BFD.<br><br>* Ensure that the gateway devices of your data center support BFD configuration before using BFD.<br><br>* In static routing, the DC Gateway will check the static route status for its route table only after you enable BFD. When BFD on a static route fails, the route table marks that static route as **Unavailable**. Otherwise, the route status defaults to **Available**.<br><br>* ECMP is unsupported between BGP and static routes. We recommend avoiding their use in an active\-standby redundancy design.<br><br>* If redundant links are both using static routing, we recommend that you associate a DC Gateway with each link, and load two DC Gateways to the same CEN, enabling BFD for associated Virtual Interfaces.<br><br>* BytePlus BFD supports only single\-hop detection mode. If enabling BFD, you must configure BFD on the data center side with identical parameters (Detection method, Detect interval, and Detect multiplier). For procedure, see [Connecting an on-premises data center to a VPC via dual Direct Connects with BGP (load-balancing redundancy)](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-5). |
|BFD echo packet<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The BFD echo packet feature is in the beta stage. If you need a trial, please contact your account manager.</div><br> |Unidirectional |BFD capability is not required on the data center side. |BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. After receiving the probe packets, the on\-premises data center returns them along the original path. BytePlus rapidly determines link connectivity based on whether the response packets are received within the expected time window. |* Virtual Interfaces that use either of route types (**BGP** and **Static**) support enabling BFD.<br><br>* In static routing, the DC Gateway will check the static route status for its route table only after you enable BFD. When BFD on a static route fails, the route table marks that static route as **Unavailable**. Otherwise, the route status defaults to **Available**.<br><br>* If redundant links are both using static routing, we recommend associating a DC Gateway with each link, and loading two DC Gateways to the same CEN, enabling BFD for associated Virtual Interfaces.<br><br>* ECMP is unsupported between BGP and static routes. We recommend avoiding their use in an active\-standby redundancy design.<br><br>* BytePlus BFD supports only single\-hop detection mode.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the local IDC gateway configures security policies, configure policies to allow line detection requests:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Source IP: Volcano Interconnection address</div><br><br><br>* <div data-tips="true" data-tips-type="default">Destination IP: Volcano Interconnection address</div><br><br><br>* <div data-tips="true" data-tips-type="default">Destination port: 3785</div><br><br><br>* <div data-tips="true" data-tips-type="default">Protocol type: UDP</div><br> |
|NQA |Unidirectional |NQA capability is required at either end of the communication link. |Uses ICMP probe mechanism, setting the source IP and destination IP as interconnected IP pair​​. Calculate packet loss rate and round\-trip time based on whether and when response packets are received. |* Only Virtual Interfaces whose route type is **Static** support enabling NQA.<br><br>* Only supports route convergence for the from\-cloud direction. To achieve route convergence for the to\-cloud direction, you must configure NQA on the local data center's routing equipment. For procedure, see [Connecting an on-premises data center to a VPC via dual Direct Connects with static routing (active-standby redundancy)](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-8).<br><br>* The DC Gateway will check the static route status for its route table only after you enable NQA. When NQA on a static route fails, the route table marks that static route as **Unavailable**. Otherwise, the route status defaults to **Available**.<br><br>* ECMP is unsupported between BGP and static routes. We recommend avoiding their use in an active\-standby redundancy design.<br><br>* If redundancy links are both using static routing, we recommend you to associate a DC Gateway with each link, and load two DC Gateways to the same Cloud Enterprise Network (CEN), enabling NQA for associated Virtual Interfaces.<br><br>* We recommend avoiding the modification of NQA configuration during a link failure, which may cause route jitter.<br><br>* If the service traffic reaches the maximum bandwidth of the link, potential packet loss may cause NQA failure. For this scenario, we recommend setting NQA Detect interval and Detect multiplier values to the maximum. |


<span id="EJiiBCHL"></span>
## Procedures


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select your target region.

3. On the Virtual Interface page, click **Create DC irtual Interface**.

4. In the **Routing information** section of the **Create DC Virtual Interface** page, configure a detection method. This section only demonstrates parameters related to line detection. For more parameters for creating a DC Virtual Interface, see [Creating a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1).

   
   |Parameter |Description |
   |---|---|
   |Detect interval |The interval between consecutive probe packets. Unit: ms.<br><br><br>* BFD: The value ranges from 200 to 1000, and defaults to 1000.<br><br>* NQA: The value ranges from 1000 to 5000, and defaults to 2000. |
   |Detect multiplier |The number of detection attempts. If a session fails to receive the defined number of consecutive packets, the system declares a route failure.<br><br><br>* BFD: The value ranges from 3 to 10, and defaults to 3.<br><br>* NQA: The value ranges from 3 to 8, and defaults to 5.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the line traffic nearly reaches the maximum bandwidth after enabling NQA, we recommend setting Detect multiplier to "8".</div><br> |
   

5. Click **Create** to complete the action.
