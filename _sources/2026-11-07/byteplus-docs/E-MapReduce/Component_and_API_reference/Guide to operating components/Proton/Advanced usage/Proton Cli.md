---
title: "Proton Cli"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_Cli"
---

Proton CLI supports operations on Proton data cache, metadata cache, and statistics.

<span id="_1-前置条件"></span>
## 1 **Prerequisites**


* Use EMR 3.5.1 or later cluster versions and select the Proton service

* For Hadoop authentication configuration regarding TOS, refer to: [Hadoop uses Proton](https://docs.byteplus.com/docs/E-MapReduce/109384)

* For Proton cache configuration, refer to: [Proton no-cache mode](https://docs.byteplus.com/docs/E-MapReduce/109380),[Proton cache mode](https://docs.byteplus.com/docs/E-MapReduce/109381)


<span id="_2-命令使用"></span>
## 2 Command usage

<span id="_2-1-缓存加载"></span>
### 2.1 Cache loading

```bash
proton load [options] <path>
```



|Parameter |Description |
|---|---|
|\-h, \-\-help |Display help information |
|\-m,\-\-meta |Load metadata from the specified path to the proton metaserver |
|\-d,\-\-data |Load data from the specified path to the proton data server.<br><br>Depends on [\-m |
|\-t,\-\-threads |Load data or metadata using multiple threads |
|\-v,\-\-verbose |Display more detailed information during the loading process |


<span id="_2-2-缓存清理"></span>
### 2.2 Cache cleanup

```bash
proton evict [options] <path>
```



|Parameter |Description |
|---|---|
|\-h, \-\-help |Display help information |
|\-t,\-\-threads |Perform cache cleanup using multiple threads |
|\-v,\-\-verbose |Display more detailed information during the loading process |


<span id="_2-3-检查缓存数据块"></span>
### 2.3 Check cache data blocks

```bash
proton fsck [options] <path>
```



|Parameter |Description |
|---|---|
|\-h, \-\-help |Display help information |
|\-t,\-\-threads |Check the health status of cache data blocks using multiple threads |
|\-v,\-\-verbose |Display more detailed information during the loading process |


<span id="_2-4-同步缓存数据块"></span>
### 2.4 Synchronize cache data blocks

```bash
proton sync [options] <path>
```



|Parameter |Description |
|---|---|
|\-h, \-\-help |Display help information |
|\-t,\-\-threads |Check the health status of cache data blocks using multiple threads |
|\-v,\-\-verbose |Display more detailed information during the loading process |


<span id="_2-5-获取缓存数据块信息"></span>
### 2.5 Obtain cache data block information

```bash
proton showblk [options] <file_path>
```



|Parameter |Description |
|---|---|
|\-h, \-\-help |Display help information |
|\-v,\-\-verbose |Display more detailed information during the loading process |


<span id="_2-6-metaserver和dataserver启动、停止、查看"></span>
### 2.6 Start, stop, and view MetaServer and DataServer

```bash
proton --daemon [start|stop|status] [metaserver|dataserver]
```



|Parameter |Description |
|---|---|
|\-\-daemon |The daemon supports the options start, stop, and status |


<span id="_3-faq"></span>
## 3 FAQ

Q1: What is the difference between the load and sync commands?


* The load command is generally used when the source data does not exist in the Proton Cache system, incrementally synchronizing the source data to the Proton Cache system. After load completes, the source data will definitely be loaded into the Proton Cache system.

* The sync command is generally used when the cache data and the source data are inconsistent. It uses the source data as the standard and synchronizes the source data to the Proton Cache system. After sync completes, the cache data and the source data will be consistent.


In summary, sync compares the differences between the two sides and uses the source data as the standard; load does not compare the differences, but only incrementally loads "new" data that has not been cached.
