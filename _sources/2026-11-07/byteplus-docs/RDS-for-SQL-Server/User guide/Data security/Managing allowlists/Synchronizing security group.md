---
title: "Synchronizing security group"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/synchronizing-security-group"
---

RDS for SQL Server allowlist has support for associating ECS security groups and for binding ECS security groups for SQL Server allowlists. After binding the ECS security group, if the ECS security group is updated, it can be synchronized in the RDS for SQL Server for allowlisting.

<span id="prerequisite"></span>
## prerequisite

There is the allowlist associated with the ECS security group.

<span id="precautions"></span>
## Precautions


* When you synchronize security groups, RDS for SQL Server automatically recognizes IP changes that exist in allowlisted security groups and updates the IP information in the allowlist. Please confirm whether the removal of the IP from the bound security group from the allowlist will affect business.

* A single allowlist can support up to 300 IPs or IP segments. If the binding security group involves an IP or the IP segment exceeds the limit, the synchronization will fail.

* A single instance can bind up to 300 IPs or IP segments through the allowlist. If the binding security group involves an IP or the IP segment exceeds the limit, the synchronization will fail.


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select Project and Region.

3. Click **Allowlist list** in the left navigation bar.

4. On the allowlist page, select  **...**  \> **Synchronize security groups** for the target allowlist action column.

5. Are **Security groups synchronized?**  Confirm the IP changes before and after synchronization in the dialog box. Click **OK** after confirming that it is correct.
