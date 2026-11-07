---
title: "Managing the jumbo frames"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enabling_or_Disabling_jumbo_frames"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Introduction

In BytePlus, a jumbo frame refers to an Ethernet frame whose payload exceeds the IEEE 802.3 standard of 1500 bytes. When a BytePlus Network Interface (ENI) transmits jumbo frames, the MTU can be set to a maximum of 8500 bytes.

For the same amount of data, compared with standard Ethernet frames, jumbo frames transmit larger data blocks per transfer, which reduces the CPU interrupt frequency for packet processing and protocol stack overhead, thereby easing the computing burden. They also use fewer packets, which can reduce network protocol processing overhead, queuing delay, and switch forwarding times, shortening network processing time. Therefore, jumbo frames are suitable for scenarios requiring large data block transmission, such as database synchronization, data migration, distributed computing, and video and multimedia processing.

<span id="6H6mY2x8"></span>
## Basic terms


|Term |Explanation |
|---|---|
|MTU |MTU (Maximum Transmission Unit) refers to the maximum amount of data that a single data link layer frame can carry in network communication. |
|PMTU |PMTU (Path Maximum Transmission Unit) refers to the minimum MTU along the transmission path from the source host to the destination host. |
|Fragmentation<br><br> |Fragmentation means that during transmission, when the outbound interface MTU of a forwarding device is smaller than the total length of an IP packet, the device splits the packet into multiple small IP fragments, forwards them separately, and reassembles them at the destination host to restore the original packet.<br><br>Fragmentation increases the burden on network devices and also carries the risk of packet loss. |
|DF flag<br><br> |The DF (Don't Fragment) flag is a bit in the Flags field of the IP header, used to indicate whether forwarding devices are allowed to fragment the packet. When DF=1, fragmentation is not allowed; when DF=0, fragmentation is allowed. |
|PMTU response<br><br> |PMTU Response refers to the ICMP error message sent back to the source host by a device when it discovers that a packet is too large and DF=1 during the Path MTU Discovery (PMTUD) process. The message carries the MTU value of the next\-hop link, based on which the source host reduces the packet size and retransmits.<br><br><br>* IPv4：ICMP Type 3, Code 4（Fragmentation Needed and DF set）<br><br>* IPv6：ICMPv6 Type 2（Packet Too Big） |
|PMTUD<br><br> |PMTUD (Path Maximum Transmission Unit Discovery) is a technology that dynamically detects the minimum MTU along the transmission path from the source host to the destination host by setting DF=1 in IP packets and combining it with the path MTU information fed back by the ICMP protocol. |
|MSS<br><br> |MSS (Maximum Segment Size) is the maximum amount of application data that a TCP segment can carry. MSS = MTU \- 20 (IP header) \- 20 (TCP header). |
|TCP MSS adjustment |TCP MSS Adjustment (MSS Clamping) is the most common method for intermediate devices to forcibly reduce the MSS during the TCP handshake, so that subsequent packets naturally do not exceed the path MTU without relying on ICMP. It is used to solve the problem of PMTU responses being intercepted (PMTUD black hole) in VPN/tunnel scenarios. |


<span id="hKt9THR4"></span>
## Action notes


* The specifications that support jumbo frames are as follows:

   
   |Topic |Specification |
   |---|---|
   |General |[g4i](https://docs.byteplus.com/en/docs/ecs/General-purpose), g4ie, g4il, g4al, g4als, g4ale |
   |Compute\-optimized |[c4i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized), c4ie, c4il, c4al, c4als, c4ale |
   |Memory\-optimized |[r4i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized), r4ie, r4il, r4ale |
   |Elastic bare metal type |ebmg4id, ebmc4id, ebmhfr4id |
   |Local SSD |i4 |
   

* Different traffic paths support different maximum MTU values, as follows:

   
   |Source host |Destination host |Traffic path |Maximum MTU supported by the communication link |
   |---|---|---|---|
   |Enable jumbo frames |Enable jumbo frames |Both are in the same VPC and communicate over the VPC private network. |8500 |
   ||Enable jumbo frames |Both are in the same region but different VPCs and communicate through **CEN**.<br><br>Explanation<br><br>In cross\-region scenarios, enabling jumbo frames is not currently supported for communication over CEN. |8500 |
   ||Jumbo frames not enabled |Both are in the same VPC and communicate over the VPC private network. |1500 |
   ||Jumbo frames not enabled |Both are in the same region but different VPCs and communicate through Cloud Enterprise Network (CEN) |1500 |
   ||Enable jumbo frames |Both are in different VPCs and communicate through a transit router (TR) or Direct Connect. |1500 |
   ||Enable jumbo frames |Both communicate through products such as EIP, NAT Gateway, Load Balancer, or PrivateLink |1500 |
   ||Enable jumbo frames |Both are in different VPCs and communicate through a VPN connection |1400 |
   

* If an instance is changed from a specification that supports jumbo frames to one that does not, jumbo frames must be disabled first.

* Jumbo frames support both IPv4 and IPv6.


<span id="Y01qzS89"></span>
## Recommendations


* Jumbo frames are only applicable to large data block transmission, and there are strict restrictions on traffic paths and instance specifications. Before use, confirm whether the traffic path, protocol, and ECS specification support jumbo frames; otherwise, packets may be fragmented or dropped, affecting transmission reliability, occupying network resources, and degrading network performance.

* It is recommended to enable PMTUD, make applications compatible with PMTUD, and adjust packet size as much as possible to avoid fragmentation during transmission and prevent network performance degradation. [Learn more](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface)


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Unless necessary, do not modify the MTU value. This is because modifying the ENI MTU value may cause data to be fragmented or dropped.</div>


* <div data-tips="true" data-tips-type="danger">Modifying jumbo frame settings requires restarting the instance. During the restart, services are unavailable.</div>


* <div data-tips="true" data-tips-type="danger">If any device on the communication link from the source host to the destination host does not support jumbo frames, disable jumbo frames on the source host.</div>



<span id="r2jZUQap"></span>
## Enable jumbo frames


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the target project and region.

4. Click " **···**  \> Network and security group \> Modify Jumbo Frame config" on the right side of the target ECS instance.

5. In the Enable Jumbo Frames field, check "Yes" and click "OK" to complete the enabling.

6. [Reboot ECS](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).

7. To view the MTU of an ENI, perform the following steps:

   
   <Tabs>
   <Tab zoneid="XjlMlOoQ" title="Linux system">
   <TabTitle>Linux system</TabTitle>
   
   Taking CentOS 7.9 as an example, the procedure is as follows:
   
   
   1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).
   
   2. Run the ifconfig command to view the ENI MTU value. The output is as follows:
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe5327430e6eb85a7773dc8c4882ee4b.png) </span>
   
   
   </Tab>
   <Tab zoneid="zU2Q3jKE" title="Windows system">
   <TabTitle>Windows system</TabTitle>
   
   Using Windows Server 2016 as an example, the steps are as follows:
   
   
   1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).
   
   2. On the Windows desktop, click Start \> Windows PowerShell to open Windows PowerShell.
   
   3. Run the following command to view the ENI name and MTU.
   
      ```Bash
      netsh interface ipv4 show subinterfaces
      ```
      
   
   4. The output is as follows:
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f41341d71c3bf9fd05c725f0bd68a496.png) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="mXxa3N76"></span>
## Disable jumbo frames


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the target project and region.

