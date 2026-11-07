---
title: "Bucket QPS metrics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-qps-related-indicators-description"
---

This topic discusses metrics related to queries per second (QPS) at the bucket level. These metrics offer insights into TOS performance, categorized by request type including GetObject and PutObject.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring metrics are divided into two categories: non\-billable and billable. Non\-billable metrics do not incur charges, while billable metrics do.</div>


<span id="2d41d380"></span>
## Non\-billable metrics


|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|GetObjectQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for GetObject requests |
|PutObjectQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for PutObject requests |
|ListObjectsQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for ListObjects requests |
|HeadObjectQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for HeadObject requests |
|UploadPartQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for UploadPart requests |
|DeleteObjectQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for DeleteObject requests |
|PostObjectQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for PostObject requests |
|DeleteObjectsQps |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for DeleteObjects requests |
|AcceleratorReadQPS |qps |Count/Second |ResourceID |Consumption |QPS for TOS Accelerator read requests |
|BucketAsyncFetchQPS |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for asynchronous fetch requests |
|BucketAsyncFetchSuccessQPS |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for successful asynchronous fetch requests |
|BucketAsyncFetchFailedQPS |qps |Count/Second |ResourceID and ErrorCode (optional) |Alerting, and consumption |QPS for failed asynchronous fetch requests |


<span id="49136540"></span>
## Billable metrics


|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|VideoProcessCount |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for video processing requests |
|ImageInspectRequestNum |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for image inspection requests |
|AdvImageProcLowCount |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for requests to process low specs images using the advanced image compression feature |
|AdvImageProcMedCount |qps |Count/Second |ResourceID |Alerting, and consumption |QPS for requests to process high specs images using the advanced image compression feature |
