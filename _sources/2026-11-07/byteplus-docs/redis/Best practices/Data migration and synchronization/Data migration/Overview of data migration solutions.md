---
title: "Overview of data migration solutions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/data-migration-solution"
---

Cache for Redis supports multiple data migration solutions provided by About DTS and redis\-shake to meet the needs of Redis data migration in different service scenarios.

<span id=".6L-B56e75bel5YW35LuL57uN"></span>
## Introduction to migration tools

Cache for Redis supports various database migration tools, including:


* **DTS (recommended)** 

   Database Transmission Service (DTS) is a data stream service that integrates data migration, synchronization, and subscription. It supports data interaction between relational databases, non\-relational databases, and other data sources, reducing the complexity of data flow between databases. DTS helps you easily migrate databases to the cloud without interrupting business operations, effortlessly build high\-availability database disaster recovery architectures through real\-time synchronization channels, and freely consume real\-time incremental data provided by cloud databases according to your own needs. For more information on DTS, refer to [About DTS](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service).

* **redis\-shake**

   If data migration cannot be implemented via DTS under certain circumstances (for example, the source database has not been granted `sync` and `psync` permissions), you can use the redis\-shake tool for data migration. Redis\-shake is an open\-source Redis data migration tool that decodes, restores, dumps, and synchronizes/rumps Redis data. In Restore mode, you can migrate data from self\-built Redis or third\-party cloud Redis databases to BytePlus Cache for Redis, without obtaining `sync` and `psync` permissions, via the RDB file in the Redis database. For more information on redis\-shake, refer to [redis-shake](https://github.com/alibaba/RedisShake/wiki/).


<span id=".6L-B56e76YWN572u5qGI5L6L"></span>
## Migration configuration examples


|Migration tools |DTS (recommended) |Redis\-shake (Restore mode) |
|---|---|---|
|Configuration examples |* [Migrating BytePlus Redis to another BytePlus Redis](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_redis)<br><br>* [Migrate data from Self-managed redis connected over Express Network to BytePlus Redis](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_expressredis)<br><br>* [Migrating internet-based self-built Redis to BytePlus Redis](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_publicredis) |[Migrating data with RDB files by redis-shake](https://docs.byteplus.com/en/docs/redis/migrate-data-with-rdb-via-redis-shake) |
