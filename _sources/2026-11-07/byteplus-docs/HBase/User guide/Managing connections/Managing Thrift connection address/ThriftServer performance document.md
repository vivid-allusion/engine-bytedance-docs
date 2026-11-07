---
title: "ThriftServer performance document"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Thrift"
---

This document presents the benchmark results of HBase ThriftServer for both 4C8GiB and 8C16GiB specifications, helping you choose the suitable one.

<span id=""></span>
## Test environment


|**Project** |**Configuration** |
|---|---|
|Load generator |4 ECSs |
|ECS specifications |ecs.g3a.2xlarge，8 vCPU、32 GiB |
|HBase Master |2 × 8C16GiB |
|HBase RegionServer |6 × 16C64GiB |
|HBase ThriftServer |2 × 4C8GiB，2 × 8C16GiB |


<span id=""></span>
## Test tool

The test uses YCSB and the Java HBase Thrift2 Client to generate load by accessing HBase through a high\-availability Thrift endpoint.


* Four ECS instances generate load simultaneously, with each instance running 48 threads, for a total of 192 concurrent connections.

* Latency is measured by the end\-to\-end time on the client side.

* The APIs tested include Get, Put, MultiGet, MultiPut, and Scan.


<span id=""></span>
## Test model


|**Project** |**Description** |
|---|---|
|Column family |Single\-column cluster |
|Data volume |1 billion rows, approximately 400 GB before compression |
|Single\-row data |20 columns, 20 bytes per column, approximately 400 bytes/row before compression |
|RowKey distribution |100 Regions; approximately 10 million rows and 4 GB of data per Region |
|Get / Put |Read and write 1 row per call |
|MultiGet |Read 50 rows per call |
|MultiPut |Write 100 rows per call |
|Scan |50 rows |
|Test preprocessing |Completed flush and major compaction; warmed up for 20 minutes before the formal test. |


<span id=""></span>
## Test metrics


|**Metric** |**Description** |
|---|---|
|call/s |Thrift API calls completed per second |
|row/s |Rows processed per second; for batch APIs, this is calls/s × rows per call |
|avg |Average client end\-to\-end latency |
|p99 |The client\-side end\-to\-end latency for the 99th percentile is the primary latency metric for this test. |
|max |Maximum client end\-to\-end latency observed in the test window |


<span id=""></span>
## Test results: ThriftServer specs 4C8GiB

<span id=""></span>
### Throughput


|**API** |**Rows per call** |**call/s** |**row/s** |
|---|---|---|---|
|Get |1 |54,872.6 |54,872.6 |
|Put |1 |171,436.8 |171,436.8 |
|MultiGet |50 |10,487.3 |524,365 |
|MultiPut |100 |7,684.1 |768,410 |
|Scan |50 |19,286.7 |964,335 |


<span id=""></span>
### Latency


|**API** |**avg** |**p99** |**max** |
|---|---|---|---|
|Get |1.77 ms |3.84 ms |28.41 ms |
|Put |0.82 ms |1.57 ms |19.76 ms |
|MultiGet |7.46 ms |15.92 ms |61.88 ms |
|MultiPut |10.85 ms |18.63 ms |74.55 ms |
|Scan |6.32 ms |13.27 ms |49.37 ms |


<span id=""></span>
## Test results: ThriftServer specs 8C16GiB

<span id=""></span>
### Throughput


|**API** |**Rows per call** |**call/s** |**row/s** |
|---|---|---|---|
|Get |1 |89,991.1 |89,991.1 |
|Put |1 |250,297.7 |250,297.7 |
|MultiGet |50 |16,674.8 |833,740 |
|MultiPut |100 |10,988.3 |1,098,830 |
|Scan |50 |32,401.7 |1,620,085 |


<span id=""></span>
### Latency


|**API** |**avg** |**p99** |**max** |
|---|---|---|---|
|Get |1.09 ms |2.71 ms |23.68 ms |
|Put |0.57 ms |1.18 ms |16.92 ms |
|MultiGet |4.71 ms |11.34 ms |51.27 ms |
|MultiPut |7.63 ms |14.86 ms |63.41 ms |
|Scan |3.79 ms |9.18 ms |40.72 ms |


<span id=""></span>
## Recommended specifications

The 8C16GiB specification is recommended for ThriftServer. It is particularly suitable for throughput\-sensitive scenarios, those with a high proportion of batch read/write operations, strict P99 latency requirements, or expected rapid business growth.
