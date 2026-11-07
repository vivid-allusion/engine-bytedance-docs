---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_quickstart"
---

<span id="_1-执行"></span>
## **1. Execute**


* Format a new distributed file system:

   ```Plain
   $ bin/hadoop namenode -format
   ```
   

* Start the Hadoop daemon processes:

   ```Plain
   $ bin/start-all.sh
   ```
   

   The logs of the Hadoop daemon processes are written to the ${HADOOP_LOG_DIR} directory (the default is ${HADOOP_HOME}/logs).

* Browse the NameNode web interface: its address is, by default:

   * NameNode \- http://namenode\-name:50070/

* Copy the input file to the distributed file system:

   ```Plain
   $ bin/hadoop fs -put conf input
   ```
   

* Run the sample program provided by the distribution:

   ```Plain
   $ bin/hadoop jar hadoop-*-examples.jar grep input output 'dfs[a-z.]+'
   ```
   

* View the output file:

   * Copy the output file from the distributed file system to the local file system to view it:

   ```Plain
   $ bin/hadoop fs -get output output
   $ cat output/*
   ```
   

   * Alternatively, view the output file on the distributed file system:

   ```Plain
   $ bin/hadoop fs -cat output/*
   ```
   

* After completing all operations, stop the daemon processes:

   ```Plain
   $ bin/stop-all.sh
   ```
   


<span id="_2-web接口"></span>
## **2. Web interface**

The NameNode and DataNode each start a built\-in web server that displays the current basic status and information of the cluster.

With the default configuration, the home page address of the NameNode is [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109242).


* This page lists all DataNodes in the cluster and the basic status of the cluster.

* This web interface can also be used to browse the entire file system (using the "Browse the file system" link on the NameNode home page).


<span id="_3-shell命令"></span>
## **3. Shell commands**

Hadoop includes a series of shell\-like commands that allow direct interaction with HDFS and other file systems supported by Hadoop.


* The bin/hadoop fs \-help command: lists all commands supported by the Hadoop shell.

* The bin/hadoop fs \-help command\-name command: displays detailed information about a specific command.


These commands support most common file system operations, such as copying files, changing file permissions, and so on. They also support some operations specific to HDFS, such as changing the number of file replicas.
