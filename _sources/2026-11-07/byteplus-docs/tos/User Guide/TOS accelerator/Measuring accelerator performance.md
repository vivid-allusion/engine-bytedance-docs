---
title: "Measuring accelerator performance"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Accelerator_performance_test_results"
---

This topic describes the observed performance differences when using TOS's intranet domain name versus the accelerated domain name in specific business scenarios.

<span id="AYPgIiJe"></span>
## Bulk data operations

<span id="QqxsMPin"></span>
### Test method

We tested the read performance using tosutil in two scenarios: accessing TOS via its intranet and accelerator domain names. The test dataset consisted of 10,000 100\-KB objects, totaling approximately 976 MB.

We used the tosutil `cp` command to download this set of 100\-KB objects from TOS to a local directory for both the intranet and the accelerated domain names. Then, we compared the performance metrics between the two scenarios.


* tosutil parameters: The default parameters were used.

* TOS intranet domain name: ./tosutil cp tos://accelerator\-tos\-rd\-test\-beijing\-azd/100k_files ./temp \-r.

* TOS accelerated domain name: ./tosutil cp tos://accelerator\-tos\-rd\-te\-01987847e6127cc48d150322293dafc8\-tosalias/100k_files ./temp \-r.


<span id="DlktHQRd"></span>
### Test results


|Item |Average latency (ms) |QPS |Bandwidth (MB/s) |
|---|---|---|---|
|TOS intranet domain name |7.53 |372 |36.60 |
|TOS accelerated domain name |3.17 |856 |85.14 |


Using tosutil alongside a TOS accelerator improved performance by about 2.3 times compared to not using the accelerator. The TOS accelerator can boost data transfer and access speeds for bulk data operations.

<span id="smcKmFQZ"></span>
## Big data (HNS)

<span id="L3liN00v"></span>
### Test method

We performed nnbench and DFSIO benchmark operations against both the intranet and the accelerated domain names using Hadoop with Proton. Then, we compared the key read metrics of the two scenarios.

<span id="pihB8Ntg"></span>
### nnbench test results

We used 100 maps, each accessing 5,000 objects, for a total of 500,000 1\-MB objects.


|Item |Read latency |QPS |
|---|---|---|
|TOS intranet domain name |65 ms |1,280 |
|TOS accelerated domain name |10 ms |4,982 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Read latency refers to the delay that occurs during a GetObject operation.</div>


The TOS accelerator increased QPS by nearly fourfold and reduced read latency to about one\-sixth of the value without the accelerator.

<span id="HmqlbAve"></span>
### DFSIO test results

We performed read operations on a test dataset consisting of 100 objects, each 100 MB in size.


|Item |Throughput |
|---|---|
|TOS intranet domain name |99.86 MB/s |
|TOS accelerated domain name |252.24 MB/s |


<span id="9OYpljDm"></span>
## Machine learning

<span id="WvWGqZQc"></span>
### Test method

We simulated the loading of machine learning data using the TOS Torch Connector in order to compare TOS's read performance via the intranet and the accelerated domain names. The test dataset consisted of two million images, averaging 120 KB each, for a total of approximately 228 GB.

Performance scales linearly in multi\-machine, multi\-process deployments. Here, a single\-process setup is used as an example.

Test parameters:


* batch_size: 256

* num_workers: 32

* tostorchconnector==1.1.2


<span id="kdvnFvyK"></span>
### Test results


|Test tool |Item |Average batch load latency (ms) |QPS (img/s) |Bandwidth (MB/s) |
|---|---|---|---|---|
|TOSTorchConnector |TOS intranet domain name |160.07 |1,600 |192 |
||TOS accelerated domain name |32.12 |7,936 |952 |


The TOS accelerator improved performance by about five times compared to not using it. The results indicate that, in comparable AI scenarios, leveraging the TOS accelerator can lead to enhanced throughput and reduced latency.

<span id="q1NwCaeT"></span>
## Measuring response latency during downloads

<span id="2REkhUaJ"></span>
### Test method

To test latency, we downloaded an object of about 10 MB using both the intranet and the accelerated domain names, and we recorded the response latency percentiles.

<span id="fnyUpQyh"></span>
### Test results


|Item |Average latency (ms) |P50 |P90 |P95 |P99 |
|---|---|---|---|---|---|
|TOS intranet domain name |113.555 |102.514 |137.896 |163.218 |251.795 |
|TOS accelerated domain name |28.309 |30.503 |36.927 |41.692 |61.646 |
