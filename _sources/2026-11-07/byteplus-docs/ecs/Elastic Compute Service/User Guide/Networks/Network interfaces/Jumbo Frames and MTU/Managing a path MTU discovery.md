---
title: "Managing a path MTU discovery"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing-a-path-MTU-discovery"
---

<span id="iRPYJZnY"></span>
## Introduction​

PMTUD (Path Maximum Transmission Unit Discovery) is a technique that dynamically detects the minimum MTU along the transmission path from a source host to a destination host by setting the DF flag in IP packets and using path MTU information fed back by the ICMP protocol.

<span id="Qz9fsd65"></span>
## How it works

When sending a packet, the source host sets DF=1. If a device with a smaller MTU exists on the path, that device drops the packet and returns an ICMP error. The source host records that MTU value and adjusts the packet size until the destination host receives the packet. Steps:


1. **Set DF flag**: When sending a packet, the source host sets the **DF (Don't Fragment) flag** to 1 in the IP header, indicating that devices on the network path are not allowed to fragment the packet.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The IPv6 header has no DF flag and does not support fragmentation.   </div>
   

2. **Processing by devices on the path**:

   * If the MTU of all devices on the path is greater than or equal to the packet size, the packet reaches the destination host successfully.

   * If a device finds that the packet size is larger than its own MTU and DF=1, the device **drops** the packet.

3. **ICMP error message**: After dropping the packet, the device sends an ICMP error message to the source host.

   * **IPv4**: Sends ICMP Type 3, Code 4 (Fragmentation Needed and DF set) to the source host, carrying the device's MTU value in the message.

   * **IPv6**: Sends ICMPv6 Type 2 (Packet Too Big) to the source host, carrying the device's MTU value in the message.

4. **Source host adjustment**: After receiving the ICMP error message, the source host performs the following actions:

   * Parses the MTU value contained in the ICMP message.

   * Records the MTU to that destination address in its routing table or connection cache.

   * Repackages and sends the previously failed data using this new, smaller MTU value.

5. **PMTU update**:

   PMTU is not permanently valid. The default aging time of the Linux system route cache is 600 seconds. After aging, re\-detection is required. When a small MTU exists on the link, it is recommended to perform periodic detection or adjust the aging time.

   This process repeats until an MTU small enough is found so that packets can reach the destination without fragmentation.


<span id="JdKKeYr0"></span>
## Enable/Disable PMTUD

When PMTUD is enabled on all devices along the transmission path, the source host sends packets to the destination host. If a device (such as a router) on the path has an MTU smaller than the packet, it fragments the data and returns an ICMP message (containing its MTU) to the source host. The source host's application can then adapt accordingly, proactively adjusting the packet size to avoid network performance degradation caused by fragmentation during transmission. [Learn more](https://www.rfc-editor.org/rfc/rfc1191.html)

<span id="7MHXchbd"></span>
### Action notes

Ensure that all devices along the transmission path allow PMTUD ICMP messages, such as security groups, network ACLs, and firewalls on the source/destination hosts.

<span id="T79jLLIz"></span>
### Procedures

Taking CentOS 7.9 as an example, the procedure is as follows:


1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Enter the following command to check whether PMTUD is enabled.

   `sysctl net.ipv4.ip_no_pmtu_disc`

   If the return value is `0`, PMTUD is enabled; if the return value is `1`, PMTUD is disabled.

3. Enable and disable actions:

   * **Enable**: Run the following command to Enable PMTUD.

      `sysctl -w net.ipv4.ip_no_pmtu_disc=0`

   * **Disable**: Run the following command to Disable PMTUD.

      `sysctl -w net.ipv4.ip_no_pmtu_disc=1`


<span id="HWX50FkV"></span>
## Manually detect PMTU

Taking CentOS 7.9 as an example, the procedure is as follows:


1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to detect the minimum MTU from the source host to the destination host.

   `ping -c 1 -M do -s [packet size] destination address`

   * \-c 1: Send only one probe packet.

   * \-M do: Do not allow the probe packet to be fragmented.

   * \-s [packet size]: Size of the probe packet to send. Test a 1500\-byte MTU (1472 packet size + 20\-byte IP header + 8\-byte ICMP header).

   Example: `ping -c 1 -M do -s 1472 192.168.1.66`

3. If the ping succeeds, adjust the probe packet size; if an ICMP error message is returned, the PMTU is obtained.


&nbsp;
