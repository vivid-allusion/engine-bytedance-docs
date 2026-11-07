---
title: "Daft distributed UDF parameter configuration"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Daft_distributed_UDF_parameter_configuration"
---

In AI data processing scenarios, the analysis and manipulation of multimodal data (such as text, images, point clouds, audio, and more) have become core requirements. **Daft, as a lightweight and efficient distributed multimodal data processing framework**, relies on user\-defined functions (UDFs) as a key capability supporting these complex operations. Within the Daft ecosystem, using UDFs to implement customized processing of multimodal data—for example, image feature extraction, text format cleansing, cross\-modal data association, and so on—is not only a common industry practice but also highly accessible due to the framework's low barrier to entry. Developers do not need to deeply understand its underlying distributed logic; by simply encapsulating business logic in concise code, they can quickly integrate custom data processing operations into Daft's data pipeline, significantly lowering the technical threshold for multimodal data processing.

To accommodate different development habits and requirements across various scenarios, Daft provides **diverse usage options**, including Batch UDF, Row\-wise UDF, Async UDF, and more, while supporting seamless switching between local debugging and distributed deployment.

Caution: Efficient operation of Daft UDFs is not "out\-of\-the\-box"; performance is highly dependent on **business\-adapted parameter configuration**—especially the two core parameters, `batch_size` (batch size) and `concurrency` (number of concurrent tasks). The configuration of these two parameters must be based on an understanding of Daft's operating mechanism: `batch_size` determines the maximum amount of data processed per UDF invocation. If set too high, it may cause memory overflow; if too low, it increases function call overhead. `concurrency` controls the number of UDF tasks executed in parallel. If set too high, it may lead to resource contention (such as CPU, GPU, or network bandwidth bottlenecks); if too low, distributed resources are not fully utilized. If parameter settings do not match the business data volume (such as the size of individual data items or total data volume) and hardware resources, the result may be reduced task concurrency efficiency in mild cases, or task blocking or crashes in severe cases. Therefore, when developers use Daft UDFs, they need to adjust parameters appropriately based on the specific business scenario (such as the type of multimodal data and the complexity of processing logic) and resource configuration, in order to fully leverage Daft's distributed advantages.

<span id="bcb39a0d"></span>
## UDF example

Daft supports running UDFs in either single\-node mode or distributed mode. There are some subtle differences in the scheduling mechanism. Running UDFs in distributed mode relies on Ray's distributed scheduling capabilities. Next, we will use an example to illustrate which aspects should be considered when configuring UDF parameters for running a Daft Batch UDF in distributed mode with Ray.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current Daft version is v0.6.4.</div>


```Python
import logging
import time
import os


def configure_logging():
    logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                        datefmt='%Y-%m-%d %H:%M:%S.%s'.format())

    logging.getLogger("tracing.span").setLevel(logging.WARNING)
    logging.getLogger("daft_io.stats").setLevel(logging.WARNING)
    logging.getLogger("DaftStatisticsManager").setLevel(logging.WARNING)
    logging.getLogger("DaftFlotillaScheduler").setLevel(logging.WARNING)
    logging.getLogger("DaftFlotillaDispatcher").setLevel(logging.WARNING)
    logging.getLogger("MyBatchUdf").setLevel(logging.WARNING)


configure_logging()

import daft
from daft import col, Series


@daft.udf(return_dtype=daft.DataType.string())
class MyBatchUdf:
    def __init__(self, sleep: int = 0):
        self._id = id(self)
        self.counter = 0
        self.sleep = sleep
        self.logger = logging.getLogger(f"MyBatchUdf-{self._id}")

    def __call__(self, a: Series) -> Series:
        self.counter += len(a)

        self.logger.info(f"Actor got {len(a)} records, total: {self.counter}")

        if self.sleep > 0:
            time.sleep(self.sleep)

        return a


if __name__ == "__main__":
    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import ray

        ray.init(runtime_env={"worker_process_setup_hook": configure_logging})

    partition = 2
    udf_concurrency = 4
    udf_batch_size = 200
    sleep_seconds = 2

    paths = [f"file-{i}" for i in range(1000)]
    df = daft.from_pydict({"path": paths})

    # Repartition not supported on the NativeRunner
    df = df.repartition(partition, "path")

    udf = (MyBatchUdf
           .override_options(batch_size=udf_batch_size)
           .with_concurrency(udf_concurrency)
           .with_init_args(sleep=sleep_seconds))
    df = df.with_column("batch", udf(col("path")))
    df.collect()
```


