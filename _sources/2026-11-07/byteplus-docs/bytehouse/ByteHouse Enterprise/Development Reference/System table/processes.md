---
title: "processes"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/processes"
---

The system table `process` is used to implement the `SHOW PROCESSLIST` query.

<span id="c818dd2e"></span>
## Column name


|**Field name** |**Data types** |**Explanation of field meanings** |
|---|---|---|
|is_initial_query |UInt8 |Query initiation types. The following values are supported:<br><br><br>* 1: The query is initiated by the client.<br><br>* 0: A query initiated by another query as part of distributed query execution. |
|user |String |The user who made the query. Keep in mind that for distributed processing, queries are sent to remote servers under the default user. The field contains the username for a specific query, not for a query that this query initiated. |
|query_id |String |Query statement ID. |
|address |IPv6 |The IP address the query was made from. The same for distributed processing. To track where a distributed query was originally made from, check `system.processes` on the query requestor server. |
|port |UInt16 |The client port the query was made from. |
|initial_user |String |The name of the user who runs the initial query (used for distributed query execution). |
|initial_query_id |String |The ID of the initial query (used for distributed query execution). |
|initial_address |IPv6 |Specify the IP address of the parent query. |
|initial_port |UInt16 |Start the client port for the parent query. |
|interface |UInt8 |The interface type for initiating a query. Supported values are as follows:<br><br><br>* 1：TCP.<br><br>* 2：HTTP. |
|os_user |String |Operating system username who runs the client. |
|client_hostname |String |Hostname of the client machine where the ByteHouse<br><br>client or another TCP client is run. |
|client_name |String |ByteHouse client or other TCP client names. |
|client_revision |UInt32 |The version of the ByteHouse client or other TCP clients. |
|client_version_major |UInt32 |The main version of the ByteHouse client or another TCP client. |
|client_version_minor |UInt32 |The minor versions of the ByteHouse client or other TCP clients. |
|client_version_patch |UInt32 |Patch component versions for the ByteHouse client and other TCP clients. |
|http_method |UInt8 |HTTP method for initiating a query. Possible values:<br><br><br>* 0: The query was launched from the TCP interface.<br><br>* 1: GET method was used.<br><br>* 2: POST method was used. |
|http_user_agent |String |HTTP header UserAgent passed in the HTTP query. |
|http_referer |String |HTTP header Referer passed in the HTTP query (contains an absolute or partial address of the page making the query). |
|forwarded_for |String |HTTP header X\-Forwarded\-For passed in the HTTP query. |
|quota_key |String |The quota key specified in quota settings. |
|elapsed |Float64 |Elapsed time since the request execution started (in seconds). |
|is_cancelled |UInt8 |Check whether it has been cancelled. The following values are supported:<br><br><br>* The query was canceled.<br><br>* 0: Query not canceled. |
|read_rows |UInt64 |Number of rows read from the table. On the requesting server, for distributed processing, this is the sum of all remote servers. |
|read_bytes |UInt64 |Number of uncompressed bytes read from the table. On the request server, for distributed processing, this is the sum of all remote servers. |
|total_rows_approx |UInt64 |Approximate value for the total number of rows to be read. On the request server, for distributed processing, this represents the sum of all remote servers. During request processing, when a new processing source becomes known, it can be updated. |
|written_rows |UInt64 |For INSERT queries, this column displays the number of rows written; for other query types, the value in this column is 0. |
|written_bytes |UInt64 |For INSERT queries, this column displays the number of bytes written (uncompressed); for other query types, the value in this column is 0. |
|memory_usage |Int64 |Amount of RAM requested. It may not include certain types of dedicated memory. Please refer to the [max_memory_usage](https://clickhouse.com/docs/operations/settings/query-complexity#settings_max_memory_usage) setting. |
|peak_memory_usage |Int64 |Peak memory usage. |
|query |String |Query texts. Regarding `INSERT`, it does not include the data to be inserted. |
|thread_ids |Array(UInt64) |Thread ID involved in query execution. |
|ProfileEvents |Map(String, UInt64) |ProfileEvents calculated for this query. |
|Settings |Map(String, String) |Configured parameters are used when running a query. |
|current_database |String |The name of the currently connected database. |
|resource_group |String |The resource group which is used during query execution. |


<span id="ff3a2316"></span>
## **Example**

```SQL
SELECT * FROM system.processes LIMIT 10 FORMAT Vertical; 
```


```SQL
Row 1:
──────
is_initial_query:     1
user:                 default
query_id:             35a360fa-3743-441d-8e1f-228c938268da
address:              ::ffff:172.23.0.1
port:                 47588
initial_user:         default
initial_query_id:     35a360fa-3743-441d-8e1f-228c938268da
initial_address:      ::ffff:172.23.0.1
initial_port:         47588
interface:            1
os_user:              bharatnc
client_hostname:      tower
client_name:          ClickHouse
client_revision:      54437
client_version_major: 20
client_version_minor: 7
client_version_patch: 2
http_method:          0
http_user_agengt:
http_referer:
forwarded_for:
quota_key:
elapsed:              0.000582537
is_cancelled:         0
read_rows:            0
read_bytes:           0
total_rows_approx:    0
written_rows:         0
written_bytes:        0
memory_usage:         0
peak_memory_usage:    0
query:                SELECT * from system.processes LIMIT 10 FORMAT Vertical;
thread_ids:           [67]
ProfileEvents:        {'Query':1,'SelectQuery':1,'ReadCompressedBytes':36,'CompressedReadBufferBlocks':1,'CompressedReadBufferBytes':10,'IOBufferAllocs':1,'IOBufferAllocBytes':89,'ContextLock':15,'RWLockAcquiredReadLocks':1}
Settings:             {'background_pool_size':'32','load_balancing':'random','allow_suspicious_low_cardinality_types':'1','distributed_aggregation_memory_efficient':'1','skip_unavailable_shards':'1','log_queries':'1','max_bytes_before_external_group_by':'20000000000','max_bytes_before_external_sort':'20000000000','allow_introspection_functions':'1'}

1 rows in set. Elapsed: 0.002 sec.
```
