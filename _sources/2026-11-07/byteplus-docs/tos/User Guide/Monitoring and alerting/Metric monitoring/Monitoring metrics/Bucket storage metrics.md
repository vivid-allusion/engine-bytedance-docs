---
title: "Bucket storage metrics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-capacity-related-indicators-description"
---

This topic covers storage metrics at the bucket level, including the total amount of data in a bucket and the amount of data stored in Standard Storage.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring metrics are divided into two categories: non\-billable and billable. Non\-billable metrics do not incur charges, while billable metrics do.</div>


<div data-tips="true" data-tips-type="tip">Bucket storage metrics fall under the non\-billable category. Therefore, the data they measure is exempt from billing.</div>



|Metric name |SubNamespace |Metric unit |Dimension |Purpose |Description |
|---|---|---|---|---|---|
|TotalStorage |storage |Gibibytes |ResourceID |Alerting, and consumption |The total amount of data that is stored in a bucket |
|StandardStorage |storage |Gibibytes |ResourceID |Alerting, and consumption |The amount of data that is stored in Standard Storage |
|InfrequentAccessStorage |storage |Gibibytes |ResourceID |Alerting, and consumption |The amount of data that is stored in Infrequent Access Storage |
