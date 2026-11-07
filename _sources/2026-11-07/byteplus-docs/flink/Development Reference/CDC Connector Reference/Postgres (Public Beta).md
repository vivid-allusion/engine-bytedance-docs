---
title: "Postgres (Public Beta)"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/cdc_connector_postgres"
---

The PostgreSQL CDC Pipeline Source Connector is used to read the initial snapshot and subsequent WAL incremental changes from PostgreSQL tables, and deliver change events to downstream components in the Flink CDC Pipeline.

<span id="e130851e"></span>
## Feature Overview


|Category |Details |
|---|---|
|Supported Types |Source |
|Job Type |Flink CDC Pipeline YAML |
|Execution Mode |Streaming mode; `snapshot` startup mode only performs a bounded snapshot |
|Read Phase |Initial snapshot, WAL incremental |
|Supported Change Types |INSERT, UPDATE, DELETE; when Schema Change Inference is enabled, supports adding, dropping, renaming, and modifying columns |
|Delivery Method |Both the Connector and PostgreSQL JDBC Driver are built into the platform; no additional JAR upload is required |
|Processing Semantics |Source saves snapshot progress and WAL read position based on Checkpoint; end\-to\-end consistency depends on the downstream Sink |


<span id="9fbae060"></span>
### Version Compatibility


|Component |Supported Versions |Description |
|---|---|---|
|BytePlus Flink |Flink 1.16、Flink 1.20 |Both the Connector and PostgreSQL JDBC Driver are built into the platform. |
|Flink CDC |BytePlus Flink CDC 3.4 |Includes enhanced PostgreSQL Schema Change Inference. |
|PostgreSQL |No explicit version restrictions |In principle, supports instances that implement the PostgreSQL\-compatible protocol and provide logical replication capability. |


<span id="95437d2f"></span>
## Key Features


* **Full and Incremental Synchronization**: The `initial` mode first reads a consistent snapshot, then continuously reads WAL.

* **Parallel Incremental Snapshot**: Splits table snapshots into multiple chunks to improve full read parallelism and recovery capability.

* **Multi\-table Selection**: Use `database.schema.table` and regular expressions to select or exclude tables.

* **Multiple Start Positions**: The community baseline supports full plus incremental, latest incremental only, committed position of replication slot, and snapshot only.

* **Source\-side Metadata**: Can output operation time, database, schema, and table names for Transform or downstream use.

* **Schema Change Inference**: When using `pgoutput`, column addition, deletion, renaming, and type modification events can be inferred based on differences between Relation messages and cached schema.


<span id="6ea3a1b7"></span>
## Prerequisites


1. Instances must implement the PostgreSQL\-compatible protocol and provide logical replication, WAL, Replication Slot, and other capabilities, ensuring network connectivity between the Flink resource pool and the database.

2. PostgreSQL must have logical replication enabled, `wal_level` set to `logical`, and sufficient capacity reserved for `max_replication_slots` and `max_wal_senders`.

3. Database users with target table read and logical replication permissions must be prepared, and the Flink resource pool must be allowed to connect via `pg_hba.conf` or cloud database allowlist.

4. A Primary Key or an appropriate Replica Identity must be configured for target tables to ensure UPDATE and DELETE operations are correctly identified.

5. A unique Replication Slot must be planned for each running job; when using `pgoutput`, confirm that the Connector user can use or create a Publication.

6. The PostgreSQL username and password must be stored using Flink encrypted variables.

7. Confirm that all tables matched within the same Pipeline belong to the same PostgreSQL database.


<span id="cbd773e0"></span>
## Usage Restrictions


* The Connector only supports use as a Flink CDC Pipeline Source.

* Each Pipeline can connect to only one PostgreSQL database; the database in `tables` must be the same.

* The handling of Schema Evolution depends on `pipeline.schema.change.behavior` and downstream Sink capabilities.

* `schema-change.enabled` is disabled by default and only supported when used with `pgoutput`.

* TRUNCATE TABLE and DROP TABLE events are ignored and will not be delivered downstream.

* A Replication Slot cannot be used by multiple active consumers simultaneously; each parallel running job should use a separate Slot.

