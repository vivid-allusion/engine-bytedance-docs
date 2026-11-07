---
title: "Task Backpressure"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Task_Backpressure"
---

This article introduces common causes of Task Backpressure in Flink and suggestions for handling it.

<span id="ddc0ea2b"></span>
## Background Information

Before reviewing this content, it is recommended to first check the background information.

**What is Backpressure?** 

First, understand backpressure through the classic "producer\-consumer model".

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTI1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxMjIgMzIgTCAxOTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMDAuODggMzIgTCAxOTMuODggMzUuNSBMIDE5NS42MyAzMiBMIDE5My44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PlByb2R1Y2VyczwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzOTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggMzIgTCAzOTMuODggMzUuNSBMIDM5NS42MyAzMiBMIDM5My44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjAyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UXVldWU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQwMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNvbnN1bWVyczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

In this model, there are producers, consumers, and a fixed\-size queue. Producers are responsible for generating data and writing it into the queue, while consumers retrieve data from the queue. When the consumer's capacity to consume is less than the producer's capacity to produce, data will begin to accumulate in the queue until it is full, at which point the producer will be blocked and unable to continue producing data. The producer may also be a consumer of other queues, and the accumulation phenomenon will continue to propagate upstream to the source, which is the phenomenon of backpressure.

When a Flink Job is deployed on different TaskManagers, backpressure may also occur during the transition from TaskA to TaskB.

**Flink Internal Communication Model**

Scenario Simulation: A Flink Job contains TaskA and TaskB, with a parallelism of 4, namely TaskA.1~4 and TaskB.1~4. This Flink Job is deployed across 2 taskmanagers, each allocating 2 slots. Since Flink supports different types of Tasks being placed in the same slot, the entire allocation is as follows:


| |**B.1** |**B.2** |**B.3** |**B.4** |
|---|---|---|---|---|
|**A.1** |local ||remote ||
|**A.2** |||||
|**A.3** |remote ||local ||
|**A.4** |||||


TaskManager1 allocates A1, A2, B1, B2; TaskManager2 allocates A3, A4, B3, B4. Tasks located within the same Taskmanager communicate via `local` transmission, and Tasks between different TaskManagers communicate via `remote` transmission.

**Data Flow Process Within TaskManager**

The TCP Channel between two TaskManagers is shared, for example, A1 \-\> B3/B4 and A2 \-\> B3/B4 use the same TCP Channel.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61665a054bd72b259b3bbaf1f241f17b.png) </span>

From the diagram above, it can be concluded that producer TaskA needs to go through 2 steps to send data to TaskB:


* TaskA writes the data it generates through RecordWriter serialization to an Output Queue Buffer. The Output Queue Buffer has a fixed length and will block writing when full.

* Through the underlying network transmission, data from the Output Queue Buffer in TaskManager1 is transferred to the Input Queue Buffer in TaskManager2. Then, RecordReader reads and deserializes the data from the Input Queue Buffer for processing by TaskB. The Input Queue Buffer also has a fixed length and cannot continue to receive data from the underlying network when full.


**Flink Backpressure Mechanism**

If Subtask B.4's processing capability decreases, falling below the QPS of Subtask A.2's input, the following phenomenon will occur:


1. First, the Input Queue Buffer of Subtask B.4 will fill up, then backpressure will propagate upward, causing congestion in the network transmission channel.

2. Continuing to propagate backpressure, the Output Queue Buffer of Subtask A.2 also fills up, then continues to exert backpressure on the data processing QPS of Subtask A.2.

3. Continuing to propagate backpressure, until reaching the data source. If it is a KafkaSource, it cannot continue consuming data from Kafka, thus resulting in Lagsize.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f95f862db3c4f29a920e5c8dd304709.png) </span>

This backpressure mechanism has a drawback. When data skew occurs and Subtask A.2 generates a large volume of data to Subtask B.4, the backpressure can affect the production capability of Subtask A.1. If you would like to learn more about Flink's backpressure mechanism, please refer to [Flink's Network Stack](https://flink.apache.org/2019/06/05/flink-network-stack.html).

<span id="69bd0b77"></span>
## Common causes of backpressure

Introduction to common causes of backpressure.

<span id="24f8efd5"></span>
### Reason one: Insufficient resources

Insufficient Container CPU, leading to inadequate computing capacity and resulting in backpressure.

You can observe the usage of **Container CPU** and **Application CPU**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24ea563c68cae7a83fc748248b6713cd.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70aa29a971cc09a8d1f79a88fff35648.png) </span>

Due to cgroup policy reserving 20% buffer for each Container, you can distinguish between high and low load by considering 100%.


|**Is there a shortage of resources?**  |**Container CPU < 100% \* tm_cores** |**Container CPU \> 100% \* tm_cores** |
|---|---|---|
|Application CPU < 80% \* total_cores |No |Uneven load |
|Application CPU \> 80% \* total_cores |NA (not applicable) |Yes |


