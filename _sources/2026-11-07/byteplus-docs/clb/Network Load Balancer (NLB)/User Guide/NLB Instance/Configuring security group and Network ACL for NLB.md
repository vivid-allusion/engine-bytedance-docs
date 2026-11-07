---
title: "Configuring security group and Network ACL for NLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

To ensure that the NLB instance functions properly, both the **NLB instance and backend server** must have security groups and Network ACs to allow necessary traffic. This article explains how to allow the necessary traffic for the NLB instance's security group and Network Access Control List.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24784dc3e4480185429690275f70823b.png) </span>

For allowing traffic in the backend server's security group and Network Access Control List, please refer to [Configuring the backend server's security group and Network Access Control List](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).

<span id=".6YWN572u6K-05piO"></span>
## Precautions

The requirements for allowing traffic in the security group and Network Access Control List associated with the NLB instance are as follows:


|Instance IAM ||Traffic Allowance Configuration Guide |
|---|---|---|
|Security group  ||* Ingress:<br><br>   * Client access request: Traffic from the client IP address based on the listening protocol and the listening port.<br><br>   * **Traffic used by the system to detect the availability of the NLB private IP address:** <br><br>      * ICMP protocol traffic from `100.64.0.0/10` CIDR block<br><br>      * ICMPv6 protocol traffic from `fd00:64::/32` CIDR block<br><br>* Egress:<br><br>   * Traffic for NLB forwarding access requests: IP address of the backend server based on the server group protocol and server port<br><br>   * Health check: Traffic for the backend server private IP address based on the health check protocol and health check port |
|Network ACL |NLB instances and backend servers belong to same subnets |* Client access request: Client IP address traffic based on listening protocol and listening port<br><br>* Forward access request: No configuration required.<br><br>* Health check: No configuration required.<br><br>* Traffic used by the system to detect the availability of the NLB private IP address:<br><br>   * ICMP protocol traffic from `100.64.0.0/10` CIDR block<br><br>   * ICMPv6 protocol traffic from `fd00:64::/32` CIDR block |
||NLB instances and backend servers belong to different subnets |* Client access request: Client IP address traffic based on listening protocol and listening port<br><br>* Forward access requests: Traffic of the backend server private IPv4 address based on the listening protocol and backend server port<br><br>* Health check: Traffic for the backend server private IP address based on the health check protocol and health check port<br><br>* Traffic used by the system to detect the availability of the NLB private IP address:<br><br>   * ICMP protocol traffic from `100.64.0.0/10` CIDR block<br><br>   * ICMPv6 protocol traffic from `fd00:64::/32` CIDR block |


<span id=".6YWN572u56S65L6L"></span>
## Configuration examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For IPv4 NLB instances, no IPv6 traffic allowance rules are required as below.</div>


<span id=".5a6J5YWo57uE"></span>
### Security group 


* Only allow specific IP addresses to access NLB

   
   |Direction |Priority |Policy  |Protocol Type |Port range |Source or Destination Address |Description |
   |---|---|---|---|---|---|---|
   |<div style="text-align: center"><br>Inbound</div><br> |1 |Allow  |ALL |Listening port |Client IP address |Allow client access traffic |
   ||1 |Allow  |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
   ||1 |Allow  |ICMPV6 |ALL |fd00:64::/32 |Allow the traffic probing the availability of the private IPv6 address of the NLB instance |
   ||100 |Reject |ALL |ALL |0.0.0.0/0 |Deny\-all fallback policy |
   |Outbound |100 |Allow  |ALL |ALL |0.0.0.0/0 |Deny\-all fallback policy |
   

* Reject specific IP addresses from accessing NLB

   
   |Direction |Priority |Policy  |Protocol Type |Port range |SourceAddress |Description |
   |---|---|---|---|---|---|---|
   |Inbound |1 |Reject |ALL |Listening port |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
   


<span id=".572R57ucQUNM"></span>
### Network ACL


|Backend server and NLB's subnet  |Rule direction |Priority |Policy  |Term |Source or Destination Address |Destination port |Description |
|---|---|---|---|---|---|---|---|
|Same |Inbound |1 |Allow  |Protocol of listeners |Client IP address |Listening port |Allow client access traffic |
|||2 |Allow  |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
|||3 |Allow  |ICMPV6 |fd00:64::/32 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv6 address |
||Outbound |1 |Allow  |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
|||2 |Allow  |ALL |::/0 |ALL |Allows all IPv6 traffic. |
|Different |Inbound |1 |Allow  |Protocol of listeners |Client IP address |Listening port |Allow client access traffic |
|||2 |Allow  |Health check protocol |Backend server private IP address |Health check port number |Allow the health check response traffic from backend server to the NLB |
|||3 |Allow  |Protocol of listeners |Backend server private IP address |Port number of the server |Allow the client's response traffic from backend server to the NLB |
|||4 |Allow  |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
|||5 |Allow  |ICMPV6 |fd00:64::/32 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv6 address |
||Outbound |1 |Allow  |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
|||2 |Allow  |ALL |::/0 |ALL |Allows all IPv6 traffic. |
