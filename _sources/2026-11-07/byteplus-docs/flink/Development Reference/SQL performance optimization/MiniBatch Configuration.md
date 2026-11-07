---
title: "MiniBatch Configuration"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/MiniBatch_Configuration"
---

MiniBatch functions to cache a certain amount of data before triggering processing, thus reducing the number of State accesses, increasing throughput, and reducing data output.

<span id="06593326"></span>
## Applicable Scenarios


1. **Reduces the CPU overhead caused by frequent state access**.

   If RocksDB is used as the State Backend. Each state access requires serialization and deserialization, resulting in significant CPU overhead. Enabling MiniBatch can reduce the number of state accesses, thereby reducing some CPU overhead.

2. **Reduce the output of Aggregation**.

   In normal Aggregation, each incoming piece of data outputs the current aggregate result directly; however, with MiniBatch enabled, if there are multiple pieces of data within a mini\-batch, only one output is generated, effectively reducing the amount of output data.


For a detailed understanding of MiniBatch principles, please refer to the open\-source document: [MiniBatch Aggregation](https://nightlies.apache.org/flink/flink-docs-release-1.11/dev/table/tuning/streaming_aggregation_optimization.html#minibatch-aggregation).

<span id="cd328c32"></span>
## How to Enable MiniBatch

MiniBatch is disabled by default. To enable it, configure the following parameters in the Flink settings:


|**Configuration** |**Example Value** |**Description** |
|---|---|---|
|table.exec.mini\-batch.enabled |true |Whether to enable MiniBatch.<br><br><br>* True: Enable<br><br>* False: Default value, disabled. |
|table.exec.mini\-batch.allow\-latency |5s |Interval for MiniBatch.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enabling MiniBatch buffers a batch of data instead of processing it immediately, which causes some delay. You need to configure <code>mini-batch.allow-latency</code> based on business needs and make a trade\-off between task throughput and data timeliness.</div><br> |
|table.exec.mini\-batch.size |10000 |The number of records for a single concurrent buffer.<br><br>It is recommended to control the number of buffer records under abnormal traffic (such as data backtracking, excessive lag, etc.) by reasonably configuring `mini-batch.size` to prevent excessive data records in the buffer from directly causing memory OOM.<br><br>You can roughly calculate using the formula below and then reasonably configure `mini-batch.size` to limit the maximum number of data records in the buffer.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32d2d0569dd341b6b1fa52969ddf18f0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* In the numerator, **f** represents the coefficient, **Max(QPS)**  represents the maximum QPS written by the operator, and **f \* Max(QPS)**  represents the maximum allowed traffic.<br><br>* In the numerator, **latency** is taken from `mini-batch.allow-latency`, and is measured in seconds.<br><br>* The denominator is the job's concurrency, calculated by multiplying the data volume of **Tm** by the number of **slots**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of data records and the time interval belong to an <strong>either/or</strong> relationship; satisfying any condition forms a MiniBatch.</div><br> |


<span id="d657a110"></span>
## Frequently Asked Questions


1. The relationship between MiniBatch and LocalGlobal.

   LocalGlobal splits the original Aggregation into Local and Global two\-stage aggregation. The first stage aggregates a batch of data locally at the upstream node (localAgg) and outputs the incremental value of this micro\-batch (Accumulator); the second stage merges the received Accumulators (Merge) to obtain the final result (GlobalAgg).

   LocalGlobal can use LocalAgg's aggregation to screen out some skewed data, thus reducing the hot spots of GlobalAgg and enhancing performance. For a detailed understanding of the principles of LocalGlobal, please refer to the open\-source document: [Local-Global Aggregation](https://nightlies.apache.org/flink/flink-docs-release-1.11/dev/table/tuning/streaming_aggregation_optimization.html#local-global-aggregation).

   The prerequisite for LocalGlobal is that MiniBatch must be enabled. **prerequisite**. LocalGlobal does not need to be manually activated; it is enabled by default. Therefore, after enabling the MiniBatch configuration, LocalGlobal will automatically optimize.

2. Can job be restored from an existing Checkpoint after enabling MiniBatch?

   After enabling MiniBatch, if you want to revert to the state before MiniBatch was enabled, LocalGlobal must be turned off.

   Please use the following parameters to disable LocalGlobal.

   ```YAML
   // When MiniBatch is enabled, LocalGlobal is also enabled by default, and the default value is TWO_PHASE. 
   // To disable it, set it to ONE_PHASE.
   
   table.optimizer.agg-phase-strategy = ONE_PHASE
   ```
