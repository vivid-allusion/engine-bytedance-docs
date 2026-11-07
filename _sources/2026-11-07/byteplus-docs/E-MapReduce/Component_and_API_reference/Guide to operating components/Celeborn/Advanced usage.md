---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/celeborn_advanced_usage"
---

<span id="_1-celeborn-on-hdfs"></span>
## 1 Celeborn On HDFS

Celeborn natively supports multiple storage media, including HDD, SSD, and HDFS. In most cases, HDD and SSD are used as the default storage, which ensures higher shuffle efficiency and lower memory usage. However, when disk resources are insufficient but there are idle HDFS resources, Celeborn on HDFS can be used to improve the stability of Spark jobs.


* Compared with HDD and SSD, HDFS is at a disadvantage in terms of read and write performance.

* Celeborn on HDFS requires more OffHeap memory.


<span id="_1-1-配置修改"></span>
### 1.1 Configuration modification

Go to Service List \-\> Celeborn \-\> Service Parameters \-\> celeborn\-defaults.conf, and make the following configuration changes


|Configuration item |Parameter value |Note |
|---|---|---|
|celeborn.worker.storage.dirs |None |This configuration must be commented out in HDFS mode |
|celeborn.storage.activeTypes |HDFS |Fixed value |
|celeborn.storage.hdfs.dir |hdfs://${NN_IP}/user/celeborn |The HDFS directory for storing shuffle data must be created in advance, and the permissions must be set to 755 |


Go to Service List \-\> Celeborn \-\> Service Parameters \-\> celeborn\-env.sh, and make the following configuration changes

```sql
# 适当增大该参数，可参考下面推荐值设置
CELEBORN_WORKER_OFFHEAP_MEMORY
HADOOP_CONF_DIR=/etc/emr/hadoop/conf
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In On HDFS mode,</div>


<div data-tips="true" data-tips-type="warning">For shuffle data volumes below 100G, it is recommended to set OffHeap to 1G–3G.</div>


<div data-tips="true" data-tips-type="warning">For shuffle data volumes between 100G and 1T, it is recommended to set OffHeap to 3G–30G.</div>


<span id="_1-2-提交作业"></span>
### 1.2 Submit Job

The job submission process is transparent and does not require any changes.

<span id="_2-spark-使用外置集群-celeborn"></span>
## 2 Spark uses external Celeborn cluster

Spark supports using a Celeborn service deployed in a different cluster under the same tenant. When multiple Spark clusters or multiple compute clusters are deployed in the same environment, users may consider using a unified Celeborn service to reduce redundant storage and improve resource utilization. Within the same tenant, for cross\-access between different EMR clusters, the VPCs of the clusters must be the same and configured identically.

<span id="_2-1-配置修改"></span>
### 2.1 Configuration modification

Open the compute engine, for example, the cluster console where Spark is located

Go to Service List \-\> Spark \-\> Service Parameters, search for the celeborn.master.endpoints parameter, and make the following configuration changes:


|Configuration item |Parameter value |Note |
|---|---|---|
|spark.celeborn.master.endpoints |Celeborn endpoints of the external Celeborn cluster |Search for the celeborn.master.endpoints parameter in the target cluster's Celeborn service parameters |


<span id="_2-2-验证配置是否生效"></span>
### 2.2 Verify whether the configuration takes effect

Check the log to confirm that the external Celeborn is being used

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f5adf5e2be3e874f9de2e6979894fdc.png) </span>
