---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview11"
---

As next\-generation information technologies, such as AI and big data analytics, evolve rapidly, businesses are seeking faster data access speeds and higher throughput. In response, TOS has launched an accelerator feature at the availability zone level that stores frequently accessed objects on NVMe SSDs, a high\-performance storage medium. This feature provides quick responses with millisecond\-level latency and high data transfer rates for demanding business workloads.

<span id="1135bcdf"></span>
## Introduction

TOS accelerators are deeply integrated into TOS. They deliver the same strong consistency and native interface experience as standard TOS services. With two modes — **read\-only cache** and **read/write cache** — these accelerators can meet the performance and cost requirements of different business scenarios.


* **Read\-only cache**: Suitable for read\-intensive workloads. It caches hot data to significantly improve read performance. However, write acceleration is not supported, and write requests pass through to the backend storage.

* **Read/write cache**: Suitable for mixed read/write or write\-intensive workloads. Written data goes directly into the high\-speed cache and is asynchronously flushed to the backend, achieving acceleration for both reads and writes.


<span id="HeB33yux"></span>
## Benefits

TOS accelerators offer the following benefits: low latency, high throughput, high\-throughput density, strong consistency, elastic scalability, separation of storage and compute, multiple warm\-up options, and free bandwidth for data transfer.


* **Low latency**

   The accelerator enables you to deploy your data and clients within the same availability zone using NVMe SSDs, which allow for millisecond\-latency in the single digits.

* **High throughput**

   The accelerator provides a linear increase in bandwidth with capacity, delivering burst throughput of hundreds of GB/s and ensuring smooth and stable data transfer for businesses.

* **High\-throughput density**

   * In read\-only cache mode, the accelerator provides up to 300 MB/s per TiB of storage.

   * In read/write cache mode, the accelerator provides up to 125 MB/s per TiB of storage. Among these, the accelerator provides up to 125 MB/s per TiB for pure reads and up to 42 MB/s per TiB for pure writes.

* **Strong consistency**

   The accelerator automatically reloads new data whenever changes are made to TOS, ensuring that you always have access to the latest information.

* **Elastic scaling**

   The accelerator's cache capacity and provisioned bandwidth can be flexibly scaled up or down to adapt to rapidly changing business needs. Scaling up takes effect immediately. Scaling down allows one adjustment per hour, with a maximum reduction of 100 TiB each time. Deleting an accelerator counts as a scaling\-down operation.

* **Separation of storage and compute**

   Unlike cache spaces on compute servers, the accelerator operates independently. This enables adjustments to be made online to the cache size and performance.

