---
title: "View connection address of the read-only instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/view-connection-address-of-the-read-only-instance"
---

RDS for SQL Server supports the creation of read\-only instances to share the read pressure of the primary instance, and also provides a unified read\-only cluster connection address for multiple read\-only instances to help you manage read\-only instances. You can reasonably configure the connection address of the master instance and the connection address of the unified read\-only cluster in the application, so as to reduce the reading pressure of the master instance and improve the overall processing power of the system.

<span id="background-information"></span>
## Background information

In order to reduce the read pressure of the primary instance, RDS for SQL Server provides the following two connection addresses for read\-only instances:


* Provide a unified read\-only cluster connection address for multiple read\-only instances: The system provides a unified connection address for all read\-only instances under the primary instance's connection management tab. If the read\-only address is configured in an application, the system distributes all read requests equally across all read\-only instances.

* Provide a connection address for each read\-only instance: The system provides a connection address for the read\-only instance on the Connection Management tab of the read\-only instance. If the connection address of a single read\-only instance is configured in an application, when a read request is encountered, the system assigns all read requests to that read\-only instance.


<span id="prerequisite"></span>
## prerequisite

A Cloud Database SQL Server Moderator instance and a Read\-Only instance have been created, and the primary instance meets the following conditions.


* Compatible version: SQL Server 2019 Enterprise Edition.

* Instance Type: Cluster Edition.

* Instance status: Running.


<span id="precautions"></span>
## Precautions


* When a read\-only instance is created, a read\-only node end point connection address is created separately for each read\-only instance by default.

* When a read\-only instance is created, the system defaults to creating a single read\-only cluster connection address for multiple read\-only instances. The connection address of the end point of the unified read\-only cluster is fixed, and it will not change with the addition or deletion of read\-only instances. There is no need to change the application multiple times, which reduces maintenance costs.

* Read\-only addresses are free and currently only charge for read\-only instances.


<span id="operation-steps"></span>
## Operation steps

**View multiple read\-only instances Unified read\-only cluster connection address**

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Unified read\-only cluster connection addresses can be viewed in the Connection Management tab of the primary instance.</div>



1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, click **Instance List**.

4. On the **Instance List** page, click the name of the instance to which the target read\-only instance belongs.

5. On the target instance's **instance information** page, click **Connection Management**.

6. In the **Connection Topology** area of the Connection tab, point the mouse over the **read\-only cluster end point** card.

7. In the pop\-up window, you can view the unified private network access addresses and ports of all read\-only instances under the current primary instance.


**View the connection address for a single read\-only instance**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, click **Instance List**.

4. On the **Instance List** page, click the plus icon before the target instance name, and then click the name of the target read\-only instance.

5. On the **Instance Information** page for the target read\-only instance, click **Connection Management**.

6. In the **Connection Topology** area of the Connection tab, point the mouse over the **read\-only node end point** card.

7. In the pop\-up window, you can view the private network access address, public network access address, and port of the read\-only instance.
