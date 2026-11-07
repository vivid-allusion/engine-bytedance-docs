---
title: "Editing connection endpoints"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints"
---

The primary node endpoint, default endpoint and custom endpoint all support editing. This article introduces the operation steps of editing the connection endpoint.

<span id=".5Y-Y5pu06K-05piO"></span>
## Change description

Different types of endpoints support different items for modification. See the table below for details.


|Feature |Default_endpoint |Primary node endpoint |Custom read/write endpoint |Custom read\-only endpoint |
|---|---|---|---|---|
|**Enabling or disabling public network access** |Support |Support |Support |Support |
|**Enabling or disabling public network resolution** |Support |Support |Support |Support |
|**Modifying address prefix and port** |Support |Support |Support |Support |
|**Set read/write mode** |Not supported |Not supported |Support |Support |
|**Modify endpoint name** |Support |Support |Support |Support |
|**Adjust the consistency level** |Support |Not supported |Support |Not supported |
|**Set timeout** |Support |Not supported |Support |Not supported |
|**Set timeout policy** |Support |Not supported |Support |Not supported |
|**Set primary node accepts read requests** |Support |Not supported |Support |Not supported |
|**Set up transaction splitting** |Support |Not supported |Support |Not supported |
|**Configure connection pool** |Support |Not supported |Support |Not supported |
|**Adjust the associated node** |Support |Not supported |Support |Support |
|**Set up automatically add new node** |Support |Not supported |Support |Support |



* The read/write modes of the primary node endpoint and the default endpoint are both read/write, and modification is not allowed.

* The **Primary node accepts read requests** function of the primary node endpoint is enabled by default and cannot be disabled.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Switching the primary node may affect custom endpoint node associations. For details, refer to [Switching the primary node](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node#.5rOo5oSP5LqL6aG5).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Edit** in the destination endpoint area.

6. On the **Modify endpoint** page, you can make the following modifications to the endpoint.

   
   |Classification |Configuration item |**Description** |
   |---|---|---|
   |**Connection information** |Enabling or disabling public network access |For detailed instructions, please refer to [Enabling or disabling public network access](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_access). |
   ||Enabling or disabling public network resolution |For detailed instructions, please refer to [Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_resolution). |
   ||Modifying address prefix and port |For more details, see [Modifying address prefix and port](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port). |
   |**Endpoint information** |Set read/write mode |In the **Endpoint information** area, click **Read\-only** or **Read/Write** in read/write mode to complete the setup.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After switching from Read/Write mode to Read\-only mode:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">All connections to the database through this endpoint cannot perform update, write, delete or other change operations.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Automatically disassociate the primary node, that is, automatically remove the primary node from the selected nodes.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The <strong>primary node accepts read requests</strong> function failure.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After switching from Read\-only mode to Read/Write mode:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">After switching from Read\-only mode to Read/Write mode, the business is not affected.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Automatically associate the primary node, that is, automatically add the primary node to the <strong>selected nodes</strong>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The <strong>primary node accepts read requests</strong> function to take effect, which is disabled by default.</div><br> |
   ||Modify endpoint name |In the **Endpoint information** area of the **Endpoint name** text box, enter a new endpoint name. The endpoint name setting rules are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~64 characters. |
   ||Consistency levels |For more information about consistency levels, see [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels).<br><br><br>* When the read/write mode is **Read/Write**, the selectable consistency levels are **Eventual consistency**, **Session consistency**, and **Global consistency**.<br><br>* When the read/write mode is ** Read\-only**, the consistency level defaults to **Eventual consistency** and cannot be changed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The effect of adjusting the consistency level is as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Adjustments from eventually consistent to session consistency or global consistency take effect only for new connections.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the session consistency or global consistency is adjusted to the eventual consistency, the existing connections take effect immediately.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The mutual adjustment between session consistency and global consistency takes effect only for new connections.</div><br> |
   ||Timeout |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us, and the default value is 10000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured only when the consistency level is <strong>Session consistency</strong> or <strong>Global consistency</strong>.</div><br> |
   ||Timeout policy |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* **SQL error**: If the leader/follower delay is too large and exceeds the threshold, it will directly return an error (`wait replication complete timeout, please retry`).<br><br>* **Send request to primary node**: If the master\-slave delay is too large and the configured timeout threshold is small, the read request will be sent to the primary node, increasing the pressure on the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured only when the consistency level is <strong>Session consistency</strong> or <strong>Global consistency</strong>.</div><br> |
   ||Primary node accepts read requests |Select to enable or disable **Primary node accepts read requests**.<br><br><br>* When the **Primary node accepts read requests** function is enabled, non\-transactional read requests are sent to the primary node or read\-only node in a load\-balanced manner based on the number of active requests.<br><br>* When the **Primary node accepts read requests** function is disabled, the primary node only accepts transaction read requests, and non\-transaction read requests will not be sent to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Configuring this parameter is supported only at the read/write endpoint.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Enabling or disabling the primary node accepts read requests function takes effect immediately for all connections.</div><br> |
   ||Transaction splitting |Select to enable or disable **Transaction splitting**. For a detailed description of transaction splitting, see [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Configuring this parameter is supported only at the read/write endpoint.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Enabling or disabling the transaction splitting function is only effective for new connections. Existing connections retain their original configuration.</div><br> |
   ||Connection pool |The connection pool is **Disable** by default. You can configure the connection pool based on your business scenarios. It supports **Session\-level connection pool** and **Transaction\-level connection pool**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Changes to the connection pool configuration apply only to new connections.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For an introduction to the working principles of the two types of connection pools, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool">Connection pool</a>.</div><br> |
   |**Associate node** |Associate node |Add or delete read\-only nodes associated with the connection endpoint.<br><br><br>* When the read\-write mode is **Read/Write**, you must select the primary node, and you can choose whether to associate with the read\-only node as needed.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to associate a primary node and at least one read\-only node. When only the primary node is associated, read\-write separation is not supported.   </div><br>   <br><br>* When the read\-write mode is **Read\-only**, only one or more read\-only nodes can be selected.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once a read\-only node is added, new requests are automatically dispatched to the new node immediately.</div><br> |
   ||Automatically associate new node |Select to enable or disable **Automatically add new node**. Once enabled, the connection endpoint will automatically associate with the newly created read\-only node. |
   

7. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) |Call the ModifyDBEndpoint to modify the connection endpoint. |
