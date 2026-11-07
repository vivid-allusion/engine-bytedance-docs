---
title: "Bucket latency metrics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-latency-metrics-description"
---

This topic discusses latency metrics at the bucket level. These metrics provide insight into information such as the average first\-byte latency for GET requests and the average end\-to\-end latency for PUT requests within a given bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring metrics are divided into two categories: non\-billable and billable. Non\-billable metrics do not incur charges, while billable metrics do.</div>


<div data-tips="true" data-tips-type="tip">Bucket latency metrics fall under the non\-billable category. Therefore, the data they measure is exempt from billing.</div>



|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|GetRequestFirstByteAverageLatency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average first\-byte latency of GET requests |
|PutRequestFirstByteAverageLatency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average first\-byte latency of PUT requests |
|GetRequestFirstByteP99Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile first\-byte latency of GET requests |
|GetRequestFirstByteP95Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile first\-byte latency of GET requests |
|GetRequestFirstByteP90Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile first\-byte latency of GET requests |
|PutRequestFirstByteP99Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile first\-byte latency of PUT requests |
|PutRequestFirstByteP95Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile first\-byte latency of PUT requests |
|PutRequestFirstByteP90Latency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile first\-byte latency of PUT requests |
|DownloadRequestEndToEndLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of GET requests for small objects (<=1 MB) |
|DownloadRequestEndToEndPCT99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of GET requests for small objects (<=1 MB) |
|DownloadRequestEndToEndPCT95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of GET requests for small objects (<=1 MB) |
|DownloadRequestEndToEndPCT90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of GET requests for small objects (<=1 MB) |
|UploadRequestEndToEndPCT99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of PUT requests for small objects (<=1 MB) |
|UploadRequestEndToEndPCT95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of PUT requests for small objects (<=1 MB) |
|UploadRequestEndToEndPCT90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of PUT requests for small objects (<=1 MB) |
|UploadRequestEndToEndLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of PUT requests for small objects (<=1 MB) |
|DownloadRequestEndToEndLatency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of GET requests for medium\-sized objects (1–10 MB) |
|DownloadRequestEndToEndPCT99Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of GET requests for medium\-sized objects (1–10 MB) |
|DownloadRequestEndToEndPCT95Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of GET requests for medium\-sized objects (1–10 MB) |
|DownloadRequestEndToEndPCT90Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of GET requests for medium\-sized objects (1–10 MB) |
|UploadRequestEndToEndLatency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of PUT requests for medium\-sized objects (1–10 MB) |
|UploadRequestEndToEndPCT99Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of PUT requests for medium\-sized objects (1–10 MB) |
|UploadRequestEndToEndPCT95Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of PUT requests for medium\-sized objects (1–10 MB) |
|UploadRequestEndToEndPCT90Latency_MediumObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of PUT requests for medium\-sized objects (1–10 MB) |
|DownloadRequestEndToEndLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of GET requests for large objects (\>10 MB) |
|DownloadRequestEndToEndPCT99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of GET requests for large objects (\>10 MB) |
|DownloadRequestEndToEndPCT95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of GET requests for large objects (\>10 MB) |
|DownloadRequestEndToEndPCT90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of GET requests for large objects (\>10 MB) |
|UploadRequestEndToEndLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of PUT requests for large objects (\>10 MB) |
|UploadRequestEndToEndPCT99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile end\-to\-end latency of PUT requests for large objects (\>10 MB) |
|UploadRequestEndToEndPCT95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile end\-to\-end latency of PUT requests for large objects (\>10 MB) |
|UploadRequestEndToEndPCT90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile end\-to\-end latency of PUT requests for large objects (\>10 MB) |
|GetRequestEndToEndAverageLatency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of GET requests |
|PutRequestEndToEndAverageLatency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of PUT requests |
|TotalRequestEndToEndAverageLatency |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average end\-to\-end latency of all requests |
|GetRequestNetAvgLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for small objects (<=1 MB) on the network side |
|GetRequestNetP99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for small objects (<=1 MB) on the network side |
|GetRequestNetP95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for small objects (<=1 MB) on the network side |
|GetRequestNetP90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for small objects (<=1 MB) on the network side |
|GetRequestNetAvgLatency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for medium\-sized objects (1–10 MB) on the network side |
|GetRequestNetP99Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the network side |
|GetRequestNetP95Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the network side |
|GetRequestNetP90Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the network side |
|GetRequestNetAvgLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for large objects (\>10 MB) on the network side |
|GetRequestNetP99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for large objects (\>10 MB) on the network side |
|GetRequestNetP95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for large objects (\>10 MB) on the network side |
|GetRequestNetP90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for large objects (\>10 MB) on the network side |
|PutRequestNetAvgLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for small objects (<=1 MB) on the network side |
|PutRequestNetP99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for small objects (<=1 MB) on the network side |
|PutRequestNetP95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for small objects (<=1 MB) on the network side |
|PutRequestNetP90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for small objects (<=1 MB) on the network side |
|PutRequestNetAvgLatency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for medium\-sized objects (1–10 MB) on the network side |
|PutRequestNetP99Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the network side |
|PutRequestNetP95Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the network side |
|PutRequestNetP90Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the network side |
|PutRequestNetAvgLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for large objects (\>10 MB) on the network side |
|PutRequestNetP99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for large objects (\>10 MB) on the network side |
|PutRequestNetP95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for large objects (\>10 MB) on the network side |
|PutRequestNetP90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for large objects (\>10 MB) on the network side |
|GetRequestServerAvgLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for small objects (<=1 MB) on the server side |
|GetRequestServerP99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for small objects (<=1 MB) on the server side |
|GetRequestServerP95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for small objects (<=1 MB) on the server side |
|GetRequestServerP90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for small objects (<=1 MB) on the server side |
|GetRequestServerAvgLatency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for medium\-sized objects (1–10 MB) on the server side |
|GetRequestServerP99Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the server side |
|GetRequestServerP95Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the server side |
|GetRequestServerP90Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for medium\-sized objects (1–10 MB) on the server side |
|GetRequestServerAvgLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of GET requests for large objects (\>10 MB) on the server side |
|GetRequestServerP99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of GET requests for large objects (\>10 MB) on the server side |
|GetRequestServerP95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of GET requests for large objects (\>10 MB) on the server side |
|GetRequestServerP90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of GET requests for large objects (\>10 MB) on the server side |
|PutRequestServerAvgLatency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for small objects (<=1 MB) on the server side |
|PutRequestServerP99Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for small objects (<=1 MB) on the server side |
|PutRequestServerP95Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for small objects (<=1 MB) on the server side |
|PutRequestServerP90Latency_SmallObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for small objects (<=1 MB) on the server side |
|PutRequestServerAvgLatency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for medium\-sized objects (1–10 MB) on the server side |
|PutRequestServerP99Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the server side |
|PutRequestServerP95Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the server side |
|PutRequestServerP90Latency_MiddleObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for medium\-sized objects (1–10 MB) on the server side |
|PutRequestServerAvgLatency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |Average latency of PUT requests for large objects (\>10 MB) on the server side |
|PutRequestServerP99Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |99th percentile latency of PUT requests for large objects (\>10 MB) on the server side |
|PutRequestServerP95Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |95th percentile latency of PUT requests for large objects (\>10 MB) on the server side |
|PutRequestServerP90Latency_LargeObject |bucket_latency |Millisecond |ResourceID |Alerting, and consumption |90th percentile latency of PUT requests for large objects (\>10 MB) on the server side |
|AcceleratorReadCacheLatency |bucket_latency |Millisecond |ResourceID |Consumption |Read cache latency for TOS Accelerator |
