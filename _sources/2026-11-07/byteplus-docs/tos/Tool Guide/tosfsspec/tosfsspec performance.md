---
title: "tosfsspec performance"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_performance"
---

This article primarily introduces the performance of tosfsspec in different scenarios.

<span id="0c19da9c"></span>
## Test scenarios and environment


* **Test scenarios**:

   * Write scenario: Use `open(..., 'wb')` to get a writable file handle, continuously write multiple GB\-sized objects, and compare end\-to\-end write bandwidth.

   * Read scenario: Use `open(..., 'rb')` to get a readable file handle, continuously read multiple GB\-sized objects, and compare end\-to\-end read bandwidth.

* **Test data**:

   * 1 concurrency: Write/read a total of N items, about 10GB in total.

   * 32 concurrency: Write/read a total of N items, about 10GB in total.

* **Test environment**:

   BytePlus instance specification `ecs.g3ine.24xlarge`, 96 vCPU / 384 GiB memory, 144 Gbps internal network bandwidth.


<span id="43e88bab"></span>
## Concurrent write bandwidth for large files

The table below shows the end\-to\-end bandwidth performance (unit: MB/s) of writing large files using different tools and concurrency levels.


|**Installation package** |**Concurrency** |**Write bandwidth (MB/s)**  |
|---|---|---|
|tosfsspec |1 |1933.25 |
||32 |15425.33 |
|[tosfs](https://github.com/fsspec/tosfs)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Legacy TOS fsspec implementation, not officially provided by TOS.</div><br> |1 |66.03 |
||32 |2054.13 |
|[s3fs](https://github.com/fsspec/s3fs) |1 |67.53 |
||32 |2121.28 |


<span id="93ceda28"></span>
## Concurrent read bandwidth for large files

The table below shows the end\-to\-end bandwidth performance (unit: MB/s) of reading large files under the same conditions.


|**Installation package** |**Concurrency** |**Read bandwidth (MB/s)**  |
|---|---|---|
|tosfsspec |1 |1702.18 |
||32 |10102.15 |
|[tosfs](https://github.com/fsspec/tosfs)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Legacy TOS fsspec implementation, not officially provided by TOS.</div><br> |1 |147.84 |
||32 |2189.14 |
|[s3fs](https://github.com/fsspec/s3fs) |1 |427.41 |
||32 |4586.67 |


<span id="3efff546"></span>
## Summary

tosfsspec offers higher end\-to\-end read and write bandwidth and overall performance compared to similar `fsspec` implementations. It is suitable for scenarios requiring high bandwidth access to TOS, such as data warehouse import/export, large\-scale log archiving, and machine learning training data preparation.
