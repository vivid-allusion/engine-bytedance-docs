---
title: "Viewing connection endpoints"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_connection_endpoints"
---

The connection endpoint is a network proxy service located between the database and the application, which is used to proxy all requests when the application accesses the database. The client accesses the instance through the connection address or IP of the connection endpoint. This article describes how to view detailed information about a connection endpoint.

<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click the name of the target instance on the **Instances** page to go to the **Summary** page.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **View** in the destination endpoint area to view the details of that end point in the sidebar.

   
   |Information classification |Description |
   |---|---|
   |**Private network** |Including private network address, private network port, private network IP, public network resolution status, etc. |
   |**Public network** |Including public network address, public network port, public network IP.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To view the public network address of an instance, you must first enable public network access for the instance. For detailed instructions, please refer to <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_access">Enabling or disabling public network access</a>.</div><br> |
   |**Endpoint information** |Including endpoint name, endpoint read/write mode, consistency levels, primary node accepts read requests state, transaction splitting state, etc. |
   |**Associate node** |Including the number of associated nodes, the status of automatically joining new nodes, etc. |
   


<span id="相关-api"></span>
### Related APIs


|API |Description |
|---|---|
|[DescribeDBEndpoint](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint) |Call the DescribeDBEndpoint to query the details of the instance connection endpoint. |
