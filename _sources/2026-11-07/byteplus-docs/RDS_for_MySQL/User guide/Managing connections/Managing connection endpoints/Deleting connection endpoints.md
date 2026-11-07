---
title: "Deleting connection endpoints"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_connection_endpoints"
---

This topic describes how to delete a connection endpoint for an RDS for MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Connection endpoints associated with PrivateLink cannot be deleted.

* Deleting an endpoint will interrupt all database connections accessed through this endpoint, operate carefully.

* Only manually created connection endpoints can be deleted. Default endpoints created by the system cannot be deleted. A multiple\-node instance automatically creates three connection endpoints upon creation, while a single\-node instance automatically creates one direct endpoint. These endpoints cannot be deleted.

* Deleting a connection endpoint releases its associated private and public network addresses.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. On the left navigation bar, click **Instances** to go to the **Instances** page.

4. On the **Instances** page, click the name of the target instance to enter the instance.Instances

5. On the **Connectivity** tab, in the **Endpoints** list, click **Edit** in the **Actions** column of the target connection endpoint. In the dialog box that appears, click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After clicking <strong>OK</strong>, the instance status changes to <strong>Network changing</strong>. After the connection endpoint is deleted, the instance state changes to <strong>Running</strong>.</div>


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbendpoint) |Call the DeleteDBEndpoint API to delete an Endpoint. |


ustom\-md\-table}#
