---
title: "Pay as you go"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/pay-as-you-go"
---

VMP supports the pay\-as\-you\-go (postpaid) billing method. The system changes fees based on the actual reported metric samples or written metric volume, generates bills per settlement cycle, and deducts the corresponding fees from your account balance. This article introduces the billing items and billing formulas for workspaces of different specifications.

<span id=".6K6h6LS56aG5"></span>
## Billing Items

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Vital Managed Service for Prometheus classifies the metrics you report into 3 types, including:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Basic metrics of cloud services</strong>: A subset of cloud service metrics that meets your basic metric observability needs for cloud services. For a detailed list of currently available basic metrics, see <a href="https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Vital-Kubernetes-Engine">Basic VKE metrics</a>, <a href="https://docs.byteplus.com/en/docs/vmp/Basic-metrics-of-API-Gateway">Basic API Gateway metrics</a>, and <a href="https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Microservices-Engine">Basic Microservices Engine metrics</a>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Cloud Service Other Metrics</strong>: All other metrics in cloud service metrics except <strong>basic metrics</strong>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Custom Metrics</strong>: User\-developed metrics or metrics from self\-buit open\-source exporters.</div>



<span id="WU1iuXHH"></span>
### Bill by written metric volume

For standard workspaces using the billing\-by\-written\-volume method, fees are accrued based on the cumulative volume of written metrics, with a daily settlement cycle. Written metric volume refers to the size of uncompressed metric samples ingested into Prometheus instances. This billing method is suitable for scenarios where metrics carry only a small number of labels.


|Storage Duration |Storage precision |Metric Classification |Free quota |Unit price for the Chinese mainland (USD/GB) |Unit price outside the Chinese mainland (USD/GB) |
|---|---|---|---|---|---|
|7 days |Raw |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |0.3 |0.45 |
|15 days |Raw |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |0.32 |0.48 |
|30 days |Raw |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |0.36 |0.54 |
|90 days |Raw |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |0.38 |0.57 |
|180 days |5 minutes |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |0.58 |0.87 |
|1 year |1 hour |Cloud Service Basic Metrics |Free of charge |Free of charge |Free of charge |
|||Cloud Service Other Metrics<br><br>Custom Metrics |50 GB/month |1.5 |2.25 |


<span id="wyXUBCzm"></span>
### Bill by reported metric samples

For standard workspaces using the billing\-by\-reported\-volume method, tiered billing is applied based on the cumulative volume of reported metrics. The cumulative cycle is daily (tiered billing is calculated on a daily basis), and the settlement cycle is hourly. Reported metric samples are the total samples collected and reported. A sample data contains the metric name, label set, sampling timestamp, and value. For more details on Prometheus data formats, please refer to [Prometheus Time Series Format](https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data).


|Storage Duration |Metric Classification |Reported Metric Sample Count Range (million entries) |Unit Prices in China's Mainland Region (USD/million entries) |Unit Prices in Regions Except China's Mainland (USD/million entries) |
|---|---|---|---|---|
|15 days |Cloud Service Basic Metrics |\- |0 |0 |
||Cloud Service Other Metrics<br><br>Custom Metrics |0\-200 |0.6 |0.9 |
|||200\-800 |0.4 |0.6 |
|||800\-1,500 |0.2 |0.3 |
|||above 1,500 |0.15 |0.225 |
|30 days |Cloud Service Basic Metrics |0\-200 |0.16 |0.24 |
|||200\-800 |0.14 |0.21 |
|||800\-1,500 |0.12 |0.18 |
|||above 1,500 |0.1 |0.15 |
||Cloud Service Other Metrics<br><br>Custom Metrics |0\-200 |0.7 |1.2 |
|||200\-800 |0.5 |0.975 |
|||800\-1,500 |0.35 |0.6 |
|||above 1,500 |0.25 |0.45 |
|90 days |Cloud Service Basic Metrics |0\-200 |0.64 |0.96 |
|||200\-800 |0.49 |0.735 |
|||800\-1,500 |0.36 |0.54 |
|||above 1,500 |0.2 |0.3 |
||Cloud Service Other Metrics<br><br>Custom Metrics |0\-200 |1.4 |2.1 |
|||200\-800 |1 |1.5 |
|||800 to 1,500 |0.6 |0.9 |
|||above 1,500 |0.28 |0.42 |
|180 days |Cloud Service Basic Metrics |0\-200 |1 |1.5 |
|||200\-800 |0.8 |1.2 |
|||800\-1,500 |0.5 |0.75 |
|||above 1,500 |0.4 |0.6 |
||Cloud Service Other Metrics<br><br>Custom Metrics |0\-200 |2 |3 |
|||200\-800 |1.5 |2.25 |
|||800\-1,500 |1 |1.5 |
|||above 1,500 |0.5 |0.75 |
|1 year |Cloud Service Basic Metrics |0\-200 |2 |3 |
|||200\-800 |1.5 |2.25 |
|||800\-1,500 |1 |1.5 |
|||above 1,500 |0.8 |1.2 |
||Cloud Service Other Metrics<br><br>Custom Metrics |0\-200 |3 |4.5 |
|||200\-800 |2 |3 |
|||800\-1,500 |1.2 |1.8 |
|||Above 1,500 |1 |1.5 |


<span id="K3hzs0iL"></span>
## Billing examples

<span id="6ZA1kFDq"></span>
### Example of billing by written metric volume

The cost calculation for standard workspaces is as follows: **Actual cost = (Volume of daily accumulated paid written metrics \- Remaining monthly free quota) × Unit price of paid metrics + Volume of written basic metrics × Unit price of basic metrics**.

If your reported metrics include basic, other, and custom metrics, different unit prices apply to each metric type.

Suppose your remaining monthly free quota is 50 GB, and your daily written metric volume in the Chinese mainland is 300 GB (including 200 GB of basic cloud service metrics and 100 GB of custom metrics), with a 30\-day data retention period. Your daily cost is as follows:

```Plain Text
Actual Cost =（100 - 50）* 0.36 + 200 * 0 = 18
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The above billing example is for reference only to help you understand the billing methods of different types of instances. Actual charges are subject to the console page.</div>


<span id="AfUMfBsM"></span>
### Example of billing by reported metric samples

The formula for calculating the cost of standard workspaces is as follows: **Instance cost = Daily cumulative tiered unit price × Reported metric samples**.

<span id=".6K6h566X56S65L6LIDE="></span>
#### Calculation Example 1

When your reported metrics include basic metrics, other metrics, and custom metrics, different unit prices apply to different metrics.

For example, suppose your daily metric reporting volume in China's mainland region is 300 million, among which: cloud service basic metrics are 200 million, custom metrics are 100 million, and the metrics need to be retained for 30 days. Then your daily cost it:

```Plain Text
Actual Cost = 200 * 0.16 + 100 * 0.7 = 102
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The above billing example is for reference only to help you understand the billing methods of different types of instances. Actual charges are subject to the console page.</div>


<span id=".6K6h566X56S65L6LIDI="></span>
#### Calculation Example 2

Vital Managed Service for Prometheus adopts a tiered billing method. When your reported metrics span different tiers, the metric quantity within each tier is calculated using the corresponding tier unit price.

For example: Suppose you report 1600 million basic metrics daily in China's mainland region, and the metrics need to be retained for 30 days. Then your daily cost it:

```Plain Text
Actual Cost = 200 × 0.16 + 600 × 0.14 + 700 × 0.12 + 100 × 0.1 = 210
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The above billing example is for reference only to help you understand the billing methods of different types of instances. Actual charges are subject to the console page.</div>
