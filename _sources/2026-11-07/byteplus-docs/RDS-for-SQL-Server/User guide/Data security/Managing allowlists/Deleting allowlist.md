---
title: "Deleting allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-allowlist"
---

Allowlist is a security measure for database connections. Only IP addresses added to the allowlist can successfully access SQL Server instances. To ensure the security of database connections, the allowlist needs to be maintained periodically to remove IP addresses that no longer need to access the database. This article describes how to remove allowlists to manage IP addresses.

<span id="prerequisite"></span>
## **prerequisite**


* It has been confirmed that the IPs in the allowlist to be deleted no longer need to access the database.

* The instance has been unbound from the allowlist. The allowlist of already bound instances is not allowed to be deleted. If you need to delete, please unbind first. For details, see [Disassociating Instances from allowlist](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-instance-from-allowlist).


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Allowlist list** in the left navigation bar.

4. On the **Allowlist list** page, click on the Target allowlist **Action** column  **...**  \> **Delete**.

5. Are you **Sure to delete the allowlist?**  Dialog box Click **OK**.