* **Multiple warm\-up options**

   The accelerator provides several warm\-up options, such as write‑through, read\-through, synchronous, and asynchronous, to enhance access efficiency and adapt to various business scenarios.

   * Write\-through warm\-up: This option is only available in read/write cache mode. It is enabled by default and not configurable. When a client writes data, it is written directly into the accelerator.

   * Read\-through warm\-up: When a read request results in a cache miss, the accelerator automatically retrieves the requested data from TOS. The accelerator then stores the data and returns it to the client. This option is enabled by default and cannot be disabled.

   * Synchronous warm\-up: This option is only available in read\-only cache mode. Data written to TOS through accelerated domain names is also cached synchronously in the accelerator. For more information, see [Creating TOS accelerators](https://docs.byteplus.com/docs/tos/Creating-tos-accelerators).

   * Asynchronous warm\-up: Data is cached in advance in the accelerator. For more information, see [Creating warm-up tasks](https://docs.byteplus.com/docs/tos/Creating-warm-up-tasks).

* **Free bandwidth for data transfer**

   Bandwidth consumed by data transfers between your accelerator and TOS is provided free of charge. It does not deduct from your account's intranet bandwidth quota. This ensures seamless interaction between your accelerator and TOS.


<span id="mHXYukf6"></span>
## Use cases

TOS accelerators provide business applications with fast access and elastic scaling. They are ideal for scenarios involving high bandwidth and frequent data reads.


* **Workloads requiring high write throughput**

   In large model training, writing checkpoint files requires an extremely high level of throughput. Using the read/write cache accelerator increases throughput, allowing for more efficient data writes and enabling training to resume immediately.

* **Fast caching of intermediate results**

   In big data computing, the read/write cache accelerator can serve as a high\-performance buffer for ETL (extract, transform, load) tasks in MapReduce frameworks, providing high read and write performance. Once a task is complete, the cached data can be removed.

* **Model training and inference**

   * During the pre\-training and informal training stages on development machines and similar environments, high bandwidth and QPS are necessary, but latency requirements are relatively relaxed; single\-digit millisecond latency is acceptable. The accelerator provides a better cost\-to\-performance ratio.

   * Advanced caching solutions located close to computing resources are primarily required to meet the demand for high bandwidth, high QPS, and strict latency requirements during model training or inference. However, since cache space for computing on the server is limited, an efficient data flow is essential when the near\-compute cache is inadequate. In this case, the accelerator can serve as a secondary cache to accelerate access to TOS and mitigate the impact of limited cache space.

* **Big data analytics**

   In big data analytics, querying and analyzing data typically involves large volumes of data, ambiguous query scopes, and tight time constraints. The accelerator can be used to preload data from TOS into the cache, thereby reducing analysis delays and improving efficiency.

* **Data rendering**

   In rendering scenarios such as producing special effects and game scenes, a high QPS is typically required to ensure a smooth user experience. The accelerator can preload large assets from TOS into the cache, which enhances data access speed and meets high QPS demands in scenarios involving small files.


<span id="M30fx3Vs"></span>
## How it works

TOS accelerators use intelligent caching and data flow mechanisms to transparently accelerate data access for your business. The core operating principle varies depending on the cache mode.

<span id="M4IdYQ17"></span>
### Read\-only cache mode

In read\-only cache mode, the accelerator transparently caches data from TOS in the background. Its purpose is to improve data read performance.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b807d628c6deccd35c60fc28eae95060.png) </span>

**Read requests**

Using the accelerator in read\-only cache mode can improve data reading performance. The process is as follows:


1. A client sends a read request to the accelerator via an accelerated domain name. The request is then automatically forwarded to the accelerator.

2. Upon receiving the read request, the accelerator looks for data in the cache.

   * If the data is available in the cache, it will be sent directly to the client.

   * If the data is not found in the cache, it is retrieved from TOS and sent back to the client. At the same time, the data is written to the cache.


<span id="fdVcsJP4"></span>
#### **Write requests**

In read\-only cache mode, the accelerator does not process write requests. Instead, all write requests pass through the accelerator and the data are written directly to, and therefore stored in, TOS. This process does not use cache space or receive write acceleration. However, you can proactively load written data into the cache using either synchronous or asynchronous warm\-up.

<span id="2TM2M5gp"></span>
#### **Cache eviction**

If the cache is full, the data with the lowest access frequency is removed to make space for new data.

<span id="gs9HGjIN"></span>
### Read/write cache mode

In read/write cache mode, the accelerator speeds up reads and significantly reduces write latency via a "foreground cache writing and background asynchronous flushing" mechanism.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2670721195a717d80df60840da248470.png) </span>

<span id="ekeDcEF9"></span>
#### **Read requests**

The read flow in read/write cache mode is similar to that in read\-only cache mode. Regardless of whether data has been written to the cache but not yet flushed, or has been flushed and exists as read cache, data can be read at high speed. When an object is updated in TOS, the cache is automatically invalidated to ensure that the latest data is read.

<span id="Btnp9XzH"></span>
#### **Write requests**


1. A client sends a write request to the accelerator via an accelerated domain name. The data is written to the accelerator synchronously. Once the write succeeds, the client receives a successful response, achieving extremely fast writes.

2. After the data is written to the cache, the accelerator asynchronously flushes it to TOS for storage.


<span id="XAEgkjEF"></span>
#### **Cache eviction**

Based on the configured expiration time, data that has been flushed to TOS and has expired is evicted from the cache space.

<span id="d8399dce"></span>
## Performance metrics

