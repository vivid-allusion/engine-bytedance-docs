---
title: "EMR storage-compute separation Job Committer best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_storage-compute_separation_Job_Committer_best_practices"
---

<span id="_1-前言"></span>
## 1 Introduction

EMR storage\-compute separation is an elastic, low\-cost product model that is gaining widespread acceptance. For more information about Volcano EMR storage\-compute separation, please refer to [Proton overview](https://docs.byteplus.com/docs/E-MapReduce/109367).

There are some semantic differences between TOS object storage and HDFS. These differences are mainly reflected in the following aspects:


* Rename operations (including directories and files) in TOS object storage are time\-consuming, and simulated rename implementations usually cannot guarantee atomicity and performance.

* List operations in TOS object storage are more time\-consuming compared to HDFS.


Therefore, the Volcano EMR team has made appropriate optimizations to the big data write process for the EMR storage\-compute separation scenario, enabling EMR writes to TOS to match the performance and consistency of the HDFS integrated storage\-compute scenario. The most critical optimization in the EMR write path is the customized implementation of the Hadoop Job Committer.

<span id="_2-什么是-job-committer"></span>
## 2 What is Job Committer

The overall write logic for an MR job is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0cd0c4d042de4b63e279d71faa0198f.png) </span>

The engine first writes data to a temporary directory. After the data is written, it uses the rename command to move the data to the final directory. In the HDFS scenario, since the rename operation only involves metadata changes and can be completed in the NameNode, the time complexity is O(1), and there is almost no significant time overhead.

However, in object storage, since there is no rename semantics, rename actions can only be achieved by combining the copy and delete capabilities provided by object storage. This means that when renaming a large file, the file must first be copied and then the original file deleted in object storage, resulting in an additional full file write time compared to HDFS.

Therefore, without any optimization, using object storage as the storage medium will be more than twice as slow as HDFS in terms of performance. The Job Committer is a means to improve the speed of writing to object storage under these circumstances.

The Job Committer leverages the MPU (MultipartUpload) capability of object storage to split a large file into multiple parts, assign a number to each part, upload them in parallel, and make the entire file visible once all parts have been uploaded.

The main concepts related to MultipartUpload include:


* **CreateMultipartUpload:**  Before writing data to a key, it is necessary to first create or register an Upload request and obtain the corresponding uploadID. Multiple concurrent Upload writes may exist for a single key, but only the data from one Upload will be used as the final result.

* **UploadPart:**  Initiate an UploadPart request to write data. A single Upload operation can consist of multiple different UploadPart write operations. Each UploadPart write request includes the key's path, uploadId, current part number, and current part data.

* **AbortUpload:**  Each UploadPart write in an Upload operation may encounter failure scenarios. AbortUpload can be explicitly called to discard the contents of a particular Upload operation.

* **CompleteUpload:**  After all UploadPart writes for the current Upload succeed, CompleteUpload is called to sort and merge the data from multiple UploadPart operations and write it to the key.


By leveraging MPU capabilities, files that are not yet fully written can be prevented from being read during the write process. Therefore, there is no need to write to a temporary directory; the final directory can be written directly. Under the Job Committer workflow, the write process for MR jobs is optimized as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7c9771628cc1453038fe0bc5d83b9d6.png) </span>

As can be seen, with the Job Committer, there is no need to write temporary files; the final directory can be written directly. Once the file is fully written, the file is made visible by calling MPU's CompleteUpload, reducing the original copy and delete steps, and greatly improving write speed.

As shown in the figure below, in common Hadoop MR test scenarios, the deeply optimized Job Committer functionality implemented by Volcano EMR enables TOS write performance to be twice as fast as open\-source solutions.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f0e91b090daac9057b54b8dc5b4b9d7.png) </span>

<span id="_3-hive-tpc-ds测试"></span>
## 3 Hive TPC\-DS test

