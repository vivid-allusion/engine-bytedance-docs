---
title: "Create and Submit Job"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_and_Submit_Job"
---

This article introduces how to create and submit Spark jobs for an EMR on ECS cluster through the console. EMR on ECS clusters support PySpark, SparkJar, and SparkSQL jobs.

<span id="995e1616"></span>
# Context

Job: A job is a complete data computing task. When a user needs to submit a data computing task in an EMR on ECS cluster, they can submit a job in EMR. After the job is submitted, the system uses the cluster's computing resources to execute the job.

<span id="b166ef7b"></span>
# Prerequisites

An available EMR on ECS cluster exists, and the cluster has enabled the Spark service. For detailed operations on creating a cluster, see [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

<span id="03937498"></span>
# Limits

Supported Spark job types for EMR on ECS clusters:


|**Job type** |**Note** |**Console submission supported** |**Command line submission supported** |
|---|---|---|---|
|PySpark |Spark jobs written in Python, run by submitting .py scripts. Suitable for data processing, machine learning, and similar scenarios. |✅ |✅ (submitted via spark\-submit) |
|Spark JAR |Spark jobs written in Java or Scala and packaged as .jar files. Suitable for scenarios with high performance requirements or existing JVM environments. |✅ |✅ (submitted via spark\-submit) |
|Spark SQL |Spark jobs written in SQL and executed through Spark's SQL engine. Suitable for data queries, report statistics, and similar scenarios. |✅ |✅ |
|Spark R |Spark jobs written in R (based on SparkR), suitable for statistical analysis and data science scenarios. |❌ |✅ (submitted via spark\-submit) |


<span id="cdfd3464"></span>
# Create and submit jobs: via the console

You can create jobs in the EMR console at \*\*Job center \*\*\> \*\*Job management \*\* or **Job instance**, and click \*\*Create job \*\* in the upper right corner to create a job. The operation entry is as follows. For detailed operations on creating jobs via the console, see: [作业中心](https://docs.byteplus.com/docs/undefined/6a5c65bbc5a03805304ff848). The actual job operation details for EMR on ECS are subject to the interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8c3388e6103451b81b600e4fe711922~tplv-goo7wpa0wc-image.image) </span>

<span id="6c065266"></span>
# Create and submit jobs: via the command line

<span id="93b1caa7"></span>
## Job creation entry

Log in to the primary node from the EMR console:


1. Log in to [EMR console ](https://console.volcengine.com/emr/)[EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). In the left navigation bar, select **Resource Management \> on ECS**, and click the created cluster name to enter **the cluster details page.**  Then, click **Service List \> Spark \> expand Spark Client** on the left, and click the primary node ID to jump to the primary node details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79aa6ddf5825412d9d5c17591811e9f3~tplv-goo7wpa0wc-image.image) </span>

2. Click **Remote Connection** in the upper right corner of the primary node details page, select **Log in to ECS Terminal now** in the pop\-up window to enter the **Remote Login** page, enter the username and password, and log in to the node terminal. For detailed operations, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec1e6e78407d42be978b99589cb1ee6a~tplv-goo7wpa0wc-image.image) </span>


<span id="25538c17"></span>
## Submit Job

Submit Spark jobs via the command line.

This article takes the built\-in Spark examples as an example. You can directly submit this job in the command line.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The sample resource <code>spark-examples_<Versino>.jar</code> is provided with the cluster, and the specific file name varies depending on the Spark version. After or <a href="https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/instance?projectName=default">logging in to the cluster</a>, you can run the <code>find / -name "spark-examples*.jar" 2>/dev/null</code> command to view the actual JAR package name and path in the current cluster. For more Spark operations, see <a href="https://docs.byteplus.com/docs/E-MapReduce/spark_quickstart">Quickstart</a>.</div>


* <div data-tips="true" data-tips-type="tip">If Kerberos is enabled for the cluster, see <a href="https://docs.volcengine.com/docs/6491/1126555?lang=zh">Using Kerberos\-authenticated clusters</a> to complete user authentication before running jobs.</div>



Using `Spark 3.5.1` as an example, submit via the terminal command line:

```bash
spark-submit --class org.apache.spark.examples.SparkPi --master yarn --num-executors 3 --driver-memory 512m --executor-memory 512m --executor-cores 1 /opt/emr/current/spark3/examples/jars/spark-examples_2.12-3.5.1.jar
```


The important task parameters are explained as follows:


|**Parameter** |**Example** |**Note** |
|---|---|---|
|`class` |org.apache.spark.examples.SparkPi |Main class of the program |
|`master` |yarn |Program execution mode; options are yarn and yarn\-client |
|`num-executors` |3 |Number of parallel executors |
|`driver-memory` |512m |Memory used by the driver program; must not exceed the total memory resources of the node |
|`executor-memory` |512m |Memory size used by a single executor; must not exceed the total memory resources of the node |
|`executor-cores` |1 |Number of parallel tasks per executor |


<span id="40c6f70e"></span>
# View job execution results

After the job is executed, in the **Job center**\>**Job instance** page:


1. Select **Resource type\> EMR on ECS.** 

2. Select **Resource name\>**  and select the cluster name.


You can view the list and instance details of the **Job instance** submitted to the cluster (including job ID/name, status, type, log/diagnostic entry, and other information), and you can also jump to the corresponding job details page for troubleshooting and tracing. For more information, see [查看并管理作业实例](https://docs.byteplus.com/docs/undefined/6a5c65bbc5a03805304ff848#efb9c81f).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8672cc82cdc142518c6f84debf6bd2b3~tplv-goo7wpa0wc-image.image) </span>
