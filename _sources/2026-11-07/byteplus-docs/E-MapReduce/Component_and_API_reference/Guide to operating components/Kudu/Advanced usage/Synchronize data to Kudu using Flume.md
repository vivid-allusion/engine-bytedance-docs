---
title: "Synchronize data to Kudu using Flume"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Synchronize_data_to_Kudu_using_Flume"
---

Apache Flume is an open\-source, distributed, large\-scale log aggregation system developed by Cloudera. It can be used to collect, aggregate, and transfer large volumes of log data from various data sources within a system to a centralized storage location. As a streaming log collection tool, Flume provides the capability to perform simple processing on data and write it to various (customizable) data sinks.

Volcano Engine E\-MapReduce (EMR) has integrated Flume. You can use Flume to synchronize data from different data sources to Kudu.

<span id="_1-添加-flume-服务"></span>
## 1 Add Flume service

In a Hadoop cluster, Flume is an optional component. To use Flume, you need to manually add the Flume component.


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, select and enter the **Cluster List \> Cluster Name \> Service List** page.

3. Click the [**Add Service**] button in the upper right corner.

4. Select Flume, click the **OK** button, and proceed with the installation.


<span id="_2-使用-flume-写-kudu"></span>
## 2 Write to Kudu using Flume

Flume in Volcano Engine EMR has integrated the dependencies for writing to Kudu by default. The following describes how to use the official Kudu component to consume data and write it to Kudu.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Flume in Volcano Engine EMR integrates version 1.9.0 of kudu\-flume\-sink and kudu\-client.</div>


<span id="_2-1-前提条件"></span>
### 2.1 Prerequisites

The EMR cluster has Kudu and Flume installed. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-2-获得-kudu-的-master-地址"></span>
### 2.2 Obtain the Kudu master address


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, select and enter the **Cluster List \> Cluster Name \> Service List \> Kudu** page.

3. Click to expand Kudu Master to display the list of machines of Kudu Master.


<span id="_2-3-登录集群操作"></span>
### 2.3 Log in to the cluster


* Option 1: Use SSH to log in to one of the Kudu Master machines. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

* Option 2: You can access the ECS instance in the EMR cluster's Kudu component service deployment topology, go to the cloud server instance page, click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.


After logging in to the cluster, directly execute the following related Kudu commands in the shell:


1. Create a Kudu table using the kudu command.

   ```shell
   kudu table create emr-3432jdr2za2uxxx-master-1:7051,emr-3432jdr2za2uxxx-core-1:7051,emr-3432jdr2za2uxxx-core-2:7051 '{"table_name":"test","schema":{"columns":[{"column_name":"id","column_type":"INT32","default_value":"1"},{"column_name":"name","column_type":"STRING","is_nullable":false,"comment":"user name"}],"key_column_names":["id"]},"partition":{"hash_partitions":[{"columns":["id"],"num_buckets":2,"seed":100}]},"extra_configs":{"configs":{"kudu.table.history_max_age_sec":"3600"}},"num_replicas":1}'
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the above command, replace the Kudu master address with your actual address.</div>



2. Configure flume

   Create a new file and edit /tmp/flume\-kudu.conf with the following content:

   ```shell
   a1.sources = s1
   a1.sinks = k1
   a1.channels = c1
   
   a1.sources.s1.type = exec  
   a1.sources.s1.command = cat /tmp/test.log  
   a1.sources.s1.channels = c1 
   
   # Use a channel which buffers events in memory
   a1.channels.c1.type = memory
   a1.channels.c1.capacity = 1001
   a1.channels.c1.transactionCapacity = 1000
   
   # Describe the sink
   a1.sinks.k1.type = org.apache.kudu.flume.sink.KuduSink
   a1.sinks.k1.masterAddresses = emr-3432jdr2za2uxxx-master-1:7051,emr-3432jdr2za2uxxx-core-1:7051,emr-3432jdr2za2uxxx-core-2:7051
   a1.sinks.k1.tableName = test
   a1.sinks.k1.operation = insert
   a1.sinks.k1.batchSize = 50
   a1.sinks.k1.producer = org.apache.kudu.flume.sink.RegexpKuduOperationsProducer
   a1.sinks.k1.producer.pattern = (?<id>\\d+),(?<name>\\w+)
   a1.sinks.k1.channel = c1
   ```
   

3. Prepare input data

   Create /tmp/test.log and write data to it

   ```shell
   rm /tmp/test.log
   echo "1,fang" > /tmp/test.log
   ```
   

4. Start flume, read data from /tmp/test.log, and write it to kudu

   ```shell
   /usr/lib/emr/current/flume/bin/flume-ng agent --conf conf --conf-file /tmp/flume-kudu.conf --name a1
   ```
   

5. Check whether data has been written to kudu

   ```shell
   root@emr-3432jdr2za2uxxx-master-1:~# kudu table scan emr-3432jdr2za2uxxx-master-1:7051,emr-3432jdr2za2uxxx-core-1:7051,emr-3432jdr2za2uxxx-core-2:7051 test
   (int32 id=6, string name="fang")
   T 234196e2550f45e09aaa178ab42dcb7a scanned count 1 cost 0.00311413 seconds
   T 13247a58bdf84c248caf7c2f14116a83 scanned count 0 cost 0.00306098 seconds
   Total count 1 cost 0.00329723 seconds
   ```
   


<span id="_3-使用自定义的-kuduoperationsproducer"></span>
## 3 Use a custom KuduOperationsProducer

RegexpKuduOperationsProducer is the built\-in message body parsing implementation of kudu. In addition, kudu provides other parsing implementations such as AvroKuduOperationsProducer, SimpleKeyedKuduOperationsProducer, and SimpleKuduOperationsProducer. To meet specific requirements not covered by these parsers, you can implement a custom solution.


1. Create a Maven project

   ```shell
   mvn archetype:generate -DgroupId=com.example -DartifactId=kudu-flume-sink -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   

2. Add POM dependencies

   ```xml
   <dependency>
         <groupId>org.apache.kudu</groupId>
         <artifactId>kudu-flume-sink</artifactId>
         <version>1.9.0</version>
   </dependency>
   ```
   

3. Write the Processor

   ```java
   package com.example;
   
   import org.apache.flume.Context;
   import org.apache.flume.Event;
   import org.apache.kudu.client.KuduTable;
   import org.apache.kudu.client.Operation;
   import org.apache.kudu.flume.sink.KuduOperationsProducer;
   
   import java.util.LinkedList;
   import java.util.List;
   
   public class MyProcessor implements KuduOperationsProducer {
       public void initialize(KuduTable kuduTable) {
       }
   
       public List<Operation> getOperations(Event event) {
           List<Operation> operations = new LinkedList<Operation>();
           // TODO Parse the event and generate the Operation for Kudu
           return operations;
       }
   
       public void close() {
   
       }
   
       public void configure(Context context) {
   
       }
   }
   ```
   

4. Package

   ```shell
   mvn package -DskipTests
   ```
   

5. Upload the package to /usr/lib/emr/current/flume/lib on the server

6. Use the custom Processor

   ```shell
   a1.sinks.k1.producer = com.example.MyProcessor
   ```
