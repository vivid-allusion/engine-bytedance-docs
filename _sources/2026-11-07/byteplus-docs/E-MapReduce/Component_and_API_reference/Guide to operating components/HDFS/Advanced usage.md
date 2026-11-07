---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_advanced_usage"
---

<span id="_1-snapshot使用"></span>
## **Snapshot usage**

HDFS snapshots are read\-only, point\-in\-time copies of the file system. Snapshots can be taken for a subtree of the file system or for the entire file system. Some common use cases for snapshots are data backup, preventing user errors, and disaster recovery.

Snapshots are not simple copies of data; only differences are replicated, so snapshot creation is typically very fast. When creating a snapshot, blocks are not copied. The snapshot file only records the block list and file size, and does not copy any data.

The specific operation commands are as follows:


1. **Enable and disable snapshots for a specified directory**


```Plain
hdfs dfsadmin -allowSnapshot <hdfs path> #开启

hdfs dfsadmin -disallowSnapshot <hdfs path> #禁用

```



2. **Create a snapshot for a specified directory**


```Plain
hdfs dfs -createSnapshot <hdfs path>
# 创建快照之前，先要允许该目录创建快照(开启)

```



3. **Specify the name for the snapshot to be created**


```Plain
hdfs dfs -createSnapshot <hdfs path> <snapshot name>

# 其中<snapshot name>是自己指定的快照别名
# example：
hdfs dfs -createSnapshot /test snapshot1

```



4. **Rename a snapshot**


```Plain
hdfs dfs -renameSnapshot <hdfs path> <oldname> <newname>

#example:
hdfs dfs -renameSnapshot /test snap1 snap2
```



5. **Delete a snapshot**


```Plain
hdfs dfs -deleteSnapshot <path> <snapshotName>
```



6. **Obtain the list of snapshot directories for the current user**


```Plain
hdfs lsSnapshottableDir
```



7. **Compare the differences between two snapshots**


```Plain
hdfs snapshotDiff <path> <Snapshot1> <Snapshot2>
# example：
hdfs dfs -createSnapshot /test snapshot1
hdfs dfs -createSnapshot /test snapshot2
hdfs snapshotDiff /test snapshot1 snapshot2
```


For more detailed information about HDFS snapshots, refer to the Apache Hadoop community documentation.

<span id="_2-balance工具的使用"></span>
## **Using the Balance tool**

In a Hadoop cluster, it is common for disk space usage to be unevenly distributed across DataNodes. To balance space utilization, the balance tool is used in the HDFS cluster to perform **rebalancing**.

<span id="_2-1-emr-控制台-balance-操作"></span>
### Balance operations in the EMR console

