---
title: "Creating connection endpoints"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_connection_endpoints"
---

This article describes how to create custom read\-only endpoints and custom read\-write endpoints.

<span id=".5Yqf6IO95LuL57uN"></span>
## Function introduction

The primary node endpoint and the default endpoint are created by default when the instance is created and do not need to be created manually.

For businesses with isolation requirements, you can connect the businesses with isolation requirements to the NDB for MySQL database using the corresponding connection endpoint according to business needs. For example, you have purchased the NDB for MySQL instance with 1 primary node and 3 read\-only nodes, and there are read\-only business A and read\-write business B that need to connect to the database. To isolate read\-only business A from read\-write business B, you can create a custom read\-only endpoint, associate read\-only node 1 and read\-only node 2, and enable read\-only business A to connect to the instance through the custom read\-only endpoint; create a custom read\-write endpoint, associate the primary node and read\-only node 3, and enable read\-write business B to connect to the instance through the custom read\-write endpoint. The above method can achieve physical isolation of the two businesses in terms of database usage to avoid mutual impact.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The **Primary node accepts read requests** function of newly created custom read/write endpoints is enabled by default. To turn this feature off, see [Editing connection endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_connection_endpoints).

* An instance supports the creation of up to 5 custom connection endpoints.

* Supports creating a single\-node custom connection endpoint. If this node fails, the address may be unavailable for up to 1 hour. Do not use it in a production environment. To ensure business continuity, it is recommended to associate multiple nodes.

* Switching the primary node may affect custom endpoint node associations. For details, refer to [Switching the primary node](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node#.5rOo5oSP5LqL6aG5).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Add endpoint** in the instance topology area.

6. On the **Create endpoint** page, configure the following parameter items based on business requirements.

   
   |Classification |Name |Description |
   |---|---|---|
   |**Endpoint information** |Read/Write mode |Select the read/write mode of the connection endpoint, the optional modes are **Read\-only** or **Read/Write**. |
   ||Endpoint name |Customize the connection endpoint name, set the rules as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~64 characters. |
   ||Consistency levels |For more information about consistency levels, see [Consistency levels.](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels)<br><br><br>* When the read/write mode is **Read/Write**, the selectable consistency levels are **Eventual consistency** (default), **Session consistency**, and **Global consistency**.<br><br>* When the read/write mode is ** Read\-only**, the consistency level defaults to **Eventual consistency** and cannot be changed. |
   ||Timeout |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us, and the default value is 10000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured only when the consistency level is <strong>Session consistency</strong> or <strong>Global consistency</strong>.</div><br> |
   ||Timeout policy |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* **SQL error**: If the leader/follower delay is too large and exceeds the threshold, it will directly return an error (`wait replication complete timeout, please retry`).<br><br>* **Send request to primary node**: If the master\-slave delay is too large and the configured timeout threshold is small, the read request will be sent to the primary node, increasing the pressure on the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured only when the consistency level is <strong>Session consistency</strong> or <strong>Global consistency</strong>.</div><br> |
   ||Primary node accepts read requests |Select to enable or disable **Primary node accepts read requests**, which is enabled by default.<br><br><br>* When the **Primary node accepts read requests** function is enabled, non\-transactional read requests are sent to the primary node or read\-only node in a load\-balanced manner based on the number of active requests.<br><br>* When the **Primary node accepts read requests** function is disabled, the primary node only accepts transaction read requests, and non\-transaction read requests will not be sent to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configuring this parameter is supported only at the read/write endpoint.</div><br> |
   ||Transaction splitting |Select to enable or disable **Transaction splitting**, which is enabled by default. For a detailed description of transaction splitting, see [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configuring this parameter is supported only at the read/write endpoint.</div><br> |
   ||Connection pool |The connection pool is **Disable** by default. You can configure the connection pool based on your business scenarios. It supports **Session\-level connection pool** and **Transaction\-level connection pool**.<br><br>For an introduction to the working principles of the two types of connection pools, refer to [Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool). |
   |**Associate node** |Associate node |* When the read\-write mode is **Read/Write**, you must select the primary node, and you can choose whether to associate with the read\-only node as needed.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to associate a primary node and at least one read\-only node. When only the primary node is associated, read\-write separation is not supported.   </div><br>   <br><br>* When the read\-write mode is **Read\-only**, only read\-only nodes can be selected. |
   ||Automatically associate new node |Select to enable or disable **Automatically add new node**, which is disabled by default. Once enabled, the connection endpoint will automatically associate with the newly created read\-only node. |
   

7. Click **OK** to complete the creation.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint) |Call the CreateDBEndpoint to create a connection endpoint for instance. |
