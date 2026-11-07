---
title: "Load balancing"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing"
---

NDB for MySQL currently uses a load balancing strategy based on active requests to ensure load balancing between multiple read\-only nodes.

<span id=".5Z-65LqO5rS76LeD6K-35rGC5pWw6LSf6L295Z2H6KGh"></span>
## Based on active request load balancing

When the primary node accepts read requests, Round\-Robin mode load balancing is in read\-write mode. All read requests sent from a database agent are sent to the primary node and read\-only nodes in a round\-robin manner. However, in actual business, load traffic often appears in a mixed form (such as 50 write requests and 100 read requests). Based on the Round\-Robin mode, the traffic borne by the primary node is "50 write requests + 50 read requests", and the traffic borne by the read\-only node is "50 read requests". The primary node has to bear not only write requests but also read requests, which leads to greater pressure on the primary node and lower resource utilization of the read\-only node.

To solve the problems in the Round\-Robin mode and improve the utilization of read\-only nodes, NDB for MySQL introduces a load balancing strategy based on the number of active requests.

Through the load balancing strategy based on the number of active requests, in the above example, the traffic that the primary node needs to bear is "50 write requests + 25 read requests", and the traffic that the read\-only node needs to bear is "75 read requests". It can effectively reduce the pressure on the primary node, improve the resource utilization of read\-only nodes, and improve overall performance.

<span id=".5Li76IqC54K55piv5ZCm5o6l5Y-X6K-7"></span>
## Whether the primary node accepts read requests

When the connection endpoint is a read\-write endpoint, you can choose to enable or disable the primary node to accept read requests. When the primary node is read request acceptance function is disabled, the primary node only accepts transactional read requests, and non\-transactional read requests are not sent to the primary node. However, when all read\-only nodes are unavailable, the request is still routed to the master node.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The function of accepting read requests by the primary node of the default terminal is enabled by default. To disable it, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Editing connection endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip">Enabling or disabling the primary node accepts read requests function takes effect immediately for all connections.</div>
