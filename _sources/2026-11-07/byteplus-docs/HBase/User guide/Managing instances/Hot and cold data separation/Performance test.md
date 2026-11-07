---
title: "Performance test"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Performance_test"
---

HBase provides Capacity storage as a cold storage medium to effectively reduce storage costs. This article introduces the performance test results for hot and cold data separation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Capacity storage has been enabled for the instance. For more information, see [Enabling Capacity storage](https://docs.byteplus.com/en/docs/HBase/Enabling_Capacity_storage).

<span id=".5oCn6IO95rWL6K-V"></span>
## Performance test

<span id=".546v5aKD6K-05piO"></span>
### Environmental specifications


* Master node: hbase.x2.large, 4C16G.

* 2 RegionServers: hbase.x2.2xlarge, 8C32G.

* Test machine: 4C16G.


<span id=".5YaZ5oCn6IO9"></span>
### Write performance


|Table type |avg rt |p99 rt |
|---|---|---|
|Hot table |560 us |1639 us |
|Cold table |546 us |1540 us |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each record has 10 columns, each column is 100 bytes, that is, a single row is 1KB, and 16 threads are used for writing.</div>


<span id=".6ZqP5py6LWdldC3mgKfog70="></span>
### Random Get performance


|Table type |avg rt |p99 rt |
|---|---|---|
|Hot table |417 us |2073 us |
|Cold table |18513 us |120959 us |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Disable the BlockCache of the table and read the entire disk. Each record has 10 columns, each column is 100 bytes, that is, a single row is 1KB. Read with 8 threads, fetching 1 KB per read.</div>


<span id=".6IyD5Zu0LXNjYW4t5oCn6IO9"></span>
### Range Scan performance


|Table type |avg rt |p99 rt |
|---|---|---|
|Hot table |1584 us |5307 us |
|Cold table |42447 us |206975 us |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Disable BlockCache for the table. Each record has 10 columns, each column is 100 bytes, and each row is 1KB. Read with 8 threads, fetching 1 KB per read. The Scan Caching setting is 30.</div>


<span id=".5oiQ5pys5pS255uK5YiG5p6Q"></span>
## Cost\-benefit analysis

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following examples do not take into account any product discounts and are for reference only. Please refer to the actual business invoice for details.</div>


Currently, HBase hot storage provides HDD and SSD storage types. The detailed prices are as follows:


|Storage type |Pay\-as\-you\-go（USD/Hour/GiB） |Yearly/monthly subscription（USD/Month/GiB） |
|---|---|---|
|HDD file storage |0.0015 |0.7 |
|SSD file storage |0.0042 |2 |
|Capacity storage |0.00020625 |0.099 |


Example: Taking a storage capacity of 20,000 GiB as an example, the prices for using HDD storage and Capacity storage for one month (30 days) are as follows.


|Storage type |Pay\-as\-you\-go |Subscription |
|---|---|---|
|HDD storage |**21600 USD** = 0.0015 USD/Hour/GiB × 20,000GiB × 24 Hours × 30 |**14000 USD** = 0.7 USD/Month/GiB × 20,000GiB × 1 Month |
|Capacity storage |**2970 USD** = 0.00020625 USD/Hour/GiB × 20,000GiB × 24 Hours × 30 |**1980 USD** = 0.099 USD/Month/GiB × 20,000GiB × 1 Month |


As can be seen from the above example, for the cost of storing 20,000 GiB, Capacity storage is relatively more affordable than HDD storage, which can effectively reduce storage costs.
