---
title: "Monitoring and alarm metrics"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Monitoring_and_alarm_metrics"
---

This topic describes monitoring and alarm metrics supported by Milvus for VectorDB.

<span id="RZX8kkP0"></span>
## Monitoring metrics

Milvus for VectorDB displays monitoring information for the following indicators on the instance's **Monitoring overview** page, helping you keep track of the instance's operation status in a timely manner.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For information about how to view monitoring information, see <a href="https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_monitoring_information">View instance monitoring information</a>.</div>



<Tabs>
<Tab zoneid="Uah6zAAuzR" title="Dedicated instance">
<TabTitle>Dedicated instance</TabTitle>


|**Metric Name** |**MetricName**<br><br> |**Unit** |**Dimension** |**Subnamespace**<br><br> |**Description** |**Supported dimension** |
|---|---|---|---|---|---|---|
|Read QPS |ReadQPS |times/second |Performance |performance |Number of read requests per second, including search and query requests. |Instance |
|Read VPS |ReadVPS |per second |Performance |performance |Number of vector search requests per second. VPS does not apply to query requests because query operations do not involve vectors. |Instance |
|Read Latency P99 |ReadLatencyP99 |Millisecond |Performance<br><br> |performance |The latency between a client sending a read request, such as query or search request,  to the server and the client receiving the response, measured at the 99th percentile. |Instance |
|Write QPS<br><br> |WriteQPS |times/second |Performance |performance |Number of write requests per second, including insert, bulk insert, upsert, and delete requests. |Instance |
|Write VPS |(Including 3 metrics)<br><br>InsertVPS, UpsertVPS, andDeleteVPS |per second |Performance |performance |The number of vector write requests per second, including insert, upsert, and delete requests. |Instance |
|Write Latency P99 |WriteLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a write request, such as insert, bulk insert, upsert, or delete request, to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Read Failures<br><br> |ReadFailureCnt |\-<br><br> |Performance |performance |Number of failed search and query requests.<br><br> |Instance |
|Write Failures |WriteFailureCnt |\- |Performance |performance |Number of failed requests, including insert, delete, upsert, and bulk insert requests. |Instance |
|Collection Number |CollectionNum |\- |Data |meta |Number of collections created in the cluster. |Instance |
|Entity Number |EntityNum |\- |Data |meta |Total number of entities inserted in the cluster. |Instance |
|Memory usage. |Memory_Usage |byte |Resource |resource |Actual physical memory size used by the node. |Node |
|Memory usage |NodeMemoryUsage |% |Resource |resource |Node memory usage. |Node |
|CPU usage |NodeCpuUsage |% |Resource |resource |CPU usage of the node. |Node |
|Data storage usage |TOSUsage |GB |Resource |resource |Data storage usage. |Instance |
|Read request QPS |ReadRequestQPS |per second |Collections |collection |Read request QPS, including Search and Query. |Collection |
|Read failed requests |ReadRequestFailureCnt |\- |Collections |collection |Number of failed search and query requests. |Collection |
|Read request P99 latency |ReadRequestLatencyP99 |Millisecond |Collections |collection |Take the maximum P99 of Search and Query requests. |Collection |
|Average latency for read requests |ReadRequestLatencyAvg |Millisecond |Collections |collection |Average read request latency, including Search and Query requests. |Collection |
|Search request VPS |SearchRequestVPSV2 |per second |Collections |collection |Number of vector search requests per second in Search requests. |Collection |
|Write request QPS |WriteRequestQPS |per second |Collections |collection |Write request QPS, including Insert, Upsert, Delete, ImportV2. |Collection |
|Write failed requests |WriteRequestFailureCnt |\- |Collections |collection |Number of failed write requests, including Insert, Delete, Upsert, and ImportV2. |Collection |
|P99 write request latency |WriteRequestLatencyP99 |Millisecond |Collections |collection |Take the P99 maximum value of Insert, Upsert, and Delete requests. |Collection |
|write request average latency |WriteRequestLatencyAvg |Millisecond |Collections |collection |Write the average request latency, including Insert, Delete, and Upsert. |Collection |
|Insert request VPS |InsertRequestVPS |per second |Collections |collection |Number of vector insert requests per second. |Collection |
|Upsert request VPS |UpsertRequestVPS |per second |Collections |collection |Number of vectors per second for Upsert requests. |Collection |
|Delete request VPS |DeleteRequestVPS |per second |Collections |collection |Delete request vector count per second. |Collection |
|Index file storage size |DataCoordStoredIndexFilesSize |byte |Collections |collection |Index file storage size. |Collection |
|Number of Partitions |NumOfPartition |\- |Collections |collection |The number of partitions in this Collection. |Collection |
|Segment quantity |DataCoordSegmentNum |\- |Collections |collection |The total number of segments in this Collection. |Collection |
|Binlog storage size |StoredBinlogSizeV2 |byte |Collections |collection |Binlog storage size. |Collection |
|Data count |CollectionEntityNum |\- |Collections |collection |Number of data entries in this Collection. |Collection |



