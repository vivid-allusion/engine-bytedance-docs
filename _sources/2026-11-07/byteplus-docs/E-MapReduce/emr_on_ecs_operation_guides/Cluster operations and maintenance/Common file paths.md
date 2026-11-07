---
title: "Common file paths"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_common_file_paths"
---

This document introduces the common file paths in E\-MapReduce. You can log in to the primary node to view the installation paths of common files.

<span id="_1-大数据组件目录"></span>
## **Big data component directories**

The software installation directory is located at /usr/lib/emr/current/xxx. For example:


* Hadoop:/usr/lib/emr/current/hadoop

* Spark:/usr/lib/emr/current/spark

* Hive:/usr/lib/emr/current/hive

* Flink:/usr/lib/emr/current/flink

* Flume:/usr/lib/emr/current/flume

* Presto:/usr/lib/emr/current/presto

* Proton:/usr/lib/emr/current/proton


You can also log in to the primary node and run the env |grep xxx command to view the software installation directory. For example, run the following command to view the installation directory of Hadoop.

```plaintext
env |grep hadoop
```


The following information is returned. /usr/lib/emr/current/hadoop is the installation directory of Hadoop.

```plaintext
HADOOP_LIBEXEC_DIR=/usr/lib/emr/current/hadoop/libexec
HADOOP_CONF_DIR=/etc/emr/hadoop/conf
HADOOP_HOME=/usr/lib/emr/current/hadoop
OLDPWD=/usr/lib/emr/current/hadoop
```


<span id="_2-日志目录"></span>
## **Log directories**

The component log directories are located at /var/log/emr/xxx. For example:


* Yarn ResourceManager log: /var/log/emr/yarn/hadoop\-yarn\-resourcemanager\-master\-1\-1.emr\-xxx.log

* Yarn NodeManager log: /var/log/emr/yarn/hadoop\-yarn\-nodemanager\-core\-1\-1.emr\-xxx.log

* HDFS NameNode log: /var/log/emr/hdfs/hadoop\-hdfs\-namenode\-master\-1\-2.emr\-xxx.log

* HDFS DataNode log: /var/log/emr/hdfs/hadoop\-hdfs\-datanode\-core\-1\-2.emr\-xxx.log

* Hive Metastore log: /var/log/emr/hive/metastore.log

* Presto Coordinator/Worker log: /var/log/emr/presto/log/server.log

* Proton MetaServer log: /var/log/emr/proton/metaserver/proton\-metaserver.log


<span id="_3-配置文件"></span>
## **Configuration files**

The configuration file directories are located at /etc/emr/xxx/conf. For example:


* Hadoop:/etc/emr/hadoop/conf

* Spark:/etc/emr/spark/conf

* Hive:/etc/emr/hive/conf

* Flink:/etc/emr/flink/conf

* Flume:/etc/emr/flume/conf

* Presto:/etc/emr/presto/conf

* Proton:/etc/emr/proton/conf


To modify parameters in configuration files, log in to the E\-MapReduce console. Parameters in configuration files can only be viewed via SSH.
