---
title: "VPN gateway FAQs"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/VPN-gateway-FAQs"
---

* [How many VPN gateways can be created within the same VPC?](https://docs.byteplus.com/en/docs/52/5089#.5ZCM5LiAVlBD5LiL5Y-v5Yib5bu65Yeg5LiqVlBO572R5YWz77yf)

* [Can a single VPN gateway establish multiple IPsec connections?](https://docs.byteplus.com/en/docs/52/5089#.5LiA5LiqVlBO572R5YWz5piv5ZCm5Y-v5Lul5bu656uL5aSa5LiqSVBzZWPov57mjqXvvJ8=)

* [Do I need to purchase an additional public IP address to use VPN Connect?](https://docs.byteplus.com/en/docs/52/5089#.5L2_55SoVlBO6L-e5o6l5piv5ZCm6ZyA6KaB6aKd5aSW6LSt5Lmw5YWs572RSVDvvJ8=)

* [Will the system-assigned egress IP be retained after deleting the VPN gateway?](https://docs.byteplus.com/en/docs/52/5089#.5Yig6ZmkVlBO572R5YWz5ZCO57O757uf5YiG6YWN55qE5Ye65Y-jSVDmmK_lkKbkv53nlZnvvJ8=)

* [What is the relationship between a VPC and a VPN gateway?](https://docs.byteplus.com/en/docs/52/5089#.VlBD5LiOVlBO572R5YWz5pyJ5LuA5LmI5YWz57O777yf)

* [How to plan the VPC network address for VPN Connect?](https://docs.byteplus.com/en/docs/52/5089#.VlBO6L-e5o6l5aaC5L2V6KeE5YiSVlBD55qE572R57uc5Zyw5Z2A77yf)

* [What is the priority of VPN gateway routes compared to other routes?](https://docs.byteplus.com/en/docs/52/5089#.VlBO572R5YWz6Lev55Sx5LiO5YW25LuW6Lev55Sx55qE5LyY5YWI57qn5piv5LuA5LmI77yf)

* [Can multiple routes be added to a single VPN gateway?](https://docs.byteplus.com/en/docs/52/5089#.5Y-v5Lul5re75Yqg5aSa5p2hVlBO572R5YWz6Lev55Sx5LmI77yf)

* [Can local VPN gateway routes and peer gateway routes overlap?](https://docs.byteplus.com/en/docs/52/5089#.5pys56uvVlBO572R5YWz6Lev55Sx5ZKM5a-556uv572R5YWz6Lev55Sx5piv5ZCm5Y-v5LulT3ZlcmxhcO-8nw==)

* [Why is the measured traffic lower than the VPN gateway's bandwidth specification?](https://docs.byteplus.com/en/docs/52/5089#.5Li65LuA5LmI5a6e5rWL5rWB6YeP5bCP5LqOVlBO572R5YWz55qE5bim5a696KeE5qC877yf)

* [After the subscription VPN gateway expires and is stopped, will the IPsec-VPN connection automatically reconnect upon renewal?](https://docs.byteplus.com/en/docs/52/5089#.5YyF5bm05YyF5pyIVlBO572R5YWz5Yiw5pyf5YWz5YGc5ZCO5YaN57ut6LS577yMSVBzZWPov57mjqXmmK_lkKbkvJroh6rliqjph43ov57vvJ8=)

* [What new features do different versions of the VPN gateway support?](https://docs.byteplus.com/en/docs/52/5089#.5LiN5ZCM54mI5pysVlBO572R5YWz5pSv5oyB55qE5paw5Yqf6IO95pyJ5ZOq5Lqb77yf)

* [Why is the configured VPN gateway route not delivered to the associated VPC route table?](https://docs.byteplus.com/en/docs/52/5089#.5Li65LuA5LmI6YWN572u55qEVlBO572R5YWz6Lev55Sx5pyq5LiL5Y-R6Iez5omA5bGeVlBD55qE5YWo6YOo6Lev55Sx6KGoPw==)

* [How to view the egress IP address of the VPN gateway?](https://docs.byteplus.com/en/docs/52/5089#.5aaC5L2V5p-l55yLVlBO572R5YWz55qE5Ye65Y-jSVDlnLDlnYDvvJ8=)

* [Why did the bandwidth limit of the VPN gateway exceed without triggering the configured bandwidth monitoring alarm?](https://docs.byteplus.com/en/docs/52/5089#.5Li65LuA5LmIVlBO572R5YWz5bim5a696LaF6ZmQ5rKh5pyJ6Kem5Y-R5bey6YWN572u55qE5bim5a6955uR5o6n5ZGK6K2m77yf)


<span id=".5ZCM5LiAVlBD5LiL5Y-v5Yib5bu65Yeg5LiqVlBO572R5YWz77yf"></span>
## How many VPN gateways can be created within the same VPC?

The number of VPN gateways supported within the same VPC is limited by the quota item "number of VPN gateways allowed per account per region." By default, if there is only one VPC in the target account, a maximum of 5 VPN gateways can be created under that VPC.

<span id=".5LiA5LiqVlBO572R5YWz5piv5ZCm5Y-v5Lul5bu656uL5aSa5LiqSVBzZWPov57mjqXvvJ8="></span>
## Can a single VPN gateway establish multiple IPsec\-VPN connections?

Yes. A single VPN gateway can establish up to 10 IPsec\-VPN connections.

<span id=".5L2_55SoVlBO6L-e5o6l5piv5ZCm6ZyA6KaB6aKd5aSW6LSt5Lmw5YWs572RSVDvvJ8="></span>
## Is it necessary to purchase additional public IP addresses when using a VPN attachment?

No. When using a VPN attachment, after the VPN gateway is created, the system automatically assigns a public IP address to the VPN gateway as its egress IP address. Therefore, you do not need to purchase additional public IP resources.

<span id=".5Yig6ZmkVlBO572R5YWz5ZCO57O757uf5YiG6YWN55qE5Ye65Y-jSVDmmK_lkKbkv53nlZnvvJ8="></span>
## Will the egress IP address assigned by the system be retained after deleting the VPN gateway?

No. The egress IP address is a public IP address automatically assigned by the system when creating the VPN gateway, and its lifecycle follows the VPN gateway. After you delete the VPN gateway, all resources associated with it and related configuration information will be released.

<span id=".VlBD5LiOVlBO572R5YWz5pyJ5LuA5LmI5YWz57O777yf"></span>
## What is the relationship between a VPC and a VPN gateway?

The VPN gateway is deployed on the VPC and connects all resources within the VPC.

<span id=".VlBO6L-e5o6l5aaC5L2V6KeE5YiSVlBD55qE572R57uc5Zyw5Z2A77yf"></span>
## How does a VPN attachment plan the network addresses of a VPC?

When using the VPN attachment feature to establish a connection between an on\-premises data center and a Virtual Private Cloud (VPC), make sure the subnet of the on\-premises data center does not overlap or match the subnet of the VPC where the VPN gateway is located.

<span id=".VlBO572R5YWz6Lev55Sx5LiO5YW25LuW6Lev55Sx55qE5LyY5YWI57qn5piv5LuA5LmI77yf"></span>
## What is the priority of the VPN gateway route compared to other routes?


* VPN gateway route entries and other route entries only differ in priority based on the destination address mask. The larger the mask, the higher the priority.

* When the route table contains custom route entries with the same next hop type and overlapping target subnets, traffic is forwarded following the Longest Prefix Match (LPM) principle.


<span id=".5Y-v5Lul5re75Yqg5aSa5p2hVlBO572R5YWz6Lev55Sx5LmI77yf"></span>
## Can a VPN gateway have multiple routes added?

Yes. A VPN gateway supports creating up to 20 route entries.

<span id=".5pys56uvVlBO572R5YWz6Lev55Sx5ZKM5a-556uv572R5YWz6Lev55Sx5piv5ZCm5Y-v5LulT3ZlcmxhcO-8nw=="></span>
## Can the local VPN gateway routes overlap with the peer gateway routes?

No. When using VPN Connect to link a VPC with an on\-premises data center or another VPC, configuring the VPN gateway route with overlapping CIDR blocks between the VPN gateway route and the private CIDR blocks of the data center or other VPC will create a routing loop at the VPN gateway. This causes routes published on the BytePlus VPN gateway to loop back directly to the VPN gateway, resulting in network connectivity failure between both ends of the VPN connection.

For example, if the VPN gateway CIDR block is `10.0.1.0/24` and the private CIDR blocks of the on\-premises IDC or other VPCs are `10.0.2.0/24` and `10.0.3.0/24`, you must not configure a large CIDR block including `10.0.1.0/24`, `10.0.2.0/24`, and `10.0.3.0/24`, such as `10.0.0.0/8`, in the VPN gateway route.

You should configure route entries on the VPN gateway with the next hop set to the IPsec\-VPN connection, where the peer CIDR blocks of the IPsec\-VPN connection are `10.0.2.0/24` and `10.0.3.0/24`.

<span id=".5Li65LuA5LmI5a6e5rWL5rWB6YeP5bCP5LqOVlBO572R5YWz55qE5bim5a696KeE5qC877yf"></span>
## Why is the measured traffic lower than the bandwidth specification of the VPN gateway?

When using VPN Connect, if the actual service data traffic significantly exceeds the bandwidth specification of the VPN gateway, the sequence number order of the service data packets may differ greatly from the normal order. The anti\-replay detection will treat this as packet replay and actively discard some data packets, causing the measured traffic to be lower than the VPN gateway's bandwidth specification.

<span id=".5YyF5bm05YyF5pyIVlBO572R5YWz5Yiw5pyf5YWz5YGc5ZCO5YaN57ut6LS577yMSVBzZWPov57mjqXmmK_lkKbkvJroh6rliqjph43ov57vvJ8="></span>
## Will the IPsec\-VPN connection automatically reconnect after renewing the Subscription when the Subscription VPN gateway expires and shuts down?

No. An IPsec\-VPN connection disconnects when the VPN gateway expires and shuts down. After renewing the VPN gateway subscription, please refer to the following steps to reconnect the IPsec\-VPN connection.


* **Method 1**

   When the peer (on\-premises data center or other VPC) actively initiates IKE SA and IPsec SA, then executes the `Ping` command to access the VPC or when data passes through, the IPsec tunnel is triggered to re\-establish the connection.

* **Method 2**

   1. Log in and go to the [VPN Connection](https://console.byteplus.com/vpn/vpnConnect) page.

   2. Find the IPsec\-VPN connection associated with the VPN gateway to be renewed in the IPsec\-VPN connection list, click the **Modify** button on the right side to enter the edit page.

   3. No information needs to be changed; click the **Authorize** button.

   4. When the `Ping` command is executed to access the VPC or when data passes through, the IPsec tunnel is triggered to re\-establish the connection.


<span id=".5LiN5ZCM54mI5pysVlBO572R5YWz5pSv5oyB55qE5paw5Yqf6IO95pyJ5ZOq5Lqb77yf"></span>
## What new features do different versions of the VPN gateway support?

The features supported by different versions of the VPN gateway vary. For new features supported by each version, see [New feature release notes](https://docs.byteplus.com/en/docs/vpn/What-is-New).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Previous versions that have not been upgraded do not support features introduced in later versions. To use new features, upgrade the VPN gateway to the latest version. For details, see <a href="https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway">Upgrading a VPN gateway</a>.</div>


<span id=".5Li65LuA5LmI6YWN572u55qEVlBO572R5YWz6Lev55Sx5pyq5LiL5Y-R6Iez5omA5bGeVlBD55qE5YWo6YOo6Lev55Sx6KGoPw=="></span>
## Why are the routes configured on the VPN gateway not pushed to all route tables of the associated VPC?


* **Issue cause**

   Route entries added on the VPN gateway only apply to the **system route table of the VPN gateway’s host VPC**. They do not apply to the custom route table of that VPC. Therefore, if the VPN gateway’s host VPC has a custom route table, traffic from subnets associated with this custom route table cannot be forwarded to the VPN gateway.

* **Solution**

   If traffic from a subnet associated with a custom route table needs to be forwarded to the VPN gateway, you can manually add a route entry in the custom route table. Set the destination CIDR to the peer network segment (on\-premises data center or other VPC) and the next hop to the VPN gateway to forward the subnet traffic to the VPN gateway. For detailed steps, refer to [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).


<span id=".5aaC5L2V5p-l55yLVlBO572R5YWz55qE5Ye65Y-jSVDlnLDlnYDvvJ8="></span>
## How to check the VPN gateway’s egress IP address?

After the VPN gateway is created, the system automatically assigns a public IP address as the VPN gateway's egress IP. You can view the egress IP in the BytePlus VPN gateway console.

**Procedure**


1. Log in to the VPN gateway console, then select the target region and project of the VPN gateway in the top navigation bar.

2. In the VPN gateway list, the **IP address** column of the target VPN gateway shows the VPN gateway's egress IP.


<span id=".5Li65LuA5LmIVlBO572R5YWz5bim5a696LaF6ZmQ5rKh5pyJ6Kem5Y-R5bey6YWN572u55qE5bim5a6955uR5o6n5ZGK6K2m77yf"></span>
## Why did the configured bandwidth monitoring alert not trigger when the VPN gateway bandwidth exceeded its limit?

The bandwidth limit of the VPN gateway applies to the traffic of encapsulated encrypted packets, while the bandwidth monitoring alert metrics actually collect the sum of the inbound and outbound IPsec traffic of the VPN gateway, which is the traffic of the original packets before encapsulation. This causes the CloudMonitor alert not to trigger when the actual inbound and outbound VPN gateway traffic exceeds the bandwidth limit.

To avoid this issue, when configuring alarm policies to monitor VPN gateway metrics on the CloudMonitor platform, select monitoring metrics that include packet encapsulation overhead for the trigger condition, such as: VPN gateway outbound/inbound bandwidth utilization.
