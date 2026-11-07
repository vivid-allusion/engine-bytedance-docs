---
title: "Query circuit breaker configuration"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query-circuit-breaker-configuration"
---

System resource usage is calculated based on each query, and specific circuit breaker rules consist of many different configuration items, which need to be defined in the user profile. If the resource usage of a query reaches the threshold, it will be interrupted. ByteHouse calculates statistics based on partitions as the smallest unit (not the granularity of data rows), which means that the actual memory usage of a single query may slightly exceed the threshold.

Most limits have an `overflow_mode` configuration item, dictating the action when the limit is exceeded. It can take one of the following two values: `throw` or `break`:


* `throw` – Throws an error and stops the query when a fault occurs (default)

* `break` – Stops the query and returns the results already queried.


The following introduces a set of circuit breaker configurations for general queries:

<span id="只读-query-complexity-readonly"></span>
## Read\-only query\-complexity\-readonly


* When the value is 0, any query can be executed.

* If the value is 1, only read requests such as SELECT and SHOW can be executed.

* Requests for writing and changing settings (INSERT, SET) are prohibited. When the value is 2, read queries (SELECT, SHOW) and changing settings (SET) can be handled.


Once read\-only mode is enabled, it cannot be disabled in the current session.

When using the GET method in the HTTP interface, 'readonly = 1' is automatically set. In other words, for queries that modify data, you can only use the POST method. You may send the query itself in the POST body or URL parameters.

<span id="内存限制"></span>
## Memory Limit

After the following three memory parameters are modified, saved, and delivered in the ByteHouse Enterprise console, they will take effect dynamically without restarting ByteHouse in the backend. After modification, you can execute the command `show settings like '%memory%'` in data queries to verify the modified results.

<span id="max-memory-usage"></span>
### max_memory_usage

The maximum amount of memory for running queries on a single server. In the default configuration file, the maximum value is 10GB.

This setting does not consider the amount of memory available on the computer or the total memory. This limit applies to a single query on a single server. You can use `SHOW PROCESSLIST` to view the current memory consumption of each query. Additionally, it tracks the peak memory consumption of each query and logs it.

This parameter cannot restrict the memory usage of some aggregate function states. It does not completely restrict the memory usage of certain aggregate function states such as `min`, `max`, `any`, `anyLast`, `argMin`, `argMax`.

<span id="max-memory-usage-for-user"></span>
### max_memory_usage_for_user

The maximum amount of memory for running user queries on a single server.

The default value is defined in Settings.h. By default, the amount is unlimited (`max_memory_usage_for_user = 0`).

<span id="max-memory-usage-for-all-queries"></span>
### max_memory_usage_for_all_queries

The maximum amount of memory for running all queries on a single server.

The default value is defined in Settings.h. By default, the amount is unlimited (`max_memory_usage_for_all_queries = 0`).

<span id="读取行数限制"></span>
## Limit on number of rows read

<span id="max-rows-to-read"></span>
### max_rows_to_read

It is possible to check the following limits on each block, rather than every row. That is, the limit may be exceeded.

The maximum number of rows that can be read from a table when running a query.

<span id="max-bytes-to-read"></span>
### max_bytes_to_read

The maximum number of bytes (of uncompressed data) that can be read from a table when running a query.

<span id="read-overflow-mode"></span>
### read_overflow_mode

Setting that can be applied when the amount of data read exceeds one of the limits.


* `throw` – Throws an error and stops the query if a problem occurs (default).

* `break` – Stops the query and returns the results that have been found.


<span id="max-rows-to-group-by"></span>
### max_rows_to_group_by

The maximum number of unique keys received from aggregation. This setting allows you to limit memory consumption during aggregation.

<span id="聚合-排序限制"></span>
## Aggregation/Sorting Limitations

<span id="group-by-overflow-mode"></span>
### group_by_overflow_mode

When the number of unique keys in aggregation exceeds the limit:


* `throw` \- Throws an error when a problem occurs, and stops the query (default).

* `break` \- Stops the query and returns the results already queried.

* `any` \- Allows you to run an approximate GROUP BY. The quality of such approximations depends on the statistical nature of the data.


<span id="max-rows-to-sort"></span>
### max_rows_to_sort

Maximum number of rows before sorting.

<span id="max-bytes-to-sort"></span>
### max_bytes_to_sort

Maximum bytes before sorting.

<span id="sort-overflow-mode"></span>
### sort_overflow_mode

If the number of rows received before sorting exceeds one of these limits:


* `throw` \- Throws an error when an error occurs, and the query stops (default).

* `break` \- Stops the query, returning the results already queried.


<span id="行数限制"></span>
#### Row count limit

<span id="max-result-rows"></span>
### max_result_rows

Limit the number of rows in the results.

This limit also checks subqueries and distributed queries.

<span id="max-result-bytes"></span>
### max_result_bytes

Limit the number of bytes in the results.

<span id="result-overflow-mode"></span>
### result_overflow_mode

What to do if the result exceeds one of the limits:


* `throw` – Throw an error and stop the query when an error occurs (default).

* `break` – Stop the query and return the results already obtained.


<span id="查询时间限制："></span>
## Query time limit:

<span id="max-execution-time"></span>
#### max_execution_time

