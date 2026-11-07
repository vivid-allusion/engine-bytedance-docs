---
title: "Optimizing FSX performance"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Fsx-performance-tuning"
---

This article introduces how to adjust parameters to enhance prefetch performance and write performance.

<span id="44d93695"></span>
## Recommendations

FSX supports prefetch, read cache, and write cache modes. You can choose the appropriate mode according to your actual usage scenario. Detailed explanations are as follows:


|**Application scenarios** |Recommendated mode |**Performance** |
|---|---|---|
|Scenarios of sequential reading or small\-range random reading |Default (Prefetch) |Prefetch performance depends on the size of the prefetched data and the number of prefetch threads. For a detailed explanation, see [Prefetch performance](https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#65d6bdc6). |
|Scenarios requiring repeated file reads with small data volumes |Read Cache |Read cache performance may be affected by disk read performance. For more details, please refer to [Read cache performance](https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#dc99714b). |
|Scenarios sensitive to write performance |Write Cache |You can improve write bandwidth by increasing the number of threads uploading multiple data segments. For detailed information, see [Write performance](https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#ebcd14ca). |


<span id="65d6bdc6"></span>
## Prefetch performance

For sequential read or small\-range random read scenarios, the FSX client enables the prefetch feature by default, which loads subsequent file content into memory in advance by issuing multiple parallel Range download requests. You can control the bandwidth and memory usage of single\-file prefetching through the following parameters. Detailed explanations are as follows:


* Prefetch data size

   The formula for calculating the size of prefetch data is: Maximum prefetch data size per file = Prefetch data block size (prefetch_buffer_size) × Maximum number of prefetch data blocks (prefetch_forward_buffer_count)

   The default maximum prefetch data size for a single file is 128MB. You can adjust the maximum amount of data prefetched for a single file by configuring the prefetch_forward_buffer_count and prefetch_buffer_size parameters. The specific parameter descriptions are as follows:

   * `prefetch_buffer_size`: Sets the size of the data block read from TOS for each prefetch request; the default value is 4MB. Larger values can reduce the number of requests sent by the FSX client to TOS, but may also affect the throughput bandwidth of prefetch requests.

   * `prefetch_forward_buffer_count`: Sets the maximum number of data blocks to be prefetched for a single file; the default value is 32.

   * `prefetch_backward_buffer_count`: Sets the number of prefetched data blocks to retain before the offset of the current read request; the default value is 1. Used in conjunction with `prefetch_buffer_size`.

* Read bandwidth

   The number of prefetch threads can be adjusted via the `num_prefetch_threads` parameter, with a default value of 32. The maximum read bandwidth is affected by prefetch threads and the single\-file bandwidth throttling value; you can increase the number of prefetch threads to improve read bandwidth.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enhance prefetch efficiency, set higher values for <code>num_prefetch_threads</code> and <code>prefetch_forward_buffer_count</code>, depending on your available resources.</div>


<span id="dc99714b"></span>
## Read cache performance

For scenarios involving frequent reads of a batch of files with small data volumes, the FSX client provides a read data cache feature. When data is read repeatedly, the content is retrieved from the read cache instead of accessing TOS, thereby reducing access latency and improving read performance. The performance of read caching is affected by the read performance of the disk where the cache directory is located. It is recommended to select a disk with better performance or use the tmpfs memory file system as the read cache directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In scenarios involving one\-time or non\-repetitive data reading, it is not recommended to enable the read cache function.</div>


You can enable the read cache feature using the following parameters:


* `read_cache_dir`: Configures the read cache directory. The cache path can be specified as a directory on disk or as a tmpfs memory file system.

* `max_read_cache_size`: Configures the size of the read cache space, measured in MB. The default value is 0. It is recommended to estimate the read cache size based on the amount of data that needs to be cached.


<span id="ebcd14ca"></span>
## Write cache performance

By default, FSX writes data to a local temporary directory. You can specify a directory using the `temp_dir` parameter when mounting a bucket. This directory will be generated under `/tmp/`. If performance is important to you, specify `tmpfs` as the directory for temporary files. You can adjust the write performance using the following parameters:


* `temp_dir`: Sets the write cache directory; you can specify `tmpfs` as the write cache directory.

* `num_bg_threads`: Sets the number of threads for uploading multiple segments of data; the default is 32. The maximum upload bandwidth is affected by `num_bg_threads` and the bandwidth throttling value for a single file. You can improve write bandwidth by increasing the number of threads for uploading multiple data segments.

* `max_temp_capacity`: Sets the maximum disk space occupied by the write cache, in GiB, with a default value of 10. This parameter, together with part_size, determines the maximum concurrency of write requests. The calculation formula is: maximum concurrency = max_temp_capacity / part_size. When part_size is fixed, increasing the value of max_temp_capacity can improve the concurrency of write requests.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you wish to improve write efficiency, you can set a higher value for <code>num_bg_threads</code> parameter according to your available resources.</div>
