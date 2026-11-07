---
title: "HDFS external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-hdfs-external-table"
---

This engine offers integration with the [Apache Hadoop](https://en.wikipedia.org/wiki/Apache_Hadoop) ecosystem, allowing management of data on [HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html) through ByteHouse / ClickHouse. This engine is similar to [File](https://clickhouse.com/docs/engines/table-engines/special/file#table_engines-file) and [URL](https://clickhouse.com/docs/engines/table-engines/special/url#table_engines-url) engines, but provides specific features of Hadoop.
<span id="f341de6a"></span>
## Usage
```SQL
ENGINE = HDFS(URI, format)
```

The `URI` parameter is the URI of the entire file in HDFS. The `format` parameter specifies an available file format. When executing `SELECT` queries, the format must support input, and when executing `INSERT` queries, the format must support output. You can view the available formats in the [Format](https://clickhouse.com/docs/interfaces/formats#formats) section. The path part of `URI` may contain glob wildcard characters. In this case, the table will be read-only.
**Example:**
**1.** Set `hdfs_engine_table` table:
```SQL
CREATE TABLE hdfs_engine_table (name String, value UInt32) ENGINE=HDFS('hdfs://hdfs1:9000/other_storage', 'TSV')
```

**2.** Populate file:
```SQL
INSERT INTO hdfs_engine_table VALUES ('one', 1), ('two', 2), ('three', 3)
```

**3.** Query data:
```SQL
SELECT * FROM hdfs_engine_table LIMIT 2
```

```Plain
┌─name─┬─value─┐
│ one  │     1 │
│ two  │     2 │
└──────┴───────┘
```

<span id="2c236c12"></span>
## Implementation details

* Reading and writing can be parallel
* Not supported:
   * `ALTER` and `SELECT...SAMPLE` actions.
   * Indexes.
   * Copy.

**Wildcard Character in Path**
Multiple path components can include globs. For the files being processed, they should exist and match the entire path pattern. File list determination is done at the time of `SELECT` (not at the time of `CREATE`).

* `*` replaces any number of any characters, except `/` and an empty string.
* `?` Replaces any single character.
* `{some_string,another_string,yet_another_one}` replaces any of the strings `'some_string', 'another_string', 'yet_another_one'`.
* `{N..M}` replaces any number within the range from N to M, including both boundary values.

The structure with `{}` is similar to [remote](https://clickhouse.com/docs/sql-reference/table-functions/remote) table functions.
**Example**
Assume we have several files in TSV format on HDFS, with the following URIs:

* ‘hdfs://hdfs1:9000/some_dir/some_file_1’
* ‘hdfs://hdfs1:9000/some_dir/some_file_2’
* ‘hdfs://hdfs1:9000/some_dir/some_file_3’
* ‘hdfs://hdfs1:9000/another_dir/some_file_1’
* ‘hdfs://hdfs1:9000/another_dir/some_file_2’
* ‘hdfs://hdfs1:9000/another_dir/some_file_3’
1. There are several methods to create a table consisting of all six files:

```SQL
CREATE TABLE table_with_range (name String, value UInt32) ENGINE = HDFS('hdfs://hdfs1:9000/{some,another}_dir/some_file_{1..3}', 'TSV')
```

Another method:
```SQL
CREATE TABLE table_with_question_mark (name String, value UInt32) ENGINE = HDFS('hdfs://hdfs1:9000/{some,another}_dir/some_file_?', 'TSV')
```

The table consists of all files from two directories (all files must satisfy the formats and patterns described in the query):
```SQL
CREATE TABLE table_with_asterisk (name String, value UInt32) ENGINE = HDFS('hdfs://hdfs1:9000/{some,another}_dir/*', 'TSV')
```

:::danger
If the file list contains numerical ranges with leading zeros, use constructions with braces or a `?` separately.
:::
**Example**
Creating a table with files named `file000`, `file001`, … , `file999`:
```SQL
CREARE TABLE big_table (name String, value UInt32) ENGINE = HDFS('hdfs://hdfs1:9000/big_dir/file{0..9}{0..9}{0..9}', 'CSV')
```

<span id="776fc943"></span>
## Configuration
Similar to GraphiteMergeTree, the HDFS engine supports enhanced configuration using the ClickHouse configuration file. There are two configuration keys available: global (`hdfs`) and user level (`hdfs_*`). Global configurations take effect first, followed by user-level configurations (if they exist).
```XML
 
  <hdfs>
        <hadoop_kerberos_keytab>/tmp/keytab/clickhouse.keytabhadoop_kerberos_keytab>
        <hadoop_kerberos_principal>clickuser@TEST.CLICKHOUSE.TECHhadoop_kerberos_principal>
        <hadoop_security_authentication>kerberoshadoop_security_authentication>
  hdfs>

  
  <hdfs_root>
        <hadoop_kerberos_principal>root@TEST.CLICKHOUSE.TECHhadoop_kerberos_principal>
  hdfs_root>
```

<span id="b1e44e4f"></span>
### List of optional configuration options and their default values
<span id="1dde6cb9"></span>
#### Supported by libhdfs3

| | | \
|**Parameter** |**Default** |
|---|---|
| | | \
|rpc_client_connect_tcpnodelay |true |
| | | \
|dfs_client_read_shortcircuit |true |
| | | \
|output_replace-datanode-on-failure |true |
| | | \
|input_notretry-another-node |false |
| | | \
|input_localread_mappedfile |true |
| | | \
|dfs_client_use_legacy_blockreader_local |false |
| | | \
|rpc_client_ping_interval |10 * 1000 |
| | | \
|rpc_client_connect_timeout |600 * 1000 |
| | | \
|rpc_client_read_timeout |3600 * 1000 |
| | | \
|rpc_client_write_timeout |3600 * 1000 |
| | | \
|rpc_client_socket_linger_timeout |-1 |
| | | \
|rpc_client_connect_retry |10 |
| | | \
|rpc_client_timeout |3600 * 1000 |
| | | \
|dfs_default_replica |3 |
| | | \
|input_connect_timeout |600 * 1000 |
| | | \
|input_read_timeout |3600 * 1000 |
| | | \
|input_write_timeout |3600 * 1000 |
| | | \
|input_localread_default_buffersize |1 *1024* 1024 |
| | | \
|dfs_prefetchsize |10 |
| | | \
|input_read_getblockinfo_retry |3 |
| | | \
|input_localread_blockinfo_cachesize |1000 |
| | | \
|input_read_max_retry |60 |
| | | \
|output_default_chunksize |512 |
| | | \
|output_default_packetsize |64 * 1024 |
| | | \
|output_default_write_retry |10 |
| | | \
|output_connect_timeout |600 * 1000 |
| | | \
|output_read_timeout |3600 * 1000 |
| | | \
|output_write_timeout |3600 * 1000 |
| | | \
|output_close_timeout |3600 * 1000 |
| | | \
|output_packetpool_size |1024 |
| | | \
|output_heartbeat_interval |10 * 1000 |
| | | \
|dfs_client_failover_max_attempts |15 |
| | | \
|dfs_client_read_shortcircuit_streams_cache_size |256 |
| | | \
|dfs_client_socketcache_expiryMsec |3000 |
| | | \
|dfs_client_socketcache_capacity |16 |
| | | \
|dfs_default_blocksize |64 *1024* 1024 |
| | | \
|dfs_default_uri |"hdfs://localhost:9000" |
| | | \
|hadoop_security_authentication |"simple" |
| | | \
|hadoop_security_kerberos_ticket_cache_path |"" |
| | | \
|dfs_client_log_severity |"INFO" |
| | | \
|dfs_domain_socket_path |"" |

<span id="14eb0e35"></span>
#### ClickHouse Additional Configuration

| | | \
|**Param** |**Default** |
|---|---|
| | | \
|hadoop_kerberos_keytab |"" |
| | | \
|hadoop_kerberos_principal |"" |
| | | \
|libhdfs3_conf |"" |

<span id="0634e652"></span>
#### Limit

* The hadoop_security_kerberos_ticket_cache_path can only be set in the global configuration, not for specific users.

<span id="d01e13ff"></span>
## Virtual column

* `_path` — File Path.
* `_file` — File Name.
