---
title: "Read data in Hadoop clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Read_data_in_Hadoop_clusters"
---

This article describes how to configure an EMR Serverless StarRocks instance to query data in a Hadoop high availability cluster.

<span id="_1-前提条件"></span>
## 1 **prerequisites**


* A cluster that includes the HDFS service and has high availability enabled has been created. For details, see [Create clusters (3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

* An EMR Serverless StarRocks instance has been created. For details, see instance creation.


<span id="_2-操作步骤"></span>
## 2 **procedure**


1. Go to the EMR Serverless StarRocks instance configuration page.

   a. [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

   b. In the top menu bar, select the region as needed.

   c. On the instance list page, click the name of the instance you want to view.

   d. Click the **Instance Configuration** tab.

2. Modify the hdfs\-site.xml configuration.

   a. Click **hdfs\-site.xml**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6a17d2ceef74d549ad2f9052c16b2c7~tplv-goo7wpa0wc-image.image) </span>

   b. Modify or add the following configuration items.

   
   |Parameter |Description |
   |---|---|
   |dfs.nameservices |The configuration value must be consistent with the value of dfs.nameservices in the hdfs\-site.xml configuration file of the existing high availability cluster HDFS service. The default value is emr\-cluster. |
   |dfs.ha.namenodes.<cluster_name\> |The configuration values must be consistent with the corresponding configuration items in the hdfs\-site.xml file of the existing high\-availability HDFS cluster service. |
   |dfs.namenode.rpc\-address.<cluster_name\> ||
   |dfs.client.failover.proxy.provider.<cluster_name\> ||
   

   c. Click **OK**.

3. Save the configuration.

   a. Click **Submit Parameters**.

   b. In the pop\-up dialog box, enter the **reason description** and click **OK**.


<span id="_3-示例"></span>
## Example 3


1. Prepare test data in Parquet format in the Hadoop cluster

   Start the Hive CLI and execute the following commands

   ```sql
   CREATE TABLE table1(name STRING, id INT) STORED AS PARQUET;
   INSERT INTO table1 values('a', 1), ('b', 2), ('c', 3), ('d', 4), ('e', 5), ('f', 6);
   ```
   


Use `SHOW CREATE TABLE table1` to determine the location of the data on HDFS.


2. In the StarRocks instance console, modify the hdfs\-site.xml parameters as shown below:

   ```properties
   <?xml version="1.0" encoding="UTF-8"?>
   <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
   <configuration>
   <property>
       <name>dfs.nameservices</name>
       <value>emr-cluster</value>
   </property>
   <property>
       <name>dfs.ha.namenodes.emr-cluster</name>
       <value>emr-f65a635e7a7d7a1146c4-master-1,emr-f65a635e7a7d7a1146c4-master-2</value>
   </property>
   <property>
       <name>dfs.namenode.rpc-address.emr-cluster.emr-f65a635e7a7d7a1146c4-master-1</name>
       <value>192.168.xx.xx:8020</value>
   </property>
   <property>
       <name>dfs.namenode.rpc-address.emr-cluster.emr-f65a635e7a7d7a1146c4-master-2</name>
       <value>192.168.xx.xx:8020</value>
   </property>
   <property>
       <name>dfs.client.failover.proxy.provider.emr-cluster</name>
       <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
   </property>
   </configuration>
   ```
   

3. Query data in HDFS files in StarRocks

   ```sql
   CREATE DATABASE db_example;
   USE db_example;
   CREATE EXTERNAL TABLE t0
   (
       name string, 
       id int
   ) 
   ENGINE=file
   PROPERTIES 
   (
       "path"="hdfs://emr-cluster/warehouse/tablespace/managed/hive/table1/", 
       "format"="parquet"
   );
   --Query data in the table
   SELECT * FROM db_example.t0;
   ```
   


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14610e5f54f584c481427a97fb07d1cb.png) </span>

<span id="_4-访问keberos的集群"></span>
## 4 Accessing a Kerberos cluster

<span id="_4-1-kerberos与starrocks混合部署"></span>
### 4.1 Kerberos and StarRocks hybrid deployment

Add properties to the hdfs\-site.xml file and restart the StarRocks cluster

```xml
<property>
    <name>dfs.data.transfer.protection</name>
    <value>integrity</value>
</property>
```


<span id="_4-2-kerberos与starrocks独立部署"></span>
### 4.2 Kerberos and StarRocks standalone deployment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">First, copy the contents of the core\-site.xml file in Hadoop to the configuration items of StarRocks, then restart the cluster.</div>


The community edition of HDFS supports two authentication methods: simple authentication and Kerberos authentication (Broker Load uses simple authentication by default), and supports HA configuration for NameNode nodes. If the storage system is the community edition of HDFS, you can specify the authentication method and HA configuration as follows:


* Authentication method

   * If you use simple authentication, configure `StorageCredentialParams` as follows:

   ```plain
   "hadoop.security.authentication" = "simple"
   "username" = "<hdfs_username>",
   "password" = "<hdfs_password>"
   ```
   

   * `StorageCredentialParams` includes the following parameters.

   
   |Parameter name |Parameter description |
   |---|---|
   |hadoop.security.authentication |Specifies the authentication method. Value range: simple and kerberos. Default value: simple. simple means simple authentication, that is, no authentication. kerberos means Kerberos authentication. |
   |username |The username used to access the NameNode node in the HDFS cluster. |
   |password |The password used to access the NameNode node in the HDFS cluster. |
   

   * If you use Kerberos authentication, configure `StorageCredentialParams` as follows:

   ```plain
   "hadoop.security.authentication" = "kerberos",
   "kerberos_principal" = "nn/zelda1@ZELDA.COM",
   "kerberos_keytab" = "/keytab/hive.keytab",
   "kerberos_keytab_content" = "YWFhYWFh"
   ```
   

   * `StorageCredentialParams` includes the following parameters.

   
   |Parameter name |Parameter description |
   |---|---|
   |hadoop.security.authentication |Specifies the authentication method. Value range: simple and kerberos. Default value: simple. simple means simple authentication, that is, no authentication. kerberos means Kerberos authentication. |
   |kerberos_principal |Used to specify the Kerberos user or service (Principal). Each Principal is unique within the HDFS cluster and consists of the following three parts: username or servicename: the name of the user or service in the HDFS cluster. instance: the name of the server where the node to be authenticated in the HDFS cluster is located, used to ensure the global uniqueness of the user or service. For example, there are multiple DataNode nodes in the HDFS cluster, and each node requires independent authentication. realm: the domain, which must be in uppercase. Example: [nn/zelda1@ZELDA.COM](mailto:nn/zelda1@ZELDA.COM). |
   |kerberos_keytab |Used to specify the path to the Kerberos Key Table (commonly referred to as the "keytab") file. |
   |kerberos_keytab_content |Used to specify the content of the keytab file in Kerberos after it has been encoded in Base64. This parameter and the kerberos_keytab parameter are mutually exclusive; configure one or the other. |
   

   * Important: In scenarios with multiple Kerberos users, you must ensure that at least one independent set of [Broker](https://docs.starrocks.io/zh/docs/deployment/deploy_broker) is deployed, and specify which set of Broker to use in the import statement by using `WITH BROKER "<broker_name>"`. Additionally, you need to open the Broker process startup script file start_broker.sh, and modify the information near line 42 so that the Broker process reads the krb5.conf file information:

   ```plain
   export JAVA_OPTS="-Dlog4j2.formatMsgNoLookups=true -Xmx1024m -Dfile.encoding=UTF-8 -Djava.security.krb5.conf=/etc/krb5.conf"
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The path to the /etc/krb5.conf file should be modified according to actual conditions, and the Broker must have permission to read this file. When deploying multiple Brokers, each Broker node must modify the above information, then restart each Broker node to make the configuration take effect.</div>


* <div data-tips="true" data-tips-type="tip">You can use the <a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/Administration/SHOW_BROKER">SHOW BROKER</a> statement to view the Brokers already deployed in the StarRocks cluster.</div>
