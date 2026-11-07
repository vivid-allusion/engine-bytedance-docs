---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_FAQs"
---

This article summarizes common issues encountered when using HDFS.

<span id="namenode服务重启时特别慢。"></span>
## **Restarting the NameNode service is particularly slow.** 


* Symptom description: In an otherwise healthy HDFS cluster, after restarting the NameNode service, the restart time for NameNode is unusually long (greater than 10 minutes), as it remains in the process of loading FsImage and EditsLog files. During this period, NameNode stays in the 'safe mode on' state.

* Cause analysis: During the NameNode startup process, loading FsImage and EditsLog consumes a significant amount of memory, and NameNode only exits safe mode after loading the latest FsImage and all subsequent EditsLog files.

* Solution: It is recommended to increase the NameNode HeapSize in the HDFS configuration file to accelerate the loading process of metadata files.


<span id="如何处理missing-blocks-或corrupted-blocks问题？"></span>
## **How to handle Missing Blocks or Corrupted Blocks issues?** 


* Symptom description: When using the fsck command to check the health status of the HDFS file system, Missing Blocks or Corrupted Blocks are reported.

* Cause analysis: Data loss can occur when DataNode services stop, disks fail, or abnormal operations take place.

* Solution: If a DataNode service has stopped, restart the DataNode. If data loss is caused by disk failure or abnormal operations, manual recovery is required. You can use the `hdfs fsck / -files` command to scan for damaged files, export the file list, delete the files and re\-upload them.


<span id="namenode的元数据目录中有大量的editslog文件"></span>
## **A large number of Editslog files in the NameNode metadata directory**


* Symptom description: The data directory on the NameNode occupies a large amount of disk space, and a large number of Editslog files are found.

* Cause analysis: Checking the health status of the Secondary NameNode reveals that the Secondary NameNode service is not functioning properly, resulting in Editslog files not being merged in a timely manner. The service malfunction is likely caused by insufficient memory.

* Solution: Adjust the HeapSize of the Secondary NameNode appropriately to ensure it starts normally.


<span id="集群外读写hdfs"></span>
## Read and write HDFS from outside the cluster


* Symptom description: Unable to read, write, or delete HDFS data from outside the cluster

* Cause analysis: When the HDFS client accesses HDFS, the metadata information obtained from NameNode includes the DataNode address, which by default is an internal IP address. If external clients cannot communicate with the internal IP address, they cannot read, write, or delete HDFS data.

* Solution: Establish connectivity between external clients and the internal cluster network through dedicated lines, VPN, or similar methods; alternatively, bind the HDFS DataNode to a public IP address and set dfs.client.use.datanode.hostname to true. In this case, the returned DataNode address will be the hostname. Configure the HDFS client's /etc/hosts to map the hostname to the public IP address.
