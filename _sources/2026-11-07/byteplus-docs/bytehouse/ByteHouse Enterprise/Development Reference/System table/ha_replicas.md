---
title: "ha_replicas"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ha_replicas"
---

The system table `ha_replicas` displays the specific status of HaMergeTree tables.

<span id="aeee8905"></span>
## Column name


|**Field name** |**Data types** |**Field definitions** |
|---|---|---|
|is_leader |UInt8 |Whether this replica is a leader. |
|can_become_leader |UInt8 |Whether this replica can become a leader. |
|is_readonly |UInt8 |Whether the table is in a read\-only state. |
|is_session_expired |UInt8 |Whether the connection to Zookeeper has timed out. |
|is_lost |UInt8 |Whether this table is in the is_lost state. |
|is_offline |UInt8 |Whether this table is in the is_offline state. |
|zookeeper_path |String |The Zookeeper path. |
|replica_name |String |The replica name. |
|replica_path |String |The path of the node in Zookeeper corresponding to the table. |
|queue_size |UInt32 |The amount of unfinished log entries in the table currently. |
|clones_in_queue |UInt32 |The amount of clone_part in the unfinished log entry. clone_part will cause absolute_delay to be 864000. |
|inserts_in_queue |UInt32 |The amount of get_part in unfinished log entries. |
|merges_in_queue |UInt32 |The amount of merges in unfinished log entries. |
|part_mutations_in_queue |UInt32 |The amount of mutate_parts in unfinished log entries. |
|committed_lsn |UInt64 |The LSN that has been completed by all tables on different nodes within the shard. |
|updated_lsn |UInt64 |The completed LSN of tables on this node. |
|latest_lsn |UInt64 |The newly requested LSN for the entire shard. |
|absolute_delay |UInt64 |The delay on a node is defined as the time elapsed from the creation of the oldest unexecuted get_part or replace_range operation to the current time. Queries are routed to the node with the smallest delay value. |
|active_replicas |UInt8 |The current amount of active nodes under this shard. |
|main_log_file_status |String |Whether the status of the main log.bin of this table is healthy. |
|mirror_log_file_status |String |Whether the status of the backup log.bin file for the table is healthy. |


<span id="b0266fb2"></span>
## Example

```SQL
SELECT * FROM system.ha_replicas WHERE TABLE = 'test_table' AND DATABASE = 'test'
```


```SQL
Row 1:
──────
database:                    test
table:                       test_table
engine:                      HaMergeTree
is_leader:                   1
can_become_leader:           1
is_readonly:                 0
is_session_expired:          0
is_lost:                     0
is_offline:                  0
zookeeper_path:              /clickhouse/id/clustername/xxx/shard_0
replica_name:                192.18.x.x
replica_path:                /clickhouse/id/clustename/xxx/xxx/replicas/192.18.x.x
queue_size:                  0
clones_in_queue:             0
inserts_in_queue:            0
merges_in_queue:             0
merges_of_self:              0
part_mutations_in_queue:     0
part_mutations_of_self:      0
last_queue_update:           2025-06-09 21:22:22
queue_oldest_time:           1970-01-01 08:00:00
clones_oldest_time:          1970-01-01 08:00:00
inserts_oldest_time:         1970-01-01 08:00:00
merges_oldest_time:          1970-01-01 08:00:00
part_mutations_oldest_time:  1970-01-01 08:00:00
oldest_part_to_clone:       
oldest_part_to_get:      
oldest_part_to_merge_to:      
oldest_part_to_mutate_to:     
parts_to_check:              0
committed_lsn:               0
updated_lsn:                 0
latest_lsn:                  0
absolute_delay:              0
total_active_rows:           0
total_replicas:              2
active_replicas:             1
main_log_file_status:        Healthy
mirror_log_file_status:      Healthy
```
