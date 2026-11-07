---
title: "Why is the total number of sessions in the session management tab inconsistent with the number of connections in the MySQL instance?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/what-to-do-when-session-connection-error-when-log-in-to-redis-instance-on-data-interaction-platform"
---

Because the session management of Database Workshop (DBW) filters out connections from internal accounts of the MySQL instance (e.g., `root`, `repl`, `byte_rds_agent`, `byte_rds_backup`, `byte_rds_proxy`) and internal accounts of DBW (e.g., `dbw_admin`), the number of connections displayed in the session management tab of DBW is inconsistent with the number of connections in the MySQL instance.
