---
title: "Technical principles"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Technical_principles"
---

Daft is a computing engine designed for DATA + AI multimodal data processing and analysis scenarios. It supports both standalone and distributed operation modes, is implemented in Rust, and provides two interaction methods: SQL and Python DataFrame.

<span id="ace14f18"></span>
# Overall architecture

Considering the characteristics of multimodal data processing in DATA + AI scenarios, Daft adopts a Pipeline execution model for its overall architecture design. Applications written by users through the Daft DataFrame or SQL API are first represented internally in Daft as an abstract syntax tree (AST: Abstract Syntax Tree). After a series of optimization and transformation rules are applied, this abstract syntax tree is converted into a Pipeline tree that can be executed by the underlying execution engine, and is finally submitted to either the standalone or distributed execution engine for execution.

<span id="a0615447"></span>
## Architecture layering

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67ce46f7b5e24fa59234bf0193d9c955~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, the overall architecture of Daft can be divided into three layers: the API layer, the Plan layer, and the execution layer:


* **API layer**: Provides two access APIs, SQL and Python DataFrame. By abstracting distributed data into tables and partitioning it by rows into multiple partitions distributed across the nodes of the cluster for distributed processing, parallel computation of data is achieved. By default, Daft partitions data using heuristic strategies (for example, by adopting the default partitioning strategy of files), and also supports manual repartitioning.

* **Plan layer**: Based on the SQL input by the user or the constructed DataFrame object, a logical execution plan (LogicalPlan) is built. The built\-in LogicalPlan optimizer is used to optimize it (for example, eliminating CrossJoin/Subquery/Repartition, predicate pushdown, column pruning, join reordering, and more) to obtain an optimized LogicalPlan. The optimized LogicalPlan is further converted into a PhysicalPlan, and the PhysicalPlan optimizer is used for further optimization (for example, eliminating unnecessary repartitioning).

* **Execution layer**: Daft supports both standalone and distributed operation modes. The PhysicalPlan constructed by the Plan layer needs to be further divided into a series of executable tasks according to the specific operation mode. The Scheduler then dispatches these tasks to the standalone Swordfish engine or the distributed Flotilla engine for execution, while also managing the execution status of the tasks.


<span id="8d3f62ec"></span>
## Plan example

Let us take the following DataFrame as an example to explain, from the perspective of the overall execution pipeline, how Daft starts from this DataFrame and ultimately generates the execution flow of the PhysicalPlan through optimization and transformation.

```Python
df = daft.read_parquet("/opt/workspace/daft/data")

df = (
    df
    .select("id", "name")
    .sort(by="id", desc=True)
    .filter(col("id") < 127)
    .offset(100)
    .limit(10)
)

df.to_pydict()
```


This is a relatively simple DataFrame example, used to read a parquet dataset and filter out 10 records as required. Internally, Daft represents the DataFrame by converting it into a LogicalPlan according to the construction order:

```Plain
* Limit: 10
|
* Offset: 100
|
* Filter: col(id) < lit(127)
|
* Sort: Sort by = (col(id), descending, nulls first)
|
* Project: col(id), col(name)
|
* GlobScanOperator
|   Glob paths = [/opt/workspace/daft/data]
|   Coerce int96 timestamp unit = Nanoseconds
|   IO config = ...
|   Use multithreading = true
|   File schema = id#Int64, name#Utf8, email#Utf8
|   Partitioning keys = []
|   Output schema = id#Int64, name#Utf8, email#Utf8
```


Considering that the DataFrame or SQL written by the user may not be optimal, Daft's internal LogicalPlan optimizer traverses and applies a series of optimization rules to the above LogicalPlan to achieve maximum execution efficiency, ultimately producing the following optimized LogicalPlan:

```Plain
* TopN: Sort by = (col(id), descending, nulls first), Num Rows = 10, Offset = 100
|   Stats = { Approx num rows = 110, Approx size bytes = 3.01 KiB, Accumulated
|     selectivity = 0.01 }
|
* Num Scan Tasks = 112
|   File schema = id#Int64, name#Utf8, email#Utf8
|   Partitioning keys = []
|   Projection pushdown = [id, name]
|   Filter pushdown = col(id) < lit(127)
|   Output schema = id#Int64, name#Utf8
|   Stats = { Approx num rows = 3,279, Approx size bytes = 92.09 KiB, Accumulated
|     selectivity = 0.30 }
```


