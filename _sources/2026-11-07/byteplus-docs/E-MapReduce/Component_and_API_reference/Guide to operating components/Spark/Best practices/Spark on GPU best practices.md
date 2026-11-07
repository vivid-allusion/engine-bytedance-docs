---
title: "Spark on GPU best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_on_GPU_best_practices"
---

<span id="_1-简介"></span>
## 1 Introduction

With the advancement of computing technology, optimizations at the software logic layer have gradually reached a plateau, so various engines are shifting toward leveraging underlying hardware. A typical example is native computing engines represented by Databricks Photon. These computing engines fully utilize the computational advantages of CPUs, including SIMD acceleration, pipelined computation, and efficient CPU caching.

Unlike approaches that fully leverage CPU features, computation on GPU adopts a different strategy. The main characteristic of GPUs is their large number of compute cores, making them particularly suitable for parallel processing of many computational subunits with identical logic. For scenarios such as data warehouses, where large batches of rows are processed according to the same logic at once, GPUs are highly suitable.

Based on this, Nvidia launched the Rapids project. The [Spark Rapids](https://nvidia.github.io/spark-rapids/) subproject uses GPUs to accelerate Spark operators. According to Nvidia's tests, GPU\-based acceleration can achieve an average performance improvement of several times, while cost savings can reach 30%–80% of the original (depending on different hardware test environments).

Volcano Engine E\-MapReduce (EMR) provides GPU instance types and supports Spark Rapids. You can select this instance type when creating a cluster and, with simple configuration, use Spark Rapids.

<span id="_2-使用限制"></span>
## 2 Limits


1. Spark Rapids supports most DQL operators, but not all of them. When encountering unsupported operators, Spark Rapids will fall back to native operators.

2. Spark Rapids is more **suitable** for high\-cardinality join, aggregation, window, sort, and scenarios where UDFs include CUDA computation or encoding computation. It is **less suitable** for small data volumes, heavy I/O (including shuffle), GPUs with limited memory, and scenarios where UDFs involve extensive logical computation (frequent interaction with CPU).

3. There are certain compatibility issues between Spark Rapids operators and native operators, such as floating\-point calculations. For more details, refer to the [Spark Rapids official documentation](https://nvidia.github.io/spark-rapids/docs/compatibility.html).

4. Currently, EMR does not support instance types other than T4 and V100 (does not support [Multi-Instance GPU](https://github.com/NVIDIA/spark-rapids-examples/tree/main/examples/MIG-Support), Mig).

5. For cards that do not support Mig, it is not possible to virtualize multiple cards from a single physical card, so the number of GPUs per node is equal to the number of physical cards. This means that during Yarn scheduling, only one container on a node can own this card. Therefore, **one card can only serve one executor**. However, you can still launch a large executor and achieve high concurrency by configuring multiple tasks (spark.rapids.sql.concurrentGpuTasks).

   For cards that support Mig (such as A100), a single card can be virtualized into multiple virtual cards, so this issue does not exist.

6. We are aware of the following GPU cluster risks and will gradually address them in future versions:

   * In scenarios suitable only for mixed deployment of regular Spark tasks and custom GPU computing, the cluster's non\-Master nodes contain both GPU instances and non\-GPU instances. Submitting Spark on GPU tasks is not supported; only regular Spark tasks can be submitted.

   * Currently, GPU instances do not support submitting Spark on GPU tasks that include Delta Lake, Hudi, or Iceberg formats.


<span id="_3-集群开通"></span>
## 3 Cluster activation


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. After selecting project and region information, on the **Overview** page, click the **Create cluster** button to enter the cluster creation process page.

3. After completing the basic **software settings**, go to the **Hardware configuration \> Instance settings** page, and click the **Edit** button in the **Actions** column on the right side of the Core node group to select GPU compute nodes for the Core node group.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because GPU resources in ECS are currently limited, if GPU compute instances are not currently available, you can try switching the availability zone information, or provide feedback to ECS support by submitting a ticket via .   </div>
   

4. Click the **Confirm** button to complete the selection of GPU instance types.

5. For the remaining steps in cluster creation, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0601e83c2fb35539bb79a701f98660df.png) </span>

<span id="_4-yarn-配置"></span>
## 4 Yarn configuration

To use Spark Rapids, you only need to make simple configurations to the Yarn component service.

For different hardware cards, the Yarn component requires different configurations:


* For ordinary cards that do not support Multi\-Instance (mig), you can use the built\-in Yarn gpu plugin.

* For high\-performance cards like A100 that can virtualize multiple cards in hardware, you need to use the Nvidia\-provided miggpu plugin.


<span id="_4-1-普通卡"></span>
### 4.1 Ordinary cards


* resource\-types.xml (or yarn\-site.xml)

   ```java
      <property>
        <name>yarn.resource-types</name>
        <value>yarn.io/gpu</value>
   </property>
   ```
   

* yarn\-site.xml

   ```java
   <property>
       <name>yarn.nodemanager.resource-plugins</name>
       <value>yarn.io/gpu</value>
   </property>
     
   <property>
        <name>yarn.nodemanager.resource-plugins.gpu.allowed-gpu-devices</name>
        <value>auto</value>
   </property>
   ```
   


After configuring, restart Yarn. You will see that GPU resources are now supported:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7284a29541d3713b525ff2f10c88e8b.jpg) </span>

<span id="_4-2-mig-卡"></span>
### 4.2 Mig cards

Refer to the [configuration reference](https://github.com/NVIDIA/spark-rapids-examples/tree/main/examples/MIG-Support/device-plugins/gpu-mig) provided by Nvidia.

<span id="_5-使用"></span>
## 5 Usage

<span id="_5-1-启动任务"></span>
### 5.1 Start tasks


* You can use Spark directly as before; EMR has already completed the relevant configuration:

   ```java
   ./bin/spark-shell
   ```
   

* The manual configuration steps are as follows:

   ```java
   ./bin/spark-shell \
       --conf spark.plugins=com.nvidia.spark.SQLPlugin \
       --conf spark.rapids.sql.concurrentGpuTasks=2
   ```
   


<span id="_5-2-确认是否已启用-gpu-资源"></span>
### 5.2 Confirm whether GPU resources are enabled


1. After you click Submit Job, you can see that GPU resources are enabled in the Spark UI interface:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ae4b11dad813563bf9708e3e99b7482.png) </span>

2. Start spark\-shell and execute the following statements. You can see in the diagram that the operator has already run on the GPU:

   ```java
   val seq= Seq(("1","xiaoming",15),("2","xiaohong",20),("3","xiaobi",10))
   var rdd1 = sc.parallelize(seq)
   val df = rdd1.toDF("id","name","age")
   df.select("name","age").filter("age >10").show
   df.select("name","age").filter("age >10").explain //Display the execution plan
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1868a43e54211bccd3b9665f86c841ba.png) </span>
