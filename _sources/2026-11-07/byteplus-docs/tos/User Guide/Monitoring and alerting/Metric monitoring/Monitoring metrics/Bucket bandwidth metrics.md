---
title: "Bucket bandwidth metrics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-bandwidth-metrics-description"
---

This topic introduces bucket bandwidth metrics that provide insights into the bandwidth usage of a specified bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring metrics are divided into two categories: non\-billable and billable. Non\-billable metrics do not incur charges, while billable metrics do.</div>


<span id="73aeb3c0"></span>
## Non\-billable metrics


|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|TotalUploadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Total upload bandwidth (unit: MB/s) |
|InternetUploadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Upload bandwidth over the public network (unit: MB/s) |
|IntranetUploadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Upload bandwidth over the private network (unit: MB/s) |
|TotalDownloadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Total download bandwidth (unit: MB/s) |
|InternetDownloadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Download bandwidth over the public network (unit: MB/s) |
|IntranetDownloadBandwidth |bandwidth |Megabytes/Second |ResourceID |Alerting, and consumption |Download bandwidth over the private network (unit: MB/s) |
|TotalUploadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Total upload bandwidth (unit: Mbit/s) |
|InternetUploadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Upload bandwidth over the public network (unit: Mbit/s) |
|IntranetUploadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Upload bandwidth over the private network (unit: Mbit/s) |
|TotalDownloadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Total download bandwidth (unit: Mbit/s) |
|InternetDownloadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Download bandwidth over the public network (unit: Mbit/s) |
|IntranetDownloadBandwidthV2 |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Download bandwidth over the private network (unit: Mbit/s) |
|AcceleratorReadCacheBandWidth |bandwidth |Megabits/Second |ResourceID |Consumption |Read cache bandwidth for TOS accelerator |
|AcceleratorPrefetchBandWidth |bandwidth |Megabits/Second |ResourceID |Consumption |Back\-to\-origin bandwidth for TOS accelerator |
|BucketAsyncFetchBandwidth |bandwidth |Mebibits/Second |ResourceID |Alerting, and consumption |Bandwidth for asynchronous fetch requests |


<span id="847c1b4a"></span>
## Billable metrics


|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|ImageProcessSize |bandwidth |Megabits/Second |ResourceID |Alerting, and consumption |Size of the images processed per second |
