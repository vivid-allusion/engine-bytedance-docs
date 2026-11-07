---
title: "Best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_best_practices"
---

<span id="_1-控制小文件个数"></span>
## **1. Control the number of small files**


* Background: The HDFS NameNode loads all file metadata into memory. When the cluster disk capacity is fixed, having too many small files can cause a memory bottleneck for the NameNode.

* Recommendation: Minimize the number of small files as much as possible. For existing small files, it is recommended to merge them into larger files.


<span id="_2-配置回收站机制"></span>
## **2. Configure the trash mechanism**


* Background: In HDFS, deleted files are moved to the trash so that deleted data can be recovered in case of accidental operations. You can set the time threshold for files to remain in the trash. Once a file has been saved in the trash for longer than this threshold, the system will automatically and permanently delete the file from the trash. You can also manually delete files in the trash.

* Recommendation: On the **Service Parameters** page of the HDFS service in the EMR console, search for the parameter **fs.trash.interval**. This parameter specifies the trash retention time in minutes. Data in the trash that exceeds this time will be deleted. If set to 0, the trash mechanism is disabled. The default value is 360.


<span id="_3-配置-hdfs-单目录文件数量"></span>
## **3. Configure the number of files per HDFS directory**


* Background: When the cluster is running, different components (such as Spark and YARN) or clients may continuously write files to the same HDFS directory. However, the number of files supported in a single HDFS directory has an upper limit. Therefore, it is necessary to plan ahead to prevent the number of files in a single directory from exceeding the threshold, which could cause tasks to fail.

* Recommendation: On the **Service Parameters** page of the HDFS service in the EMR console, click the **hdfs\-site** tab, then click **Add Custom Parameter**, and add the parameter **dfs.namenode.fs\-limits.max\-directory\-items** to set the maximum number of files that can be stored in a single directory.


<span id="_4-在网络不稳定的情况下，降低客户端运行异常概率"></span>
## **4. Reduce the probability of client operation failures in unstable networks**


* Background: In unstable network conditions, adjusting the **ipc.client.connect.max.retries.on.timeouts** and **ipc.client.connect.timeout** parameters to appropriately increase the number of client retries and the timeout duration can reduce the probability of client operation failures.

* Recommendation: On the EMR console HDFS service **Service Parameters** page, search for the parameter **ipc.client.connect.max.retries.on.timeouts**. You can increase the value of this parameter to raise the maximum number of connection retries. Search for the parameter **ipc.client.connect.timeout**. You can increase the value of this parameter to extend the connection establishment timeout.


<span id="_5-配置可容忍的磁盘坏卷"></span>
## **5 Configure tolerable failed volumes**


* Background: If multiple data storage volumes are configured for a DataNode, by default, if any one volume fails, the DataNode will stop providing services.

* Recommendation: On the EMR console HDFS service **Service Parameters** page, search for the parameter **dfs.datanode.failed.volumes.tolerated**. You can modify this parameter to specify the number of tolerated failures. If the number of failed volumes is less than this value, the DataNode can continue to provide services.


<span id="_6-防止目录被误删"></span>
## **6 Prevent accidental directory deletion**


* Background: HDFS allows certain directories to be configured as protected to prevent accidental deletion. However, directories can still be moved to the recycle bin.

* Recommendation: On the EMR console HDFS service **Service Parameters** page, click the **core\-site** tab, then click **Add Custom Parameter**, and add the parameter **fs.protected.directories**. Set the parameter value to the directories you want to protect. Use commas (,) to separate multiple directories, and save the configuration.


<span id="_7-使用balancer进行容量均衡"></span>
## **7 Use Balancer for capacity balancing**


* Background: The HDFS cluster may experience imbalanced disk utilization across DataNode nodes, for example, when new DataNodes are added to the cluster. If HDFS data becomes unbalanced, it may cause excessive load on individual DataNodes.

* Recommendation: You can use the Balancer operation to balance capacity. Log in to a cluster node and run the following command:


```Plain
su hdfs
$hadoop-current/sbin/start-balancer.sh -threshold 10
```
