---
title: "Create endpoint"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_connection_endpoints"
---

This topic describes how to create a connection endpoint.

## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

## Precautions

* Proxy endpoints depend on the database proxy feature of the MySQL instance. You cannot create a proxy endpoint if the database proxy feature is not enabled for the instance.

* To ensure high availability of the proxy read\-only endpoint, associate at least two read\-only nodes. If the proxy read\-only endpoint is associated with only one read\-only node, the endpoint cannot provide services during fault recovery when this node fails. For instances without the database proxy enabled, it is also recommended to enable the database proxy and associate at least two read\-only nodes with the connection endpoint.

* A multiple node instance automatically creates three connection endpoints upon creation, and also supports creating three Read/Write direct endpoints.

* A double node instance only supports selecting the primary node or a read\-only node when creating a proxy endpoint or a direct endpoint.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

> **tip**

> If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, click the name of the target instance to enter the instance.

5. Under the **Connectivity** tab, in the **Instance topology** area, click  **+Add endpoint** to go to the **Create endpoint** page.

   > **tip**

   > Alternatively, click **Add endpoint** in the **Endpoints** area.

6. On the **Create endpoint** page, configure the following settings and click **OK**.

   |**Configuration item** |Applicable endpoint type |Description |
   |---|---|---|
   |Endpoint type |\- |Set the type of the connection endpoint. You can select **Proxy endpoint** or **Direct endpoint**.<br><br><br>* **Proxy endpoint**: Connections through this endpoint pass through the proxy and can use proxy\-related features and functions, such as read/write separation, load balancing, Wait_timeout, and Multi\-Statements.<br><br>* **Direct endpoint**: Connections to the database through this endpoint will connect directly to the corresponding node, and proxy\-related features cannot be used.<br><br><br>> **tip**<br><br><br><br>* > For details about the functional differences between proxy endpoints and direct endpoints, refer to [About connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_connection_endpoints).<br><br><br>* > Proxy endpoints depend on the database proxy feature of the MySQL instance. You cannot create a proxy endpoint if the database proxy feature is not enabled for the instance. For more information about how to enable the database proxy for an instance, refer to [Enabling database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).<br> |
   |Read/Write mode |Proxy endpoint and direct endpoint |Select the Read/Write mode of the connection endpoint. You can select **Read/Write** or **Read\-only**. |
   |Connection pool |Proxy endpoint |Select the connection pool mode for the connection endpoint. You can select **Transaction\-level connection pool** or **Direct connection mode**. For more information about the connection pool mode, refer to [About connection pool modes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_connection_pool_mode). |
   |Wait_timeout |Proxy endpoint |Select whether to enable the Wait_timeout feature.<br><br><br>* When enabled, connections through the proxy will be automatically disconnected if they have been idle for longer than the period specified in `wait_timeout`, reducing resource usage.<br><br>* When disabled, connections through the proxy will not be automatically disconnected even if they have been idle for longer than the period specified in `wait_timeout`, which may consume more system resources.<br><br>* The Wait_timeout feature relies on the MySQL session tracker mechanism. This feature will not work if the [session_track_state_change](https://dev.mysql.com/doc/refman/8.4/en/server-system-variables.html#sysvar_session_track_state_change) parameter is set to `OFF` and the [session_track_system_variables](https://dev.mysql.com/doc/refman/8.4/en/server-system-variables.html#sysvar_session_track_system_variables) parameter is left empty.<br><br>* If the Database proxy feature for the instance is disabled after the Wait_timeout feature is enabled, the Wait_timeout feature will not take effect and will not be displayed on the Modify endpoint page. When the Database proxy feature for the instance is re\-enabled, the Wait_timeout feature is automatically restored. |
   |Endpoint name |Proxy endpoint and direct endpoint |Set the name of the connection endpoint. The rules for the endpoint name are as follows:<br><br><br>* Cannot be empty.<br><br>* It cannot start with a digit or hyphen (\-).<br><br>* The name length is limited to 1–64 characters.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   |Associate node |Proxy endpoint and direct endpoint |Associate nodes with the connection endpoint. The rules for associating nodes vary for different types of connection endpoints:<br><br><br>* For a proxy endpoint, in Read/Write mode it can be associated with only the primary node or with the primary node and up to 10 read\-only nodes; in Read\-only mode, it can only be associated with 1 to 10 read\-only nodes.<br><br>* For a direct endpoint, it can only be associated with the primary node in Read/Write mode, and only with 1 read\-only node in Read\-only mode. |
   |Automatically add new nodes |Proxy endpoint |Select whether to automatically add new nodes. When enabled, the connection endpoint automatically associates with newly added nodes. |
   |Connection persistence |Proxy endpoint |Select whether to enable connection persistence for the endpoint. For more information about the connection persistence feature, refer to [Enable or disable connection persistence](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_connection_persistence). |
   |Read/Write separation |Proxy endpoint |Select whether to enable the Read/Write separation feature. Once enabled, you can configure read requests to be forwarded to read\-only nodes to reduce the read load on the primary node.<br><br>> **tip**<br><br><br>> Only connection endpoints in Read/Write mode support the Read/Write separation feature.<br> |
   |Consistency level.<br><br> |Proxy endpoint |Select one of the following levels based on your business scenario:<br><br><br>* Eventual consistency (Default value).<br><br>* Session consistency.<br><br>* Global consistency.<br><br><br>> **tip**<br><br><br><br>* > Only connection endpoints with an **Endpoint type** of **Proxy endpoint** and a **Read/Write mode** of **Read/Write** support setting the consistency level.<br><br><br>* > For the application scenarios of Eventual consistency, Session consistency, and Global consistency, refer to [Consistency introduction](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Set_consistency_level?lang=en).<br> |
   |Consistent read timeout<br><br> |Proxy endpoint |Sets the maximum time for the proxy to wait for read\-only nodes to catch up to the target data position. The default value is 10 ms. The value range is 0~60,000, and the unit is ms (milliseconds). When this parameter is set to 0, no waiting is required.<br><br>> **tip**<br><br><br>> This parameter can only be configured when the **consistency level** is set to **Session consistency** or **Global consistency**.<br> |
   |Timeout policy |Proxy endpoint |Set the method used by the proxy to handle read requests when the read\-only node fails to catch up with the target position within the timeout period. Values are as follows:<br><br><br>* **Switch to primary node** (Default value): Forwards read requests to the primary node. This approach may increase the load on the primary node.<br><br>* **Return error**: Returns an error message. It is recommended that your application has a retry mechanism.<br><br><br>> **tip**<br><br><br>> This parameter can only be configured when the **consistency level** is set to **Session consistency** or **Global consistency**.<br> |
   |Multi\-Statements mode |Proxy endpoint |Select Multi\-Statements mode. You can select **Strict mode** or **Loose mode**.<br><br><br>* Strict mode<br><br>   In this mode, Multi\-Statements will be sent to the primary node, and subsequent requests for read/write separation of the current connection will fail. All requests will be routed to the primary node. Disconnecting the current connection and reconnecting is needed to restore read/write separation. The connection endpoints in this mode does not parse Multi\-Statements, has good performance, and is suitable for short connection and connectionless multiplexing scenarios.<br><br>* Loose mode<br><br>   In this mode, Multi\-Statements are sent to the primary node, and subsequent requests for the current connection can still be read/write separation. The connection endpoints in this mode does not parse Multi\-Statements, and has good performance. It is suitable for scenarios where Multi\-Statements only contain DML SQL and do not contain operations such as setting session variables, creating temporary tables, creating stored procedures, and executing uncommitted transactions.<br><br><br>> **tip**<br><br><br>> The Multi\-Statements mode for the endpoint can only be adjusted when read/write separation is enabled.<br> |
   |Overload protection |Proxy endpoint |Select whether to enable overload protection. When enabled, a protection mechanism for the primary node is activated if all its read\-only nodes become abnormal, preventing it from being overwhelmed by traffic spikes.<br><br>> **tip**<br><br><br><br>* > When enabled, the overload protection time must be set. The overload restriction on the primary node is lifted after the configured protection time expires. The value range for the overload protection time is 60 to 7200s.<br><br><br>* > If the connection endpoint of your instance does not have the overload protection feature, upgrade the kernel version of the instance. To upgrade the kernel version of the instance, refer to [Manually upgrade instance kernel version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).<br><br><br>* > The overload protection feature is enabled only when read/write separation is enabled for the connection endpoint and the associated nodes include both the primary node and read\-only nodes.<br><br><br>* > Only proxy endpoints support the overload protection feature.<br> |
   |Read request scheduling policy |Proxy endpoint |Select the read request scheduling policy for the connection endpoint. The options are **Round robin scheduling** or **Connection schedule**.<br><br><br>* Round robin scheduling<br><br>   Recommended option. When this scheduling policy is selected, the system dispatches new connections to the associated nodes according to the weight configuration.<br><br>* Connection schedule<br><br>   The system automatically distributes new connections to nodes with lighter loads based on the node's active request volume and response time. |
   |Weight allocation policy |Proxy endpoint |The weight allocation policy when the read request scheduling policy is set to **Round robin scheduling**. You can select **Automatic assignment** or **Custom assignment**.<br><br><br>* Automatic assignment<br><br>   When this assignment policy is selected, the system automatically assigns a weight to each associated node based on its specification.<br><br>* Custom assignment<br><br>   With custom assignment, the page displays the associated nodes, and you can set a weight for each node in the list. The default weight is automatically calculated based on the node specification. Weight ranges from 0 to 10000 and must be an integral multiple of 100.<br><br><br>> **tip**<br><br><br>> Set the weight according to the proportion of node specifications to prevent uneven node pressure from wasting resources.<br> |
   |Primary node routing |Proxy endpoint |Select whether to enable primary node routing for the connection endpoint. When enabled, the primary node is evaluated along with read\-only nodes, and the node with the fewest connections handles new read requests. When disabled, separable read requests are not routed to the primary node.<br><br>> **tip**<br><br><br><br>* > This feature is only available for instances with kernel version 20241215 or later. If needed, you can manually upgrade the instance kernel version. For more information, refer to [Manually upgrade instance kernel version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).<br><br><br>* > This feature is only supported when read/write separation is enabled for the connection endpoint, the endpoint is associated with both the primary and read\-only nodes, and the read request scheduling policy is **Connection schedule**.<br> |
   |Read\-only latency threshold |Proxy endpoint |Set the read\-only latency threshold for the connection endpoint. Read\-only nodes with a latency exceeding this threshold will not be assigned read requests. The range of values is 1 to 3600, in seconds, with a step size of 1.<br><br>> **tip**<br><br><br>> Only Read/Write endpoints support this setting.<br> |
   |Transaction splitting |Proxy endpoint |Select whether to enable transaction splitting for the connection endpoint. For more information about transaction splitting, refer to [Enable or disable transaction splitting](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transaction_splitting). |
   |Forwarding rules<br><br> |Proxy endpoint |Set SQL forwarding rules for the endpoint. For more information about setting SQL forwarding rules, refer to [Configure SQL forwarding rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Configuring_SQL_forwarding_rules). |

> **tip**

> After clicking **OK**, the instance status changes to**Network changing**. After the connection endpoint is created, the instance state changes to **Running**.

## Related API

|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |Call the CreateDBEndpoint API to create an endpoint. |