The optimized LogicalPlan is much more streamlined compared to the original, resulting in improved execution efficiency. From the optimized LogicalPlan above, we can also infer that Daft has roughly applied the following optimization rules:


* **Predicate pushdown**: Operations such as `.filter(col("id") < 127)` and `.select("id", "name")` are pushed down to the data scan stage, significantly reducing the amount of data scanned.

* **Limit Offset rewriting**: The semantics of `.offset(100).limit(10)` are achieved by rewriting it as `global_limit(10, 100)` and `local_limit(0, 110)` to implement `offset...limit`.

* **Sort Limit rewriting**: The semantics of sorting and truncation are implemented by rewriting `.sort(by="id", desc=True).limit(10, 100)` as a TopN operator.


The optimized LogicalPlan is further converted into a PhysicalPlan, with additional optimization rules applied specifically to the PhysicalPlan. For example, the optimized LogicalPlan above would be converted into the following PhysicalPlan:

```Plain
* TopN: Sort by = (col(0: id), descending, nulls first), Num Rows = 10, Offset
|     = 100
|   Stats = { Approx num rows = 110, Approx size bytes = 3.01 KiB, Accumulated
|     selectivity = 0.01 }
|
* ScanTaskSource:
|   Num Scan Tasks = 112
|   Estimated Scan Bytes = 180568
|   Pushdowns: {projection: [id, name], filter: col(id) < lit(127)}
|   Schema: {id#Int64, name#Utf8, email#Utf8}
|   Scan Tasks: [ ... ]
|   Stats = { Approx num rows = 3,279, Approx size bytes = 92.09 KiB, Accumulated
|     selectivity = 0.30 }
```


<span id="8fd5aef3"></span>
# Execution engine

Currently, mainstream data computation engines in the DATA + AI field (such as Pandas and Polars) only provide single\-node execution mode by default. The distributed version of Polars is only available in the commercial edition, while Dask, although considered a distributed version of Pandas, has relatively low execution efficiency. Daft provides both single\-node and distributed execution modes in its open\-source version, and allows switching freely between these two modes.

<span id="91a438fe"></span>
## Single\-node execution engine

By default, Daft executes user\-input SQL or constructed DataFrames in single\-node mode. Its single\-node execution engine, Swordfish, is implemented in Rust and designed based on the Pipeline computation model, leveraging multithreading to achieve parallel data processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0c4eda40f73402f93faae6a8a256980~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, the PhysicalPlan on the left is parsed by the Swordfish engine into a Pipeline tree. The engine traverses the tree in a depth\-first manner and sequentially starts and runs each node. Swordfish PipelineNode includes four types of nodes:


|Node type |Definition |Concurrency |Operator examples |
|---|---|---|---|
|SourceNode |Data source node |Depends on the number of data shards, with a default upper limit of 8 |ScanTaskSource |
|IntermediateNode |Intermediate processing node |Depends on the specific operator type; defaults to the number of CPU cores on the node |Project、Filter、UDF、JoinProbe |
|BlockingSinkNode |Blocking data receiving node |Depends on the specific operator type; defaults to the number of CPU cores on the node |Aggregate、JoinBuild、TopN、Sort |
|StreamingSinkNode |Streaming data receiving node |Depends on the specific operator type; defaults to the number of CPU cores on the node |Limit、MonotonicallyIncreasingId |