In the example provided above, we implemented a MyBatchUdf, which includes a counter to record the number of data entries processed by the current UDF. Additionally, this UDF accepts a column of type String and returns the column itself. The main data processing flow is as follows:


* Create a DataFrame containing 1,000 data entries, with a single column named `path`.

* The DataFrame obtained via `from_pydict` contains only one partition, so we repartition the DataFrame based on the `path` column. After repartitioning, the DataFrame contains two partitions.

* We then define a UDF operator with concurrency=4 and batch_size=200 to process these 1,000 data entries. In theory, each concurrent worker should process 250 data entries.


<span id="f4cdbd7c"></span>
## Analysis of execution results

Let us first examine what issues may arise when parameter configuration is improper.

<span id="d7f1127e"></span>
### Scenario 1: Data skew

When we run this task in Ray single\-node mode, we obtain the following log. The log shows that a total of four UDFActor instances were started, but the number of data entries processed by each is `[110, 200, 290, 400]`, which does not match our expectation of 250 data entries per instance. Additionally, we can see that two UDF instances were invoked twice, and the time between invocations matches the configured sleep time, indicating that the same UDF instance executes multiple batches of data serially. If the execution time for each data entry is consistent, then the UDF instance processing 400 data entries becomes the long tail, and only one concurrent worker will be processing data in the later stages of the task.

```YAML
(UDFActor pid=80511) 2025-09-28 16:40:48.1759048848 - MyBatchUdf-5155349264 - INFO - Actor got 200 records, total: 200
(UDFActor pid=80510) 2025-09-28 16:40:48.1759048848 - MyBatchUdf-4467594448 - INFO - Actor got 200 records, total: 200
(UDFActor pid=80509) 2025-09-28 16:40:48.1759048848 - MyBatchUdf-5098474896 - INFO - Actor got 110 records, total: 110
(UDFActor pid=80512) 2025-09-28 16:40:48.1759048848 - MyBatchUdf-4548224592 - INFO - Actor got 200 records, total: 200
(UDFActor pid=80510) 2025-09-28 16:40:50.1759048850 - MyBatchUdf-4467594448 - INFO - Actor got 90 records, total: 290
(UDFActor pid=80512) 2025-09-28 16:40:50.1759048850 - MyBatchUdf-4548224592 - INFO - Actor got 200 records, total: 400
```


The uneven data distribution here is related to the execution of `repartition` (the specific reason will be explained later). Let us see what happens if the partition operation is not performed. From the following logs, we can see that the four concurrent processes each handled `[200, 200, 200, 400]` records. Although there are five batches, so one of the concurrent processes handled two batches, this situation appears to be better than the previous one.

```YAML
(UDFActor pid=96995) 2025-09-28 16:55:06.1759049706 - MyBatchUdf-5049017488 - INFO - Actor got 200 records, total: 200
(UDFActor pid=96996) 2025-09-28 16:55:06.1759049706 - MyBatchUdf-5237938000 - INFO - Actor got 200 records, total: 200
(UDFActor pid=96993) 2025-09-28 16:55:06.1759049706 - MyBatchUdf-5112045840 - INFO - Actor got 200 records, total: 200
(UDFActor pid=96998) 2025-09-28 16:55:06.1759049706 - MyBatchUdf-5887815120 - INFO - Actor got 200 records, total: 200
(UDFActor pid=96998) 2025-09-28 16:55:08.1759049708 - MyBatchUdf-5887815120 - INFO - Actor got 200 records, total: 400
```


<span id="9eee03d6"></span>
### **Scenario 2: Actual concurrency is lower than expected**

But what if the task is running on a Ray cluster with multiple workers? When this task is run on a Ray cluster with two workers, the logs below show that only two concurrent processes actually handled the data, with the number of records processed being `[400, 600]`. The concurrency for processing data did not meet expectations.

