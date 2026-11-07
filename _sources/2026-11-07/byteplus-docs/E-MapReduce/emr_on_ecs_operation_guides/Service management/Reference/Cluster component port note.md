---
title: "Cluster component port note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cluster_component_port_note"
---

This document introduces the port configuration of Volcano Engine E\-MapReduce (EMR) clusters.

<span id="hdfs"></span>
## **HDFS**


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|NameNode |50070 |dfs.namenode.http\-address |HDFS NameNode HTTP service port |
||50470 |dfs.https.port |HDFS NameNode HTTPS service port |
||8020 |dfs.namenode.rpc.port |HDFS NameNode RPC port |
|DataNode |50010 |dfs.datanode.address |HDFS DataNode service port |
||50075 |dfs.datanode.http.address |HDFS DataNode HTTP service port |
||50475 |dfs.datanode.https.address |HDFS DataNode HTTPS service port |
||8010 |dfs.datanode.ipc.address |HDFS DataNode IPC port |
|JournalNode |8485 |dfs.journalnode.rpc\-address |HDFS JournalNode RPC port |
||8480 |dfs.journalnode.http\-address |HDFS JournalNode HTTP port |
|ZKFC |8019 |dfs.ha.zkfc.port |HDFS ZKFC port |


<span id="yarn"></span>
## **YARN**


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|ResourceManager |8088 |yarn.resourcemanager.webapp.address |YARN RM HTTP service port |
||8090 |yarn.resourcemanager.webapp.https.address |YARN RM HTTPS service port |
||8050 |yarn.resourcemanager.address |RM applications manager (ASM) port |
||8030 |yarn.resourcemanager.scheduler.address |Scheduler component IPC port |
||8025 |yarn.resourcemanager.resource\-tracker.address |RM RPC port |
||8141 |yarn.resourcemanager.admin.address |RM admin port |
|NodeManager |8040 |yarn.nodemanager.localizer.address |Localizer IPC port |
||8042 |yarn.nodemanager.webapp.address |YARN NM HTTP service port |
||45454 |yarn.nodemanager.address |NodeManager process port |
|TimeLineService |10200 |yarn.timeline\-service.address |Timeline Service process port |
||8198 |yarn.timeline\-service.reader.webapp.address |Timeline Service Reader HTTP port |
||8199 |yarn.timeline\-service.reader.webapp.https.address |Timeline Service Reader HTTPS port |
||8188 |yarn.timeline\-service.webapp.address |Timeline Service web service port |
||8190 |yarn.timeline\-service.webapp.https.address |Timeline Service web HTTPS service port |


<span id="mapreduce"></span>
## MapReduce


|**Component/Service** |**Port** |**Configuration** |Note |
|---|---|---|---|
|HistoryServer |10020 |mapreduce.jobhistory.address |MR history server ipc |


<span id="hive"></span>
## Hive


|**Component/Service** |**Port** |**Configuration** |Note |
|---|---|---|---|
|HiveServer2 |10000 |hive.server2.thrift.port |HiveServer2 external JDBC connection port |
||10002 |hive.server2.webui.port |HiveServer2 web UI access port |
||10002 |hive.server2.webui.port |HiveServer2 web UI access port |
||30032 |HADOOP_OPTS environment variable |Prometheus monitors HiveServer service via JMX tool |
||10001 |hive.server2.thrift.http.port |HiveServer HTTP data transfer port in connection URL |
|Hive Metastore |9083 |METASTORE_PORT environment variable |Hive metastore access port |
||30031 |HADOOP_OPTS environment variable |Prometheus monitors MetaStore service via JMX tool |


<span id="spark"></span>
## Spark


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|ThirftServer |10016 |hive.server2.thrift.port |ThriftServer external JDBC connection port |
||30075 |SPARK_THRIFT_JAVAOPTIONS environment variable |Prometheus monitors ThriftServer service via JMX tool |
|HistoryServer |18081 |spark.history.ui.port |Spark HistoryServer web port |
|livy |8999 |livy.server.port |livy server port information |


<span id="openldap"></span>
## OpenLDAP


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|OpenLDAP |389 |Startup parameter slapd \-h configuration |OpenLDAP default data port |
||636 |Startup parameter slapd \-h configuration |OpenLDAP encrypted data port |


<span id="airflow"></span>
## Airflow


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|WebServer |8330 |airflow_web_port |Airflow WebServer web access port |
|Broker |6379 |Default value |Airflow Worker dependent Broker access port |
|Worker |8793 |Default value |Airflow Worker Log access port |


<span id="ranger"></span>
## Ranger


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|Ranger admin |6080 |Default value |Ranger admin external REST API access port |


<span id="hue"></span>
## Hue


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|Hue |8888 |http_port |HTTP port |


<span id="hbase"></span>
## Hbase


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|HBase Master |16000 |hbase.master.port |HBase master port |
||16010 |hbase.master.info.port |HBase master HTTP service port |
|Region Server |16020 |hbase.regionserver.port |Region Server port |
||16030 |hbase.regionserver.info.port |Region Server HTTP port |


<span id="kafka"></span>
## Kafka


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|Kafka Broker |9092 |listeners |Kafka listener port |
||6667 |port |Kafka Broker port |


<span id="presto"></span>
## Presto


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|presto coordinator/worker |8084 |http\-server.http.port |Presto HTTP port |
||8085 |http\-server.https.port |Presto HTTPS port |
|presto coordinator |30071 |JVM parameter |Presto monitoring port |


<span id="trino"></span>
## Trino


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|trino coordinator/worker |9084 |http\-server.http.port |Trino HTTP port |
||9085 |http\-server.https.port |Trino HTTPS port |
|trino coordinator |30072 |JVM parameter |Trino monitoring port |


<span id="zookeeper"></span>
## Zookeeper


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|Zk Server |2181 |clientPort |ZK server port |
||2888 |zoo.cfg server.$id=$ip:$por1$port2 |ZK server Quorum port |
||3888 |zoo.cfg server.$id=$ip:$por1$port2 |ZK server leader election port |
||9876 |admin.serverPort |ZK server admin port |


<span id="opensearch"></span>
## OpenSearch


|**Component/Service** |**Port** |**Configuration** |**Note** |
|---|---|---|---|
|OpenSearch |9200 |http.port |Cluster external HTTP communication port |
||9300 |transport.tcp.port |Cluster internal TCP communication port |
|Dashboard |5601 |server.port |Dashboard port |
