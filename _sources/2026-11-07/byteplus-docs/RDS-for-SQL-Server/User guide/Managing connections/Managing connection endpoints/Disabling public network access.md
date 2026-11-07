---
title: "Disabling public network access"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disabling-public-network-access"
---

When you no longer need to access an instance through the public network, you can also turn off public network access for the instance. This article describes the steps to enable public network access.

<span id="prerequisite"></span>
## **prerequisite**


* An instance has been created and is **in the running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* Public network access has been enabled for the instance. For specific operations, see [Enabling Public Network Access](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-public-network-access).


<span id="precautions"></span>
## Precautions

After closing public network access:


* The database will not be accessible through the public network, including established public network connections.

* The Elastic Public IP (EIP) will be automatically untied, but the unbound EIP will continue to be retained and charged. If you no longer use it, please release the relevant resources by yourself.

* The whitelist should be updated in a timely manner, and the IP address accessing the database through the public network should be deleted to ensure the security of the database.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance list** page.

4. In the Connection Topology area under the Connection tab, point the mouse to the master node end point card, and in the pop\-up window, click the **Close** button to the right of the public network address.

5. In the dialog box that pops up, click the **Close** button.
