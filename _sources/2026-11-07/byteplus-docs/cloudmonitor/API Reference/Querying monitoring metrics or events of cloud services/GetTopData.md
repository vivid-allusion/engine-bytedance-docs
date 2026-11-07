---
title: "GetTopData"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/GetTopData"
---

Query top\-ranked entries for the specified metrics and corresponding data of other metrics under the same dimension

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A root user and their IAM users can initiate a total of at most 10 `GetTopData` API calls per second. If the QPS for this API exceeds 10, rate limiting will be triggered.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for your service region.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=GetTopData&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetTopData&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetTopData |The name of the API. The API name is `GetTopData`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|StartTime |Integer |No |1679395680 |The start time of the time range. It is a Unix timestamp (in seconds), for example, 1632904500. |
|EndTime |Integer |No |1679482080 |The end time of the time range. It is a Unix timestamp (in seconds), for example, 1632904801.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The time range cannot span more than one day (<code>EndTime - StartTime <= 1 day</code>).</div><br> |
|Namespace |String |No |VCM_NAT |The namespace of the metrics to be queried. For details, see the **Namespace** field for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|SubNamespace |String |No |client |The dimension to which the metric to be queried belongs. The SubNamespace has different values available for different namespaces. For details, see the **SubNamespace** field for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|MetricNames |Array of String |No |["client_out_bps","client_in_bps","client_conns","client_cps"] |Names of all the metrics to be queried.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 4 metrics can be queried per call.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">All metrics must be under the same dimension in the same namespace.</div><br> |
|Instances |Array of [Instance](https://docs.byteplus.com/en/docs/39/16300#instance) |No |\- |Information of metrics to be queried. |
|GroupBy |Array of String |No |["ResourceID","ClientIP"] |The grouping identifier of the metrics to be queried. It is used to group results of multiple metrics. You can include the public dimensions of all metrics to be queried in the value of this parameter. |
|OrderByMetricName |String |No |\- |The sorting metric for table queries.​ `OrderByMetricName` has different optional values for different tables. For details, see table configuration of each product.<br><br>If `OrderByMetricName` is not specified, the first metric column of the table is used for sorting. |
|TopN |Integer |No |2 |The number of top entries for the sorted metric. It must be a positive integer.<br><br><br>* When `Asc` is `true`, query the smallest N data groups based on the sorted metric.<br><br>* When `Asc` is `false`, query the largest N data groups based on the sorted metric. |
|Asc |Boolean |No |true |Sorting order of metrics.<br><br><br>* **true**: Ascending order<br><br>* **false** (default): Descending order |


<span id="instance"></span>
### Instance


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Dimensions |Array of [Dimension](https://docs.byteplus.com/en/docs/39/16300#dimension) |No |\- |Dimensions of the metric to be queried. For dimension details, see the **Dimensions** of metrics for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.<br><br><br>* Each dimension contains only one set of KV.<br><br>* When multiple dimensions exist, the logical relationship between them is "and." |


<span id="dimension"></span>
### Dimension


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |No |ResourceID |Metric key. |
|Value |String |No |eip\-13fxxxx |Value of the corresponding KEY. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=GetTopData&Version=2018-01-01
Content-Type: application/json
{
    "Namespace": "VCM_NAT",
    "SubNamespace": "client",
    "StartTime": 1679395680,
    "EndTime": 1679482080,
    "TopN": 2,
    "Asc": true,
    "GroupBy": [
        "ResourceID",
        "ClientIP"
    ],
    "Instances": [
        {
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "eip-13fxxxx"
                }
            ]
        }
    ],
    "MetricNames": [
        "client_out_bps",
        "client_in_bps",
        "client_conns",
        "client_cps"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Object of [TopNData](https://docs.byteplus.com/en/docs/39/16300#topndata) |\- |Events that meet the query criteria. |


<span id="topndata"></span>
### TopNData


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Asc |Boolean |false |Sorting order. |
|TopDataResults |Array of [GroupMetricData](https://docs.byteplus.com/en/docs/39/16300#groupmetricdata) |\- |Query results. |
|OrderByMetricName |String |client_out_bps |Metric based on which sorting is performed. |


<span id="groupmetricdata"></span>
### GroupMetricData


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|GroupKeys |JSON Map |{"ClientIP":" **.** . **.** ", "ResourceID":"ngw\*\*\*\*\*1w1f"} |Identification data of each query result group. It corresponds to the result for the `Dimension` specified by the `GroupBy` parameter in the request. |
|MetricData |JSON Map | |Metric query results for each group of the query results. It corresponds to the query results for the metrics specified in the request parameter `MetricNames`. |


<span id="tagset"></span>
### TagSet


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|key |String |ClientIP |Metric key. |
|value |String |10.\*\*.\*\*.106 |Value of the corresponding KEY. |


<span id="metricdata"></span>
### MetricData


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|key |String |client_conns |Metric key. |
|value |Any |1 |Value of the corresponding KEY. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "GetTopData",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "Asc": false,
            "OrderByMetricName": "client_out_bps",
            "TopDataResults":[
            {
                "GroupKeys":{
                    "ClientIP":"10.**.**.105",
                    "ResourceID":"ngw*****1w1f"
                },
                "MetricData":{
                    "client_conns":2.666448230668414,
                    "client_cps":0.02404980340760158,
                    "client_in_bps":6061.495849716029,
                    "client_out_bps":6514.217038007857
                }
            },
            {
                "GroupKeys":{
                    "ClientIP":"10.**.**.106",
                    "ResourceID":"ngw*****1w1f"
                },
                "MetricData":{
                    "client_conns":1,
                    "client_cps":0.00012138868657441125,
                    "client_in_bps":5906.8803107550375,
                    "client_out_bps":5907.487448409809
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

The GetTopData API cannot query the metrics listed in the table below.


|Namespace |SubNamespace |MetricNames |Description |
|---|---|---|---|
|VCM_Redis |aggregated_proxy |AggregatedNetworkTransmitThroughput |Outbound network throughput |
||aggregated_proxy |AggregatedNetworkReceiveThroughput |Inbound network throughput |
||aggregated_proxy |AggregatedTotalQps |Total QPS |
||aggregated_proxy |AggregatedReadQps |Read QPS |
||aggregated_proxy |AggregatedWriteQps |Write QPS |
||aggregated_server |AggregatedNetworkTransmitThroughput |Outbound network throughput |
||aggregated_server |AggregatedNetworkReceiveThroughput |Inbound network throughput |
||aggregated_server |AggregatedExpiredKeyPerSec |Expired keys per second |
||aggregated_server |AggregatedEvictedKeyPerSec |Number of keys evicted per second |
||aggregated_server |AggregatedTotalEvictedKey |Total number of evicted keys |
||aggregated_server |AggregatedKeyHitPerSec |Keys hit per second |
||aggregated_server |AggregatedKeyMissPerSec |Missed keys per second |
||proxy |NetworkTransmitThroughput |Outbound network throughput |
||proxy |NetworkReceiveThroughput |Inbound network throughput |
||proxy |TotalQps |Total QPS |
||proxy |ReadQps |Read QPS |
||proxy |WriteQps |Write QPS |
||server |NetworkTransmitThroughput |Outbound network throughput |
||server |NetworkReceiveThroughput |Inbound network throughput |
||server |ExpiredKeyPerSec |Expired keys per second |
||server |EvictedKeyPerSec |Number of keys evicted per second |
||server |KeyHitPerSec |Keys hit per second |
||server |KeyMissPerSec |Missed keys per second |
||server |GeoSpatialBasedCmdsQps |Geo command QPS |
||server |HashBasedCmdsQps |Hash command QPS |
||server |HyperLogLogBasedCmdsQps |Hyperloglog command QPS |
||server |KeysBasedCmdsQps |Keys command QPS |
||server |ListBasedCmdsQps |List command QPS |
||server |PubSubBasedCmdsQps |PubSub command QPS |
||server |ScriptingBasedCmdsQps |Scripting command QPS |
||server |SetBasedCmdsQps |Set command QPS |
||server |SortedSetBasedCmdsQps |SortedSet command QPS |
||server |StringBasedCmdsQps |String command QPS |
||server |StreamBasedCmdsQps |Stream command QPS |
||server |TransactionBasedCmdsQps |Transaction command QPS |
|VCM_RDS_PostgreSQL |engine_monitor |RowsInserted |Rows inserted per second |
||engine_monitor |RowsUpdated |Rows updated per second |
||engine_monitor |RowsDeleted |Rows deleted per second |
||proxy_monitor |ProxyQPS |QPS |
|VCM_veDB_MySQL |Pod |InnodbBufferDataReads |InnoDB read throughput |
||Pod |InnodbBufferDataWritten |InnoDB write throughput |
||Pod |InnodbOsDataReads |InnoDB file read frequency |
||Pod |InnodbOsDataWrites |InnoDB file write frequency |
||Pod |InnodbLogWriteRequests |InnoDB log write request frequency |
||Pod |InnodbLogWrites |Physical write frequency of InnoDB logs |
||Pod |InnodbLogFsyncs |InnoDB log fsync write frequency |
||Pod |CreateTempTableUtil |Temporary table creation rate |
|VCM_veDB_PostgreSQL |Instance |TPS |TPS |
||Instance |WalWriteQPS |WAL log write QPS |
||Pod |PageReadQPS |Storage layer page read QPS |
||Pod |LongTransactionNum |Number of slow queries |
||Pod |ReadonlySelectQPS |Read\-only QPS |
|VCM_ESCloud |operation |DeletedDocumentRate |Document deletion frequency |
||operation |IndexOps |Index OPS |
||operation |QueryOps |Query OPS |
||operation |UpdateOps |Update OPS |
||operation |MergeOps |Merge OPS |
|VCM_HBase |Cluster |ClusterNetworkTransmitThroughput |Outbound network throughput |
||Cluster |ClusterQps |QPS |
||Cluster |ClusterNetworkReceiveThroughput |Inbound network throughput |
||Cluster |ClusterTps |TPS |
||RegionServer |NetworkTransmitThroughput |Outbound network throughput |
||RegionServer |Qps |QPS |
||RegionServer |BlockCacheHitRate |BlockCache hit rate |
||RegionServer |Tps |TPS |
||RegionServer |NetworkReceiveThroughput |Inbound network throughput |
||RegionServer |AvgRpcCallRt |Average response time for RPC requests |
||RegionServer |MaxRpcCallRT |Maximum response time for RPC requests |
|VCM_BMQ |topic |inf_bmq_produce_ProducerStatsPerTopicPartition_Count |Production request QPS |
||topic |inf_bmq_proxy_fetchRequest |Consumption request QPS |
||topic |inf_bmq_server_io_MessagesInPerSec_Count |Number of production requests |
||topic |inf_bmq_proxy_fetchMessage |Messages consumed |
||topic |inf_bmq_proxy_bytes_in |Message production traffic |
||topic |inf_bmq_proxy_bytes_out |Message consumption traffic |
||ConsumerGroup_Topic |inf_bmq_group_offset |Number of consumed messages for a single topic |
|VCM_veGraph_db |Instance |TotalQps |Total QPS |
||Pod |Throughput |Throughput |
|VCM_DTS |basic_monitoring |FullTransmissionRps |Full transmission RPS |
|VCM_veDB_MySQL |Pod |SlowQueries |Slow query count |
||Pod |SelectScan |Full table scan count |
||Pod |OperationUpdate |Update count |
||Pod |InnodbRowsUpdated |InnoDB rows updated |
||Pod |OperationDelete |Deletion count |
||Pod |InnodbRowsDeleted |InnoDB rows deleted |
||Pod |OperationInsert |Insertion count |
||Pod |InnodbRowsInserted |InnoDB rows inserted |
||Pod |OperationReplace |Replacements |
||Pod |OperationCommit |Commit count |
||Pod |HandlerCommit |Internal commit count |
||Pod |OperationRollback |Number of rollbacks |
||Pod |HandlerRollback |Internal rollback count |
||Pod |TableLocksWaited |Table lock waits |
||Pod |InnodbRowLockWaits |InnoDB row lock waits |
||Pod |CreatedTmpFiles |Number of temporary files |
||Pod |CreatedTmpDiskTables |Number of temporary disk tables |
||Pod |HandlerReadRndNext |Next\-row read request count |
||Pod |InnodbBufferPoolReadRequests |Logical InnoDB reads |
||Pod |InnodbBufferPoolReads |Physical Innodb reads |
|VCM_EMR |Doris |DorisBENodeBytesReadRate |BE node read rate |
||Doris |DorisBENodeBytesWriteRate |BE node write rate |
||Doris |DorisBENodeIOTimes |BE Node IO duration |
||Pulsar |BookkeeperServerAddEntryRequestSuccessRate |Bookkeeper ADD_ENTRY request success rate |
||Pulsar |BookkeeperServerReadEntryRequestSuccessRate |Bookkeeper READ_ENTRY request success rate |
||Pulsar |BookkeeperServerAddEntryOperateSuccessRate |Bookkeeper ADD_ENTRY operation rate |
||Pulsar |BookkeeperServerReadEntryOperateSuccessRate |Bookkeeper READ_ENTRY operation rate |
||Pulsar |BookkeeperServerAddEntryRequestRate |Bookkeeper ADD_ENTRY request rate |
||Pulsar |BookkeeperServerReadEntryRequestRate |Bookkeeper READ_ENTRY request rate |
|VCM_CFS |DanceDN |bytestore_chunkserver_block_receiver_receive_bytes |Write bandwidth |
||DanceDN |bytestore_chunkserver_block_sender_send_bytes |Read bandwidth |
||DanceDN |bytestore_chunkserver_data_xceiver_write_num |Write QPS |
||DanceDN |bytestore_chunkserver_data_xceiver_read_num |Read QPS |
||DanceDN |bytestore_chunkserver_tos_store_upload_throughput |TOS write (upload) bandwidth |
||DanceDN |bytestore_chunkserver_tos_store_read_throughput |TOS read bandwidth |
||DanceDN |bytestore_chunkserver_tos_store_put_object_throughput |TOS write (put) bandwidth |
||DanceDN |bytestore_chunkserver_tos_store_object_throughput |TOS HDFS write bandwidth |
||DanceDN |bytestore_chunkserver_tos_store_acc_upload_throughput |TOS write (transparent acceleration mode) bandwidth |


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
