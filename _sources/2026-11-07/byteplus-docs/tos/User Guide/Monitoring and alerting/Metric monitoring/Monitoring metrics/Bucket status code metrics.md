---
title: "Bucket status code metrics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-status-code-related-indicators-description"
---

This topic presents status code metrics at the TOS bucket level, which include the counts of 2xx, 3xx, 4xx and 5xx status codes, as well as queries per second (QPS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring metrics are divided into two categories: non\-billable and billable. Non\-billable metrics do not incur charges, while billable metrics do.</div>


<div data-tips="true" data-tips-type="tip">Bucket status code metrics fall under the non\-billable category. Therefore, the data they measure is exempt from billing.</div>



|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|2xxQPS |bucket_status_code |Count/Second |code, and ResourceID |Alerting, and consumption |The number of 2xx status codes returned and the QPS of the bucket |
|3xxQPS |bucket_status_code |Count/Second |code, and ResourceID |Alerting, and consumption |The number of 3xx status codes returned and the QPS of the bucket |
|4xxQPS |bucket_status_code |Count/Second |code, and ResourceID |Alerting, and consumption |The number of 4xx status codes returned and the QPS of the bucket |
|5xxQPS |bucket_status_code |Count/Second |code, and ResourceID |Alerting, and consumption |The number of 5xx status codes returned and the QPS of the bucket |
|2xxRatio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 2xx in all requests |
|3xxRatio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 3xx in all requests |
|4xxRatio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 4xx in all requests |
|5xxRatio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 5xx in all requests |
|ErrorRatio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests with a status code of 5xx out of all requests with a status code of non\-4xx |
|BucketStatusCodeReqCount |bucket_status_code |Count |code, and ResourceID |Alerting, and consumption |The number of requests with the specified status codes |
|500QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 500 status codes returned and the QPS of the bucket |
|502QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 502 status codes returned and the QPS of the bucket |
|503QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 503 status codes returned and the QPS of the bucket |
|400Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 400 in all requests |
|403Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 403 in all requests |
|404Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 404 in all requests |
|429Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 429 in all requests |
|500Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 500 in all requests |
|502Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 502 in all requests |
|503Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 503 in all requests |
|Bucket400QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 400 status codes returned and the QPS of the bucket |
|Bucket403QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 403 status codes returned and the QPS of the bucket |
|Bucket404QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 404 status codes returned and the QPS of the bucket |
|Bucket429QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 429 status codes returned and the QPS of the bucket |
|Bucket499QPS |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of 499 status codes returned and the QPS of the bucket |
|Bucket499Ratio |bucket_status_code |Percent |ResourceID |Alerting, and consumption |The percentage of requests whose status code is 499 in all requests |
|BucketGetObjectInterruption |bucket_status_code |Count/Second |ResourceID |Alerting, and consumption |The number of GetObject requests that were interrupted |


&nbsp;