* If the Slot does not exist and the user has sufficient permissions, the Connector will automatically create the Slot; by default, the Slot will not be deleted when the job stops.

* When using `pgoutput`, the Connector can automatically create a Publication if permissions are sufficient; existing Publications will be reused according to their current definitions and will not be deleted automatically when the job stops.

* If a Slot is not consumed for an extended period, it will prevent old WAL from being cleaned up, which may continuously occupy PostgreSQL disk space.

* `latest-offset` and `committed-offset` skip the initial snapshot, and data prior to the starting position will not be backfilled.

* `snapshot` reads only the snapshot, exits upon completion, and does not continuously read WAL.

* PostgreSQL multidimensional arrays are not supported; only one\-dimensional arrays are supported.

* `TIME` is always mapped to `TIME(3)`; changes in high\-precision time and Decimal modes may affect downstream types.

* Sequence and Large Object are not within the scope of row\-level WAL data synchronization.


<span id="af79655d"></span>
## Syntax Structure

```YAML
source:
  type: postgres
  name: PostgreSQL Source 
  hostname: <postgres_host>
  port: 5432
  username: ${secret_values.postgres-username}
  password: ${secret_values.postgres-password}
  tables: <database>.<schema>.<table_pattern>
  slot.name: <replication_slot_name>
  decoding.plugin.name: pgoutput
  schema-change.enabled: true
  scan.startup.mode: initial

sink:
  type: values
  name: Values Sink

pipeline:
  name: PostgreSQL CDC Pipeline
  parallelism: 2
  local-time-zone: Asia/Shanghai
  schema.change.behavior: lenient
```


<span id="d69112d5"></span>
## Parameter Description

<span id="a9c5eeb8"></span>
### Connector Configuration Items


