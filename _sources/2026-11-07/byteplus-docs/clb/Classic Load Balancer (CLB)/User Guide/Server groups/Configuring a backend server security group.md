---
title: "Configuring a backend server security group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group"
---

<span id="JQYlvyTG"></span>
## Scenario notes


|Backend server group type |Does CLB enable the feature to allow the backend security group? |Scenario notes |
|---|---|---|
|Server type |Check |No backend security group configuration is required. Security groups no longer inspect CLB traffic, which is allowed by default to simplify your CLB setup. For more details, refer to Allowing backend security group. |
||Not enabled |You need to configure the security group of the backend server to allow CLB traffic.<br><br><div style="text-align: center"><br></div><br><br><br><div style="text-align: center"><br></div><br> |
|<div style="text-align: center"><br></div><br><br><br>IP type |Check ||
||Not enabled ||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The feature of using IP address as a backend server is currently in Beta. For trial request, please contact your account manager.</div>


<span id=".SVB2NCBDTELlrp7kvovnmoTlkI7nq6_mlL7pgJror7TmmI4="></span>
## Traffic description

Traffic from Classic Load Balancer (CLB) to the backend server is categorized into the following two types:


* Forwarded client traffic.

* Health Check traffic.


Details are as follows:


<Tabs>
<Tab zoneid="SxE8GfdoQU" title="Server Type Backend (IPv4)">
<TabTitle>Server Type Backend (IPv4)</TabTitle>


|**Listener type** |**Request address** ||**Protocol of the request** |**Explanation of inbound traffic allowance for security groups** |
|---|---|---|---|---|
|TCP listener |Client request |Client IPv4 address |TCP |Allow traffic from client IPv4 address using TCP protocol to destination backend server port. |
||Health check request |100.64.0.0/10 |TCP |Allow traffic from source 100.64.0.0/10 using TCP protocol to destination backend server port. |
|UDP listener |Client request |Client IPv4 address |UDP |Allow traffic from client IPv4 address using UDP protocol to destination backend server port. |
||Health check request |100.64.0.0/10 |UDP, ICMP |Allow traffic from source 100.64.0.0/10 using UDP and ICMP protocols to destination backend server port. |
|HTTP/HTTPS Listener |Client request |100.64.0.0/10 |TCP |Allow traffic from source 100.64.0.0/10 using TCP protocol to destination backend server port. |
||Health check request |100.64.0.0/10 |TCP |Allow traffic from source 100.64.0.0/10 using TCP protocol to destination backend server port. |





</Tab>
<Tab zoneid="jcCSoBAY4t" title="IP Type Backend (IPv4)">
<TabTitle>IP Type Backend (IPv4)</TabTitle>


|**Listener type** |**Request address** ||**Allow protocol** |**Description of security group inbound traffic allowance** |
|---|---|---|---|---|
|TCP/HTTP/HTTPS Listener |client request |100.64.0.0/10 |TCP |Allow traffic from source 100.64.0.0/10 using TCP protocol to destination backend server port. |
||Health check request |100.64.0.0/10 |TCP |Allow traffic from source 100.64.0.0/10 using TCP protocol to destination backend server port. |
|UDP |Client request |100.64.0.0/10 |UDP |Allow traffic from source 100.64.0.0/10 using UDP protocol to destination backend server port. |
||Health check request |100.64.0.0/10 |UDP, ICMP |Allow traffic from source 100.64.0.0/10 using UDP and ICMP protocols to destination backend server port. |





</Tab>
<Tab zoneid="mqD6LyEfuj" title="Server Type Backend (IPv6)">
<TabTitle>Server Type Backend (IPv6)</TabTitle>


|**Listener type** |**Request address** ||**Allow protocol** |**Security group inbound traffic allowance description** |
|---|---|---|---|---|
|TCP listener |Client request |* IPv4 request: fd00:64::/32<br><br>* IPv6 request: client IPv6 address |TCP |Allow traffic from source fd00:64::/32 and client IPv6 address using TCP protocol to destination backend server port. |
||Health check request |fd00:64::/32 |TCP |Allow traffic from source fd00:64::/32 using TCP protocol to destination backend server port. |
|UDP listener |Client request |* IPv4 request: fd00:64::/32<br><br>* IPv6 request: client IPv6 address |UDP |Allow traffic from source fd00:64::/32 and client IPv6 address using UDP protocol to destination backend server port. |
||Health check request |fd00:64::/32 |UDP, ICMPv6 |Allow traffic from source fd00:64::/32 using UDP and ICMPv6 protocols to destination backend server port. |





