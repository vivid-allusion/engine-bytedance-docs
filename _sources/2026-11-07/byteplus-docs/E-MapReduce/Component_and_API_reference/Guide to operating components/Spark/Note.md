---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/spark_note"
---

<span id="概述"></span>
# Overview

Spark is an open\-source distributed computing framework designed for large\-scale data analytics and processing. By leveraging in\-memory computing technology and directed acyclic graphs (DAG), it provides faster analytics and processing capabilities than the MapReduce engine. It offers multiple computation packages, including Spark SQL, Spark Streaming, MLlib, and Graphx, which can be used for large\-scale data analytics and processing, real\-time computation, machine learning, graph computation, and more.

<span id="名词解释"></span>
### **Glossory**


* SparkContext: SparkContext is the entry point for the Spark computing framework. It is responsible for managing Spark's distributed resources, creating RDDs, scheduling tasks, and other functions.

* SparkSession: SparkSession is the entry point for SparkSQL, responsible for parsing, analyzing, and optimizing SQL, generating physical plans, and scheduling SQL tasks for execution.

* Driver: The Driver is the process within the Spark distributed processing framework that hosts the SparkContext. It is responsible for running the SparkContext and managing and scheduling Executors. There is only one Driver.

* Executor: Executors are the processes that execute distributed tasks. They are responsible for executing tasks assigned by the Driver. There are multiple Executors.


<span id="组件说明"></span>
### **Note**


* Ksana for SparkSQL: EMR's self\-developed SparkSQL Server, compatible with the Hive JDBC Driver, is a resident service responsible for receiving client SQL, executing it using SparkSQL, and returning the results. For Ksana component\-related features, you can create clusters of version **EMR\-3.3.0** or earlier to use Ksana features.

* Livy for Spark Server: Provides Livy services for notebook applications to connect with Spark development. Users can easily develop and debug Spark applications by connecting Jupyter/Zeppelin to Livy for Spark Server.

* Spark History Server: Provides services for viewing and analyzing the execution history of Spark applications.

* Spark Client: This component installs the Spark runtime environment on individual nodes and does not provide an actual service.


<span id="a7e2e00a"></span>
### Constraints and limitations

Volcano Engine EMR provides support for multiple Spark versions. The corresponding Python versions for each Spark version are as follows:


|Spark version |Python version |
|---|---|
|3.3.x |3.10.13 |
|3.5.1 |3.12.0 |


<span id="eb93ced7"></span>
## Spark on EMR

The documents in this directory introduce the usage instructions for Spark components in the semi\-managed EMR mode. For usage instructions of fully managed EMR Serverless components, see: [Engine introduction](https://docs.byteplus.com/docs/E-MapReduce/95181).