For information on enabling TOS JobCommitter in Hive 2.x and Hive 3.x, please refer to [Hive uses Proton](https://docs.byteplus.com/docs/E-MapReduce/109376).


| |**Enable TOS JobCommitter** |**Disable TOS Job Committer** |
|---|---|---|
|**Hive On MR (Load 1TB)**  |3410.943 (s) |5784.555 (s) |
|**Hive On Tez (Load 1TB)**  |2728.777 (s) |5259.840 (s) |


**Conclusion**


* In Hive on MR scenarios, enabling TOS JobCommitter for loading 1TB of tpc\-ds data can deliver a 70% performance improvement.

* In Hive on Tez scenarios, enabling TOS JobCommitter for loading 1TB of tpc\-ds data can deliver a 93% performance improvement.


<span id="_4-spark-tpc-ds测试"></span>
## 4 Spark TPC\-DS test

For information on enabling TOS JobCommitter in Spark 2.x and Spark 3.x, please refer to [Spark uses Proton](https://docs.byteplus.com/docs/E-MapReduce/109377).


| |**Enable TOS JobCommitter** |**Disable TOS Job Committer** |
|---|---|---|
|**Spark 2.x (Load 1TB)**  |1645.693 (s) |3110.361 (s) |
|**Spark 3.x (Load 1TB)**  |1507.178 (s) |2938.998 (s) |


**Conclusion**


* In Spark 2.x, enabling TOS JobCommitter for loading 1TB of tpc\-ds data can deliver an 89% performance improvement.

* In Spark 3.x, enabling TOS JobCommitter for loading 1TB of tpc\-ds data can deliver approximately 95% performance improvement.


<span id="_5-客户案例"></span>
## 5 Customer case studies


| |**Introduction to scenarios** |
|---|---|
|**A. K12 online education** |* Choose the Volcano EMR storage\-compute separation architecture, with TOS JobCommitter enabled by default;<br><br>* VIP courses are provided for customers in elementary, middle, and high schools, with devices including mobile phones, iPads, computers, televisions, and other equipment.<br><br>* The total data volume is 6 PB, with 1 PB of data analyzed daily.<br><br>* After collecting data from the online log system and the online RDS system, the data is written into Hive tables on Volcano EMR via the Volcano datasail product, with underlying storage in TOS object storage.<br><br>* More than 2,000 Hive SQL jobs are scheduled daily; Volcano EMR's elastic scheduling feature is enabled by default, automatically scaling out several node resources from 2:00 a.m. for offline data warehouse analysis to meet peak nighttime data processing demands.<br><br>* After migrating from the offline IDC data center's CDH cluster to Volcano EMR, customers reported the following core advantages of Volcano EMR:<br><br>   * Volcano EMR adopts a storage\-compute separation architecture, enabling pay\-as\-you\-go storage billing, which is more cost\-effective and flexible compared to offline IDC; customers enable cold data archiving for more than 80% of cold data, significantly reducing storage costs for cold data; after enabling storage\-compute separation, customers can flexibly upgrade component versions without moving large volumes of existing data.<br><br>   * After enabling elastic scaling on Volcano EMR, automatic, hands\-free resource elasticity is achieved, flexibly meeting customers' peak nighttime computing needs.<br><br>   * Volcano EMR offers a simple and user\-friendly product experience, comprehensive cluster status monitoring and alert information, and a responsive expert team service, greatly improving the productivity of the company's big data team and allowing the team to focus more on business and data analysis. |
|**B. Connected vehicle data analysis** |* Choose the Volcano EMR storage\-compute separation architecture, with TOS JobCommitter enabled by default;<br><br>* The existing data volume is 3 PB, with 30 TB analyzed daily in the data warehouse.<br><br>* Vehicle device data is periodically uploaded as compressed packages of semi\-structured data files such as txt, csv, and log, which are uploaded to TOS via the IoT system, and Kafka receives the event for processing. Flink consumes Kafka write events, reads and decompresses the compressed packages, flattens the data, and writes it into a wide Hive table.<br><br>* Hive performs ETL and layering of data warehouse data, and generates BI reports for the vehicle\-end. Over 5,000 HiveSQL jobs are scheduled daily.<br><br>* Customers have reported that the Volcano Engine EMR storage\-compute separation architecture offers good usability, provides a better price\-performance ratio compared to competitors, and responds quickly and efficiently to feedback. |
|**C. Intelligent driving company** |* Chose the Volcano Engine EMR storage\-compute separation architecture, with TOS JobCommitter enabled by default.<br><br>* Vehicle sensors write collected data signals to Kafka; Flink consumes data from Kafka and writes to Hive + TOS tables. Hive is used for data ETL and layered data warehousing, Spark is used for AI data insights, and Starrocks is used for real\-time queries.<br><br>* The existing data volume is approximately 2 PB, with a daily increase of 10 TB. The data volume is expected to double within six months.<br><br>* Hive SQL performs ETL cleansing on table data stored on TOS, building a layered data warehouse. Over 30,000 HiveSQL jobs are executed daily.<br><br>* As the customer's business continues to iterate, the system is currently running stably; no stability or related issues have been encountered so far. |
|**D. Foundation model vendor** |* Chose the Volcano Engine EMR storage\-compute separation architecture, with TOS JobCommitter enabled by default.<br><br>* The total volume of datasets is around 10 PB, mainly consisting of public and proprietary datasets related to LLM, with Spark used to complete data cleansing and insights in storage\-compute separation scenarios.<br><br>* Using Spark and Ray, AI data preprocessing as well as foundation model building and regression are implemented.<br><br>* The system has been running stably for more than six months, with a very stable end\-to\-end process and no failures or stability issues encountered so far. |
