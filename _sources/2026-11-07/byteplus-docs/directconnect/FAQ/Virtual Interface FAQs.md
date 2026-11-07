---
title: "Virtual Interface FAQs"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Virtual-interface"
---

* [Are there restrictions on the Local IP and Peer IP when creating a Virtual Interface?](https://docs.byteplus.com/en/docs/53/10471#.5Yib5bu66Jma5ouf5o6l5Y-j5pe25pys56uvSVDjgIHlr7nnq69JUOaYr-WQpuaciemZkOWItu-8nw==)

* [Are there regional requirements for the DC Connection and DC Gateway associated with a Virtual Interface?](https://docs.byteplus.com/en/docs/53/10471#.6Jma5ouf5o6l5Y-j5a-55YWz6IGU54mp55CG5LiT57q_44CB5LiT57q_572R5YWz55qE5Zyw5Z-f5piv5ZCm5pyJ6KaB5rGC77yf)

* [What is BFD?](https://docs.byteplus.com/en/docs/53/10471#.5LuA5LmI5pivQkZE5qOA5rWL77yf)

* [After enabling BFD, do I need to configure the on-premises IDC?](https://docs.byteplus.com/en/docs/53/10471#.5byA5ZCv5LqGQkZE5qOA5rWL5Yqf6IO95ZCO77yM5piv5ZCm6ZyA6KaB6YWN572u5pys5ZywSURD77yf)

* [Why does the BFD session fail to establish even though both the on-premises IDC side and the BytePlus side have BFD configured?](https://docs.byteplus.com/en/docs/53/10471#.5pys5ZywSURD5L6n5ZKM54Gr5bGx5L6n5Z2H6YWN572u5LqGQkZE5qOA5rWL77yM5Li65LuA5LmIQkZE5Lya6K-d5LiA55u05bu656uL5aSx6LSl77yf)

* [What is NQA?](https://docs.byteplus.com/en/docs/53/10471#.5LuA5LmI5pivTlFB5qOA5rWL77yf)

* [After enabling NQA, do I need to configure the on-premises IDC?](https://docs.byteplus.com/en/docs/53/10471#.5byA5ZCv5LqGTlFB5qOA5rWL77yM5piv5ZCm6ZyA6KaB6YWN572u5pys5ZywSURD77yf)

* [What is the difference between BFD and NQA?](https://docs.byteplus.com/en/docs/53/10471#.QkZE5qOA5rWL5ZKMTlFB5qOA5rWL55qE5beu5byC5piv5LuA5LmI77yf)

* [The configuration is complete, why is the Direct Connect network still down?](https://docs.byteplus.com/en/docs/53/10471#.5bey5a6M5oiQ5LqG5YWo6YOo6YWN572u77yM5Li65LuA5LmI5LiT57q_572R57uc6L-Y5piv5LiN6YCa77yf)

* [Why can't I configure the speed limit for the Virtual Interface?](https://docs.byteplus.com/en/docs/53/10471#683bFLEy)


<span id=".5Yib5bu66Jma5ouf5o6l5Y-j5pe25pys56uvSVDjgIHlr7nnq69JUOaYr-WQpuaciemZkOWItu-8nw=="></span>
## Are there restrictions on the Local IP and Peer IP when creating a Virtual Interface?

Yes, please adhere to the following principles:

**IPv4**


* Use private IP addresses (from `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`) for both Local and Peer IPs. They must be in the same subnet and must not conflict with any IP addresses used in your cloud or on\-premises environments.

* Do not use the `100.64.0.0/10` segment, as it is reserved for cloud services.

* The subnet mask must be between /8 and /31 (inclusive). A /30 mask (e.g., `10.0.0.1/30`) is recommended.

* The Local and Peer IPs must have the same subnet mask.

* The Local IP cannot be from the following restricted segments: `0.0.0.0/8`, `127.0.0.0/8`, `169.254.0.0/16`, `255.255.255.255`, `224.0.0.0` \- `239.255.255.255`, `240.0.0.0` \- `255.255.255.254`.


**IPv6**


* The mask must be between /64 and /127 (inclusive).

* You cannot configure the following IPv6 subnet routes:

   * Within subnets of `::1/128`, `FF00::/8`, and `FE80::/10`.

   * Equivalent to the `FE80::/9` subnet.

   * The Local IP cannot be from the following restricted segments: `FC01:A9FE::0/64` and `FE80:0:0:0:A9FE::/80`.


<span id=".6Jma5ouf5o6l5Y-j5a-55YWz6IGU54mp55CG5LiT57q_44CB5LiT57q_572R5YWz55qE5Zyw5Z-f5piv5ZCm5pyJ6KaB5rGC77yf"></span>
## Are there regional requirements for the DC Connection and DC Gateway associated with a Virtual Interface?

Yes, there are requirements. A Virtual Interface can only be associated with a DC Connection and a DC Gateway located in the same region. Therefore, ensure you select the correct region when applying for the DC Connection and creating the DC Gateway.

<span id=".5LuA5LmI5pivQkZE5qOA5rWL77yf"></span>
## What is BFD?

Bidirectional Forwarding Detection (BFD) is a universal, standardized, rapid fault detection mechanism that is media and protocol independent. It is commonly used to monitor link connectivity in IP networks, enabling rapid detection of communication failures between devices. This facilitates timely failover, ensuring business continuity.

BFD can quickly detect failures in the bidirectional forwarding path between two devices for various upper\-layer protocols (e.g., routing protocols). Typically, upper\-layer protocols use hello message mechanisms for fault detection, which takes on the order of seconds. BFD provides detection in milliseconds. Both BGP routes and Static routes can utilize BFD.

<span id=".5byA5ZCv5LqGQkZE5qOA5rWL5Yqf6IO95ZCO77yM5piv5ZCm6ZyA6KaB6YWN572u5pys5ZywSURD77yf"></span>
## After enabling BFD, do I need to configure the on\-premises IDC?

Yes. BFD performs bidirectional probing. If you enable the BFD feature when creating a Virtual Interface on the BytePlus side, you must also configure BFD on the Customer Edge (CE) device in your on\-premises data center (IDC).

Configuration commands vary slightly for different CE devices. Please consult your device vendor for specifics. Example:

Using a Huawei CE device as an example when creating the Virtual Interface with the configuration shown:


|Parameter |Value |
|---|---|
|BFD |Check |
|Detect interval |1000 |
|Detect multiplier |3 |


You need to log in to the Huawei CE device, perform the BFD configuration, and ensure the detection time and detection multiplier settings match.

```Plain Text
bgp <as_number>
peer <bgp_peer_address> bfd min-tx-interval
1000 min-rx-interval 1000 detect-multiplier 3
```


<span id=".5pys5ZywSURD5L6n5ZKM54Gr5bGx5L6n5Z2H6YWN572u5LqGQkZE5qOA5rWL77yM5Li65LuA5LmIQkZE5Lya6K-d5LiA55u05bu656uL5aSx6LSl77yf"></span>
## Why does the BFD session fail to establish even though both the on\-premises IDC side and the BytePlus side have BFD configured?

A BFD session cannot be established if the BFD configuration on the on\-premises data center and that on BytePlus are different.


1. Verify that the BFD configuration is consistent between the on\-premises IDC side and the BytePlus side, including the detection interval and detection multiplier.

2. Check if the BFD mode on the on\-premises IDC device is set to single\-hop. Since the current BytePlus BFD only supports single\-hop mode, you must ensure your on\-premises IDC device also uses single\-hop detection.


<span id=".5LuA5LmI5pivTlFB5qOA5rWL77yf"></span>
## What is NQA?

NQA: Network Quality Analyzer (NQA) is a real\-time network performance probing and statistical technology. It analyzes link status, network performance, services, and service quality by sending probe packets, and provides parameters indicating current performance, such as delay, jitter, TCP connection time, and FTP transfer time.

With NQA analysis results, you can promptly understand the network’s performance, diagnose faults, and locate issues. Using NQA requires only one end of the communication link to have NQA capability. Currently, only static routes support NQA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5byA5ZCv5LqGTlFB5qOA5rWL77yM5piv5ZCm6ZyA6KaB6YWN572u5pys5ZywSURD77yf"></span>
## After enabling NQA, do I need to configure the on\-premises IDC?

No. NQA is a unidirectional detection mechanism. If it has been configured for the Direct Connect Virtual Interface on BytePlus, it does not need to be configured on the on\-premises data center.

<span id=".QkZE5qOA5rWL5ZKMTlFB5qOA5rWL55qE5beu5byC5piv5LuA5LmI77yf"></span>
## What is the difference between BFD and NQA?


* **Differences in function availability**

   * BFD is available to all users.

   * NQA is only available to users who have had this capability enabled.

* **Differences in detection methods**

   * BFD is bidirectional detection.

   * NQA is unidirectional detection.

* **Differences in device requirements**

   * BFD requires that both communicating devices support the BFD capability.

   * Using NQA only requires that the device at either end supports NQA. As the devices of BytePlus support NQA, it is not necessary for on\-premises data center devices to support NQA.

* **Differences in detection mechanism**

   * BFD establishes a BFD session between two systems, and periodically sends BFD packets over that session. If one system fails to receive BFD packets within the negotiated detection timeout, it declares a failure on the bidirectional channel.

   * NQA uses ICMP probe mechanism, setting the source IP and destination IP as interconnected IP pairs. It calculates packet loss rate and round\-trip time based on whether and when response packets are received.

* **Differences in usage limits**

   * Limits for BFD:

      * Virtual Interfaces that use either route type (**BGP** and **Static**) support enabling BFD.

      * If redundancy links are both using static routing, we recommend that you associate a DC Gateway with each link, load two DC Gateways to the same CEN, and enable BFD for associated Virtual Interfaces.

      * BytePlus BFD supports only single\-hop detection mode. If enabling BFD, you must configure BFD on the data center side with identical parameters (Detection method, Detect interval, and Detect multiplier). For procedure, see [Connecting an on-premises data center to a VPC via dual Direct Connects with BGP (load-balancing redundancy)](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-5#.5q2l6aqk5YWt77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMQkZE).

   * Limits for NQA:

      * Only Virtual Interfaces whose route type is **Static** support enabling NQA.

      * Only supports route convergence for the from\-cloud direction. To achieve route convergence for the to\-cloud direction, you must configure NQA on the local data center's routing equipment. For procedure, see [Connecting an on-premises data center to a VPC via dual Direct Connects with static routing (active-standby redundancy)](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-5#.5q2l6aqk5YWt77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMQkZE).

      * We recommend avoiding the modification of NQA configuration during a link failure, which may cause route jitter.

      * If redundancy links are both using static routing, we recommend that you associate a DC Gateway with each link, load two DC Gateways to the same Cloud Enterprise Network (CEN), and enable NQA for associated Virtual Interfaces.

      * If the service traffic reaches the maximum bandwidth of the link, potential packet loss may cause NQA failure. For this scenario, we recommend setting NQA Detect interval and Detect multiplier values to the maximum.


<span id=".5bey5a6M5oiQ5LqG5YWo6YOo6YWN572u77yM5Li65LuA5LmI5LiT57q_572R57uc6L-Y5piv5LiN6YCa77yf"></span>
## The configuration is complete, why is the Direct Connect network still down?

In scenarios where the network connection between a data center and a VPC is established using Direct Connect, if you have completed all configurations and confirmed that there are no issues, please check whether any of the following eight IPs are used as the destination address:


* `100.96.0.32`

* `100.96.0.33`

* `100.96.0.34`

* `100.96.0.35`

* `100.96.0.36`

* `100.96.0.37`

* `100.96.0.38`

* `100.96.0.39`


Using the above addresses will result in the Direct Connect network being inaccessible. If you used the above 8 IPs as destination addresses, please modify them before performing network testing. If you have not used the above IPs as destination addresses, you can see [Direct Connect troubleshooting and solutions](https://docs.byteplus.com/en/docs/directconnect/Troubleshooting-and-solutions-for-Direct-Connect-issues) for further investigation.

<span id="683bFLEy"></span>
## Why can't I configure the speed limit for the Virtual Interface?

If the specified bandwidth of the Virtual Interface exceeds the bandwidth of its associated DC Connection, you cannot configure rate limiting.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you skip the LOA configuration, first <a href="https://docs.byteplus.com/en/docs/directconnect/Modify-dedicated-line-bandwidth">modify the bandwidth of the DC Connection</a> on DC Connection details page, and then <a href="https://docs.byteplus.com/en/docs/directconnect/Modifying-the-virtual-interface-bandwidth-limit">configure the rate limiting for the Virtual Interface</a>.</div>