Data transfer between nodes relies on the [Kanal Channel](https://github.com/fereidani/kanal).

<span id="4e9d4faf"></span>
## Distributed execution engine

Daft supports both standalone mode and distributed mode based on Ray. Users only need to configure the Ray cluster connection information to switch between standalone and distributed modes, without modifying the business logic layer.

Flotilla v1.5 is Daft's latest distributed execution engine. Its design goal is to provide better scalability, performance, and observability for multimodal data processing, supporting:


1. Robust handling of highly scalable multimodal mapping pipelines (reading URLs, downloading UDFs, and write mode).

2. Reliable shuffling of 10TB of data for exchange operations (groupby, join, sort).

3. Providing easy\-to\-understand and actionable observability tools.

4. Allowing Daft developers to quickly debug and iterate.


In terms of design philosophy, Flotilla v1.5 **uses Ray to distribute multiple Swordfish standalone execution engines, enabling data shuffling between nodes via the built\-in Flight Shuffle Server**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4ce5b650ffb47939c5617ef644045a4~tplv-goo7wpa0wc-image.image) </span>

The Flotilla distributed execution engine implementation includes the following core components:


* **Ray Worker Manager**: Manages Swordfish Worker nodes on the Ray cluster, ensures that each Ray Worker node runs a RaySwordfishActor, and is also responsible for triggering Ray cluster Autoscale as needed, as well as submitting Swordfish Tasks to target Worker nodes for execution.

* **Plan Runner**: Responsible for executing the PhysicalPlan by splitting the corresponding StagePlans into a series of SwordfishTasks, which are scheduled by the Scheduler for execution on the Ray cluster.

* **Scheduler**: Continuously monitors the task queue for pending SwordfishTasks and uses the Dispatcher to distribute tasks to the Ray cluster for execution. Additionally, the Scheduler is responsible for triggering Ray cluster Autoscale upon receiving Autoscale requests.

* **Dispatcher**: Organizes SwordfishTasks by Ray Worker node and submits tasks in batches to the target Worker nodes in the Ray cluster for execution.


A RaySwordfishActor runs persistently on each Ray Worker node, responsible for receiving the LocalPhysicalPlan contained within the SwordfishTask, which can be executed on a standalone Swordfish engine. When an execution request is received, the RaySwordfishActor submits the LocalPhysicalPlan to the local standalone Swordfish engine for execution. For details on the execution process, refer to Section 1 above.

**The Flotilla distributed execution engine has now evolved to version v1.5, with significant performance improvements compared to version v1.0. However, its feature completeness is relatively limited, so unsupported operations will fall back to version v1.0 to ensure jobs run properly.**  Unlike version v1.5, which uses the Actor model in conjunction with the standalone Swordfish execution engine to run Pipeline operators, version v1.0 splits each Stage into multiple Ray Remote Tasks and submits them in batches to the Ray cluster for execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b1d50959394c02b4079c20e85e7a31~tplv-goo7wpa0wc-image.image) </span>

As shown in the left diagram above, the core execution process of the PhysicalPlan in version v1.0 is as follows:


1. Based on the PhysicalPlanScheduler, the PhysicalPlan is divided into a series of Tasks, and Stages are split according to dependency relationships. A Task mainly consists of three attributes: input, a set of instructions, and resource description.

2. Tasks are batched according to the dependencies between Tasks and the number of tasks the current Ray cluster can execute (measured by available CPU), and are submitted in batches for execution using the Ray Remote Task mode.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23604b35922043ec82c737ee6430d0f1~tplv-goo7wpa0wc-image.image" width="1280px" /></div>



3. The Scheduler maintains a Queue internally to record the final execution results of tasks and provides an iterator for upstream access.


The Flotilla distributed execution engine was redesigned primarily because version v1.0 has the following two core issues compared to version v1.5:


1. **Low execution performance**: For moderately complex tasks, they are usually split into multiple Stages for execution, with each Stage containing a large number of Tasks. When scheduling, Daft prioritizes submitting the Tasks of child node Stages to the Ray cluster. When the number of Tasks is large, the execution mode often degrades from Pipeline to Stage by Stage. For heterogeneous computing scenarios such as multimodal data processing, Stage by Stage execution leads to insufficient resource utilization, resulting in inefficient processing performance.

2. **High memory pressure**: Ray clusters use the Object Memory Store to facilitate data exchange between tasks. The stage\-by\-stage execution model requires all upstream stage tasks to be completed before downstream stage tasks can begin. All intermediate data must be stored in the Object Memory Store, which results in significant memory pressure for Ray and can easily lead to OOM errors.