```YAML
(UDFActor pid=13825) 2025-09-28 17:08:52.1759050532 - MyBatchUdf-6049781264 - INFO - Actor got 200 records, total: 200
(UDFActor pid=13827) 2025-09-28 17:08:52.1759050532 - MyBatchUdf-5088798160 - INFO - Actor got 200 records, total: 200
(UDFActor pid=13825) 2025-09-28 17:08:54.1759050534 - MyBatchUdf-6049781264 - INFO - Actor got 200 records, total: 400
(UDFActor pid=13827) 2025-09-28 17:08:54.1759050534 - MyBatchUdf-5088798160 - INFO - Actor got 200 records, total: 400
(UDFActor pid=13825) 2025-09-28 17:08:56.1759050536 - MyBatchUdf-6049781264 - INFO - Actor got 200 records, total: 600
```


<span id="c4448266"></span>
### **Scenario 3: Actual concurrency is lower than expected**

In addition to mismatches between the number of partitions and the number of workers causing concurrency to fall short of expectations, an inappropriate batch_size setting can also lead to insufficient concurrency. Suppose we set batch_size to 500. From the logs below, we can see that even when running on a single node, only two concurrent processes handled the data, with the number of records processed being `[500, 500]`. The concurrency for processing data did not meet expectations.

```YAML
(UDFActor pid=37087) 2025-09-28 17:29:33.1759051773 - MyBatchUdf-5215119504 - INFO - Actor got 500 records, total: 500
(UDFActor pid=37086) 2025-09-28 17:29:33.1759051773 - MyBatchUdf-4822819216 - INFO - Actor got 500 records, total: 500
```


<span id="015f7f64"></span>
## Problem analysis

From the examples above, we can see that unreasonable settings for the number of DataFrame partitions, UDF batch size, and UDF concurrency can lead to data skew and insufficient concurrency. Next, we will explain the operating mechanism of Daft and the specific reasons from a theoretical perspective.

When running a Daft job in a distributed environment, the entire job code is first constructed as a logical execution plan (LogicalPlan). When `df.collect()` is executed, a materialize operation is performed. The entire logical plan is optimized by the built\-in Daft optimizer, then converted into a distributed physical execution plan (DistributedPhysicalPlan), and finally handed over to `DistributedPhysicalPlanRunner` to execute the entire plan.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd68d177881143af80345a0d10707cee~tplv-goo7wpa0wc-image.image" width="1966px" /></div>


`DistributedPhysicalPlanRunner` converts the physical plan into an executable pipeline, where each node in the plan corresponds to a `PipelineNode`. Ultimately, this pipeline is split into one or more SwordfishTask. In general, the number of **DataFrame partitions** determines the number of SwordfishTasks generated. These tasks are first dispatched to `RaySwordfishActor` instances according to the corresponding scheduling strategy (each Worker starts one RawSwordfishActor). When the scheduling strategy for a task is set to Spread, SwordfishTasks are evenly distributed across multiple RaySwordfishActor instances based on the idle status of the Workers.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a7bdd55b8f0465492608aeff4782e08~tplv-goo7wpa0wc-image.image" width="2702px" /></div>


`RaySwordfishActor` is responsible for executing SwordfishTasks, and uses NativeExecutor to execute the `LocalPhysicalPlan` contained in the task. (At this point, the execution logic of Native Runner and Ray Runner is basically the same. The difference is that in a distributed scenario, each SwordfishTask contains data from only one partition (the size of `psets` is 1), whereas Native Runner contains data from all partitions.) Each SwordfishTask contains the entire stage plan. When executing a UDF operator, the data in the current SwordfishTask is split into morsels/MicroPartitions according to batch_size, and then scheduled to the UDFActors on the current worker (executing `UDFActor.eval_input`).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826df73d1d8440ad9a2f49bf461414cb~tplv-goo7wpa0wc-image.image" width="2638px" /></div>


Therefore, there are **four key parameters** to configure here:


* **Number of workers**: Each worker starts a `RaySwordfishActor`, and a single `RaySwordfishActor` can run multiple SwordfishTasks "simultaneously" (asynchronously executing `LocalPhysicalPlan`). When the plan runner schedules tasks to each `RaySwordfishActor`, it decides whether to dispatch a task based on the current `RaySwordfishActor`'s load. Tasks that are not dispatched remain in a waiting state and can only be dispatched after previous tasks finish running. Therefore, the number of workers and the total number of worker CPUs determine the maximum concurrency for task execution.