</Tab>
<Tab zoneid="fuJy1KIdeX" title="Serverless instance">
<TabTitle>Serverless instance</TabTitle>


|**Metric Name** |**MetricName**<br><br> |**Unit** |**Dimension** |**Subnamespace**<br><br> |**Description** |**Supported dimension** |
|---|---|---|---|---|---|---|
|Read QPS |ReadQPS |times/second |Performance |performance |Number of read requests per second, including search and query requests. |Instance |
|Read VPS |ReadVPS |per second |Performance |performance |Number of vector search requests per second. VPS does not apply to query requests because query operations do not involve vectors. |Instance |
|Read Latency P99 |ReadLatencyP99 |Millisecond |Performance<br><br> |performance |The latency between a client sending a read request, such as query or search request,  to the server and the client receiving the response, measured at the 99th percentile. |Instance |
|Write QPS<br><br> |WriteQPS |times/second |Performance |performance |Number of write requests per second, including insert, bulk insert, upsert, and delete requests. |Instance |
|Write VPS |(Including 3 metrics)<br><br>InsertVPS, UpsertVPS, andDeleteVPS |per second |Performance |performance |The number of vector write requests per second, including insert, upsert, and delete requests. |Instance |
|Write Latency P99 |WriteLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a write request, such as insert, bulk insert, upsert, or delete request, to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Read Failures<br><br> |ReadFailureCnt |\-<br><br> |Performance |performance |Number of failed search and query requests.<br><br> |Instance |
|Write Failures |WriteFailureCnt |\- |Performance |performance |Number of failed requests, including insert, delete, upsert, and bulk insert requests. |Instance |
|Collection Number |CollectionNum |\- |Data |meta |Number of collections created in the cluster. |Instance |
|Entity Number |EntityNum |\- |Data |meta |Total number of entities inserted in the cluster. |Instance |
|Memory usage. |Memory_Usage |byte |Resource |resource |Actual physical memory size used by the node. |Node |
|Data storage usage |TOSUsage |GB |Resource |resource |Data storage usage. |Instance |
|Read QPS |ReadRequestQPS |per second |Collections |collection |Read request QPS, including Search and Query. |Collection |
|Read failed requests |ReadRequestFailureCnt |\- |Collections |collection |Number of failed search and query requests. |Collection |
|Read request P99 latency |ReadRequestLatencyP99 |Millisecond |Collections |collection |Get the P99 maximum value of Search and Query requests. |Collection |
|Average read request latency |ReadRequestLatencyAvg |Millisecond |Collections |collection |Average read request latency, including Search and Query requests. |Collection |
|Search request VPS |SearchRequestVPSV2 |per second |Collections |collection |Vector count per second in Search requests. |Collection |
|Write QPS |WriteRequestQPS |per second |Collections |collection |Write request QPS, including Insert, Upsert, Delete, and ImportV2. |Collection |
|write failed requests |WriteRequestFailureCnt |\- |Collections |collection |Number of failed write requests, including insert, delete, upsert, and ImportV2. |Collection |
|write request P99 latency |WriteRequestLatencyP99 |Millisecond |Collections |collection |Obtain the P99 maximum value for Insert, Upsert, and Delete requests. |Collection |
|write request average latency |WriteRequestLatencyAvg |Millisecond |Collections |collection |Average write request latency, including Insert, Delete, and Upsert. |Collection |
|Insert request VPS |InsertRequestVPS |per second |Collections |collection |The number of vectors per second for insert requests. |Collection |
|Upsert request VPS |UpsertRequestVPS |per second |Collections |collection |Number of Vectors per second for Upsert requests. |Collection |
|Delete VPS request |DeleteRequestVPS |per second |Collections |collection |The number of vectors per second for Delete requests. |Collection |
|Index file storage size |DataCoordStoredIndexFilesSize |byte |Collections |collection |Index file storage size. |Collection |
|Binlog storage size |StoredBinlogSizeV2 |byte |Collections |collection |Binlog storage size. |Collection |
|Data count |CollectionEntityNum |\- |Collections |collection |The number of data entries in this collection. |Collection |





