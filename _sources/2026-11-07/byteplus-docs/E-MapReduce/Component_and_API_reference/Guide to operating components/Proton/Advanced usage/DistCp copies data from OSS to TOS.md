---
title: "DistCp copies data from OSS to TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DistCp_copies_data_from_OSS_to_TOS"
---

DistCp is a tool for large\-scale data copying between clusters or within a cluster, enabling data transfer across different file systems. This article describes how to use DistCp to copy data from OSS to TOS.

<span id="5c6d4208"></span>
## 1 HDFS integration with Proton to access TOS

Please refer to [Proton access TOS configuration](https://docs.byteplus.com/docs/E-MapReduce/109388)

<span id="0aaad474"></span>
## 2 HDFS integration with Jindo to access OSS

<span id="13139216"></span>
### 2.1 Jindosdk preparation


1. Download and extract the latest version of jindosdk\-${version}.tar.gz. [Download address](https://github.com/cheyang/alibabacloud-jindo-sdk/blob/master/docs/user/6.x/6.2.0/jindodata_download.md)

2. On any node in the cluster, add jindo\-core\-${version}.jar and jindosdk\-${version}.jar to the Hadoop classpath.


```Shell
tar zxvf jindosdk-x.x.x-linux.tar.gz

# add link
ln -sf jindo-core-${version}.jar $HADOOP_HOME/share/hadoop/hdfs/lib/
ln -sf jindosdk-${version}.jar $HADOOP_HOME/share/hadoop/hdfs/lib/
```


<span id="36ef7777"></span>
### 2.2. Configuration file modification

Add the object storage FileSystem implementation class to core\-site.xml, using OSS as an example.

```XML
<configuration>
    <property>
        <name>fs.AbstractFileSystem.oss.impl</name>
        <value>com.aliyun.jindodata.oss.OSS</value>
    </property>
    <property>
        <name>fs.oss.impl</name>
        <value>com.aliyun.jindodata.oss.JindoOssFileSystem</value>
    </property>
</configuration>
```


To access object storage, region and authentication information are required. These can be configured in core\-site.xml:


* core\-site.xml


```XML
<configuration>
    <property>
        <name>fs.oss.accessKeyId</name>
        <value>********</value>
    </property>

    <property>
        <name>fs.oss.accessKeySecret</name>
        <value>********</value>
    </property>

    <property>
        <name>fs.oss.endpoint</name>
        <!-- In Alibaba Cloud ECS environments, it is recommended to use the internal OSS Endpoint, that is, oss-cn-xxx-internal.aliyuncs.com -->
        <value>oss-cn-xxx.aliyuncs.com</value>
    </property>
</configuration>
```


<span id="43c429e7"></span>
### 2.3. Verify connectivity to OSS with the configuration

```Shell
# 确定可以通过hdfs命令查看到OSS桶里的文件，需要集群的每个节点都能访问到OSS桶里的文件
hdfs dfs -ls oss://test-bucket/ 
```


<span id="e6bf8601"></span>
## 3 Use the DistCp command to migrate data

```Shell
# 构造 DistCp命令将HDFS数据拷贝到TOS
 hadoop distcp \
 -Dmapreduce.job.queuename=default \
 -Dmapreduce.job.name=oss->tos  \
 -i  \
 -update \
 -delete  \
 -direct \
 -m 50 \
 -bandwidth 50 \
 -numListstatusThreads=40 \
 -skipcrccheck \
 oss://bucket-name/source_path \
 tos://bucket-name/my_target_path  
```


Parameter configuration:


|Parameter |Note |
|---|---|
|\-m |The maximum copy parallelism, corresponding to the maximum number of maps in the DistCp job. |
|\-bandwidth |The maximum bandwidth available to each map, Unit: MB/s. Use the \-m and \-bandwidth parameters to control the copy speed limit for the distcp job. Speed limit = number of maps \* bandwidth. |
|\-numListstatusThreads |The number of threads used to obtain metadata information from the namenode. |
|\-update |Copy files to the target that exist in src but not in target, and files that exist in both src and target but have different content. |
|\-delete |Delete files from the target that do not exist in src but exist in target. |
|\-useiterator |Use iterator to build CopyListing to avoid OOM. |
|\-i |Ignore errors during the DistCp process. |
|\-direct |By default, DistCp writes a temporary file and then renames it to the target file. With \-direct, data is written directly to the target. |
|\-atomic |All files are copied to a temporary directory and, after all copying is complete, are renamed to the target directory. Do not use this option in TOS scenarios. |
