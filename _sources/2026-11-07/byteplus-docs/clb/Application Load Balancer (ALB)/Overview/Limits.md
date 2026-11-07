---
title: "Limits"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Limits"
---

This topic introduces the default quota limits for resources related to Application Load Balancer (ALB).

For the quota items adjustable in the table below, if the default quotas are insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to request an increase.

<span id="A5lt2WGh"></span>
## ALB resource quotas


* **Standard Edition Exclusive**

   
   |Quota parameter |Description |Maximum |Support adjustment |Adjustable quota limit |
   |---|---|---|---|---|
   |ListenerPerInstanceForStandard |Number of listeners that can be created for a single ALB instance |50 |Yes |100 |
   |ServerPerInstanceForStandard |Number of backend servers that can be added to a server group |500 |Yes |1000 |
   |RulePerInstanceForStandard |Number of forwarding rules that can be created for a single ALB instance<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Forwarding rules here refer only to custom rules, excluding the default forwarding rule.</div><br> |50 |Yes |100 |
   |AclPerListenerForStandard |Number of Access Control Policies that can be bound to a single listener |5 |No |\-\- |
   |SniDomainPerListenerForStandard |Number of additional domains supported by a single listener. |20 |Yes |40 |
   

* **Basic Edition Exclusive**

   
   |Quota parameter |Description |Maximum |Support adjustment |Adjustable quota limit |
   |---|---|---|---|---|
   |ListenerPerInstance |Number of listeners that can be created for a single ALB instance |50 |Yes |100 |
   |ServerPerInstance |Number of backend servers that can be added to a server group |500 |Yes |1000 |
   |RulePerInstance |Number of forwarding rules that can be created for a single ALB instance<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Forwarding rules here refer only to custom rules, excluding the default forwarding rule.</div><br> |50 |Yes |100 |
   |AclPerListener |Number of Access Control Policies that can be bound to a single listener |5 |No |\-\- |
   |SniDomainPerListener |Number of additional domains supported by a single listener. |20 |Yes |40 |
   

* **Shared by Standard and Basic Editions**

   
   |**Resource category** |Quota parameter |**Description** |Maximum |**Support adjustment** |Adjustable quota limit |
   |---|---|---|---|---|---|
   |Instance |InstancePerRegion |Number of ALB instances that can be created per account per region |50 |Yes |100 |
   |&nbsp;<br><br>Listener |ListenerPerAcl |Number of listeners that can be bound to a single access control policy group |50 |No |\-\- |
   ||ListenerPerCustomizedCfg |Number of listeners that a single custom configuration policy can be bound to |10 |Yes |20 |
   |&nbsp;<br><br>Server Group |ServerGroupPerRegion |Number of server groups supported per account per region. |50 |Yes |100 |
   ||ServerPerGroup |Number of backend servers that can be added to a single server group |200 |Yes |300 |
   ||None |Number of backend servers supported for addition to a single server group in one operation |20 |No |\-\- |
   |&nbsp;<br><br>Forwarding rules |RulePerGroup |Number of forwarding rules a single server group can be associated with |50 |Yes |100 |
   ||none |Number of matching condition values that can be added in a single forwarding rule |N/A |No |\-\- |
   |Extended certificate |None |Number of extended certificates that can be added to a single listener |20 |No |\-\- |
   |&nbsp;<br><br>Certificate |CertPerRegion |Number of server certificates that can be uploaded per account per region |100 |Yes |200 |
   ||CACertPerRegion |Number of CA certificates that can be uploaded per account per region |100 |Yes |200 |
   |Health check template |HealthCheckTempPerRegion |Number of health check templates that can be created per account per region |50 |Yes |100 |
   |&nbsp;<br><br>Access control |AclPerRegion |Number of access control policy groups that can be created per account per region |200 |No |\-\- |
   ||IPPerAcl |Number of IP entries that can be added to a single access control policy group |300 |No |\-\- |
   |Custom configuration |CustomizedCfgPerRegion |Number of custom configuration policies that can be created per account per region |50 |Yes |100 |
   


<span id="dc5e7c06"></span>
## Other related resource quotas


|**Resource category** |**Description** |
|---|---|
|VPC |For quota limits of VPCs, see [Limits](https://docs.byteplus.com/en/docs/vpc/Limits). |
|Elastic IP Address |For quota limits of EIPs, see [Limits](https://docs.byteplus.com/en/docs/eip/Limits). |
|Bandwidth Package |For quota limits of Bandwidth Packages, see [Limits](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits). |


<span id="2879d2ce"></span>
## Capabilities available to allowlist users only


|Category |The following capabilities are available to allowlisted users only. |
|---|---|
|EIP |* Bind an EIP of the default Security Protection type to a public ALB instance.<br><br>* Bind an EIP of the Enhanced Security Protection type to a public ALB instance.<br><br>* Adjust the bandwidth cap of an EIP (the current cap for regular users is 200 Mbps). |
|ALB instance |Create IPv4&IPv6 dual\-stack instances. |
|ALB Listeners |Create QUIC listeners. |
|ALB server group |Use an IP\-type server group when creating a server group. |
|ALB forwarding rules |* Configure [rewrite forwarding rules].<br><br>* Enable the QPS rate limiting feature when configuring forwarding rules.<br><br>* Use regular expressions when configuring forwarding rules. |
|ALB custom configuration |* Configure custom request headers.<br><br>* Enable TLS 1.3 protocol. |
