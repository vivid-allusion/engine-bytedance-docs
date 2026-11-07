---
title: "Use a Kerberos-authenticated cluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_a_Kerberos-authenticated_cluster"
---

This section provides guidance on using a secure cluster from scratch and running use cases such as MapReduce, Spark, Hive, and more.

<span id="f36ec86f"></span>
## **Limits**


* Currently, only enabling Kerberos when creating a cluster is supported; converting a regular cluster to a Kerberos cluster is not supported.

* When a user is added in user management, the corresponding principal information is registered in Kerby, and the user's keytab file can be downloaded.


<span id="创建安全集群"></span>
## **Create a secure cluster**

Volcano Engine E\-MapReduce (EMR) provides Kerberos capabilities for clusters by integrating the [Apache Kerby](https://directory.apache.org/kerby/) service. If Kerberos authentication is enabled during cluster creation, the Kerby component will be installed during cluster setup, providing a basic Kerberos environment.

For other cluster operations, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="e98d9c74"></span>
## **Create a user**

Refer to the [User management](https://docs.byteplus.com/docs/E-MapReduce/105426) section to create an authenticated user and download the corresponding keytab file.

<span id="执行-mapreduce-用例"></span>
## **Run a MapReduce use case**


1. Refer to the [User management](https://docs.byteplus.com/docs/E-MapReduce/105426) section to create the user01 user, download its keytab file, and upload it to the /etc/krb5/keytab/user directory on the ECS.

2. Generate the user's ticket.

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

3. Run the WordCount use case for MapReduce.

   ```powershell
   hadoop fs -mkdir /tmp/input
   hadoop fs -put /usr/lib/emr/current/hadoop//README.txt /tmp/input/data
   yarn jar /usr/lib/emr/current/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.4-ve-1.jar wordcount /tmp/input/data /tmp/output
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>hadoop-mapreduce-examples-3.3.4-ve-1.jar</code>, the Hadoop version number in this path may vary depending on the EMR version, so you need to configure it according to the specific environment.   </div>
   

<span id="执行-spark-用例"></span>
## **Run a Spark use case**


1. Generate the user's ticket

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

   User authentication information can also be added in the command line: Example:

   ```powershell
   spark-submit --conf spark.kerberos.principal=user01 --conf spark.kerberos.keytab=/etc/krb5/keytab/user/user01.keytab ....
   ```
   

2. Run the SparkPi use case for Spark

   ```powershell
   spark-submit  --master yarn --class org.apache.spark.examples.SparkPi  --conf spark.kerberos.principal=user01 --conf spark.kerberos.keytab=/etc/krb5/keytab/user/user01.keytab /usr/lib/emr/current/spark/examples/jars/spark-examples_2.12-3.2.1.jar
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Spark version number of <code>spark-examples_2.12-3.2.1.jar</code> in the example varies across different EMR versions. You need to fill it in according to the actual environment.   </div>
   

3. Run a Spark SQL use case.

   1. Enter spark\-sql to access the Spark SQL console.

      ```powershell
      spark-sql --conf spark.kerberos.principal=user01  -conf spark.kerberos.keytab=/etc/krb5/keytab/user/user01.keytab
      ```
      

   2. Enter the following SQL statement.

      ```sql
      CREATE TABLE IF NOT EXISTS t1(i INT, s STRING);
      INSERT INTO t1 VALUES(0, 'a');
      SELECT * FROM t1;
      ```
      


<span id="执行hive用例"></span>
## **Run a Hive use case**


1. Generate the user's ticket.

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

2. Run the Hive CLI.

   1. Enter 'hive' to access the Hive console.

   2. Enter the following HQL statement.

      ```sql
      CREATE TABLE IF NOT EXISTS t2(i INT, s STRING);
      INSERT INTO t1 VALUES(0, 'a');
      SELECT * FROM t2;
      ```
      

3. Connect to HiveServer2.

   ```powershell
   beeline -u "jdbc:hive2://${zookeeper的地址}/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2;principal=${HiveServer2的principal}"
   ```
   

   Example:

   ```powershell
   beeline -u "jdbc:hive2://10.0.255.9:2181,10.0.255.7:2181,10.0.255.8:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2;principal=hive/_HOST@2FDE5608A274D0A2320C.EMR.COM"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>2FDE5608A274D0A2320C.EMR.COM</code> is the domain name of the KDC, which needs to be specified according to the specific environment.   </div>
   

4. Run the following HQL statement.

   ```sql
   CREATE TABLE IF NOT EXISTS t3(i INT, s STRING);
   INSERT INTO t3 VALUES(0, 'a');
   SELECT * FROM t3;
   ```
   


<span id="执行-flink-用例"></span>
## **Run a Flink use case**


1. Generate the user's ticket.

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

2. Run the Flink jar command.

   1. Run the built\-in WordCount use case for Flink.

      ```powershell
      hadoop fs -put /usr/lib/emr/current/hadoop//README.txt /tmp/flink_data.txt 
      flink run -m yarn-cluster /usr/lib/emr/current/flink/examples/streaming/WordCount.jar --input hdfs://emr-cluster/tmp/flink_data.txt --output hdfs://emr-cluster/tmp/flinktest_out
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The HDFS path needs to be modified according to the actual environment.      </div>
      

   2. View the WordCount execution result.

      ```powershell
      hadoop fs -cat /tmp/flinktest_out/*/*
      ```
      


<span id="执行-hbase-用例"></span>
## **Run an HBase use case**


1. Generate the user's ticket.

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

2. Run the Hive CLI.

   1. Enter 'hbase shell' to access the console.

   2. Enter the following statement.

      ```sql
      create 't1', 'f1', SPLITS => ['10', '20', '30', '40']
      put 't1', 'r1', 'f1:c1', 'value'
      scan 't1'
      ```
      


<span id="执行-presto-trino-用例"></span>
## **Run a Presto/Trino use case**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since Presto and Trino are used in the same way, the following uses Presto as an example.</div>



1. Run the Presto command:

   ```powershell
   presto \
   --krb5-principal=${用户的principal} \
   --krb5-keytab-path=${principal对应的keytab文件} \
   ```
   

   Example:

   ```powershell
   presto --krb5-principal=user01 --krb5-keytab-path=/etc/krb5/keytab/user/user01.keytab
   ```
   

2. Enter the Presto SQL statement `select * from tpch.sf1.nation`:

   ```powershell
   presto> select * from tpch.sf1.nation;
    nationkey |      name      | regionkey |                                                      comment                                                       
   -----------+----------------+-----------+--------------------------------------------------------------------------------------------------------------------
            0 | ALGERIA        |         0 |  haggle. carefully final deposits detect slyly agai                                                                
            1 | ARGENTINA      |         1 | al foxes promise slyly according to the regular accounts. bold requests alon                                       
            2 | BRAZIL         |         1 | y alongside of the pending deposits. carefully special packages are about the ironic forges. slyly special         
            3 | CANADA         |         1 | eas hang ironic, silent packages. slyly regular packages are furiously over the tithes. fluffily bold              
            4 | EGYPT          |         4 | y above the carefully unusual theodolites. final dugouts are quickly across the furiously regular d                
            5 | ETHIOPIA       |         0 | ven packages wake quickly. regu                                                                                    
            6 | FRANCE         |         3 | refully final requests. regular, ironi                                                                             
            7 | GERMANY        |         3 | l platelets. regular accounts x-ray: unusual, regular acco                                                         
            8 | INDIA          |         2 | ss excuses cajole slyly across the packages. deposits print aroun                                                  
            9 | INDONESIA      |         2 |  slyly express asymptotes. regular deposits haggle slyly. carefully ironic hockey players sleep blithely. carefull 
           10 | IRAN           |         4 | efully alongside of the slyly final dependencies.                                                                  
           11 | IRAQ           |         4 | nic deposits boost atop the quickly final requests? quickly regula                                                 
           12 | JAPAN          |         2 | ously. final, express gifts cajole a                                                                               
           13 | JORDAN         |         4 | ic deposits are blithely about the carefully regular pa                                                            
           14 | KENYA          |         0 |  pending excuses haggle furiously deposits. pending, express pinto beans wake fluffily past t                      
           15 | MOROCCO        |         0 | rns. blithely bold courts among the closely regular packages use furiously bold platelets?                         
           16 | MOZAMBIQUE     |         0 | s. ironic, unusual asymptotes wake blithely r                                                                      
           17 | PERU           |         1 | platelets. blithely pending dependencies use fluffily across the even pinto beans. carefully silent accoun         
           18 | CHINA          |         2 | c dependencies. furiously express notornis sleep slyly regular accounts. ideas sleep. depos                        
           19 | ROMANIA        |         3 | ular asymptotes are about the furious multipliers. express dependencies nag above the ironically ironic account    
           20 | SAUDI ARABIA   |         4 | ts. silent requests haggle. closely express packages sleep across the blithely                                     
           21 | VIETNAM        |         2 | hely enticingly express accounts. even, final                                                                      
           22 | RUSSIA         |         3 |  requests against the platelets use never according to the quickly regular pint                                    
           23 | UNITED KINGDOM |         3 | eans boost carefully special requests. accounts are. carefull                                                      
           24 | UNITED STATES  |         1 | y final packages. slow foxes cajole quickly. quickly silent platelets breach ironic accounts. unusual pinto be     
   (25 rows)
   
   Query 20230720_031745_00001_v2hmn, FINISHED, 2 nodes
   Splits: 32 total, 32 done (100.00%)
   [Latency: client-side: 225ms, server-side: 192ms] [25 rows, 0B] [130 rows/s, 0B/s]
   ```
   


<span id="执行-kafka-用例"></span>
## **Run a Kafka use case**


1. Prepare the client configuration file.

   1. Edit the `kafka_client_jaas.conf` file (for example, place it in the `/etc/emr/kafka/conf` directory. If there is a file with the same name in the directory, you can change the directory, file name, or rename the existing file).

      ```properties
      KafkaClient {
         com.sun.security.auth.module.Krb5LoginModule required
         useTicketCache=true
         renewTicket=true;
      };
      ```
      

   2. Edit the `client.properties` file (for example, place it in the `/etc/emr/kafka/conf` directory. If there is a file with the same name in the directory, you can change the directory, file name, or rename the existing file).

      ```properties
      security.protocol=SASL_PLAINTEXT
      sasl.mechanism=GSSAPI
      sasl.kerberos.service.name=kafka
      ```
      

2. Generate a user ticket.

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

3. Create a topic.

   ```bash
   export KAFKA_OPTS="-Djava.security.krb5.conf=/etc/krb5.conf -Djava.security.auth.login.config=/etc/emr/kafka/conf/kafka_client_jaas.conf" && /usr/lib/emr/current/kafka/bin/kafka-topics.sh --create --bootstrap-server {broker地址}:9092 --command-config /etc/emr/kafka/conf/client.properties --topic test --replication-factor 3 --partitions 12
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, {broker address} refers to the IP address of Kafka's Broker, which needs to be configured according to the specific environment.   </div>
   

4. View the topic list.

   ```bash
   export KAFKA_OPTS="-Djava.security.krb5.conf=/etc/krb5.conf -Djava.security.auth.login.config=/etc/emr/kafka/conf/kafka_client_jaas.conf" && /usr/lib/emr/current/kafka/bin/kafka-topics.sh --list --bootstrap-server {broker地址}:9092 --command-config /etc/emr/kafka/conf/client.properties
   ```
   

5. Produce messages.

   ```bash
   export KAFKA_OPTS="-Djava.security.krb5.conf=/etc/krb5.conf -Djava.security.auth.login.config=/etc/emr/kafka/conf/kafka_client_jaas.conf" && /usr/lib/emr/current/kafka/bin/kafka-console-producer.sh --broker-list {broker地址}:9092 --topic test --producer.config /etc/emr/kafka/conf/client.properties
   ```
   

6. Consume messages.

   ```bash
   export KAFKA_OPTS="-Djava.security.krb5.conf=/etc/krb5.conf -Djava.security.auth.login.config=/etc/emr/kafka/conf/kafka_client_jaas.conf" && /usr/lib/emr/current/kafka/bin/kafka-console-consumer.sh --bootstrap-server {broker地址}:9092 --group testGroup --topic test --from-beginning earliest --consumer.config /etc/emr/kafka/conf/client.properties
   ```
   


<span id="执行-kyuubi-用例"></span>
## **Run Kyuubi cases**


1. Generate a user ticket

   ```powershell
   kinit  -k -t  /etc/krb5/keytab/user/user01.keytab user01
   ```
   

2. Connect to Kyuubi

   Enter the following command:

   ```shell
   beeline -u "jdbc:hive2://${zookeeper的地址}/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=kyuubi;principal=${Kyuubi服务参数中的kyuubi.kinit.principal参数值}"
   ```
   

   Example:

   ```shell
   beeline -u "jdbc:hive2://10.0.255.9:2181,10.0.255.7:2181,10.0.255.8:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=kyuubi;principal=hive/_HOST@2FDE5608A274D0A2320C.EMR.COM"
   ```
   

   Then enter the following SQL statement:

   ```sql
   CREATE TABLE IF NOT EXISTS t3(i INT, s STRING);
   INSERT INTO t3 VALUES(0, 'a');
   SELECT * FROM t3;
   ```
   


<span id="执行-flume-用例"></span>
## Run Flume cases


1. Add the configuration file flume_jaas.conf in the /etc/emr/flume/conf directory with the following content:

   ```python
   KafkaClient {
      com.sun.security.auth.module.Krb5LoginModule required
      useKeyTab=true
      keyTab="/etc/krb5/keytab/serv/kafka.keytab"
      storeKey=true
      serviceName="kafka"
      principal="${principal}";
   };
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, ${principal} needs to match the kafka.keytab file, which can be obtained using the command <code>klist -k -t /etc/krb5/keytab/serv/kafka.keytab</code>.   </div>
   

2. Configure the parameter file for Flume to read Kafka in the /etc/emr/flume/conf directory: flume\-kerberos\-kafka.properties, with the following content:

   ```python
   a1.sources = source1
   a1.sinks = k1
   a1.channels = c1
   
   a1.sources.source1.type = org.apache.flume.source.kafka.KafkaSource
   a1.sources.source1.channels = c1
   a1.sources.source1.kafka.consumer.group.id = flume-test-group
   a1.sinks.k1.type = hdfs
   a1.sinks.k1.hdfs.path = hdfs://emr-cluster/tmp/flume/test-data
   a1.sinks.k1.hdfs.fileType=DataStream
   # Use a channel which buffers events in memory
   a1.channels.c1.type = memory
   a1.channels.c1.capacity = 1001
   a1.channels.c1.transactionCapacity = 1000
   # Bind the source and sink to the channel
   a1.sources.source1.channels = c1
   a1.sinks.k1.channel = c1
   a1.sources.source1.kafka.bootstrap.servers = ${broker地址}:9092
   a1.sources.source1.kafka.topics = ${topic名字}
   
   a1.sources.source1.kafka.consumer.security.protocol=SASL_PLAINTEXT
   a1.sources.source1.kafka.consumer.sasl.mechanism=GSSAPI
   a1.sources.source1.kafka.consumer.sasl.kerberos.service.name=kafka
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The HDFS path in the example needs to be modified according to the actual environment.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <strong>{broker address}</strong> refers to the IP address of Kafka's Broker, which needs to be configured according to the specific environment.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <strong>${topic name}</strong> is a topic created according to the previous Kafka case.   </div>
   

3. Add the following parameters to the flume\-env.sh configuration file:

   ```python
   export JAVA_OPTS="$JAVA_OPTS -Djava.security.krb5.conf=/etc/krb5.conf"
   export JAVA_OPTS="$JAVA_OPTS -Djava.security.auth.login.config=/etc/emr/flume/conf/flume_jaas.conf
   ```
   

4. Start Flume

   ```python
   nohup /usr/lib/emr/current/flume/bin/flume-ng agent --name a1 --conf /etc/emr/flume/conf/ --conf-file flume-kerberos-kafka.properties > nohup.out 2>&1 &
   ```
