---
title: "Connection persistence"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_persistence"
---

To ensure the availability and stability of database connections during maintenance operations (such as active/standby switching, configuration changes, etc.), NDB for MySQL provides a connection persistence function. This feature ensures that connections are not actively disconnected during operation, thus enhancing the stability of the business system.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Connection persistence is currently invite\-only features. If you need to use it, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5Y6f55CG5LuL57uN"></span>
## Principle introduction


* **Switch to primary node**

   In planned primary node switching scenarios, such as upgrading or downgrading configurations, manual master/slave switching, and changing instance versions, the database proxy will suspend routing connection requests to the old primary node while the old primary node is switching to the new primary node. If the write capability of the new primary node is restored within 30 seconds, the connection from the database proxy to the new primary node will be reestablished, and the connection status (such as character set encoding, user variables) will remain consistent with that before the primary node switch. The suspended requests will be routed to the new primary node. During this process, the application connection will not be disconnected or an error will be reported. If the new primary node fails to restore write capability within 30 seconds, the database proxy then terminates the connection to the application.

* **Read\-only node offline**

   When reducing the number of read\-only nodes or changing the specifications of read\-only nodes, the database proxy will not route new requests to the read\-only node after it senses that the read\-only node is offline. Requests being executed on read\-only nodes need to be completed within 20 seconds, otherwise the connection will report an error.

* **Database proxy configuration changes**

   When changing the instance node specifications or the number of read\-only nodes, the database proxy will automatically adjust its own specifications and number of replicas according to certain rules. By retaining the old database proxy replica, it ensures that the existing connection will not be disconnected immediately, and the new connection will be routed to the new database proxy replica.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitations

In some scenarios, the connection cannot be maintained. In the case where the connection cannot be maintained, the connection will be disconnected during the operation and maintenance operation, as follows:


* Binlog transport exists.

* Use the LOAD DATA statement on the connection.

* A temporary table exists.

* There are transactions that have not been committed for a long time. After the connection is disconnected, the uncommitted transactions are rolled back.

* Large SQL queries (including queries returning results and queries in progress) that fails to complete execution within the backoff wait time.


In addition, for some special scenarios, the connection will not be disconnected when performing operation and maintenance operations, but it will cause information loss. For example, if there is warning information in the last execution result, the connection can be maintained in this scenario, but the `show warnings` result may be empty.

<span id="dlX3y45q"></span>
## Change scene

When changing the instance configuration, the connection persistence status and change impact are shown in the following table:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Connections may fail to be maintained when repeatedly making configuration changes or upgrading instance versions.</div>


* <div data-tips="true" data-tips-type="warning">After enabling connection persistence, the time required for operations such as switching to the primary node and modifying the configuration may be slightly extended.</div>




|Change scene |Connection persistence |Whether QPS drops to zero |Impact of enabling connection persistence |Impact of not enabling connection persistence |
|---|---|---|---|---|
|Reduce the number of read\-only nodes<br><br> |Yes |No |Maintain the connection within the cool\-off period (24 hours) of the database proxy configuration change. After the cool\-off period, the database connection may be temporarily disconnected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The cool\-off period for database proxy configuration changes means that after the proxy configuration is changed, the system will enter a buffer period, during which the new configuration will not be applied immediately, but will wait for a period of time to ensure the stability of the change and business continuity. This mechanism is mainly used to avoid connection interruptions or performance fluctuations caused by frequent changes.</div><br> |During the configuration change, the database connection may be temporarily disconnected. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism.<br><br> |
|Increase the number of read\-only nodes |Yes |No<br><br> |Maintain the connection within the cool\-off period (24 hours) of the database proxy configuration change. After the cool\-off period, the database connection may be temporarily disconnected. |During the configuration change, the database connection may be temporarily disconnected. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism. |
|Upgrade node specification |Yes |Yes, duration < 30s |Maintain the connection within the cool\-off period (24 hours) of the database proxy configuration change. After the cool\-off period, the database connection may be temporarily disconnected. |During the configuration change, the database connection may be temporarily disconnected. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism. |
|Reduce node specifications |Yes |Yes, duration < 30s |Maintain the connection within the cool\-off period (24 hours) of the database proxy configuration change. After the cool\-off period, the database connection may be temporarily disconnected. |During the configuration change, the database connection may be temporarily disconnected. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism. |
|Restarting instances<br><br> |No |Yes, duration < 30s<br><br> |Instance restart will cause connection interruptions. Schedule businesses accordingly before restarting. We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism. |Instance restart will cause connection interruptions. Schedule businesses accordingly before restarting. We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism. |
|Manually switch the primary node<br><br> |Yes |Yes, duration < 30s<br><br> |The connection is normal, but the write request will be blocked for 10s~30s.<br><br> |When switching the primary node, 1 to 2 brief disconnections may occur. Ensure your application implements automatic reconnection to minimize business impact. |
|Upgrade instance version |Yes |Yes, duration < 30s |The connection is normal, but the write request will be blocked for 10s~30s. |During the instance version upgrade, 1 to 2 brief disconnections may occur. Ensure your application implements automatic reconnection to minimize business impact. |


<span id="KyIIqiNv"></span>
## Connection address

The support for connection persistence by different types of connection addresses is as follows:


|Connection address type |Whether to support connection persistence |
|---|---|
|Primary node address |Support |
|Default address |Support |
|custom read/write address |Support |
|Custom read\-only address |Support<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a custom read\-only end point is associated with only one read\-only node, connection retention is not supported.</div><br> |


<span id="l0sXAaWh"></span>
## Enabling or disabling connection persistence


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the **Summary** page, in the **Configuration** section, click **Enable** or **Disable** next to **Connection persistence**.

5. In the dialog box that appears, confirm the impact of enabling or disabling connection persistence on the instance, and click **OK**.


<span id="aco8SdlW"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[ModifyConnectionPersistence](https://docs.volcengine.com/docs/6357/2582727) |Call the ModifyConnectionPersistence API to enable or disable connection persistence for the instance. |
