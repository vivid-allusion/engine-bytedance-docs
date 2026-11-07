---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/mapreduce2_note"
---

<span id="_1-概述"></span>
## **1 Overview**

MapReduce is a software framework for parallel processing of large data sets. It is used for parallel computation on large\-scale data sets (greater than 1 TB). The concepts of "Map (mapping)" and "Reduce (reduction)", as well as their main ideas, are borrowed from functional programming languages, along with features derived from vector programming languages. For more information, see [MapReduce tutorial](https://hadoop.apache.org/docs/r3.2.1/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html).

This article introduces how to use mapreduce2 to execute SQL jobs.

<span id="_2-前提条件"></span>
## **2 Prerequisites**


* A Volcano Engine E\-MapReduce (EMR) cluster with the Hive component service has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

* The OpenLDAP service has been installed and users have been added.


<span id="_3-操作指南"></span>
## **3 Operation guide**

<span id="_3-1-使用-hive-提交-mr-任务"></span>
### 3.1 Submit MR tasks using Hive

To submit MR tasks using Hive, first switch Hive to use MR as the execution engine:


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, click to enter the **Cluster Management \> Cluster List \> Cluster Details \> Service List \> Hive \> Service Parameters** page.

3. Modify the Hive parameter `hive.execution.engine` to mr, then click the **Service Operations \> Restart** button in the upper right corner to restart the Hive service.


<span id="jump"></span>
#### **3.1.1 Log in to the EMR primary node**


1. Click the **Cluster List \> Cluster Name \> Service List \> Hive \> Deployment Topology** tab to enter the deployment topology page for the Hive component service.

2. Expand the HiveServer2 component name, click the ECS ID of its host name to go to the cloud server instance page, and click the **Remote Connection** button in the upper right corner.

3. Select a remote connection method (ECS Terminal is recommended), enter the relevant cluster authentication information, and log in to the command\-line environment of the Hive cluster to perform the required command\-line operations.


<span id="_3-1-2-连接-hiveserver2"></span>
#### **3.1.2 Connect to HiveServer2**

Refer to the [Hive connection methods](https://docs.byteplus.com/docs/E-MapReduce/109265) section to connect to HiveServer2. The following is an example:

```plaintext
beeline -u "jdbc:hive2://<HiveServer2地址>:10000/" -n <username> -p <password>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The username and password parameters passed via the command line are the credentials that you imported as IAM users or manually added on the <strong>EMR console Cluster Details \> User Management</strong> page. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105426">User management</a>.</div>


<span id="_3-1-3-执行-hive-语句"></span>
#### **3.1.3 Execute Hive statements**

After connecting to HiveServer2, you can execute relevant Hive statements according to your actual scenario. The following is an example:

```SQL
select orderkey,count(*) from lineitem group by orderkey limit 100;
```


<span id="_3-2-使用-jar-包直接提交"></span>
### 3.2 Submit directly using a Jar package

Refer to “[3.1.1 Log in to the EMR primary node](https://docs.byteplus.com/docs/E-MapReduce/109348#jump)[3.1.1 Log in to the EMR primary node](https://docs.byteplus.com/docs/E-MapReduce/109348#jump)[3.1.1 Log in to the EMR primary node](https://docs.byteplus.com/docs/E-MapReduce/109348#jump)[3.1.1 Log in to the EMR primary node](https://docs.byteplus.com/docs/E-MapReduce/109348#jump)[3.1.1 Log in to the EMR primary node](https://docs.byteplus.com/docs/E-MapReduce/109348#jump)”, log in to the cluster, and then execute the following hadoop jar submission command:

```javascript
/usr/lib/emr/current/hadoop/bin/hadoop jar /usr/lib/emr/current/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.4.jar pi 16 100000
// Submit the jar package. The parameters are as follows
// The location of the jar package to be executed, for example /usr/lib/emr/current/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.4.jar
// The main class name, for example pi
// Submission parameters, for example 16 100000. Some tasks specify the input and output file locations through parameters, and so on
```
