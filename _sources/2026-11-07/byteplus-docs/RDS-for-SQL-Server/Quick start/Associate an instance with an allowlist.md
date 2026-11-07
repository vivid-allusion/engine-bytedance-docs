---
title: "Associate an instance with an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-instances-to-allowlists"
---

After adding an IP address to an allowlist, you must also associate the allowlist with an instance to enable access to the SQL Server instance. Since allowlists and instances have a many\-to\-many relationship, you can either associate an instance with an allowlist or an allowlist with an instance. This topic describes how to associate an instance with an allowlist.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Description**


* Whether you access an instance over a VPC or the public network, you must first configure an allowlist for the instance to ensure connectivity.

* Maintain your allowlists regularly. Remove the IP addresses of devices that no longer need to access the SQL Server instance to ensure the security of your database connections.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* A single instance can be associated with up to 100 IP allowlists, and each allowlist supports up to 300 IP addresses or IP ranges. If you have a large number of IP addresses, we recommend consolidating them into IP ranges, such as `10.10.10.0/24`.

* Each allowlist can be associated with up to 500 instances.

* Configuring an allowlist will not affect the normal operation of the SQL Server instance.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance has been created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. In the left navigation pane, click **Allowlists**.

4. Click **Associate instance** for the target allowlist to go to the **associate instance** page.

5. On the **associate instance** page, select the target instance from the instance list, and click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can quickly locate the target instance by searching for its instance name or instance ID.</div>