* **DataFrame partitions:**  In general, each partition corresponds to a `SwordfishTask`, so the number of `SwordfishTasks` determines the maximum parallelism of the entire pipeline. If the number of `SwordfishTasks` is less than the number of `RaySwordfishActor` instances, some `RaySwordfishActor` instances will remain idle because they do not receive any tasks. When the number of DataFrame partitions is relatively small, you can increase the number of partitions using `repartition` or `into_partition`, thereby increasing the number of tasks. You can also use `into_batches` to split a partition into multiple tasks, with each task containing part of the original partition's data, thus increasing the maximum concurrency for task execution.

* **UDF concurrency:**  This value determines the maximum parallelism for UDF execution. In Ray mode, it determines how many `UDFActor` instances are started. When the workers in the Ray cluster are homogeneous, `UDFActor` instances are generally evenly distributed across all workers. When a worker has a `UDFActor` for that UDF (for example, when UDF concurrency is less than the number of workers, some workers will not start a `UDFActor` for that UDF), the corresponding `RaySwordfishActor` will only schedule morsels to the UDFActor on the current worker. Therefore, when the number of morsels split by `RaySwordfishActor` is less than the number of `UDFActor` instances on the current worker, some `UDFActor` instances will idle because they do not receive any data, resulting in `UDFActor` idling.

* **UDF batch_size:**  This value determines the maximum number of data records passed in a single UDF call. When batch_size is set relatively large, it requires more execution memory on one hand, and on the other hand, it causes fewer morsels to be split by `RaySwordfishActor`, making it impossible to fully utilize all `UDFActor` instances on the worker. When batch_size is set relatively small, it increases the overhead of function calls. Therefore, it is necessary to adjust this value based on the actual business scenario and optimization objectives.


**In Scenario 1**, we encountered a situation where data processing was uneven. When we used `repartition` to repartition a partition containing 1,000 data records into two partitions, the resulting partitions were not completely balanced. This is because we used the hash value of the path as the repartition key, so the degree of skew depends on the distribution of the hash values. In the above example, after repartitioning, we obtained two partitions containing 510 and 490 records, respectively. Each partition was then further split by the daft engine with batch size = 200 into `[200, 200, 110, 200, 200, 90]` six batches, which were then scheduled across four concurrent workers. It can be seen that the splitting of each partition is independent, and data from different partitions cannot be merged. Therefore, the last batch of each partition contains significantly fewer records than the other batches.

**In Scenario 2**, we encountered a situation where actual concurrency was lower than expected. This is because the original DataFrame had only one partition, resulting in only one task, which was scheduled to a single worker. The concurrent UDF instances are already "evenly" distributed across all workers during the plan phase, and when `RaySwordfishActor` schedules batches/morsels, it prioritizes scheduling to the local worker, causing only the UDFActor instance on one worker to process data. Therefore, only when the number of tasks is greater than or equal to the number of workers can we maximize concurrency. So, how can we both increase the number of tasks/partitions and balance the data volume across different tasks/partitions? When there are similar requirements, consider using the `into_batches` API. This API splits the partition data into different tasks based on execution size, then distributes them to different `RaySwordfishActor` instances. For example, when running `df.into_batches(200).with_column("batch", udf(col("path")))` in a single\-worker Ray cluster, you will get the following result:

```YAML
(UDFActor pid=29906) 2025-09-28 19:15:04.1759058104 - MyBatchUdf-4816300688 - INFO - Actor got 200 records, total: 200
(UDFActor pid=29907) 2025-09-28 19:15:04.1759058104 - MyBatchUdf-4952482832 - INFO - Actor got 200 records, total: 200
(UDFActor pid=29909) 2025-09-28 19:15:04.1759058104 - MyBatchUdf-4548368464 - INFO - Actor got 200 records, total: 200
(UDFActor pid=29906) 2025-09-28 19:15:06.1759058106 - MyBatchUdf-4816300688 - INFO - Actor got 200 records, total: 400
(UDFActor pid=29906) 2025-09-28 19:15:08.1759058108 - MyBatchUdf-4816300688 - INFO - Actor got 200 records, total: 600
```


