---
title: "About connection endpoint"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/About_connection_endpoint"
---

The connection endpoint is a network proxy service located between the database and the application. It is used to proxy all requests when the application accesses the database. It has the characteristics of high availability, high performance, maintainability, and ease of use.

<span id="wrPNlYS3"></span>
## Connection endpoint type

A connection endpoint corresponds to a connection address, back\-end routing mappings, and related routing configurations. By selecting different connection endpoints, you can flexibly meet the traffic routing needs of different business scenarios. The following table shows basic information about different types of connection endpoints.


|**Endpoint type** |**Primary node endpoint** |**Default endpoint** |Custom **endpoint** ||
|---|---|---|---|---|
||||**Custom read/write endpoint** |**Custom read\-only endpoint** |
|Creation method |Created by default when creating an instance |Created by default when creating an instance |Create manually |Create manually |
|Read/write type |Read/Write |Read/Write separation |Read\-write or read\-write separation |read\-only |
|Whether to support deletion |Not supported |Not supported |Support |Support |
|Number of endpoints |1 |1 |An instance supports the creation of up to 5 custom connection endpoints. ||
|Optional configurations<br><br> |[Primary node accepts read requests](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing#.5Li76IqC54K55piv5ZCm5o6l5Y-X6K-7) is enabled by default and cannot be disabled. |* [Load balancing](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing)<br><br>* [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting)<br><br>* [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels)<br><br>* [Primary node accepts read requests](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing#.5Li76IqC54K55piv5ZCm5o6l5Y-X6K-7) |* [Load balancing](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing)<br><br>* [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting)<br><br>* [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels)<br><br>* [Primary node accepts read requests](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing#.5Li76IqC54K55piv5ZCm5o6l5Y-X6K-7)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Same as the primary node endpoint when connecting to the primary node only.</div><br> |Not supported |
|Description |Connect to the primary node. Request for proxy access to the primary node. |Connect the primary node and all read\-only nodes for proxy access requests to the primary and read\-only nodes.<br><br>When modifying, you can cancel the association of the newly added read\-only node with the default endpoint. |* Connect only the primary node.<br><br>   When a custom read/write endpoint is associated with only the primary node, read/write separation is not supported.<br><br>   * Connect the primary node to at least one read\-only node. |Connect read\-only nodes. Read\-only endpoints should be connected to at least one read\-only node. To ensure service availability, it is recommended to connect two or more nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When a custom read\-only endpoint is associated with only one node. If a master\-slave switch occurs due to a primary node failure, and the node under the read\-only endpoint becomes the new primary node, the old primary node has not recovered, traffic is not forwarded, and the read\-only endpoint address is unavailable. For more information, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node">Switching the primary node</a>.</div><br> |


<span id="Pbcn3Vcl"></span>
## Connection endpoint use cases

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a2cb5de547eec8801c2a7e71a82e807.png) </span>


* **Use connection endpoints for resource isolation**: You can use connection endpoints to vertically isolate resources when multiple read\-only nodes exist. For example, an instance has 1 primary node and 4 read\-only nodes. The primary node and 2 read\-only nodes serve online services, while the remaining 2 read\-only nodes serve offline analysis services.

* **Create different endpoints to meet varying business requirements**: Different services have varying requirements for consistency, transaction splitting, and timeouts. You can create different endpoints to accommodate these needs.
