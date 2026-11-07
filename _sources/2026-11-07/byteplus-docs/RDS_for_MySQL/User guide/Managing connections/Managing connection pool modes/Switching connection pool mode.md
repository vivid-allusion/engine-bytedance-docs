---
title: "Switching connection pool mode"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_connection_pool_mode"
---

A database connection pool is responsible for allocating, managing, and releasing database connections. By selecting the corresponding connection pool mode based on specific business scenarios, you can improve the performance of the database and improve the utilization of database resources. RDS for MySQL provides direct connection pools and transaction\-level connection pools. This topic describes how to switch between these two modes.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status.

* The status of the instance's database agent feature is **Enabled**. To turn it on, refer to [Enabling the database agent](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).


<span id="precautions"></span>
## Precautions

After the connection pool mode is switched, it only takes effect for new connections, while old connections are disconnected and the mode takes effect after the transaction is committed.

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. Click **Instances** at the left\-side navigation bar to go to the **Instances** page.

4. Click the target instance name on the **Instances** page to go to the instance.

5. In the endpoint list on the **Connectivity** page, click **Edit** in the **Actions** column of the target connection endpoint to enter the **Edit endpoint** page.

6. In the **Basic configuration** area of the **Edit endpoint** page, switch the connection pool for the connection endpoint and click **OK**.


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyconfig) |Call the ModifyDBProxyConfig interface to modify the connection pool mode of the specified MySQL instance. |