</Tab>
</Tabs>


<span id="dqH1axPm"></span>
## Alarm metrics

To help you understand changes in the instance's status in a timely manner, Milvus for VectorDB allows you to configure alarm policies for the following metrics, so that you can receive notifications when the status changes. You can also view the alarm history of instances in the current region on the Alarm history page. For more information, see [View alarm history](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_alarm_history).


<Tabs>
<Tab zoneid="u5ulbv9gW6" title="Dedicated instance">
<TabTitle>Dedicated instance</TabTitle>


|**Alarm metrics** |**MetricName** |**Unit** |**Dimension** |**Subnamespace** |**Description** |**Supported dimension** |
|---|---|---|---|---|---|---|
|Search Latency P99 |SearchLatencyP99 |Millisecond |Performance |performance |The latency between the client sending a search request to the server and the client receiving the response, measured at the 99th percentile. |Instance |
|Query Latency P99 |QueryLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a query request to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Write Latency P99 |WriteLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a write request, such as insert, bulk insert, upsert, or delete request, to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Number of failed read requests. |ReadFailureCnt |\- |Performance |performance |Number of failed search and query requests. |Instance |
|Number of failed write requests |WriteFailureCnt |\- |Performance |performance |The number of failed write requests, including insert, delete, upsert, and bulk insert requests.. |Instance |
|Node memory usage rate. |NodeMemoryUsage |% |Resource |resource |Node memory usage. |Node |
|Node CPU usage |NodeCpuUsage |% |Resource |resource |CPU usage of the node. |Node |



</Tab>
<Tab zoneid="q3xRFRJkYY" title="Serverless instance">
<TabTitle>Serverless instance</TabTitle>


|**Alarm metrics** |**MetricName** |**Unit** |**Dimension** |**Subnamespace** |**Description** |**Supported dimension** |
|---|---|---|---|---|---|---|
|Search Latency P99 |SearchLatencyP99 |Millisecond |Performance |performance |The latency between the client sending a search request to the server and the client receiving the response, measured at the 99th percentile. |Instance |
|Query Latency P99 |QueryLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a query request to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Write Latency P99 |WriteLatencyP99 |Millisecond |Performance |performance |The latency between a client sending a write request, such as insert, bulk insert, upsert, or delete request, to the server and the client receiving a response, measured at the 99th percentile. |Instance |
|Number of failed read requests. |ReadFailureCnt |\- |Performance |performance |Number of failed search and query requests. |Instance |
|Number of failed write requests |WriteFailureCnt |\- |Performance |performance |The number of failed write requests, including insert, delete, upsert, and bulk insert requests.. |Instance |



</Tab>
</Tabs>