From the above log, we can see that the data is evenly split into 5 batches. However, this does not match the expected even scheduling across 4 concurrent instances; only 3 concurrent instances received data, and one instance processed 3 batches (the result is random—sometimes two instances may each process 2 batches), resulting in an imbalance in data processing among concurrent instances. The reason for this phenomenon is consistent with **Scenario 3**. Although the data for the 5 tasks is balanced, after each task is split by `RaySwordfishActor`, only one morsel is generated, which is then randomly assigned to a `UDFActor`. Because data processing between tasks is independent, in extreme cases, all 5 morsels generated by these tasks may be scheduled to the same `UDFActor`. To ensure maximum concurrency, it is necessary to guarantee that after splitting, the data from each task can be evenly distributed to every `UDFActor` on the current worker. For example, when udf_batch_size is set to 50, each task's data will be split into 4 morsels, which are then evenly distributed to each `UDFActor` using a round\-robin strategy.

```YAML
(UDFActor pid=43813) 2025-09-28 19:27:04.1759058824 - MyBatchUdf-5061156240 - INFO - Actor got 50 records, total: 50
(UDFActor pid=43815) 2025-09-28 19:27:04.1759058824 - MyBatchUdf-5090240720 - INFO - Actor got 50 records, total: 50
(UDFActor pid=43814) 2025-09-28 19:27:04.1759058824 - MyBatchUdf-5906907600 - INFO - Actor got 50 records, total: 50
(UDFActor pid=43816) 2025-09-28 19:27:04.1759058824 - MyBatchUdf-4546699600 - INFO - Actor got 50 records, total: 50
(UDFActor pid=43813) 2025-09-28 19:27:06.1759058826 - MyBatchUdf-5061156240 - INFO - Actor got 50 records, total: 100
(UDFActor pid=43815) 2025-09-28 19:27:06.1759058826 - MyBatchUdf-5090240720 - INFO - Actor got 50 records, total: 100
(UDFActor pid=43814) 2025-09-28 19:27:06.1759058826 - MyBatchUdf-5906907600 - INFO - Actor got 50 records, total: 100
(UDFActor pid=43816) 2025-09-28 19:27:06.1759058826 - MyBatchUdf-4546699600 - INFO - Actor got 50 records, total: 100
(UDFActor pid=43813) 2025-09-28 19:27:08.1759058828 - MyBatchUdf-5061156240 - INFO - Actor got 50 records, total: 150
(UDFActor pid=43815) 2025-09-28 19:27:08.1759058828 - MyBatchUdf-5090240720 - INFO - Actor got 50 records, total: 150
(UDFActor pid=43814) 2025-09-28 19:27:08.1759058828 - MyBatchUdf-5906907600 - INFO - Actor got 50 records, total: 150
(UDFActor pid=43816) 2025-09-28 19:27:08.1759058828 - MyBatchUdf-4546699600 - INFO - Actor got 50 records, total: 150
(UDFActor pid=43813) 2025-09-28 19:27:10.1759058830 - MyBatchUdf-5061156240 - INFO - Actor got 50 records, total: 200
(UDFActor pid=43815) 2025-09-28 19:27:10.1759058830 - MyBatchUdf-5090240720 - INFO - Actor got 50 records, total: 200
(UDFActor pid=43814) 2025-09-28 19:27:10.1759058830 - MyBatchUdf-5906907600 - INFO - Actor got 50 records, total: 200
(UDFActor pid=43816) 2025-09-28 19:27:10.1759058830 - MyBatchUdf-4546699600 - INFO - Actor got 50 records, total: 200
(UDFActor pid=43813) 2025-09-28 19:27:12.1759058832 - MyBatchUdf-5061156240 - INFO - Actor got 50 records, total: 250
(UDFActor pid=43815) 2025-09-28 19:27:12.1759058832 - MyBatchUdf-5090240720 - INFO - Actor got 50 records, total: 250
(UDFActor pid=43814) 2025-09-28 19:27:12.1759058832 - MyBatchUdf-5906907600 - INFO - Actor got 50 records, total: 250
(UDFActor pid=43816) 2025-09-28 19:27:12.1759058832 - MyBatchUdf-4546699600 - INFO - Actor got 50 records, total: 250
```


