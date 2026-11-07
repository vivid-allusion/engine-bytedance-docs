---
title: "SNAT entry FAQs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/SNAT-entry-FAQ"
---

* [Why use SNAT?](https://docs.byteplus.com/en/docs/51/10042#.5Li65LuA5LmI5L2_55SoU05BVO-8nw==)

* [What is an SNAT connection?](https://docs.byteplus.com/en/docs/51/10042#.5LuA5LmI5pivU05BVOi_nuaOpe-8nw==)

* [Elastic Compute Service with configured SNAT rule cannot access the internet](https://docs.byteplus.com/en/docs/51/10042#.5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw==)

* [How to handle packet loss or connection failure of the Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10042#.5YWs572RTkFU572R5YWz5Lii5YyF5oiW6L-e5o6l5LiN6YCa6K-l5aaC5L2V5aSE55CG77yf)

* [Can multiple SNAT entries share one EIP? Can one SNAT entry be associated with multiple EIPs?](https://docs.byteplus.com/en/docs/51/10042#.5aSa5p2hU05BVOinhOWImeaUr-aMgeWFs-iBlOS4gOS4quWFrOe9kUlQ5ZCX77yf5LiA5p2hU05BVOinhOWImeaUr-aMgeWFs-iBlOWkmuS4quWFrOe9kUlQ5ZCX77yf)

* [What is the bandwidth of the Internet NAT Gateway when Elastic Compute Service accesses the internet? Where to configure?](https://docs.byteplus.com/en/docs/51/10042#.5LqR5pyN5Yqh5Zmo6YCa6L-H5YWs572RTkFU572R5YWz6K6_6Zeu5YWs572R77yM5YWs572RTkFU572R5YWz55qE5bim5a695piv5aSa5bCR77yf5Zyo5ZOq6YeM6K6-572u77yf)

* [What is the relationship and difference between the Internet NAT Gateway subnet and the subnet in SNAT rules?](https://docs.byteplus.com/en/docs/51/10042#.5YWs572RTkFU572R5YWz5a2Q572R5LiOU05BVOinhOWImemHjOeahOWtkOe9keacieS7gOS5iOWFs-iBlOS4juWMuuWIq--8nw==)

* [How to handle occasional failures when accessing remote services through the Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10042#.6YCa6L-H5YWs572RTkFU572R5YWz6K6_6Zeu6L-c56uv5pyN5Yqh5qaC546H5oCn5aSx6LSl6K-l5aaC5L2V5aSE55CG77yf)


<span id=".5Li65LuA5LmI5L2_55SoU05BVO-8nw=="></span>
## Why use SNAT?

When multiple Elastic Compute Service instances need to access the internet, using SNAT rules is recommended.

Compared to assigning a public IP to each Elastic Compute Service instance, SNAT rules offer the following advantages:


* Shared public IP. Multiple Elastic Compute Service instances share one public IP address and bandwidth, reducing internet usage costs.

* Higher security. Using SNAT rules does not expose the IPs of Elastic Compute Service instances, reducing the risk of attacks to some extent.

* Easy to use. SNAT rules can be set as needed. Adding or removing cloud server instances within the corresponding CIDR block does not require modifying SNAT rules.

* High availability. Supports dual\-cluster cold backup and cross\-availability zone disaster recovery to ensure business operation.


<span id=".5LuA5LmI5pivU05BVOi_nuaOpe-8nw=="></span>
## What is an SNAT connection?

A connection is a physical path from client to server. An SNAT connection is defined by five elements: source IP address, source port, destination IP address, destination port, and transport layer protocol. The source IP address and source port refer to the public IP and port after SNAT translation.

The system sets default aging times (TCP: 900 seconds, UDP: 90 seconds), meaning the duration without packet transmission. If an SNAT connection has no packet transmission exceeding the aging time, it automatically disconnects.

When an SNAT rule is associated with a single public IP, the source port of the SNAT connection is randomly assigned by the system.

When an SNAT rule is associated with multiple public IPs, the system randomly assigns the source IP address and source port of the SNAT connection.

<span id=".5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw=="></span>
## Cloud servers configured with SNAT rules cannot access the internet?

Possible causes:


|Cause |Description |
|---|---|
|Route does not exist |Check whether the route table associated with the subnet of the cloud server instance contains a custom route entry with the destination CIDR block 0.0.0.0/0 and the next hop set to the target Internet NAT Gateway instance. If not, add it manually. For proceduer, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH). |
|Security group and network ACL configuration conflict |Check whether related rules of the corresponding security group and network ACL allow access. For more details, see [Network ACL overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) and [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |
|Cloud resource status exception |Check whether the ECS, EIP, and Internet NAT Gateway statuses are normal, such as not expired or suspended due to overdue payments. |
|Associate an EIP |Check whether the cloud server instance is associated with an Elastic IP Address (EIP). EIPs have higher priority than route tables. When an ECS instance is associated with an EIP, its traffic is forwarded through the EIP and cannot use SNAT rules to access the internet. |


<span id=".5YWs572RTkFU572R5YWz5Lii5YyF5oiW6L-e5o6l5LiN6YCa6K-l5aaC5L2V5aSE55CG77yf"></span>
## How to handle internet NAT Gateway packet loss or connection failure?

You can analyze the monitoring data in Cloud Monitor to troubleshoot errors. For more information, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/natgateway/Viewing-monitoring-data-vpcnat).

Possible causes:


* The current specification of the internet NAT Gateway has reached the connection limit. For details, see [Performance](https://docs.byteplus.com/en/docs/natgateway/Specifications) and [Changing specification for Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Changing-the-specification-of-an-Internet-NAT-gateway).

* The bandwidth limit of the public IP associated with the SNAT rule has been reached. For more operations, see [Modifying the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

* The forwarding bandwidth limit of the internet NAT Gateway has reached 5 Gbps. You can create another Internet NAT Gateway in the current VPC. For procedure, see [Creating an Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway).

* Data sent to the Internet NAT Gateway that does not match SNAT/DNAT rules is discarded by the Internet NAT Gateway. This data is reflected in the metric **New Discarded Connection Rate**. You can configure corresponding SNAT/DNAT rules for all outbound and inbound internet traffic. For procedure, see [Managing an SNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules) and [Managing a DNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules).


<span id=".5aSa5p2hU05BVOinhOWImeaUr-aMgeWFs-iBlOS4gOS4quWFrOe9kUlQ5ZCX77yf5LiA5p2hU05BVOinhOWImeaUr-aMgeWFs-iBlOWkmuS4quWFrOe9kUlQ5ZCX77yf"></span>
## Can multiple SNAT entries share one EIP? Can one SNAT entry be associated with multiple EIPs?

Both are yes. Multiple SNAT entries can be associated with the same EIP, and a single SNAT entry can be associated with multiple EIPs.

<span id=".5LqR5pyN5Yqh5Zmo6YCa6L-H5YWs572RTkFU572R5YWz6K6_6Zeu5YWs572R77yM5YWs572RTkFU572R5YWz55qE5bim5a695piv5aSa5bCR77yf5Zyo5ZOq6YeM6K6-572u77yf"></span>
## What is the bandwidth of the Internet NAT Gateway when ECS accesses the internet through it? Where is it set?

The forwarding bandwidth of the Internet NAT Gateway equals the sum of the associated EIP bandwidths, capped at 5Gbps. If the bandwidth exceeds 5Gbps, the forwarding bandwidth of the Internet NAT Gateway is limited.

<span id=".5YWs572RTkFU572R5YWz5a2Q572R5LiOU05BVOinhOWImemHjOeahOWtkOe9keacieS7gOS5iOWFs-iBlOS4juWMuuWIq--8nw=="></span>
## What is the relation and difference between the subnet of an Internet NAT Gateway and the subnet in SNAT rules?

They are unrelated. The specific differences are as follows:


* When creating an Internet NAT Gateway, selecting a subnet causes the system to automatically pick an available private IP address from that subnet to create the Internet NAT Gateway network interface.

* When creating an SNAT rule and selecting a subnet, all cloud servers in that subnet share one EIP through the SNAT rule to access the Internet.


<span id=".6YCa6L-H5YWs572RTkFU572R5YWz6K6_6Zeu6L-c56uv5pyN5Yqh5qaC546H5oCn5aSx6LSl6K-l5aaC5L2V5aSE55CG77yf"></span>
## How to handle occasional failures when accessing remote services through an Internet NAT Gateway?

<span id=".5o6S5p-l5pa55rOV"></span>
### Troubleshooting methods

If a cloud server accessing an Internet server through SNAT encounters TCP connection failures, use the following methods to troubleshoot.


1. Run the following command to check if the remote server has enabled "tcp_tw_recycle."

   `sysctl -a|grep tcp_tw_recycle`

   If tcp_tw_recycle is set to 1, it means it is enabled.

2. Run the following command to check the number of kernel packet losses on the remote server.

   `cat /proc/net/netstat | awk '/TcpExt/ { print $21,$22 }'`

   If the ListenDrops value is not 0, packet loss exists, indicating a network problem.


<span id=".5aSE55CG5pa55rOV"></span>
### Troubleshooting steps

Modify the kernel parameters on the remote server.


* Run the following command to temporarily change the parameter (this setting will be lost after restarting the remote server and must be reapplied).

   `sysctl -w net.ipv4.tcp_tw_recycle=0`

* Method to permanently change the parameter:

   1. Run the following command to edit the "/etc/sysctl.conf" file.

      `vi /etc/sysctl.conf`

      Add the following content to the file:

      `net.ipv4.tcp_tw_recycle=0`

   2. Press the "esc" key on the keyboard and enter  **`:wq!`**  , save and exit the file.

   3. Run the following command to apply the configuration.

      `sysctl -p`