When resources are insufficient, you can choose to reduce single tm_slots and increase the number of tm_num. If load imbalance occurs, please refer to the troubleshooting approach for load imbalance.

<span id="59004fef"></span>
### Reason two: Load imbalance

When there is an uneven load, two reasons need to be analyzed:


* Whether there is data skew;

* Whether the Task scheduling is uneven.


**Judge whether there is data skew**

You can view the Max and AVG values of each Operator QPS in Flink Metric. If there is a significant difference between the two values, it indicates data skew.

As shown in the diagram below, if the max and avg difference in Bolt QPS is about 9 times, it indicates data skew.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77aef9fd43e4d46ab8747f766c07e5c9.png) </span>

**Whether the Task is scheduled unevenly**

If the concurrency of Tasks and Containers is not proportional, it means different numbers of Tasks are allocated to different Containers.


* GC pressure

   In the Flink Dashboard by default, there are indicators for YGC and FGC. Please view the relevant indicators as needed. Generally, it is only necessary to pay attention to the FULL GC indicator.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3f9ac9b73b1c9e34246df926fd89e07.png) </span>

* Task Latency is relatively high.

   Some tasks take a long time to execute. If there are IO operations between tasks, check if IO Latency is too high. You can view Latency on the Flink Dashboard, which records the execution time of each task.

   As shown in the diagram below, the map latency is 10s. In such cases, you can optimize the task processing capability or increase concurrency.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34dcfcb925053e6e5d621b696e5c5c35.png) </span>

* System Resources

   When encountering high overall load on a single machine (commonly seen in Bigbang queues and shared Share queues), this situation generally causes local Partition delays.

   When encountering network anomalies on a single machine, it generally leads to a slower Network Stack, causing delays.

   Such issues are difficult to troubleshoot independently; please submit to **Oncall**.

* Single\-thread bottleneck

   Flink Java/SQL tasks generally run a single Task on a single thread, which can only fully utilize one CPU.

   You can monitor the number of Tasks assigned per Container and the CPU usage of that Container. If Container CPU usage reaches the number of cores equal to the Tasks assigned, a single\-thread bottleneck may occur.

   If a single\-thread bottleneck occurs, you can increase concurrency.


<span id="382f92e6"></span>
## Flink backpressure monitoring

How to determine if lag size is caused by backpressure? You can manually trigger backpressure in the Flink WebUI to check its status; alternatively, check the InputQueueUsage and OutputQueueUsage ratios of Tasks within the Flink Job.

Assuming the Job has two Tasks connected by key, to simulate backpressure, you can add a 10\-second sleep logic in the Map Operator.

The GAG diagram is shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba2c371f374b6df31a5b901f3a400752.png) </span>

<span id="0bf01d7c"></span>
### Flink WebUI

You can perform backpressure detection on any Task in Flink Web. Backpressure detection requires manual activation. After activation, TaskManager uses Thread.getStackTrace to sample and detect whether the Task Thread is waiting for NetworkBuffer.

The backpressure state is determined based on the sampling ratio and is categorized into three states: OK, LOW, and HIGH. Ratio indicates the proportion of n samples in which the thread is waiting for NetworkBuffer.


* OK：`ratio ≤ 0.10`

* LOW：`0.10 < Ratio ≤ 0.5`

* HIGH：`0.5 < Ratio ≤ 1`


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6db5a22fff5f31c992309ffd2bd76e41.png) </span>

You can check from Sink → Source in reverse order. The first Task found in a HIGH state might be the root cause of backpressure (not absolute). Since this Task is under backpressure, it will propagate this state upstream until Source. This detection method has some inherent drawbacks:


* Instant triggering, unable to observe historical situations.

* Tasks with high concurrency require a long detection time.

* Impacts the normal running state of tasks.

* Unable to accurately determine the root cause of backpressure.


<span id="8feb16ca"></span>
### Flink Network Metric

In each Flink Job, every Task has an InputQueue and OutputQueue. You can judge by observing the ratio of InputQueueUsage to OutputQueueUsage.


|**Proportional situation** |**OutputQueueUsage < 1.0** |**OutputQueueUsage == 1.0** |
|---|---|---|
|InputQueueUsage < 1.0 |Normal |Under backpressure, possibly due to insufficient downstream processing capability of this Task. If this continues, this Task will pass backpressure upstream. |
|InputQueueUsage == 1.0 |Under backpressure, this Task may be the source of the backpressure. If this continues, this Task will pass backpressure upstream. |Under backpressure, possibly blocked by downstream. |


When a task is under backpressure, you can check in reverse order from Sink \-\> Source until you find the first task with InputQueueUsage High and OutputQueueUsage Low.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_222b9cbe7b7815ca570b20b05b120eda.png) </span>
