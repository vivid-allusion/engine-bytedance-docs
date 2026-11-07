---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/spark_quickstart"
---

This article introduces how to quickly access the Volcano Engine E\-MapReduce (EMR) cluster and develop content related to Spark services.

<span id="_1-前提条件"></span>
## **1. Prerequisites**


* An E\-MapReduce (EMR) cluster has been created and the Spark service is installed. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456) **.** 

* The cluster must include the OpenLDAP service and have users added. For details, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109349).

* Features related to the Ksana component are only supported in EMR\-3.3.0 and earlier cluster versions.


<span id="_2-登录-emr-集群节点"></span>
## **2. Log in to an EMR cluster node**


1. Go to the **Cluster Management \> Cluster List \> Specific Cluster Name, enter the cluster details** page.

2. In the navigation bar, click **Service List**, then click **Spark** to enter the service.

3. Click the ECS ID of the EMR cluster node (host name emr\-master\-1\-1) to go to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f1d3600a12449f426c34789f3def3f37) </span>

<span id="_3-交互式开发"></span>
## **3. Interactive development**

After logging in to the cluster node, go to the spark file directory.

```Plain
cd /usr/lib/emr/current/spark
```


<span id="_3-1-使用-scala-交互式编程环境"></span>
### **3.1 Use the Scala interactive programming environment**

Run the spark\-shell script in the bin directory to start the program. The command template is as follows

```Plain
./bin/spark-shell
```


<span id="_3-2-使用-python-交互式编程环境"></span>
### **3.2 Use the Python interactive programming environment**

Run the pyspark script in the bin directory to start the program. The command template is as follows

```Plain
./bin/pyspark
```


<span id="_3-3-使用-sql-交互式编程环境"></span>
### **3.3 Use the SQL interactive programming environment**

Run the spark\-sql script in the bin directory to start the program. The command template is as follows

```Plain
./bin/spark-sql
```


<span id="_4-程序提交"></span>
## **4. Program submission**

Log in to the cluster node and go to the spark file directory.

```Plain
cd /usr/lib/emr/current/spark
```


First, use the Spark API to implement a program with an entry point (main), then submit it using spark\-submit.

For example, run the built\-in Spark Pi sample program.

```Plain
jar包提交:
./bin/spark-submit --class org.apache.spark.examples.SparkPi examples/jars/spark-examples.jar 10
python file:
./bin/spark-submit examples/src/main/python/pi.py 10
```


If the run is successful, logs and an application_id link will be returned.

To view the status of a specific task, log in to the yarn interface and search for the application_id to view the task.

<span id="_5-jdbc方式sql操作"></span>
## **5. SQL operations via JDBC**

<span id="_5-1-连接-ksana-for-sparksql"></span>
### **5.1 Connect to Ksana for SparkSQL**

Ksana for SparkSQL is a SparkSQL Server developed in\-house by the EMR team. It can be used in production environments and resolves issues with Spark Thrift Server. The default port is 10005. Connect to Ksana for SparkSQL using beeline. Some initial account passwords can be obtained from the OpenLDAP configuration in the cluster management interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In EMR\-3.4.0 and later versions, features related to the Ksana component will be taken down.</div>


* <div data-tips="true" data-tips-type="tip">Ksana component\-related features are still retained in EMR\-3.3.0 and earlier versions. You can create EMR\-3.3.0 or earlier version clusters to use Ksana component\-related features.</div>



```Plain
beeline -u jdbc:hive2://emr-master-1-1:10005 -n <user> -p <password>
```


<span id="_5-2-执行-sparksql-语句"></span>
### **5.2 Execute SparkSQL statements**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> show databases;
```


Obtain the returned results

```Plain
+------------+
| namespace  |
+------------+
| default    |
+------------+
```