</Tab>
</Tabs>


<span id=".6YWN572u56S65L6L"></span>
## Configuration examples

Using backend server port 80 as an example, this section describes how to configure security group access rules for different types of listeners and backend servers. For detailed configuration steps, please refer to Adding a security group rule or call the AuthorizeSecurityGroupIngress API.


<Tabs>
<Tab zoneid="fadMdAU8ej" title="Server Type Backend (IPv4 only)">
<TabTitle>Server Type Backend (IPv4 only)</TabTitle>

* TCP listener:

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |Client address |Receive IPv4 client requests forwarded by the CLB |
   |2 |Allow |TCP |80 |100.64.0.0/10 |Receive health check requests and IPv6 client requests forwarded by CLB |
   

* UDP listener:

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |UDP |80 |Client address |Receive IPv4 client requests forwarded by the CLB |
   |2 |Allow |UDP |80 |100.64.0.0/10 |Receive Health Check requests and CLB forwarded IPv6 client requests |
   |3 |Allow |ICMP |ALL |100.64.0.0/10 |Receive health check request |
   

* HTTP/HTTPS listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |100.64.0.0/10 |Receive health check requests and IPv4/IPv6 client requests forwarded by CLB |
   





</Tab>
<Tab zoneid="PjiTVSaMyC" title="Server Type Backend (IPv6 only)">
<TabTitle>Server Type Backend (IPv6 only)</TabTitle>

* TCP listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |Client address |Receive IPv6 client requests forwarded by CLB |
   |2 |Allow |TCP |80 |fd00:64::/32 |Receive health check requests and CLB\-forwarded IPv4 client requests |
   



&nbsp;

* UDP Listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |UDP |80 |client address |Receive IPv6 client requests forwarded by CLB |
   |2 |Allow |UDP |80 |fd00:64::/32 |Receive health check requests and IPv4 client requests forwarded by the CLB |
   |3 |Allow |ICMPV6 |ALL |fd00:64::/32 |Receive health check request |
   





</Tab>
<Tab zoneid="nE12CXoZDc" title="Server Type Backend (IPv4 and IPv6)">
<TabTitle>Server Type Backend (IPv4 and IPv6)</TabTitle>

IPv4 & IPv6 indicate Elastic Compute Service (ECS) joined to both the IPv4 and IPv6 backend server groups simultaneously.


* TCP Listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |Client address |Receive IPv4/IPv6 client requests forwarded by the CLB |
   |2 |Allow |TCP |80 |100.64.0.0/10 |IPv4 backend server receives health check request |
   |3 |Allow |TCP |80 |fd00:64::/32 |IPv6 backend server receives Health Check request |
   

* UDP Listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |UDP |80 |Client address |Receive IPv4/IPv6 client requests forwarded by CLB |
   |2 |Allow |UDP |80 |100.64.0.0/10 |IPv4 backend server receives health check request |
   |3 |Allow |ICMP |ALL |100.64.0.0/10 |IPv4 backend server receives Health Check requests |
   |2 |Allow |UDP |80 |fd00:64::/32 |IPv6 backend server receives health check requests |
   |3 |Allow |ICMPV6 |ALL |fd00:64::/32 |IPv6 backend server receives health check requests |
   



&nbsp;

* HTTP/HTTPS Listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |100.64.0.0/10 |IPv4 backend server receives health check requests and IPv4/IPv6 client requests forwarded by CLB |
   





</Tab>
<Tab zoneid="MnmjSNnDQF" title="IP Type Backend (IPv4 only)">
<TabTitle>IP Type Backend (IPv4 only)</TabTitle>

* TCP/HTTP/HTTPS listener

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |80 |100.64.0.0/10 |Receive health check request, CLB forwards IPv4/IPv6 client requests |
   

* UDP listener:

   
   |**No.**  |**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
   |---|---|---|---|---|---|
   |1 |Allow |UDP |80 |100.64.0.0/10 |Receives health check requests and IPv4/IPv6 client requests forwarded by CLB |
   |2 |Allow |ICMP |ALL |100.64.0.0/10 |Receive health check request |
   





</Tab>
</Tabs>
