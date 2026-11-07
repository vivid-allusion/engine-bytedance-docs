---
title: "Restart instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restart-instance"
---

When an instance experiences full connections or performance issues, you can restart the instance manually. This article describes how to restart a SQL Server instance.

<span id="prerequisite"></span>
## **prerequisite**

The [instance was created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and is **in the running** state.

<span id="precautions"></span>
## **Precautions**


* Restarting the instance will cause the connection to be disconnected for about 10 seconds, and the backup will be interrupted. Please proceed with caution.

* When there is a read\-only instance under the master instance, the restart of the master instance and the read\-only instance will not affect each other, and the replication relationship between the master instance and the read\-only instance will be automatically restored after restart.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance List** page, click Restart Instance in the Target Instance Action column.

4. Click **OK** in the dialog box that pops up.