4. Click " **···**  \> Network and security group \> Modify Jumbo Frame config" on the right side of the target ECS instance.

5. In the Enable Jumbo Frames field, check "No" and click "OK" to complete the enabling.

6. [Reboot ECS](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).

7. To view the MTU of an ENI, perform the following steps:

   
   <Tabs>
   <Tab zoneid="OX7TLVBN" title="Linux system">
   <TabTitle>Linux system</TabTitle>
   
   Taking CentOS 7.9 as an example, the procedure is as follows:
   
   
   1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).
   
   2. Run the ifconfig command to view the ENI MTU value. The output should be similar to the following figure:
   
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_141c98809012fee4365b088eed25f8f3.png) </span>
   
   
   </Tab>
   <Tab zoneid="gHZKRen9" title="Windows system">
   <TabTitle>Windows system</TabTitle>
   
   Using Windows Server 2016 as an example, the steps are as follows:
   
   
   1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).
   
   2. On the Windows desktop, click Start \> Windows PowerShell to open Windows PowerShell.
   
   3. Run the following command to view the ENI name and MTU.
   
      ```JSON
      netsh interface ipv4 show subinterfaces
      ```
      
   
      The output is as follows:
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9653766b0f647d74ab49f8eb89725c39.png) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="uKSuF1my"></span>
## Related documentation

[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute)
