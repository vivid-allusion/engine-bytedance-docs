---
title: "Read-only node"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Read_only_node_faq"
---

<span id="什么是只读节点？"></span>
### What is read\-only node?

For read\-intensive workloads, you can create multiple read\-only nodes to handle database read requests, reducing load on the primary node.

<span id="一个实例下最多可以创建多少个只读节点？"></span>
### What is the maximum number of read\-only nodes allowed per instance?

Each instance supports a maximum of 1 primary node and up to 15 read\-only nodes.

<span id="支持将已有的只读节点切换为主节点吗？"></span>
### Is it supported to switch an existing read\-only node to a primary node?

Yes. When detecting a primary node failure, the system automatically initiates failover by switching a read\-only node to primary, ensuring rapid recovery and maintaining high availability of the instance. You can also manually switch a read\-only node to primary when business needs require. For procedures, refer to [Switching the primary node](https://www.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node)

<span id="每添加一个只读节点需要多长时间，是否会影响业务？"></span>
### How long does it take to add a read\-only node, and will it affect business availability?

Adding read\-only nodes to existing instances typically completes within minutes. When the instance specification reaches a certain threshold, the proxy will initiate corresponding changes, which may probabilistically trigger a restart during reconfiguration, resulting in brief business interruption. It is recommended to perform such operations during off\-peak hours.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default endpoint automatically routes traffic to newly added read\-only nodes.</div>


* <div data-tips="true" data-tips-type="tip">For custom connection endpoints with <strong>Automatically associate new node</strong> function enabled, newly added read\-only nodes are automatically associated. If disabled, manual association is required. For procedures, refer to <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Modifying endpoint</a>.</div>



<span id="切换主节点需要多长时间，是否会影响业务？"></span>
### How long does it take to switch the primary node, and will it affect business availability?


* Switching the primary node typically completes within 30 to 60 seconds.

* When switching the primary node, 1 to 2 brief disconnections may occur. Ensure your application implements automatic reconnection to minimize business impact.

* Switching the primary node may affect custom endpoint node associations. For details, refer to [Switching the primary node](https://www.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node).
