---
title: "Switching master node"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/switching-master-node"
---

This article describes the steps for manually switching master nodes.

<span id="background-information"></span>
## Background information

Cloud database SQL Server version supports high\-availability type instances, the data of the main and standby nodes will be synchronized in real time, only the data of the main node supports access, and the standby nodes exist only as backups. The cloud database SQL Server version provides the function of switching between the main and the standby. When an instance fails, the system will immediately trigger the switching between the main and the standby, restore the normal operation of the instance in time, and ensure the high availability of the instance. You can also manually switch the master and standby nodes according to business needs. After the switch, the original master node will become a standby node, which can realize rack\-level disaster recovery.

<span id="prerequisite"></span>
## **prerequisite**

An instance has been created and is **in the running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id="precautions"></span>
## **Precautions**

Switching the master node generally takes 30\-120 seconds to complete, during which each database will have 1\-2 flash breaks, please be careful. It is recommended that you increase the reconnection mechanism of the application, which can greatly reduce the impact of the database connection flash failure on the business.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance list** page, click the target instance name to go to the **Instance information** tab.

4. Click the **Connection Management** tab, in the **connection topology** area, point the mouse pointer to the **standby node**, click **Switch master node** in the pop\-up window, and click **OK** in the pop\-up confirmation window to complete the handover of the main and standby nodes.
