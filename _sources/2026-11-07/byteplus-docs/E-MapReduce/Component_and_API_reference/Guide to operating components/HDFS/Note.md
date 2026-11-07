---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_Note"
---

<span id="_1-概述"></span>
## **1 Overview**

HDFS, short for Hadoop Distributed File System, is the most widely used open\-source distributed file system in the industry. It has a high degree of fault tolerance and provides high\-throughput data access, making it ideal for applications on large\-scale datasets. HDFS provides a highly fault\-tolerant and high\-throughput solution for massive data storage.

<span id="_2-hdfs架构"></span>
## **2 HDFS architecture**

HDFS adopts a master/slave architecture. An HDFS cluster typically consists of one NameNode and several DataNodes. When NameNode high availability is not considered, a SecondaryNameNode is also used to handle metadata checkpoints.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_565fef71992356714ea107642631b413) </span>

<span id="_3-名词解释"></span>
## **3 Glossory**


|Parameter terms |Explanation |
|---|---|
|**NameNode** |This is the management node of the entire file system:<br><br><br>* It maintains the file directory tree of the entire file system, the metadata of files and directories, and the list of data blocks corresponding to each file.<br><br>* It receives user operation requests, such as opening, closing, or renaming files or directories.<br><br>* It is responsible for determining the mapping from files to blocks, and from blocks to specific DataNodes. |
|**SecondaryNameNode** |This is a solution for HDFS high availability, but it does not support hot standby.<br><br>Hadoop maintains an fsimage file, which is a snapshot of the metadata in the NameNode. However, fsimage does not always stay consistent with the metadata in the NameNode's memory; instead, it is updated periodically by merging the edits file.<br><br>The SecondaryNameNode is used to merge the fsimage and edits files to update the metadata of the NameNode. |
|**Client** |The client represents the user and interacts with the NameNode and DataNode to access the entire file system. HDFS exposes the file namespace externally and allows user data to be stored as files. Users communicate and interact with HDFS through the client (Client). |
|**DataNode** |DataNode is the actual data storage node of HDFS, responsible for managing the storage on its node and handling client read and write requests. It periodically reports heartbeat (Heartbeat) and block storage location information (Blockreport). DataNode creates, deletes, and replicates data blocks under the instructions of the NameNode. |
|**Block** |If a large file on HDFS exceeds the configured block size (default is 128MB), it will be divided into multiple data blocks (blocks) for storage. These data blocks are stored across different DataNodes. |
|**EditLog** |Operations such as creation, deletion, and other actions initiated in HDFS are actually transactions. The NameNode uses a transaction log (EditLog) to record every change in the file system metadata. EditLog is persisted on the NameNode's local disk. |
|**FsImage** |FsImage is a snapshot of the NameNode's metadata storage and is persisted on the NameNode's local disk. |
