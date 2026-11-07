---
title: "Overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/host_group_overview"
---

A host group is a virtual configuration unit in Torch Log Service (TLS), and a host group contains multiple hosts. TLS issues collection rules to LogCollectors by host group. Then, LogCollectors installed on the servers in the same group collects based on the collection rule associated.

In TLS, a host group is a virtual group for managing the servers from which you want to collect logs. You must add all servers from which you want to use LogCollector to collect logs to host groups. This allows you to create and manage collection rules in a unified manner. If an application or service is deployed on multiple hosts and the paths of log files on the hosts are the same, you can add the hosts to the same host group. This way, a log collection rule that you configure in the console is applied to all hosts in the host group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS supports adding IPv4 and IPv6 servers in the host groups.</div>


<span id="限制说明"></span>
## Limits


* A BytePlus account can have up to 200 host groups in a Region.

* Only Linux servers can be used as hosts of LogCollector.


<span id="机器组类型"></span>
## Types

In TLS, host groups are classified into two types: IP address\-based type and label\-based type.

<span id="ip-地址"></span>
### IP address\-based host group

For an IP address\-based host group, TLS identifies hosts in the group by IP addresses. After you create an IP address\-based host group, enter the IP addresses of servers to add the servers to the host group as hosts. TLS collects logs from the servers with the IP addresses.

IP address\-based host groups are suitable for scenarios where a small number of servers are used. In these scenarios, you can get the IP addresses of servers and add the IP addresses to a host group in a simple manner.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use a BytePlus Elastic Compute Service (ECS) instance as a host, you can add the private IP address of the ECS instance to an IP address\-based host group.</div>


* <div data-tips="true" data-tips-type="tip">If the ECS instance is associated with a host name or the network type of the ECS instance has been changed, you must add the IP address reported by LogCollector to a host group. The IP address is recorded in the <code>ip</code> field in the <code>agent_info.json</code> file of the server. For more information on how to view the IP address of a host, refer to step 1 in <a href="https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group">Create an IP address\-based host group</a>.</div>



<span id="机器标识"></span>
### Label\-based host group

For a label\-based host group, TLS uses the specified custom label to determine whether a host belongs to the host group.

Compared with IP address\-based host groups, label\-based host groups have the following advantages:


* Label\-based host groups can be dynamically scaled and are suitable for scenarios where a large number of servers are used. Assume that a system application includes multiple modules and the host group of each module is identified by a label. To scale up the host group of a module, attach the label of the host group to the new servers that you want to add to the host group.

* Using label\-based host groups can avoid the effect of private IP address conflicts. In a custom network environment such as a virtual private cloud (VPC), the IP addresses assigned to multiple servers may conflict. In this case, you can use host labels to distinguish the servers.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you collect logs from a container, we recommend that you use a label\-based host group. This prevents heartbeat failures when the IP address of the container is changed after the container is restarted.</div>
