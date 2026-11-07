---
title: "How to migrate data from a third-party cloud Redis database to Volcano Engine Cache for Redis"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/How_can_I_migrate_data_from_a_Redis_database"
---

In certain cases, the `sync` or `psync` replication permissions are not granted by the [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) Redis [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service), which makes it impossible to [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) BytePlus [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service). In such scenarios, you can use the redis\-shake tool with RDB files to perform an offline migration of the full dataset from the source Redis database to the target Redis database. When using RDB files to migration data, you can migration data from self\-built Redis or third\-party cloud Redis databases to BytePlus Cache for Redis without relying on `sync` and `psync` permissions. For more details, refer to [redis-shake](https://github.com/alibaba/RedisShake/wiki/).

For detailed instructions on how to migrate data from a third\-party cloud Redis database to BytePlus Cache for Redis, refer to [Migrating data with RDB Files Using redis-shake](https://docs.byteplus.com/en/docs/redis/migrate-data-with-rdb-via-redis-shake).
