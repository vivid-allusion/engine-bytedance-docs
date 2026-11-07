---
title: "List of supported extensions"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_supported_plugins"
---

This topic lists the extensions and their versions supported by various versions of RDS for PostgreSQL.

> **tip**

* > Before using some extensions, you need to add the extension to the shared_preload_libraries parameter. Otherwise, the extension cannot be created. Extensions involved include pg_bigm, pg_cron, pg_hint_plan, pg_pathman, pg_prewarm, pg_stat_kcache, pg_stat_statements, pgaudit, and timescaledb.

* > Some extensions have dependencies on other products. When using them, the dependent extensions must also be added to shared_preload_libraries. For more information, see the usage documentation of each extension.

* > The following extensions have certain security risks when used and are not supported on RDS for PostgreSQL instances.

   * > jsonb_plpython3u

   * > plpython3u

   * > adminpack

   * > jsonb_plperlu

   * > hstore_plpython3u

   * > pltclu

   * > hstore_plperlu

   * > bool_plperlu

   * > file_fdw

   * > lo

   * > plperlu

   * > ltree_plpython3u

   * > bool_plperl

   * > hstore_plperl

   * > jsonb_plperl

   * > plperl

|Extension name |PostgreSQL 18 |PostgreSQL 17 |PostgreSQL 16 |PostgreSQL 15 |PostgreSQL 14 |PostgreSQL 13 |PostgreSQL 12 |PostgreSQL 11 |Description |
|---|---|---|---|---|---|---|---|---|---|
|[address_standardizer](https://postgis.net/docs/standardize_address.html) |3.6.4<br><br> |3.3.6 |3.3.6 |3.3.6 |3.3.6 |3.2.5 |3.1.4 |3.1.4 |Geographical name standardization extension based on the [PAGC](http://www.pagcgeo.org/docs/html/pagc-11.html) standard. |
|[address_standardizer_data_us](https://postgis.net/docs/standardize_address.html) |3.6.4<br><br> |3.3.6 |3.3.6 |3.3.6 |3.3.6 |3.2.5 |3.1.4 |3.1.4 |Data extension for geographical name standardization (United States) based on the [PAGC](http://www.pagcgeo.org/docs/html/pagc-11.html) standard. |
|age |1.7.0 |1.6.0 |1.5.0 |1.5.0 |1.5.0 |Not support |Not support |Not support |AGE database add\-on. |
|autoinc |1 |1 |1 |1 |1 |1 |1 |1 |Functions for automatically increasing field values. |
|[bloom](https://www.postgresql.org/docs/14/bloom.html) |1.0<br><br> |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Provide an index access method based on the Bloom filter. |
|[btree_gin](https://www.postgresql.org/docs/14/btree-gin.html) |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |Provides an example of a GIN operator class that implements B\-tree equivalent behavior for multiple data types and all enum types. |
|[btree_gist](https://www.postgresql.org/docs/14/btree-gist.html) |1.8 |1.7 |1.6 |1.6 |1.6 |1.5 |1.5 |1.5 |Provide an example of a GiST operator class that implements B\-tree equivalent behavior for multiple data types and all enum types. |
|[citext](https://www.postgresql.org/docs/14/citext.html) |1.8 |1.6 |1.6 |1.6 |1.6 |1.6 |1.6 |1.5 |Provides a case\-insensitive string type. |
|[cube](https://www.postgresql.org/docs/14/cube.html) |1.5 |1.5 |1.5 |1.5 |1.5 |1.4 |1.4 |1.4 |Provides a data type for representing multidimensional cubes. |
|[dblink](https://www.postgresql.org/docs/12/dblink.html) |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Cross\-database operation table. |
|[dict_int](https://www.postgresql.org/docs/14/dict-int.html) |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Example of an add\-on dictionary template for full\-text search. |
|dict_xsyn |1 |1 |1 |1 |1 |1 |1 |1 |Text search dictionary template for extended synonym handling. |
|[earthdistance](https://www.postgresql.org/docs/14/earthdistance.html) |1.2 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |Provides two different methods to calculate the great circle distance on the surface of the Earth. |
|[fuzzystrmatch](https://www.postgresql.org/docs/current/fuzzystrmatch.html) |1.2 |1.2 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |Judge the similarity and distance between strings. |
|[hstore](https://www.postgresql.org/docs/14/hstore.html) |1.8 |1.8 |1.8 |1.8 |1.8 |1.7 |1.6 |1.5 |Store key\-value pairs in a single PostgreSQL value. |
|hstore_plpython2u |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between hstore and plpython2u. |
|hstore_plpythonu |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between hstore and plpythonu. |
|[hypopg](https://docs.byteplus.com/en/docs/RDS_for_PG/hypopg)<br><br> |1.4.2 |1.4.2 |1.4.2 |1.4.2 |1.4.2 |1.4.2 |1.4.2 |1.4.2 |Support creating hypothetical indexes in memory. |
|[index_advisor](https://docs.byteplus.com/en/docs/RDS_for_PG/index_advisor) |v0.2.0 |v0.2.0 |v0.2.0 |v0.2.0 |v0.2.0 |v0.2.0 |v0.2.0 |Not support |Support index_advisor extension, which automatically analyzes given SQL queries and recommends optimal indexes to improve query performance. |
|insert_username |1 |1 |1 |1 |1 |1 |1 |1 |Functions to track who made changes to a table. |
|[intagg](https://www.postgresql.org/docs/14/intagg.html) |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |Provides an integer aggregator and an enumerator. |
|[intarray](https://www.postgresql.org/docs/14/intarray.html) |1.5 |1.5 |1.5 |1.5 |1.5 |1.3 |1.2 |1.2 |Provides a number of useful functions and operators for manipulating null\-free arrays of integers. |
|[isn](https://www.postgresql.org/docs/14/isn.html) |1.3 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Validates inputs against a hardcoded list of prefixes, also used to connect numbers during output. |
|jsonb_plpython2u |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between jsonb and plpython2u. |
|jsonb_plpythonu |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between jsonb and plpythonu. |
|[ltree](https://www.postgresql.org/docs/14/ltree.html) |1.3 |1.3 |1.2 |1.2 |1.2 |1.2 |1.1 |1.1 |A tag used to represent data stored in a hierarchical tree structure. |
|ltree_plpython2u |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between ltree and plpython2u. |
|ltree_plpythonu |Not support |Not support |Not support |Not support |1 |1 |1 |1 |Convert between ltree and plpythonu. |
|moddatetime |1 |1 |1 |1 |1 |1 |1 |1 |Functions to track the last modification time. |
|old_snapshot |Not support |Not support |1 |1 |1 |Not support |Not support |Not support |Tools to support old_snapshot_threshold. |
|[orafce](https://docs.byteplus.com/en/docs/RDS_for_PG/compatibility_extension-orafce) |4.16<br><br> |4.14.1 |4.9.2 |4.9.2 |4.9.2 |4.9.2 |4.9.2 |4.9.2 |Provide a series of Oracle\-compatible functions to make PostgreSQL databases compatible with Oracle databases. |
|pageinspect |1.13 |1.12 |1.12 |1.11 |1.9 |1.8 |1.7 |1.7 |Views the content of the database pages at the fundamental level. |
|[pg_bigm](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_bigm) |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Provides full\-text search capabilities and allows the creation of a 2\-gram GIN index to speed up the search process. |
|[pg_buffercache](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_buffercache) |1.6<br><br> |1.5 |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |Provides a means for examining what's happening in the shared buffer cache in real time. |
|[pg_cron](https://docs.byteplus.com/en/docs/RDS_for_PG/task_scheduler_expanding-pg_cron) |1.6 |1.6.5 |1.6.5 |1.6.5 |1.6.5 |1.6.5 |1.6.5 |1.6.5 |A cron\-based PostgreSQL task scheduler extension that can directly execute PostgreSQL commands from within the database. |
|[pg_decoderbufs](https://docs.byteplus.com/en/docs/RDS_for_PG/logical_analysis-pg_decoderbufs) |0.1.0<br><br> |0.1.0 |0.1.0 |0.1.0 |0.1.0 |0.1.0 |0.1.0 |0.1.0 |Logical decoding extension that sends WAL stream changes in Protocol Buffer format. |
|[pg_freespacemap](https://www.postgresql.org/docs/14/pgfreespacemap.html) |1.3<br><br> |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Check the free space map (FSM). |
|[pg_graphql](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_graphql?lang=en) |1.5.12 |1.5.11 |1.5.11 |1.5.11 |1.5.11 |Not support |Not support |Not support |Directly parse and execute GraphQL inside the database. |
|[pg_hint_plan](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_hint_plan) |1.8.0 |1.7.0 |1.6.1 |1.5.2 |1.4.3 |1.3.10 |1.3.10 |1.3.9 |Hints PostgreSQL to change its intended execution plan via special comment statements. |
|[pg_uuidv7](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_uuidv7) |v1.7.0 |v1.7.0 |v1.7.0 |v1.7.0 |v1.7.0 |v1.7.0 |v1.7.0 |v1.7.0 |It embeds a high\-precision Unix timestamp in the high\-order bytes of the UUID, while the low\-order bytes are filled with random numbers to ensure uniqueness. |
|pg_hugepage_stat |0.1 |0.1 |0.1 |0.1 |0.1 |0.1 |0.1 |0.1 |Extension work for observing PostgreSQL hugepages. |
|[pg_ivm](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_ivm) |1.15 |1.9 |1.9 |1.9 |1.9 |1.9 |Not support |Not support |Provides the incremental view maintenance (IVM) feature for RDS for PostgreSQL. |
|[pg_jieba](https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_search-pg_jieba) |1.1.1 |1.1.1 |1.1.1 |1.1.1 |1.1.1 |1.1.1 |1.1.1 |1.1.1 |Provides full\-text search capabilities for Chinese word segmentation. |
|[pg_jobmon](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_jobmon) |1.4.1 |1.4.1 |1.4.1 |1.4.1 |1.4.1 |Not support |Not support |Not support |Provides a non\-transactional transaction and functions log recording mechanism Extension, used to retain log information when transactions or functions are Failed. Even if your functions or transactions are Failed for any reason, the logged information will not be rolled back, thus ensuring the safety of critical log data. |
|[pg_partman](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_partman) |5.4.1 |5.2.4 |5.2.4 |5.2.4 |5.2.4 |Not support |Not support |Not support |Creates and manages time\-based and sequence\-based table partition sets, designed to simplify the management of table partitions based on time or numbers/IDs. |
|[pg_pathman](https://github.com/postgrespro/pg_pathman) |Not support |Not support |Not support |Not support |Not support |1.5 |1.5 |1.5 |High\-performance partitioned table extension. |
|[pg_prewarm](https://www.postgresql.org/docs/14/pgprewarm.html) |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Provides a convenient way to load data into either the operating system buffer cache or the PostgreSQL buffer cache. |
|pg_proctab |Not support |all_version |all_version |all_version |all_version |all_version |all_version |all_version |Access information about operating system processes. |
|[pg_profile](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_profile) |4.11 |4.7 |4.4 |4.4 |4.4 |4.4 |4.4 |4.4 |Statistics of resource\-intensive activities. |
|[pg_repack](https://reorg.github.io/pg_repack/) |1.5.3 |1.5.2 |1.5.2、1.4.8 |1.5.2、1.4.8 |1.5.2、1.4.8 |1.5.2、1.4.8 |1.5.2、1.4.8 |1.5.2、1.4.8 |Provides online Vacuum Full to address the increasing physical disk space used by tables, indexes, and other objects from frequent operations such as Update and Delete.s |
|[pg_stat_kcache](https://docs.byteplus.com/en/docs/RDS_for_PG/statistics_on_system_read_or_write_information-pg_stat_kcache) |2.3.1 |2.3.0 |2.2.3 |2.2.3 |2.2.3 |2.2.1 |2.2.1 |2.2.1 |Provides statistics on read and write information of the file system during operation. |
|[pg_stat_statements](https://www.postgresql.org/docs/14/pgstatstatements.html) |1.12 |1.11 |1.9 |1.9 |1.9 |1.8 |1.7 |1.6 |Provides a means for tracking planning and execution statistics of all SQL statements executed by a server. |
|pg_surgery |1 |1 |1 |1 |1 |Not support |Not support |Not support |Extension to fix a damaged relation. |
|[pg_trgm](https://www.postgresql.org/docs/14/pgtrgm.html) |1.6<br><br> |1.6 |1.6 |1.6 |1.6 |1.5 |1.4 |1.4 |Provides functions and operators for determining the similarity of alphanumeric text, as well as index operator classes that support fast searching for similar strings. |
|pg_visibility |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Checks the visibility map (VM) and page\-level visibility details. |
|pg_walinspect |1.1<br><br> |1.1 |1.1 |1 |Not support |Not support |Not support |Not support |Functions to view the contents of PostgreSQL's write\-ahead logs. |
|[pgaudit](https://github.com/pgaudit/pgaudit) |17.0 |17.0 |16.0 |1.7.0 |1.6.2 |1.5.2 |1.4.1 |1.3.2 |Provides detailed session and object audit logging. |
|[pgcrypto](https://www.postgresql.org/docs/14/pgcrypto.html) |1.4 |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |1.3 |Provides password functions for PostgreSQL. |
|[pgjwt](https://docs.byteplus.com/en/docs/RDS_for_PG/JWT?lang=en) |0.2.0 |0.2.0 |0.2.0 |0.2.0 |0.2.0 |0.2.0 |0.2.0 |0.2.0 |Generate and validate JSON Web Token within the database. |
|[pgmq](https://docs.byteplus.com/en/docs/RDS_for_PG/pgmq?lang=en)<br><br> |1.7.0 |1.7.0 |1.7.0 |1.7.0 |1.7.0 |Not support<br><br> |Not support<br><br> |Not support |pgmq is a PostgreSQL\-based lightweight message queue extension. Its API design is similar to Amazon SQS and RSMQ, providing users with simple yet powerful message processing capabilities. |
|pgnodemx |1.7 |1.7 |1.6 |1.6 |1.6 |1.3 |1.3 |1.3 |SQL functions to collect node OS metrics from PostgreSQL. |
|[pgrouting](https://docs.pgrouting.org/) |3.4.2 |3.4.2 |3.4.2 |3.4.2 |3.4.2 |3.3.0 |3.1.3 |3.1.3 |Provides computing and analysis functions of spatial geometric networks. |
|[pgrowlocks](https://www.postgresql.org/docs/14/pgrowlocks.html) |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Provides a function to show row locking information for a specified table. |
|[pgstattuple](https://www.postgresql.org/docs/14/pgstattuple.html) |1.5 |1.5 |1.5 |1.5 |1.5 |1.5 |1.5 |1.5 |Provides various functions to obtain tuple\-level statistics. |
|[plpgsql](https://www.postgresql.org/docs/14/plpgsql.html) |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Provides the SQL procedural language. |
|pltcl |1 |1 |1 |1 |1 |1 |1 |1 |PL/Tcl programming language. |
|[postgis](https://postgis.net/docs/) |3.6.4 |3.3.6 |3.3.2 |3.3.2 |3.3.2 |3.2.5 |3.1.4 |3.1.4 |PostGIS extensions related to spatial and geographic information. |
|[postgis_sfcgal](https://postgis.net/docs/reference.html#reference_sfcgal) |3.6.4 |3.3.6 |3.3.6 |3.3.6 |3.3.6 |3.2.5 |3.1.4 |3.1.4 |PostGIS SFCGAL extension related to spatial geographic information. |
|[postgis_tiger_geocoder](https://postgis.net/docs/Extras.html) |3.6.4 |3.3.6 |3.3.6 |3.3.6 |3.3.6 |3.2.5 |3.1.4 |3.1.4 |PostGIS TIGER extensions related to spatial and geographic data information. |
|[postgis_topology](https://postgis.net/docs/Topology.html) |3.6.4 |3.3.6 |3.3.6 |3.3.6 |3.3.6 |3.2.5 |3.1.4 |3.1.4 |PostGIS extensions related to spatial and geographic topology data information. |
|[postgres_fdw](https://www.postgresql.org/docs/current/postgres-fdw.html) |1.2 |1.1 |1.1 |1.1 |1.1 |1.0 |1.0 |1.0 |Cross\-database operation table. |
|[postgresql-hll](https://docs.byteplus.com/en/docs/RDS_for_PG/postgresql) |v2.19 |v2.19<br><br> |v2.19<br><br> |v2.19<br><br> |v2.19<br><br> |v2.19<br><br> |v2.19<br><br> |v2.19<br><br> |It introduces a custom data type hll to solve large\-scale data cardinality estimation (count distinct) issues, such as billions or more, with minimal storage space and very fast computation speed. |
|[RDKit](https://docs.byteplus.com/en/docs/RDS_for_PG/RDKit) |Not support<br><br> |Not support |4.4.0 |4.4.0 |4.4.0 |3.8.0 |Not support |Not support |Generates compound fingerprints based on machine learning methods for substructure search and structural similarity calculation of compounds. |
|rds_util |1.0<br><br> |1 |1 |1 |1 |1 |1 |1 |Extension to get the real\-time status of RDS PostgreSQL. |
|refint |1 |1 |1 |1 |1 |1 |1 |1 |Functions for implementing referential integrity (outdated). |
|[roaringbitmap](https://docs.byteplus.com/en/docs/RDS_for_PG/computing_bitmap-pg_roaringbitmap) |1.1 |0.5 |0.5 |0.5 |0.5 |0.5 |0.5 |0.5 |Provides efficient Bitmap storage and computing capabilities. |
|[safeupdate](https://docs.byteplus.com/en/docs/RDS_for_PG/safeupdate?lang=en)<br><br> |1.5 |1.5 |1.5 |1.5 |1.5 |Not support |Not support |Not support |Enforces checking at the session or instance level on whether DML statements (mainly `UPDATE` and `DELETE`) contain valid filtering conditions. |
|seg |1.4 |1.4 |1.4 |1.4 |1.4 |1.3 |1.3 |1.3 |Data type for representing line segments or floating\-point intervals. |
|[sslinfo](https://www.postgresql.org/docs/14/sslinfo.html) |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |1.2 |Provides information about the SSL certificate provided by the current client. |
|[tablefunc](https://www.postgresql.org/docs/14/tablefunc.html) |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Includes various functions that return tables. |
|tcn |1 |1 |1 |1 |1 |1 |1 |1 |Triggered change notifications. |
|[Timescaledb](https://www.timescale.com/products) |2.28.2 |2.17.2 |2.15.2 |2.15.2 |2.15.2 |2.11.2 |1.7.1 |1.7.1 |Supports automatic sharding, efficient writing, retrieval, and near real\-time aggregation of time\-series data. |
|timetravel |Not support |Not support |Not support |Not support |Not support |Not support |Not support |1 |PostgreSQL extension for table versioning and historical data queries. |
|[tsm_system_rows](https://www.postgresql.org/docs/14/tsm-system-rows.html) |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Provides the SYSTEM_ROWS table sampling method. |
|[tsm_system_time](https://www.postgresql.org/docs/14/tsm-system-time.html) |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |1.0 |Provides the table sampling method SYSTEM_TIME. |
|[unaccent](https://www.postgresql.org/docs/14/unaccent.html) |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |A text search dictionary that removes accents (diacritic signs) from lexemes. |
|[uuid-ossp](https://www.postgresql.org/docs/14/uuid-ossp.html) |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |Provides functions to generate universally unique identifiers (UUIDs) using one of several standard algorithms. |
|[vector](https://docs.byteplus.com/en/docs/RDS_for_PG/searching_based_on_high-dimensional_vector_similarity-pg_vector) |0.8.2 |0.8.2 |0.8.2 |0.8.2 |0.8.2 |0.8.2 |0.6.2 |0.5.0 |Provides similarity search capabilities for high\-dimensional vectors. |
|[xml2](https://www.postgresql.org/docs/14/xml2.html) |1.2<br><br> |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |1.1 |Provides XPath querying and XSLT functionality. |
|[zhparser](https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_word_segmentation-zhparser) |2.2 |2.2 |2.2 |2.2 |2.2 |2.2 |2.2 |2.2 |Provides Chinese word segmentation and full\-text search capabilities in Chinese. |
