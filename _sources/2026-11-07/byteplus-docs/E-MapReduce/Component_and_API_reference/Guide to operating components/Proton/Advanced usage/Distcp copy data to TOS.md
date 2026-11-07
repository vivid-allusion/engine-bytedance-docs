---
title: "Distcp copy data to TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Distcp_copy_data_to_TOS"
---

DistCp is a tool used for large\-scale data copying between clusters or within a cluster. It enables data copying between different file systems (mainly HDFS),

This article describes how to use DistCp based on Proton to copy data from HDFS to TOS.

<span id="_1-安装proton-sdk组件"></span>
## 1 Install the Proton SDK component

Reference: [Proton 无缓存模式](https://docs.byteplus.com/docs/E-MapReduce/109380#_2-%E5%AE%89%E8%A3%85proton-sdk%E7%BB%84%E4%BB%B6)

<span id="_2-使用distcp命令进行数据迁移"></span>
## 2 Use the DistCp command to migrate data

<span id="_2-1-迁移命令"></span>
### 2.1 Migration command

```shell
# 构造 DistCp命令将HDFS数据拷贝到TOS
>hadoop distcp \
 -Dmapreduce.job.queuename=default \
 -Dmapreduce.job.name=test-distcp  \
 -i  \
 -update \
 -delete  \
 -m 50 \
 -bandwidth 50 \
 -numListstatusThreads=40 \
 -skipcrccheck \
 -direct \
 hdfs://source_hdfs:8020/source_path \
 tos://bucket-name/my_target_path
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Because the file verification method of HDFS is inconsistent with that of TOS, you need to use the \-skipcrccheck parameter to skip the checksum verification. There is a risk of data inconsistency.</div>


* <div data-tips="true" data-tips-type="warning">When importing data into the TOS object storage service using the distcp tool, it is recommended to enable the \-direct option. This option can prevent distcp from copying source data to a temporary file and then using the rename operation to copy the temporary file to the destination file. Enabling \-direct can reduce the network bandwidth usage of object storage by half.</div>



<span id="_2-2-参数配置"></span>
### 2.2 Parameter configuration


|**Parameter** |**Note** | | |
|---|---|---|---|
|\-m |The maximum copy parallelism corresponds to the maximum number of maps in a DistCp job. | | |
|\-bandwidth |The maximum bandwidth each map can use, Unit is MB/s. Use the \-m and \-bandwidth parameters to control the copy speed limit of the distcp job. The speed limit = number of maps \* bandwidth | | |
|\-numListstatusThreads |Number of threads for obtaining metadata information from the namenode | | |
|\-update |Files that exist in src but not in target, and files that exist in both src and target but have different content, will be copied to target | | |
|\-delete |Files that do not exist in src but exist in target will be deleted from target | | |
|\-useiterator |Use iterator to build CopyListing to avoid OOM | | |
|\-i |Ignore errors during the DistCp process | | |
|\-direct |By default, DistCp writes to a temporary file first and then renames it to the target file. With \-direct, data is written directly to the target. | | |
|\-strategy |\-strategy=uniform: By default, DistCp uses the uniform strategy, which divides the dataset as evenly as possible among map tasks before copying, based on the dataset size.<br><br>\-strategy=dynamic: The dataset is divided into multiple small chunks, and each map task tries to consume chunks as much as possible, which can optimize long\-tail situations. Reasons for long\-tail:<br><br><br>* The node where the map task is located has a high load;<br><br>* A particular file is read significantly slower than other files; | | |
|||\-append |Files can be appended when they are not the same. Do not use this in TOS scenarios. |
|\-atomic |This will copy all files to a temporary directory, and after all files are copied, they will be renamed to the target directory at once. Do not use this in TOS scenarios. | | |


<span id="_2-3-高阶用法"></span>
### 2.3 Advanced usage

<span id="_2-3-1-dynamic策略"></span>
#### 2.3.1 **dynamic strategy**

Optimize the long\-tail issue by setting \-strategy=dynamic. Set total number of files to copy = TOTAL_FILE, number of maps = TOTAL_MAP, number of files per chunk is 100 (can be adjusted based on actual needs).


* Number of files each map needs to process = AVERAGE_MAP_FILE = ceiling(TOTAL_FILE/TOTAL_MAP).

* Number of chunks each map needs to process = ceiling(AVERAGE_MAP_FILE/100). Configure as mapred.listing.split.ratio.

* Total number of chunks = number of maps \* number of chunks processed per map = TOTAL_MAP, configure as distcp.dynamic.max.chunks.tolerable.


```plain
eg
1. 总文件数500w，map数150。
2. 单个map处理records数=500w/150=33334（向上取整），单chunk文件数设100是合适的。
3. 单map需要处理的chunk数=33334/100=334（向上取整）。
4. 总chunk数=150 * 334=50100。
5. 配置如下
   mapred.listing.split.ratio=334
   distcp.dynamic.max.chunks.tolerable=50100
```


<span id="_2-3-2-snapshot"></span>
#### 2.3.2 **snapshot**

When the source directory is continuously changing, you can use a snapshot to obtain a static copy of the source data for DistCp. It is recommended to take snapshots of level 1 or level 2 directories, and not to take snapshots of the root directory.

```shell
# 允许使用snapshot
>hdfs dfsadmin -allowSnapshot /source_path
# 创建snapshot
>hdfs dfs -createSnapshot /source_path source_path_snapshot_name
# 上述Distcp命令可以变成
>hadoop distcp \
-Dmapreduce.job.queuename=default \
-Dmapreduce.job.name=test-distcp  \
-i  \
-update \
-delete  \
-m 50 \
-bandwidth 50 \
-numListstatusThreads=40 \
-skipcrccheck \
-strategy dynamic \
-direct \
hdfs://source_hdfs:8020/source_path/.snapshot/source_path_snapshot_name \
tos://bucket-name/target_path
```


<span id="_3-faq"></span>
## 3 FAQ

**When using strategy=dynamic, if you encounter the following error:** 

```Java
java.io.IOException: Too many chunks created with splitRatio:2, numMaps:250. Reduce numMaps or decrease split-ratio to proceed.
        at org.apache.hadoop.tools.mapred.lib.DynamicInputFormat.validateNumChunksUsing(DynamicInputFormat.java:185)
```


You can increase the value of `distcp.dynamic.max.chunks.tolerable`. eg. Add `-Ddistcp.dynamic.max.chunks.tolerable=10000` to the DistCp command