TOS accelerators offer two flexible performance modes to meet the needs of different workloads. The performance of an accelerator, in terms of bandwidth and IOPS, is closely related to its cache capacity and storage usage.

The table below explains how performance is determined for each accelerator mode.


|**Mode** |**Use cases** |**Performance** |
|---|---|---|
|Read\-only cache mode (provisioned capacity) |Read\-intensive scenarios, such as big data analysis, AI inference, and hot content distribution. |The performance of an accelerator is positively correlated with the capacity applied. A larger cache capacity delivers higher performance. |
|Read/write cache mode (elastic capacity) |Write\-intensive or mixed read/write scenarios, such as AI training checkpointing and high\-frequency data production and consumption. |The performance of an accelerator consists of **baseline performance** and **provisioned performance**.<br><br><br>* **Baseline performance**: It is positively correlated with your accelerator's storage usage. The more storage capacity you use, the higher your baseline performance will be. This is provided at no additional cost.<br><br>* **Provisioned performance**: You can purchase additional packages to achieve a level of performance that far exceeds the baseline and can handle high\-performance bursts or sustained demands. |


The table below describes the performance metrics for each accelerator mode.


|**Performance metric** |**Read\-only cache mode** |**Read/write cache mode** |
|---|---|---|
|Accelerator capacity |50 GiB–200 TiB.<br><br>[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need more capacity. |Limit: 10 PiB.<br><br>[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need more capacity. |
|Accelerator bandwidth |The maximum bandwidth when the data cache is hit. Formula:<br><br>`Max {600 MB/s, 0.3 MB/s/GiB × Accelerator capacity (GiB)}`<br><br>For example, if the accelerator has a capacity of 3,000 GiB, its maximum read bandwidth is 900 MB/s.<br><br>The maximum read bandwidth is 60 GB/s. [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need higher read bandwidth.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In read\-only cache mode, no data will be written to the accelerator. Therefore, the write bandwidth metric is not applicable. Write operations in read\-only cache mode are affected by both TOS's intranet upload bandwidth and the data transfer bandwidth. For more information on intranet upload bandwidth, see <a href="https://docs.byteplus.com/docs/tos/docs-restrictions">Constraints and limitations</a>.</div><br> |In read/write cache mode, the bandwidth of an accelerator consists of baseline and provisioned bandwidth. Formula:<br><br><br>* Baseline bandwidth: `Max{600 MB/s, 0.125 MB/s/GiB × Used cache capacity (GiB)}`. The upper limit is 30 GB/s.<br><br>* Provisioned bandwidth: Based on your needs, you can purchase provisioned bandwidth of up to 120 GB/s.<br><br>* Accelerator bandwidth: `Max{Baseline bandwidth, Provisioned bandwidth}`.<br><br><br>Reads and writes share the bandwidth of the accelerator:<br><br><br>* Limit for pure reads: Accelerator bandwidth. The valid range is 600 MB/s to 120 GB/s.<br><br>* Limit for pure writes: Accelerator bandwidth × 1/3. The valid range is 200 MB/s to 40 GB/s.<br><br><br>For example, if the accelerator uses 3,000 GiB of capacity and the provisioned bandwidth is 90 GB/s, the accelerator's bandwidth would also be 90 GB/s. The upper limits for pure reads and pure writes would then be 90 GB/s and 30 GB/s, respectively.<br><br>[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need higher read bandwidth. |
|Accelerator QPS |The maximum QPS when the data cache is hit. Formula:<br><br>`Accelerator bandwidth (MB/s) × 30`<br><br>The maximum QPS is 300,000. [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need higher QPS.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In read\-only cache mode, no data will be written to the accelerator. Therefore, the write QPS metric is not applicable.</div><br> |The formula for calculating the QPS of an accelerator in read/write cache mode is:<br><br>Accelerator QPS: `Accelerator bandwidth (MB/s) × 30`<br><br>Reads and writes share the QPS of the accelerator:<br><br><br>* Limit for pure reads: Accelerator QPS. The valid range is 18,000 to 900,000.<br><br>* Limit for pure writes: Accelerator QPS × 1/3. The valid range is 6,000 to 300,000.<br><br><br>[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need higher QPS. |
|Data transfer |Data transfer bandwidth: `Min{Accelerator bandwidth - Actual read bandwidth for a workload, Accelerator bandwidth × 10%}`.<br><br><br>* Actual read bandwidth for a workload: Actual accelerator read bandwidth.<br><br>* The maximum data transfer bandwidth is 6 GB/s.<br><br>* The bandwidth consumed by data transfers between the accelerator and TOS is provided free of charge, and does not count against your account's intranet bandwidth quota. However, writing data to the accelerator does use your accelerator bandwidth quota. For more information on bandwidth limits, see [Constraints and limitations](https://docs.byteplus.com/docs/tos/docs-restrictions).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Bandwidth for writes via accelerated domain names is affected by the synchronous warm\-up feature. Bandwidth values vary depending on whether the feature is enabled.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Synchronous warm\-up off: Intranet upload bandwidth. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-restrictions">Constraints and limitations</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Synchronous warm\-up on: <code>Min{Data transfer bandwidth, Intranet upload bandwidth}</code>.</div><br> |Data transfer bandwidth: `Min{Accelerator bandwidth - Actual bandwidth for a workload, Accelerator bandwidth × 30%}`<br><br><br>* Actual bandwidth for a workload: `Actual accelerator read bandwidth + Actual accelerator write bandwidth × 3`.<br><br>* The maximum data transfer bandwidth is 20 GB/s.<br><br>* The bandwidth consumed by data transfers between the accelerator and TOS is provided free of charge, and does not count against your account's intranet bandwidth quota. However, writing data to the accelerator does use your accelerator bandwidth quota. For more information on bandwidth limits, see [Constraints and limitations](https://docs.byteplus.com/docs/tos/docs-restrictions). |
|Latency (block size: 4K) |The geographic locations of your client and your accelerator affect the latency of requests sent to the accelerator.<br><br><br>* If both your client and your accelerator are in the same region and availability zone, the latency will be 2–3 ms.<br><br>* Latency increases if your client and your accelerator are in different regions or availability zones, or if they are in the same region but in different availability zones. This is due to the longer distances in the network paths. ||


<span id="4113794d"></span>
## Billing notes

You are charged for the accelerator capacity and provisioned bandwidth when you use the TOS accelerator feature. The read/write cache mode is currently in closed beta and free. This feature will become a paid service starting **July 28, 2026**.

For billing details, see [TOS accelerator](https://docs.byteplus.com/en/docs/tos/TOS_Accelerator_fee).

<span id="aOhDsm2C"></span>
## Supported regions

TOS accelerator **read\-only cache** mode became generally available on January 5, 2026. The table below lists the supported regions and availability zones.


|**Region** |**Number of available zones** |**Availability zone** |**Region ID** |
|---|---|---|---|
|China (Beijing) |4 |A, C, D, and E |cn\-beijing |
|China (Datong) |1 |C |cn\-beijing2 |
|China (Shanghai) |2 |A and E |cn\-shanghai |
|China (Guangzhou) |1 |C |cn\-guangzhou |
|China (Ulanqab) |1 |A |cn\-wulanchabu |
|Asia Pacific (Johor) |1 |B |ap\-southeast\-1 |
|China (Shanghai)\-autodriving |1 |A |cn\-shanghai\-autodriving |
|China (Beijing)\-autodriving |1 |A |cn\-beijing\-autodriving |
|China (Beijing)\-selfdriving |1 |A |cn\-beijing\-selfdrive |
|China (Wuhu) |1 |A |cn\-wuhu |


<span id="bhoIk6Yp"></span>
## Steps


1. [Creating TOS accelerators](https://docs.byteplus.com/docs/tos/Creating-tos-accelerators)

2. (Optional) [Creating warm-up tasks](https://docs.byteplus.com/docs/tos/Creating-warm-up-tasks)

3. [Using TOS accelerators](https://docs.byteplus.com/docs/tos/Using-tos-accelerators)
