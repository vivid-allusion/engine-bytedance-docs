---
title: "Disassociating instance from allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-instance-from-allowlist"
---

The allowlist and the instance have a "many\-to\-many" correspondence. The allowlist that can be unbound from the instance can also be unbound from the allowlist. This article describes how to unbind an instance from the allowlist.

<span id="prerequisite"></span>
## **prerequisite**

The allowlist has bound the instance. For details, see [Associating an instance to the allowlist ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-instance-to-allowlist).

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Allowlist list** in the left navigation bar.

4. On the **Allowlist list** page, click the **Target allowlist name**. In the pop\-up page, you can see a list of instances to which the allowlist is bound.

5. In the **List of associated instances**, click **Disassociate instance** to unbind the corresponding instance from the allowlist.
