---
title: "Disassociating allowlist from instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-allowlist-from-instance"
---

The allowlist and the instance have a "many\-to\-many" correspondence. The allowlist that can be unbound from the instance can also be unbound from the allowlist. This article describes how to unbind the allowlist from an instance.

<span id="background-information"></span>
## Background information


* Whether accessing an instance through a VPC intranet or a public network connection, you need to configure the allowlist of the instance first to ensure that the instance can be connected.

* Please maintain the allowlist regularly to clear the IP addresses of devices that do not require access to SQL Server instances to ensure the security of database connections.


<span id="precautions"></span>
## Precautions


* A single instance can bind up to 100 IP allowlists, with each allowlist supporting up to 300 IPs or IP segments. When there are many IP addresses, it is recommended to merge the fragmented IP into IP segments, such as `10.10.10.0/24`.

* Each allowlist can be bound to up to 200 instances.

* Setting up the allowlist does not affect the normal operation of your SQL Server instance.


<span id="prerequisite"></span>
## **prerequisite**


* The [instance was created ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)and is **in the running** state.

* The instance has been allowlisted. For details, see [Associating allowlists to instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-allowlist-to-instance).


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Instance list** in the left navigation bar.

4. On the **Instance list** page, click the target instance name.

5. At the top of the page, click the **Data Security** tab.

6. In the **List of associated allowlist** on the **Data Security** tab, locate the allowlist that needs to be unbound.

7. Click **Disassociate instance** and click **OK** in the dialog box that pops up.