Maximum query execution time (in seconds).

At this time, one of the sorting stages is not checked, nor is it checked during merging and finalizing the aggregation functions.

<span id="timeout-overflow-mode"></span>
#### timeout_overflow_mode

If the query runtime exceeds 'max_execution_time': 'throw' or 'break', the default value is: throw.

<span id="查询速率限制"></span>
### Query Rate Limit

<span id="min-execution-speed"></span>
#### min_execution_speed

Minimum execution speed in rows per second. The 'timeout_before_checking_execution_speed' expires when checking each data block. If the execution speed is low, an exception will be raised.

<span id="timeout-before-checking-execution-speed"></span>
#### timeout_before_checking_execution_speed

Check if the execution speed is too slow (not less than 'min_execution_speed'), after the specified time in seconds has expired.

<span id="列读取限制"></span>
##### Column Read Limits

<span id="max-columns-to-read"></span>
###### max_columns_to_read

The maximum number of columns that can be read from a table in a single query. If the query requires reading more columns, an exception will be raised.

<span id="max-temporary-columns"></span>
#### max_temporary_columns

The maximum number of temporary columns that must be retained in memory during a query execution, including constant columns. If there are more temporary columns than this, it will raise an exception.

<span id="max-temporary-non-const-column"></span>
#### max_temporary_non_const_column

The maximum number of temporary columns that must be retained in memory during a query execution, excluding constant columns.

Please note that constant columns are often formed during query execution, but they generally do not require computational resources.

<span id="查询深度限制"></span>
### Query depth limit

<span id="max-subquery-depth"></span>
#### max_subquery_depth

Maximum subquery nesting depth. If the subquery is deeper, an exception will be raised. By default, 100.

<span id="max-pipeline-depth"></span>
#### max_pipeline_depth

Maximum pipeline depth. Corresponds to the number of transformations each data block undergoes during query processing. Calculated within the limit range of a single server. If the pipeline depth is greater, an exception will be raised. By default, 1000.

<span id="max-ast-depth"></span>
#### max_ast_depth

Check the maximum nesting depth of the syntax tree. If exceeded, an exception will be raised. At this time, it will not be checked during the parsing process, but only after the query has been parsed. That is, a syntax tree that is too deep can be created during the analysis process, but the query will fail. By default, 1000.

<span id="max-ast-elements"></span>
#### max_ast_elements

The maximum number of elements in the query syntax tree. If exceeded, an exception will be raised. Similar to the previous setting, it is only checked after the query has been parsed. By default, 50,000.

<span id="set-查询限制"></span>
### Set Query Limitations

<span id="max-rows-in-set"></span>
#### max_rows_in_set

The maximum number of rows in the dataset created from the IN clause in a subquery.

<span id="max-bytes-in-set"></span>
#### max_bytes_in_set

The maximum number of bytes (uncompressed data) used by the set created from the IN clause in a subquery.

<span id="set-overflow-mode"></span>
#### set_overflow_mode

When the amount of data exceeds one of the limits:


* `throw` – Stops the query and raises an error if there's an issue (default).

* `break` – Stops the query and returns the results obtained so far.


<span id="distinct-查询限制"></span>
### Distinct Query Limitations

<span id="max-rows-in-distinct"></span>
#### max_rows_in_distinct

Maximum number of different rows when using DISTINCT.

<span id="max-bytes-in-distinct"></span>
#### max_bytes_in_distinct

Maximum number of bytes used by the hash table when using DISTINCT.

<span id="distinct-overflow-mode"></span>
#### distinct_overflow_mode

When data exceeds one of the limits:


* `throw` \- Throws an error and stops the query (default)

* `break` \- Stops the query and returns the results obtained.


<span id="global-in-查询限制"></span>
### Global in search limits

<span id="max-rows-to-transfer"></span>
#### max_rows_to_transfer

When using GLOBAL IN, the maximum number of rows that can be transferred to a remote server or saved in a temporary table.

<span id="max-bytes-to-transfer"></span>
#### max_bytes_to_transfer

When using GLOBAL IN, the maximum number of bytes (uncompressed data) that can be transferred to a remote server or saved in a temporary table.

<span id="transfer-overflow-mode"></span>
#### transfer_overflow_mode

When the data volume exceeds one of the limits:


* `throw` – When an error occurs, throw an exception and the search stops (default)

* `break` – Stop the search and return the results that have been found.


<span id="join-查询限制"></span>
### Join search limits

<span id="max-rows-in-join"></span>
#### max_rows_in_join

During a join search, limit the number of rows in the hash table.

<span id="max-bytes-in-join"></span>
#### max_bytes_in_join

In join queries, limit the size of the hash table.

<span id="join-overflow-mode"></span>
#### join_overflow_mode

When the join data exceeds one of the limits:


* `Throw` – In case of an error, it throws an exception and the query stops (default)

* `Break` – Stops the query and returns the results already obtained.


<span id="max-bytes-before-external-group-by"></span>
#### max_bytes_before_external_group_by

Limit the use of additional memory by `GROUP BY`.

Acceptable parameters:


* Non\-zero – The extra memory size used by `GROUP BY`.

* `GROUP BY` inactivates memory. (Default)
