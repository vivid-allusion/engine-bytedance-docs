---
title: "AutoScale: Using AdaptiveStreamingExecutor"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/using_adaptivestreamingexecutor"
---

Compared with StreamingExecutor, AdaptiveStreamingExecutor can dynamically adjust the concurrency of each map operator, providing greater flexibility and efficiency.

<span id="6adf1e04"></span>
## Configuration


|Configuration in DataContext |Note |Default value |
|---|---|---|
|enable_adaptive_execute |Whether to enable AdaptiveStreamingExecutor |False |
|task_backlog_timeout_secs |The maximum duration a task can remain in the pending scheduling state; exceeding this duration triggers scale up. |1s |
|actor_kill_timeout_secs |The duration an actor remains idle before being reclaimed, triggering scale down. |60s |


<span id="c3afae67"></span>
## Usage example

```Plain
DataContext.get_current().enable_adaptive_execute = True
```



* The default configuration is False, and the map operator is translated into `ActorPoolMapOperator`.


```Python
InputDataBuffer[Input] -> TaskPoolMapOperator[ReadParquet] -> ActorPoolMapOperator[MapBatches(SDTransformer)] -> TaskPoolMapOperator[Write]
```



* When using AdaptiveStreamingExecutor, the map operator is translated into `AdaptiveMapOperator`.


```Python
InputDataBuffer[Input] -> TaskPoolMapOperator[ReadParquet] -> AdaptiveMapOperator[MapBatches(SDTransformer)] -> TaskPoolMapOperator[Write]
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Within the range specified by the concurrency parameter, the concurrency of map operators (excluding read and write) can be dynamically adjusted. For example, with <code>concurrency=(10, 40)</code>, 10 to 40 actors will be used for task scheduling and computation.</div>


<span id="584214f6"></span>
## Used in conjunction with AutoScale for Ray clusters

[Ray cluster AutoScale](https://docs.byteplus.com/docs/E-MapReduce/109468) can automatically scale physical nodes based on workload, while enabling two layers of AutoScale capabilities on both the Ray Data side and the Ray cluster side, allowing for more efficient resource utilization.
