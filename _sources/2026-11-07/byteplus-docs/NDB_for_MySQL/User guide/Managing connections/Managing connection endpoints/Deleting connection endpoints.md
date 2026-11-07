---
title: "Deleting connection endpoints"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_connection_endpoints"
---

The connection endpoint created by the default instance does not support deletion, only manually created custom endpoints are supported. This topic describes how to delete connection endpoints.

<span id="注意事项"></span>
## Precautions

Deleting an endpoint will interrupt all database connections accessed through this endpoint, operate carefully.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* A custom endpoint has been created. For information about creating custom endpoints, see [Creating connection endpoints](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_connection_endpoints).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Delete** in the destination endpoint area.

6. In the pop\-up dialog box, confirm the endpoint information to be deleted. Once confirmed, click **OK** to delete the connection endpoint.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteDBEndpoint](https://www.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpoint) |Call the DeleteDBEndpoint to delete the connection endpoint. |
