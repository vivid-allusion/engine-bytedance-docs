---
title: "What should I do if an error occurs during the session connection when logging into the Redis instance on the Data Interaction Platform?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/error_occurs_when_logging_into_SQL_console"
---

When logging into a Redis instance on the Data Interaction Platform of Database Workshop DBW, the platform currently does not support executing commands such as `SUBSCRIBE`, `PUBLISH`, `HyperLogLog`, and `MULTI` in the session. If you encounter an error, please confirm whether the current session is executing these commands.