It appears that the combination of `into_batches` and UDF `batch_size` not only ensures the balance of data across tasks, but also fully leverages the concurrency of each UDFActor. However, `into_batches` is not a universal solution. For example, in scenarios with a single\-machine, single\-partition DataFrame, it is not suitable to use `into_batches`. Since there is only one partition and one worker, there is neither uneven data nor a need to distribute data across multiple workers. Therefore, there is no need to increase the number of tasks with `into_batches`, which would only add function call overhead.

Additionally, when executing `into_batches`, even if the DataFrame or partition has sufficient data, the tasks generated may not all meet the corresponding batch size. For example, if a DataFrame has two partitions, with the first partition containing 180 records and the second partition containing 220 records, when split with batch_size=200, three tasks will be generated, containing 180, 200, and 20 records respectively.

`into_batches` not only splits a large partition into multiple tasks, but also has the capability to merge several small partitions into larger tasks. For instance, suppose a DataFrame has 16 partitions, each containing only 20 records. When `df.into_batches(200)` is executed, two tasks will be generated, each containing 160 records, rather than one task with 200 records and another with 120 records. The reason behind this is that the distributed plan runner splits the logic before and after `into_batches` into two stages. It first materializes the result of the first stage, then batches the results. When the accumulated number of records exceeds 80% of the batch size, a new task is created. Therefore, in the example above, two tasks each containing 160 records are generated.

<span id="02bde6cd"></span>
## Summary

For different application scenarios, we can achieve the desired outcome by adjusting the concurrency of the UDF and the batch size parameter.

For example, to maximize UDF concurrency, suppose there are M Workers,


* First, it is necessary to ensure that all M Workers receive tasks, so the number of **tasks must be greater than or equal to the number of Workers**. By default, the number of tasks is determined by the number of partitions in the DataFrame. If the original number of partitions is small, the number of partitions in the DataFrame can be increased using `repartition` or `into_partition`, or the number of generated tasks can be increased using `into_batches`.

* Second, it is important to ensure that the data received by each Worker is as evenly distributed as possible, including both the number of tasks and the amount of data within each task. When the data within each task is relatively uniform, **the number of tasks is ideally an integer multiple of the number of Workers**, so that each Worker receives the same number of tasks. When the data volume within a task is unbalanced, you can use `repartition/into_partition` and `into_batches` to balance the data across each task. The former is suitable for scenarios with a large number of partitions (if the number of partitions is too small, there will be significant differences in data between partitions; the general logic of repartition is: each upstream partition splits its data into N chunks, and each downstream partition then merges 1/N of the upstream data chunks). When N is relatively small, the data volume in each chunk will be quite large. Even if the difference between partitions is only one chunk, there will still be chunk\-level differences in data volume. The latter is suitable for scenarios with small batches.

* Once the data volume of a task is determined, you should ensure that the number of UDF instances per worker multiplied by the UDF batch size exactly equals the task's data volume, that is, **udf_concurrency \* udf_batch_size / M = task_num_rows**. This ensures that after the task's data is split, it can be evenly distributed across multiple concurrent processes.


Above, we only discussed how to maximize concurrent computation by adjusting the number of DataFrame partitions, UDF concurrency, and batch size. In actual practice, to run UDF efficiently, you also need to pay attention to the load during UDF execution, such as CPU and memory usage. If UDF consumes a large amount of memory while processing data, you should reduce the UDF batch size to avoid OOM issues. Reducing the batch size may increase the number of morsels, and when UDFActor processes these morsel data, it may create backpressure. Therefore, to maximize concurrency, you should increase UDF concurrency. When UDF processing involves a large amount of IO operations, you should consider using asynchronous operations and coroutines within the UDF to improve CPU utilization, while also increasing the batch size to reduce the number of UDF calls. Increasing the batch size may reduce the number of morsels. If the number falls below the number of UDF instances on a worker, some instances may not receive data and remain idle.

For scenarios involving merging small files or fragmented upstream partitions, you can use `into_batches` to merge partitions, thereby reducing the number of UDF instance calls.