|Parameter |Description |Data Type |Required |Default Value |Remarks |
|---|---|---|---|---|---|
|`type` |Pipeline Source type. |STRING |Yes |None |Fixed as `postgres`. |
|`name` |Source name. |STRING |No |None |Used for job topology and log identification. |
|`hostname` |PostgreSQL address. |STRING |Yes |None |Use an address accessible by the Flink resource pool. |
|`port` |PostgreSQL port. |INTEGER |No |`5432` |Must match the actual port of the instance. |
|`username` |PostgreSQL username. |STRING |Yes |None |It is recommended to reference a Flink encrypted variable. |
|`password` |PostgreSQL password. |STRING |Yes |None |It is recommended to reference a Flink encrypted variable. |
|`tables` |Tables to capture. |STRING |Yes |None |Use `database.schema.table`; supports regex, all databases must be the same. |
|`tables.exclude` |Tables to exclude. |STRING |No |None |Further excludes from the `tables` match results; same format. |
|`slot.name` |Logical replication slot name. |STRING |Yes |None |Only lowercase letters, numbers, and underscores are allowed; different running instances must use different slots. |
|`decoding.plugin.name` |Logical decoding plugin. |STRING |No |None |Supports `decoderbufs` and `pgoutput`; use `pgoutput` when Schema Change Inference is required. |
|`server-time-zone` |PostgreSQL server session time zone. |STRING |No |System default time zone |Affects conversion of `TIMESTAMP` without time zone. |
|`scan.startup.mode` |Initial read position at first startup. |STRING |No |`initial` |Supports `initial`, `latest-offset`, `committed-offset`, and `snapshot`. |
|`scan.incremental.snapshot.chunk.size` |Number of rows per snapshot chunk. |INTEGER |No |`8096` |Increasing this value may improve throughput but also increases the recovery cost of a single chunk. |
|`scan.snapshot.fetch.size` |Maximum number of rows fetched per snapshot read. |INTEGER |No |`1024` |Affects database read batch size and client memory usage. |
|`scan.incremental.close-idle-reader.enabled` |Whether to close idle Readers after the snapshot is completed. |BOOLEAN |No |`false` |Verify Flink version compatibility before use. |
|`scan.lsn-commit.checkpoints-num-delay` |Number of checkpoints to delay LSN commit. |INTEGER |No |`3` |Commits earlier LSNs in checkpoint order. |
|`connect.timeout` |Maximum wait time for establishing a connection. |DURATION |No |`30s` |Cannot be less than `250ms`. |
|`connect.max-retries` |Maximum number of retries for establishing a connection. |INTEGER |No |`3` |Affects only connection establishment. |
|`connection.pool.size` |Database connection pool size. |INTEGER |No |`20` |Evaluate PostgreSQL maximum connections when increasing. |
|`heartbeat.interval` |Heartbeat interval. |DURATION |No |`30s` |Used to advance available WAL Offset, preventing WAL retention for low\-traffic tables. |
|`chunk-meta.group.size` |Chunk metadata group size. |INTEGER |No |`1000` |Group storage for large amounts of metadata. |
|`metadata.list` |Output metadata fields. |STRING |No |None |Supports `op_ts`, `table_name`, `database_name`, `schema_name`. |
|`table-id.include-database` |Whether Table ID includes database. |BOOLEAN |No |`false` |When enabled, Table ID is `database.schema.table`. |
|`jdbc.properties.*` |Pass\-through JDBC URL properties. |STRING |No |None |For example, JDBC parameters related to SSL. |
|`debezium.*` |Pass\-through Debezium PostgreSQL Connector properties. |STRING |No |None |Configure only Debezium parameters supported by the current Connector version.<br><br>For more information, see [Debezium Postgres Connector Properties](https://debezium.io/documentation/reference/1.9/connectors/postgresql.html). |


The following are common Debezium passthrough parameters related to the lifecycle of Slot and Publication.


|Parameter |Description |Data Type |Required |Default Value |Remarks |
|---|---|---|---|---|---|
|`debezium.slot.drop.on.stop` |Whether to delete Replication Slot when the job stops normally. |BOOLEAN |No |`false` |It is recommended to keep the default value to support state recovery; slots no longer in use should be cleaned up by the administrator after confirmation. |
|`debezium.publication.name` |Publication name when using `pgoutput`. |STRING |No |`dbz_publication` |When multiple connectors capture the same database, use different publications. |
|`debezium.publication.autocreate.mode` |Publication auto\-creation mode. |STRING |No |`all_tables` |Auto\-creation requires sufficient privileges; in production, publications can be created in advance, or select a community\-supported mode based on the permission model. |


<span id="026dc4c2"></span>
## Type Mapping


|PostgreSQL Type |Flink CDC Type |Description |
|---|---|---|
|`BOOLEAN`、`BIT(1)` |`BOOLEAN` |Multi\-bit `BIT` maps to `BYTES`. |
|`SMALLINT`、`SMALLSERIAL` |`SMALLINT` |Integer. |
|`INTEGER`、`SERIAL` |`INT` |Integer. |
|`BIGINT`、`BIGSERIAL`、`OID` |`BIGINT` |Integer. |
|`REAL`、`FLOAT4` |`FLOAT` |Floating point number. |
|`DOUBLE PRECISION`、`FLOAT8` |`DOUBLE` |Floating point number. |
|`NUMERIC(p,s)`、`DECIMAL(p,s)` |`DECIMAL(p,s)` |NUMERIC without precision defaults to `DECIMAL(38,0)`; can be changed to Double or String via Debezium parameters. |
|Character types, `TEXT`, `UUID`, `ENUM` |`STRING` |String. |
|`JSON`、`JSONB`、`XML` |`STRING` |Raw text or JSON string. |
|`BYTEA` |`BYTES` |Can be changed to strings such as Base64 or Hex via Debezium parameters. |
|`DATE` |`DATE` |Date. |
|`TIME(p)` |`TIME(3)` |Currently fixed at millisecond precision. |
|`TIMESTAMP(p)` |`TIMESTAMP(p)` or `TIMESTAMP(3)` |Depends on `debezium.time.precision.mode`. |
|`TIMESTAMPTZ` |Time type with timezone |Timezone semantics are preserved. |
|One\-dimensional ARRAY |`ARRAY` |Multidimensional arrays are not supported. |
|`HSTORE` |`STRING` or `MAP` |Depends on `debezium.hstore.handling.mode`. |
|Network address types |`STRING` |Includes `INET`, `CIDR`, `MACADDR`, `MACADDR8`. |
|PostGIS Geometry/Geography |`STRING` |Converted to a JSON string containing coordinates, type, and SRID. |


<span id="cdeb1a60"></span>
## Usage Example

<span id="e0a5d791"></span>
### Reading Full and Incremental Data from PostgreSQL

The following example reads the initial snapshot and subsequent WAL changes of matching tables in a PostgreSQL database, and writes them to a Values Sink for verification. Please replace the address, table name, Slot, and encryption variable names before running.

```YAML
source:
  type: postgres
  name: PostgreSQL Source 
  hostname: <postgres_host>
  port: 5432
  username: ${secret_values.postgres-username}
  password: ${secret_values.postgres-password}
  tables: <database>.<schema>.<table_pattern>
  tables.exclude: <database>.<schema>.<excluded_table_pattern>
  slot.name: <replication_slot_name>
  decoding.plugin.name: pgoutput
  schema-change.enabled: true
  scan.startup.mode: initial
  metadata.list: op_ts,table_name,database_name,schema_name
  heartbeat.interval: 30s

sink:
  type: values
  name: Values Sink

pipeline:
  name: PostgreSQL CDC Pipeline
  parallelism: 2
  local-time-zone: Asia/Shanghai
  schema.change.behavior: lenient
```


**Expected Result:**  The job first outputs existing records from the matching tables, then continuously outputs INSERT, UPDATE, and DELETE events. The `op_ts` of snapshot records is `0`, and incremental records contain the actual change time.

<span id="c9637518"></span>
## Operation Mechanism

<span id="0e271c70"></span>
### Snapshot and Incremental Bridging

`initial` mode splits tables into multiple chunks for parallel reading. The WAL position is recorded during the snapshot; after all snapshot chunks are completed, the job continues to consume incremental changes from the corresponding position, avoiding gaps between the snapshot and incremental phases.

<span id="ad67a0c1"></span>
### Replication Slot and LSN

The Replication Slot saves the logical consumption position and prevents the required WAL from being cleaned up prematurely. `scan.lsn-commit.checkpoints-num-delay` controls the number of checkpoints to delay the LSN commit after a successful checkpoint. The Source saves the snapshot progress and WAL read position based on checkpoints, allowing continued reading after failure recovery; end\-to\-end consistency still depends on the delivery semantics of the downstream Sink.

If the Slot does not exist and the Connector user has the necessary permissions such as `REPLICATION`, the Connector will automatically create it; by default, stopping the job will not delete the Slot. Multiple jobs cannot share the same Slot.

When using `pgoutput`, the Connector can automatically create a Publication based on the Debezium Publication configuration. If the Publication already exists, it will use the existing definition. Automatic creation requires the database `CREATE` privilege. It also requires the necessary privileges on the target tables. In production environments, you can create the Slot and Publication in advance. This enables stricter permission and lifecycle management.

<span id="58195450"></span>
### Schema Change

When `schema-change.enabled: true` and the decoding plugin is `pgoutput`, the Source will compare `pgoutput` Relation messages with the cached Schema. This helps infer events such as adding, dropping, renaming columns, and modifying column types. The Pipeline uses the `lenient` mode by default to convert schema changes in a way that avoids data loss. Whether this can actually be executed downstream still depends on the Schema Evolution capabilities of the Sink. TRUNCATE TABLE and DROP TABLE events are ignored.

<span id="5b501807"></span>
## Validation and Troubleshooting

<span id="b4f00e50"></span>
### Validation Methods


1. Verify PostgreSQL `wal_level`, Replication Slot, Publication, user privileges, and network connectivity.

2. Submit the job and confirm it enters the running state. Observe the snapshot\-related metrics to ensure the process gradually completes.

3. Perform INSERT, UPDATE, and DELETE operations on the test table. Confirm that the corresponding events are received downstream.

4. Perform schema changes such as adding columns or modifying column types on the test table. Confirm that downstream behavior matches `schema.change.behavior` and Sink capabilities.

5. After a successful Checkpoint, perform a controlled restart. Check whether the snapshot or WAL read position is correctly restored.

6. Query `pg_replication_slots` to confirm that the Slot is in the expected state. Ensure that `confirmed_flush_lsn` continues to advance.

7. Check PostgreSQL WAL disk usage. Ensure that there is no continuous unbounded growth when the job is stopped or encounters an exception.


<span id="f34f40eb"></span>
### Common Issues


|Symptom |Possible Cause |Recommended Solution |
|---|---|---|
|Unable to create or connect to Replication Slot |Slot name is invalid, occupied by other consumers, insufficient privileges, or the number has reached the limit. |Use a unique name containing only lowercase letters, digits, and underscores, and check `pg_replication_slots`, `REPLICATION` privileges, and slot capacity. |
|`pgoutput` failed to start reading |Insufficient privileges to create Publication, or the existing Publication does not include the target table. |Check Publication, database `CREATE` privileges, target table permissions, and table scope. |
|Snapshot read is slow |Chunk/FETCH configuration is too small, the source table lacks appropriate indexes, or the database load is high. |Check snapshot metrics, execution plans, and database load, then adjust Chunk and Fetch parameters. |
|WAL disk usage keeps increasing |The slot is not consumed for a long time, the job is abnormal, or the LSN has not advanced. |Check job status, heartbeat, checkpoint, and `restart_lsn` and `confirmed_flush_lsn` of the slot. |
|UPDATE and DELETE cannot correctly identify old rows |The table lacks a Primary Key or Replica Identity. |Set a Primary Key or appropriate `REPLICA IDENTITY` for the table. |
|No Schema Change generated after modifying the table structure |Inference is not enabled, the decoding plugin is not `pgoutput`, or the change type is not supported. |Check `schema-change.enabled`, `decoding.plugin.name`, and the change type. |
|Job error after modifying the table structure |The current Schema Change mode or downstream Sink does not support this change. |Check `schema.change.behavior`, the Schema Evolution capability of the Sink, and job error information. |
|Time field offset occurs |The `server-time-zone` or Pipeline time zone is inconsistent with the source. |Verify the PostgreSQL session time zone, `server-time-zone`, and `pipeline.local-time-zone`. |


<span id="b8fb851f"></span>
## Notes


* Each concurrently running job uses an independent Replication Slot. This prevents the Slot from being contended by multiple consumers.

* By default, Slots and Publications are not automatically deleted when the job stops. Before stopping a job for an extended period, evaluate the impact of the Slot on WAL retention and disk capacity. Do not directly delete Slots that are still in use or needed for state recovery.

* `latest-offset` and `committed-offset` will skip the snapshot. Before use, confirm that historical data has already been synchronized.

* Before making changes to production tables, evaluate the compatibility of `schema.change.behavior` and the downstream Sink. Type conversions in certain modes may alter field structures or cause data loss.

* When `schema-change.enabled` is enabled, `pgoutput` must be used. It is recommended to first validate the target DDL and downstream Sink behavior on a test table.

* TRUNCATE TABLE and DROP TABLE events are ignored. They will not trigger table clearing or deletion downstream.

* `debezium.*` and `jdbc.properties.*` will alter type, snapshot, and connection behaviors. Only use parameters that have been validated in the current version.

* Do not enter plaintext passwords in YAML; use Flink encrypted variables instead.


<span id="55f11520"></span>
## Related Documentation


* [Apache Flink CDC master：PostgreSQL Pipeline Connector](https://nightlies.apache.org/flink/flink-cdc-docs-master/docs/connectors/pipeline-connectors/postgres/)

* [Apache Flink CDC 3.4：Schema Evolution](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.4/docs/core-concept/schema-evolution/)

* [PostgreSQL: Logical Replication Configuration](https://www.postgresql.org/docs/current/logical-replication-config.html)

* [PostgreSQL: Publication and Replica Identity](https://www.postgresql.org/docs/current/logical-replication-publication.html)

* [Debezium：PostgreSQL Connector](https://debezium.io/documentation/reference/stable/connectors/postgresql.html)

* [Byteplus Flink: Postgres CDC](https://docs.byteplus.com/id/docs/flink/Postgres_CDC)
