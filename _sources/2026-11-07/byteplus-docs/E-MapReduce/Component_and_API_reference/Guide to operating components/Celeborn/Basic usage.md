---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/celeborn_basic_usage"
---

At this stage, Celeborn supports functioning as a Remote Shuffle Service for Spark and Flink engines. EMR provides quick integration configuration support for the Spark engine.


1. As an optional service, Celeborn must be manually selected for installation either during cluster creation or after the cluster is created. This document assumes that Celeborn has already been installed in your cluster.

2. EMR provides quick integration configuration support for the Spark engine, but does not currently support the Flink engine. You can refer to the official documentation to configure Flink integration with the Celeborn service.


<span id="_1-spark-集成"></span>
## Step 1: Spark integration

For clusters where the Celeborn service has already been installed, on the **Cluster Details \- Service List \- Spark** page in the EMR console, click the **Enable Shuffle Service** button to configure Spark to integrate with the Celeborn service in one step. This configuration will take effect after the Spark service is restarted. To disable the integration between Spark and the Celeborn service, similarly click the **Enable Shuffle Service** button again and restart the Spark service for the change to take effect.

Explanation of configuration items for Spark integration with Celeborn service (located in the `spark-defaults.conf` configuration file):


|Configuration item |Parameter value |Note |
|---|---|---|
|spark.shuffle.manager |org.apache.spark.shuffle.celeborn.SparkShuffleManager |Fixed value |
|spark.shuffle.service.enabled |false |Fixed value |
|spark.celeborn.master.endpoints | |List of Celeborn service master nodes, formatted as `<celeborn-master-ip>:<celeborn-master-port>`, separated by commas `,` |
|spark.sql.adaptive.enabled |true |Optional: Enable Spark AQE and disable local shuffle reader for better performance |
|spark.sql.adaptive.skewJoin.enabled |true ||
|spark.sql.adaptive.localShuffleReader.enabled |false ||


<span id="_2-celeborn-配置"></span>
## Step 2: Celeborn configuration

You can modify Celeborn service\-related configurations on the **Cluster Details \- Service List \- Celeborn \- Service Parameters** page in the EMR console. The most commonly used configuration items are shown in the table below:


|Configuration item |Parameter value |Note |
|---|---|---|
|CELEBORN_MASTER_MEMORY |2GB |Heap memory size for master nodes |
|CELEBORN_WORKER_MEMORY |1GB |Heap memory size for worker nodes |
|CELEBORN_WORKER_OFFHEAP_MEMORY |1GB |Off\-heap memory size for worker nodes |
|celeborn.storage.activeTypes |HDD,SSD |Storage media type, which can be HDD, SSD, or HDFS |
|celeborn.worker.flusher.buffer.size |256K |Buffer size for a single flusher on worker nodes |


For more configuration items related to Celeborn, refer to the [official configuration guide](https://celeborn.apache.org/docs/latest/configuration/).
