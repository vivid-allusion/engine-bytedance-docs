---
title: "Why can't I directly execute Create index or Drop index statements on database tables in the data interaction console?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/createindes_dropindex"
---

For security and data integrity reasons, if the security rule set of the instance bound to the database workbench DBW has enabled **prohibition** **`CREATE_TABLE`** **To execute directly in the database interaction console, please submit a ticket** or **prohibition** **`DROP_TABLE`** **If the security rule for direct execution in the database interaction console is enabled, please submit a ticket**, then you will not be able to execute `Create index` or `Drop index` statements in the data interaction console.

For index changes, please submit a ticket or disable the corresponding security rule set. For detailed operations, please refer to the following documentation


* RDS for MySQL: [Create a regular SQL change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql) or [Disable security rules](https://docs.byteplus.com/en/docs/DBW/security-rule-management#.5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ)

* NDB for MySQL: [Create a regular SQL change ticket](https://docs.byteplus.com/en/docs/DBW/Creating_a_regular_SQL_change_ticket) or [Disable security rules](https://docs.byteplus.com/en/docs/DBW/Security_rule_management#.5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ)

* RDS for PostgreSQL: [Create a regular SQL change work order](https://docs.byteplus.com/en/docs/DBW/Create_a_regular_SQL_change_ticket) or [Disable security rules](https://docs.byteplus.com/en/docs/DBW/security-rule-management_#.5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ)

* RDS for SQL Server: [Disable security rules](https://docs.byteplus.com/en/docs/DBW/security-rule-management__#.5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ)