The cluster operation page has a Rebalance button. You can quickly perform the operation by clicking the button, but it will use the default parameters for Rebalance. For details about the default parameters, see [Hdfsbalance data balancing optimization:](https://docs.byteplus.com/docs/E-MapReduce/109241#jump)


1. Log in to [the EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, click the **Cluster Management \> Cluster List \> Cluster Details \> Service List \> HDFS Service** button to enter the service overview page.

3. In the upper right corner of the service overview page, click the **Service Operations \> Rebalance** button to open the Rebalance configuration popup. Select the node range for Rebalance execution and add a note for this operation.

4. Click the **Confirm** button to complete the Rebalance operation. Wait for execution to finish to achieve balanced disk space utilization across nodes.


<span id="_2-2-balance-命令行方式操作"></span>
### **Balance command line operation**

The command to view hdfs balancer is as follows:

```Plain
hdfs balancer -help

Usage: java Balancer

[-policy <policy>] the balancing policy: datanode or blockpool

[-threshold <threshold>] Percentage of disk capacity

[-exclude [-f <hosts-file> | comma-sperated list of hosts]] Excludes the specified datanodes.

[-include [-f <hosts-file> | comma-sperated list of hosts]] Includes only the specified datanodes.

[-blockpools <comma-separated list of blockpool ids>]

[-idleiterations <idleiterations>]

[-runDuringUpgrade]
```


This tool repeatedly moves blocks from DataNodes with high utilization to those with low utilization.

The sample code for performing hdfs balance in an EMR cluster is as follows:

```Plain
start-balancer.sh -threshold 5 #其中 5是设置的阈值即5%
```


<span id="_2-3-hadoop-balance-的执行一般分为四步："></span>
### **The execution of Hadoop Balance generally consists of four steps:** 


1. Obtain the disk usage of datanodes from the namenode.

2. Calculate which data needs to be moved to which nodes.

3. Move the data accordingly, and after completion, delete the old block information.

4. Repeat the process until the balance criteria are met.


<span id="_2-4-balance-工具退出："></span>
### **Balance tool exit:** 

**The balance tool will exit automatically if any of the following five conditions are met:** 


1. The cluster is balanced;

2. No blocks can be moved;

3. No blocks have been moved for the specified number of consecutive iterations (default is 5);

4. An IOException occurs when communicating with the namenode;

5. Another balancer is running.


<span id="jump"></span>
### **Hdfsbalance data balancing optimization:** 


1. **Increase bandwidth**

   Modify the dfs.balance.bandwidthPerSec parameter in hdfs\-site.xml.

   Parameter description: Sets the bandwidth that the balance tool can use during operation. Setting this value too high may cause MapReduce jobs to run slowly. The default setting is 10M. It is usually recommended to set it to 100MB/s.

2. **Increase the maximum number of threads**

   Modify the dfs.datanode.max.transfer.threads parameter in hdfs\-site.xml.

   Parameter description: Specifies the maximum number of threads for transferring block data between DataNodes. It can be set to 4096.

3. **Increase the maximum number of threads for blocks to be moved by balance**

   Modify the dfs.datanode.balance.max.concurrent.moves parameter in hdfs\-site.xml.

   Parameter description: Specifies the maximum number of concurrent threads on a DataNode for blocks to be moved by balance. The default value is 5. It is generally set to the number of DataNode disks multiplied by 4.

   For more detailed information about using the hdfs balance tool, please refer to the Apache Hadoop community documentation.


<span id="_3-quotas使用"></span>
## **Quotas usage**

HDFS allows administrators to set quotas for each user and each folder: name quota and space quota.


* **name quota** ：

   Imposes a hard limit on the number of files and subdirectories in the directory. If the limit is exceeded, an error will be reported: quota exceed. Maximum quota: Long.MAX_Value. Newly created folders do not have a quota assigned by default.

* **space quota：** 

   Sets the size of a directory. If exceeded, block writes will fail (replicas are also counted). Maximum quota: Long.Max_Value. Directories themselves do not consume host file system space and are not counted toward the space quota. The data used by the host file system to record file metadata is also not included in the quota.


**Set quota:** 

```Plain
# 设置name quota
hdfs dfsadmin -setQuota <nums> <Directory>... <Directory>

# example:
hdfs dfsadmin -setQuota 9999 /user/test

```


```Plain
#设置space quota
hdfs dfsadmin -setSpaceQuota <capacity> <Directory>... <Directory>

#example:
hdfs dfsadmin -setSpaceQuota 15g /user/test

```


**View quota:** 

```Plain
hadoop fs -count -q [-h] [-v] [-t [comma-separated list of storagetypes]] <directory>...<directory>

#参数说明:

#-q选项，会报告为每个目录设置的name quota值，剩余的可用name quota，设置的SpaceQuota值和剩余的可用SpaceQuota。如果目录没有配额设置，则报告的值为none和inf。

#-h选项以人类可读格式显示大小。

#-v选项显示标题行。

#-t选项显示每个存储类型配额集以及每个目录的剩余可用配额

#example：

hdfs dfs -count -q /user/test

```


**Delete quota:** 

```Plain
#删除目录的name quota
hdfs dfsadmin -clrQuota <directory>...<directory>

#example：
hdfs dfsadmin -clrQuota /user/test

```


```Plain
#删除目录的sapce quota
hdfs dfsadmin -clrSpaceQuota <directory>...<directory>

#example：
hdfs dfsadmin -clrSpaceQuota /user/test

```


For more detailed information about hdfs Quotas, refer to the Apache Hadoop community documentation.

<span id="_4-dfsadmin命令"></span>
## **DFSAdmin command**

The 'bin/hadoop dfsadmin' command supports several operations related to HDFS management. The bin/hadoop dfsadmin \-help command lists all currently supported commands. For example:


* \-report: Reports basic statistics of HDFS. Some of this information can also be found on the NameNode web service homepage.

* \-safemode: Although it is usually not necessary, administrators can manually make the NameNode enter or exit safe mode.

* \-finalizeUpgrade: Deletes the cluster backup created during the previous upgrade.
