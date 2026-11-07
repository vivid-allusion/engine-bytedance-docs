---
title: "List of supported extensions"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-List_of_supported_extensions"
---

This topic lists the extensions supported by the PostgreSQL Engine of the AI Native Database Platform.

|**Extension name** |**Supported versions** |**Description** |
|---|---|---|
|address_standardizer |3.3.6 |Geographical name standardization extension based on the PAGC standard. |
|address_standardizer_data_us |3.3.6 |Data extension for geographical name standardization (United States) based on the PAGC standard. |
|[age](https://age.apache.org/#) |1.6.0 |AGE database add\-on. |
|amcheck |1.4 |Detect the logical consistency of B\-tree index structures. |
|autoinc |1.0 |Functions for automatically increasing field values. |
|bloom |1.0 |Provide an index access method based on the Bloom filter. |
|btree_gin |1.3 |Provides an example of a GIN operator class that implements B\-tree equivalent behavior for multiple data types and all enum types. |
|btree_gist |1.7 |Provide an example of a GiST operator class that implements B\-tree equivalent behavior for multiple data types and all enum types. |
|citext |1.6 |Provides a case\-insensitive string type. |
|cube |1.5 |Provides a data type for representing multidimensional cubes. |
|dict_int |1.0 |Example of an add\-on dictionary template for full\-text search. |
|dict_xsyn |1.0 |Text search dictionary template for extended synonym handling. |
|earthdistance |1.2 |Provides two different methods to calculate the great circle distance on the surface of the Earth. |
|file_fdw |1.0 |Foreign Data Wrapper (FDW) allows mapping files (CSV, text files, etc.) on the server's local file system as PG external tables and directly querying file content with SQL query. Also supports reading the output of the COPY program. Commonly used for log analysis and data import preview. |
|fuzzystrmatch |1.2 |Judge the similarity and distance between strings. |
|hstore |1.8 |Store key\-value pairs in a single PostgreSQL value. |
|[hypopg](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-hypopg) |1.4.2 |Support creating hypothetical indexes in memory. |
|[index_advisor](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-index_advisor) |0.2.0 |Automatically analyzes the given SQL query and recommends the optimal indexes that may improve query performance. |
|insert_username |1.0 |Functions to track who made changes to a table. |
|intagg |1.1 |Provides an integer aggregator and an enumerator. |
|intarray |1.5 |Provides a number of useful functions and operators for manipulating null\-free arrays of integers. |
|isn |1.2 |Validates inputs against a hardcoded list of prefixes, also used to connect numbers during output. |
|lo |1.1 |Provides management tools for large objects. Its core function is the automatic cleaning of "orphaned large objects" through triggers—when a row referencing a large object OID is deleted or updated, the corresponding lo data is automatically deleted to prevent large object leakage from occupying storage space. |
|ltree |1.3 |A tag used to represent data stored in a hierarchical tree structure. |
|moddatetime |1.0 |Functions to track the last modification time. |
|neon |1.6 |cloud storage for PostgreSQL |
|neon_rmgr |1.0 |Neon WAL Resource Manager \- custom WAL records used to make Neon work (since PG 16) |
|neon_utils |1.0 |neon_utils \- small useful functions |
|pageinspect |1.12 |Views the content of the database pages at the fundamental level. |
|[pg_bigm](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_bigm?lang=en) |1.2 |Provides full\-text search capabilities and allows the creation of a 2\-gram GIN index to speed up the search process. |
|[pg_buffercache](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_buffercache) |1.5 |Provides a real\-time window to observe the internal status of PostgreSQL shared buffers. |
|[pg_cron](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_cron) |1.6 |A cron\-based PostgreSQL task scheduler extension that can directly execute PostgreSQL commands from within the database. |
|[pg_duckdb](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_duckdb) |1.1.0 |It integrates the high\-performance DuckDB analytics engine, enabling fast analysis queries on relational data or files in Object Storage (such as TOS) in formats like Parquet and CSV within the current database environment, achieving hybrid transaction and analytical processing (HTAP) capabilities. |
|pg_freespacemap |1.2 |Check the free space map (FSM). |
|[pg_graphql](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_graphql) |1.5.11 |A PostgreSQL GraphQL extension that enables PostgreSQL databases to directly provide GraphQL APIs. |
|[pg_jieba](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_jieba) |1.1.1 |Provides full\-text search capabilities for Chinese word segmentation. |
|[pg_jobmon](https://docs.byteplus.com/en/docs/aidap/pg_jobmon) |1.4.2 |Provides a non\-transactional transaction and functions log recording mechanism Extension, used to retain log information when transactions or functions are Failed. Even if your functions or transactions are Failed for any reason, the logged information will not be rolled back, thus ensuring the safety of critical log data. |
|pg_mooncake |0.2.0 |Real\-time analytics on Postgres tables |
|pg_net |0.20.0 |Async HTTP |
|[pg_partman](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_partman) |5.2.4 |Creates and manages time\-based and sequence\-based table partition sets, designed to simplify the management of table partitions based on time or numbers/IDs. |
|pg_prewarm |1.2 |Provides a convenient way to load data into either the operating system buffer cache or the PostgreSQL buffer cache. |
|[pg_repack](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_repack) |1.5.2 |Provides online Vacuum Full to address the increasing physical disk space used by tables, indexes, and other objects from frequent operations such as Update and Delete.s |
|[pg_stat_statements](https://www.postgresql.org/docs/14/pgstatstatements.html) |1.11 |Provides a means for tracking planning and execution statistics of all SQL statements executed by a server. |
|pg_surgery |1.0 |Extension to fix a damaged relation. |
|[pg_textsearch](https://docs.byteplus.com/en/docs/aidap/pg_textsearch) |1.4.0 |Provides full\-text search, relevance ranking, and Top\-K query capabilities based on BM25. |
|pg_trgm |1.6 |Provides functions and operators for determining the similarity of alphanumeric text, as well as index operator classes that support fast searching for similar strings. |
|[pg_uuidv7](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_uuidv7) |1.7 |It embeds a high\-precision Unix timestamp in the high\-order bytes of the UUID, while the low\-order bytes are filled with random numbers to ensure uniqueness. |
|pg_visibility |1.2 |Checks the visibility map (VM) and page\-level visibility details. |
|pg_walinspect |1.1 |Functions to view the contents of PostgreSQL's write\-ahead logs. |
|[pgcrypto](https://www.postgresql.org/docs/14/pgcrypto.html) |1.3 |Provides password functions for PostgreSQL. |
|[pgjwt](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pgjwt) |0.2.0 |PostgreSQL extension for table versioning and historical data queries. |
|[pgmq](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pgmq) |1.7.0 |A lightweight PostgreSQL message queue extension offering producer\-consumer APIs similar to AWS SQS/RSMQ. All logic is implemented in built\-in SQL/PLpgSQL without background processes or external dependencies. |
|pgrowlocks |1.2 |Provides a function to show row locking information for a specified table. |
|pgstattuple |1.5 |Provides various functions to obtain tuple\-level statistics. |
|[pgvector](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_vector) |0.8.0，0.8.2 |Provides similarity search capabilities for high\-dimensional vectors. |
|[plpgsql](https://www.postgresql.org/docs/17/plpgsql.html) |1.0 |Functions to view the contents of PostgreSQL's write\-ahead logs. |
|[postgis](https://postgis.net/docs/) |3.3.6 |PostGIS extensions related to spatial and geographic information. |
|postgis_raster |3.3.6 |PostGIS raster data extension, providing storage and analysis functions for raster data. |
|postgis_sfcgal |3.3.6 |PostGIS SFCGAL extension related to spatial geographic information. |
|postgis_tiger_geocoder |3.3.6 |PostGIS TIGER extensions related to spatial and geographic data information. |
|postgis_topology |3.3.6 |PostGIS extensions related to spatial and geographic topology data information. |
|postgres_fdw |1.1 |Cross\-database operation table. |
|[rds_ai](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-rds_ai) |1.0，1.1，1.2，1.3，1.4 |A native database extension that supports directly invoking AI models via SQL functions within the database, enabling intelligent data querying and processing. |
|refint |1.0 |Functions for implementing referential integrity (outdated). |
|seg |1.4 |Data type for representing line segments or floating\-point intervals. |
|sslinfo |1.2 |Provides information about the SSL certificate provided by the current client. |
|tablefunc |1.0 |Includes various functions that return tables. |
|tcn |1.0 |Triggered change notifications. |
|tsm_system_rows |1.0 |Provides the SYSTEM_ROWS table sampling method. |
|tsm_system_time |1.0 |Provides the table sampling method SYSTEM_TIME. |
|[uuid-ossp](https://www.postgresql.org/docs/14/uuid-ossp.html) |1.1 |Provides functions to generate universally unique identifiers (UUIDs) using one of several standard algorithms. |
|xml2 |1.1 |Provides XPath querying and XSLT functionality. |
|[zhparser](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-zhparser) |2.2 |Provides Chinese word segmentation and full\-text search capabilities in Chinese. |
