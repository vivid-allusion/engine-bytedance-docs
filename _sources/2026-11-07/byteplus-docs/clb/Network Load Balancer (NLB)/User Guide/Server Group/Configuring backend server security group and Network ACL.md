---
title: "Configuring backend server security group and Network ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

If the NLB instance needs to function properly, both the **NLB instance and backend server** security group and Network ACLs must allow the relevant traffic. This article introduces how to allow relevant traffic for backend server security groups and Network ACLs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24784dc3e4480185429690275f70823b.png) </span>

For allowing relevant traffic in the NLB instance's security group and Network ACL, refer to [Configuring the NLB security group and Network ACL](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB).

<span id=".5rWB6YeP6K-05piO"></span>
## Traffic Description


|Security group and Network ACL |Condition |Client address |Traffic Allowance Guide |
|---|---|---|---|
|Security group  |Enable traffic allowance for backend security groups |\- |The security group of the backend server does not verify the traffic sent from NLB instances to the backend server, which is allowed by default. Therefore, no security group configuration is required. |
||Disable traffic allowance for backend security groups |Enable client IP address preservation |The source address for client requests is the client IP, while health check requests originate from the NLB's LIP address (from the CIDR block of the subnet where the NLB instance resides). Therefore, the following must be allowed:<br><br><br>* **Client Access Traffic**: Traffic from the client IP address based on listener protocol and backend server port.<br><br>* **Health Check Traffic**: Traffic from all subnets of the NLB instance, based on the health check protocol and health check port |
|||Disable Client IP Preservation |The source addresses of client requests and health check requests are all LIP addresses of the NLB (from the CIDR block of the subnet where NLB instance resides). Therefore, the following must be allowed:<br><br><br>* **Client Access Traffic**: Traffic from all subnets of the NLB instance, based on the listening protocol and backend server port<br><br>* **Health Check Traffic**: Traffic from all subnets of the NLB instance, based on the health check protocol and health check port |
|Network ACL |Same subnet |\- |Traffic does not pass through the Network Access Control List attached to the backend server's subnet, so no configuration is required. |
||Different subnets |Enable client IP address preservation |The source address for client requests is the client IP, while health check requests originate from the NLB's LIP address (from the CIDR block of the subnet where the NLB instance resides). Therefore, the following must be allowed:<br><br><br>* **Client Access Traffic**: Traffic from the client IP address based on listener protocol and backend server port.<br><br>* **Health Check Traffic**: Traffic from all subnets of the NLB instance, based on the health check protocol and health check port |
|||Disable Client IP Preservation |The source addresses of client requests and health check requests are all LIP addresses of the NLB (from the CIDR block of the subnet where NLB instance resides). Therefore, the following must be allowed:<br><br><br>* **Client Access Traffic**: Traffic from all subnets of the NLB instance, based on the listening protocol and backend server port<br><br>* **Health Check Traffic**: Traffic from all subnets of the NLB instance, based on the health check protocol and health check port |


&nbsp;

<span id=".5a6J5YWo57uE77yI5LuF5YWl5pa55ZCR6KeE5YiZ44CB5Ye65pa55ZCR6KeE5YiZ5peg6ZyA6YWN572u77yJ"></span>
### Security group (only inbound rules, outbound rules do not require configuration)


|Allowing backend security group |Client IP Preservation |Priority |Policy  |Protocol Type |Port range |SourceAddress |Description |
|---|---|---|---|---|---|---|---|
|Enable  |\-\- |**The security group of the backend server does not verify the traffic sent from NLB instances to the backend server, which is allowed by default. Therefore, no security group configuration is required.**  ||||||
|Disabled |Enable  |1 |Allow  |Protocol of listeners |The port where the server provides services |Client IP address |Allow client access traffic |
|||1 |Allow  |Health check protocol |Health check port number |CIDR block of the subnet where the NLB instance resides. It is recommended to reference [the Security groups associated with NLB instances](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) |Allow NLB health check traffic |
||Disable |1 |Allow  |Protocol of listeners |The port where the server provides services |CIDR block of the subnet where the NLB instance resides. It is recommended to reference [the Security groups associated with NLB instances](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) |Allow client access traffic |
|||1 |Allow  |Health check protocol |Health check port number ||Allow NLB health check traffic |


<span id=".572R57ucQUNM"></span>
### Network ACL


|Backend server and NLB's subnet  |Client IP Preservation |Rule direction |Priority |Policy  |Term |Source or Destination Address |Destination port |Description |
|---|---|---|---|---|---|---|---|---|
|Same |\-\- |**Traffic does not pass through the Network Access Control List attached to the backend server's subnet, so no configuration is required.**  |||||||
|Different |Enable  |Inbound |1 |Allow  |Protocol of listeners |Source Address: Client IP address |The port where the server provides services |Allow client access traffic |
|||Inbound |1 |Allow  |Health check protocol |Source address: CIDR block of the subnet where the NLB instance resides. |Health check port number |Allow NLB health check traffic |
|||Outbound |1 |Allow  |ALL |Destination Address: 0.0.0.0/0 |ALL |Allow all traffic |
||Disable |Inbound |1 |Allow  |Protocol of listeners |Source address: CIDR block of the subnet where the NLB instance resides. |The port where the server provides services |Allow client access traffic |
|||Inbound |1 |Allow  |Health check protocol ||Health check port number |Allow NLB health check traffic |
|||Outbound |1 |Allow  |ALL |Destination Address: 0.0.0.0/0 |ALL |Allow all traffic |


&nbsp;
