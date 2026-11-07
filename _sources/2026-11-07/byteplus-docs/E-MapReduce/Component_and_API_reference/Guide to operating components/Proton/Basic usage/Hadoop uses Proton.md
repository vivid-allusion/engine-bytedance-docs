---
title: "Hadoop uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hadoop_uses_Proton"
---

The following section first describes how to use Proton to implement a storage\-compute separation architecture in two scenarios: Volcano Engine EMR and self\-built Hadoop clusters. It then explains how to configure the recycle bin in the storage\-compute separation mode, and finally describes how to introduce the Proton dependency in the development environment.

<span id="e0710d2c"></span>
## Volcano Engine EMR

<span id="_1-1-认证配置"></span>
### Authentication configuration

<span id="_1-1-1-使用-assume-role-认证-tos"></span>
#### Use Assume Role to authenticate TOS

Assume Role does not require you to explicitly configure your account AK/SK in the cluster. The cluster will automatically obtain temporary identity credentials through IAM during operation.

<span id="b60bfc02"></span>
##### **Prerequisites**


* Enable the Volcano Engine E\-MapReduce (EMR) service and create an EMR cluster. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

* Enable the object storage service TOS and create a TOS bucket. For details, see: [TOS Quick Start](https://www.volcengine.com/docs/6349/74830).

* When creating an EMR cluster, in **Other Settings \> Advanced Settings \> Cluster Role**, select a **cluster role** that has TOS permissions:

   1. Go to [Access Control > Role Management](https://console.volcengine.com/iam/identitymanage/role), and click the **Create Role** button to create a role. For details, see: [Role Management](https://www.volcengine.com/docs/6257/64979) **.** 

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9782f2a101b7bfe157b51a25d35d689c.png) </span>

   2. Add the corresponding TOS full read/write access permission to the role: **TOSFullAccess.** 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no cluster role is selected when creating an EMR cluster, the ECS role will be added by default: <strong>VEECSforEMRRole.</strong>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting <strong>Advanced settings \> Cluster role</strong>, if the newly created role does not appear in the dropdown, check in <strong>Role details \> Trust relationships</strong> whether the "<strong>Service</strong>" parameter includes a relationship with "<strong>Volc_ECS</strong>". If not, simply add it.   </div>
   


<span id="ddb506ba"></span>
##### **Using TOS**

You can directly use the TOS service in the EMR cluster. For example, you can use HDFS commands:

```plain
hadoop fs -ls tos://{bucket name}/
```


To list files in a TOS bucket, use the following command. If you need to process data in TOS as tables in a compute engine such as Hive, set the location field value to the TOS address when creating a Hive table to analyze TOS data. For example:

```SQL
CREATE EXTERNAL TABLE `palmplay_log_pv_csv`(  
  `meta_id` STRING COMMENT 'from deserializer',
  `brand` STRING COMMENT 'from deserializer',  
  `channel` STRING COMMENT 'from deserializer',  
  `countrycode` STRING COMMENT 'from deserializer')  
PARTITIONED BY  (dt String)  
ROW FORMAT SERDE
  'org.apache.hadoop.hive.serde2.OpenCSVSerde'   
STORED AS TEXTFILE   
LOCATION
  'tos://{tos bucket name}/';
```


For any component within EMR, you can use addresses starting with tos:// to access TOS data. For more information about using TOS with other engines, please refer to the corresponding engine documentation.

<span id="_1-1-2-使用静态-ak-sk"></span>
#### Using static AK/SK

Static AK/SK records permanent identity information in the cluster configuration file, which is inconvenient to manage.

<span id="f4030fef"></span>
##### **Prerequisites**


1. Enable the EMR service and create an EMR cluster. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Enable the TOS service and create a TOS bucket. For details, see: [TOS Quick Start](https://www.volcengine.com/docs/6349/74830).

3. Obtain the Access Key ID and Secret Access Key through [IAM Access Control > Key Management](https://console.volcengine.com/iam/keymanage). For details, see: [Access Key](https://www.volcengine.com/docs/6291/65568).

4. If the TOS bucket was not created by the user whose AK/SK you are using, you must ensure that the AK/SK has read and write permissions for the TOS bucket. You can grant permissions to the user in [TOS](https://console.volcengine.com/tos/bucket/setting)  **\> Bucket \> Permission Management \> Bucket Authorization Policy Management**.

5. Add the following custom parameters to **core\-site** in the **Service Management \> HDFS \> Service Parameters \> Add Custom Parameter** configuration on the EMR cluster details page.

   ```bash
   fs.tos.access-key-id={Access Key ID}
   fs.tos.secret-access-key={Secret Access Key}
   ```
   

   To use different authentication keys for different buckets, apply the following configuration:

   ```bash
   fs.tos.bucket.您的bucket.access.key={Access Key ID}
   fs.tos.bucket.您的bucket.secret.key={Secret Access Key}
   ```
   


<span id="0a5caca0"></span>
##### **Use TOS**

TOS services can be used directly in the EMR cluster. For example, you can use the HDFS command:

```bash
hadoop fs -ls tos://{bucket name}/
```


List files in the TOS bucket. To process data in TOS as tables in a compute engine such as Hive, set the location field to the TOS address when creating the Hive table. This allows you to analyze TOS data. For example:

```SQL
CREATE EXTERNAL TABLE `palmplay_log_pv_csv`(  
  `meta_id` STRING COMMENT 'from deserializer',
  `brand` STRING COMMENT 'from deserializer',  
  `channel` STRING COMMENT 'from deserializer',  
  `countrycode` STRING COMMENT 'from deserializer')  
PARTITIONED BY  (dt String)  
ROW FORMAT SERDE
  'org.apache.hadoop.hive.serde2.OpenCSVSerde'   
STORED AS TEXTFILE  
LOCATION
  'tos://{tos bucket name}/';
```


For any component within EMR, you can access TOS data using addresses that start with tos://. For more information about using TOS with other engines, refer to the documentation for the respective engine.

<span id="_1-1-3-环境变量配置-ak-sk"></span>
#### Configure AK/SK as environment variables

<span id="b8206f4f"></span>
##### **prerequisites**


1. Enable the EMR service and create an EMR cluster. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Enable the TOS service and create a TOS bucket. For details, see [TOS Quick Start](https://www.volcengine.com/docs/6349/74830).

   ```bash
   export TOS_ACCESS_KEY_ID={Access Key ID}
   export TOS_SECRET_ACCESS_KEY={Secret Access Key}
   export ENV_TOS_SESSION_TOKEN={Token}
   ```
   

3. Inject the corresponding AK/SK as environment variables in the current shell context using the export keyword.


<span id="123d508d"></span>
##### **Use TOS**

TOS services can be used directly in the EMR cluster. For example, you can use the HDFS command:

```bash
hadoop fs -ls tos://{bucket name}/
```


List files in the TOS bucket.

<span id="_1-2-参数调优"></span>
### Parameter tuning

Since Volcano EMR integrates Proton by default and it is already enabled in the relevant components, no additional configuration is required. You can tune parameters by modifying the core\-site.xml configuration file. For specific parameter details, refer to the parameter tuning section of [Proton parameter configuration](https://docs.byteplus.com/docs/undefined/69a967da949de005696297bc).

<span id="_2-自建-hadoop-集群"></span>
## Self\-managed Hadoop cluster

<span id="_2-1-hadoop3-系列"></span>
### Hadoop3 series

<span id="_2-1-1-下载依赖"></span>
#### Download dependencies

Refer to the version information in [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371), select the appropriate Proton version, download the corresponding Proton package, and after extraction, place plugins/hadoop3/proton\-hadoop3\-bundle\-\*.jar in the share/hadoop/hdfs/lib directory under the HDFS installation path.

<span id="_2-1-2-配置修改"></span>
#### Configuration modification

Modify core\-site.xml and add the following content:

```javascript
<configuration>
   <!--Required properties-->
   <!--Filesystem implementation class for TOS-->
   <property>
       <name>fs.AbstractFileSystem.tos.impl</name>
       <value>io.proton.fs.ProtonFS</value>
   </property>
   <property>
       <name>fs.tos.impl</name>
       <value>io.proton.fs.ProtonFileSystem</value>
   </property>
   <property>
       <name>fs.tos.endpoint</name>
       <value>http://tos-cn-beijing.ivolces.com</value>
   </property>
   <property>
       <name>proton.cache.enable</name>
       <value>false</value>
   </property>
   <!--Optional properties-->
   <!--Job Commiter implementation class-->
   <property>
       <name>mapreduce.outputcommitter.factory.class</name>
       <value>io.proton.commit.CommitterFactory</value>
       <description>The job committer implementation class accelerate read and write data to TOS object storage via MPU instead of rename.</description>
   </property>
   <property>
       <name>fs.tos.credentials.provider</name>
       <value>io.proton.common.object.tos.auth.DefaultCredentialsProviderChain</value>
   </property>
   <!-- Credential provider mode 2: static AK/SK for all buckets -->
   <property>
       <name>fs.tos.credentials.provider</name>
       <value>io.proton.common.object.tos.auth.SimpleCredentialsProvider</value>
   </property>
   <property>
       <name>fs.tos.access-key-id</name>
       <value>yourAk</value>
   </property>
   <property>
       <name>fs.tos.secret-access-key</name>
       <value>yourSk</value>
   </property>
   <!--TOS Client configuration-->
   <!--we can overwrite these properties to optimize TOS read and write performance-->
   <property>
       <name>fs.tos.http.maxConnections</name>
       <value>1024</value>
   </property>
</configuration>
```


<span id="_2-2-hadoop2-系列"></span>
### Hadoop2 series

<span id="_2-2-1-下载依赖"></span>
#### Download dependencies

Refer to the version information in [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371), select the appropriate Proton version, download the corresponding Proton package, and after extraction, place plugins/hadoop2/proton\-hadoop2\-bundle\-\*.jar in the share/hadoop/hdfs/lib directory under the HDFS installation path.

<span id="_2-2-2-配置修改"></span>
#### Configuration modification

The configuration for Hadoop2 is the same as for Hadoop3. Refer to the Hadoop3 documentation for Job committer configuration. Since the open\-source Hadoop2 HDFS does not support external Job Committer interfaces by default, to use JobCommitter, you need to download the Volcano\-modified HDFS dependency package. For specific download methods, you can contact the EMR technical team for support by [submitting a ticket](https://console.volcengine.com/workorder/create/).

<span id="_2-3-参数调优"></span>
### Parameter tuning

Parameter tuning for self\-managed clusters is the same as for Volcano EMR. For usage instructions, please refer to [4 Parameter tuning](https://docs.byteplus.com/docs/E-MapReduce/109367#_4-%E5%8F%82%E6%95%B0%E8%B0%83%E4%BC%98).

<span id="_3-回收站配置"></span>
## Recycle bin configuration

After deleting a file in HDFS, the file is not deleted immediately but is moved to the recycle bin. The default location is `hdfs://cluster/user/username/.Trash/`. You can configure the lifecycle time of files in the recycle bin using the following parameter in core\-site:

```javascript
<property>  
    <name>fs.trash.interval</name>  
    <value>1440</value>  
    <description>Number of minutes after which the checkpoint gets deleted. If zero, the trash feature is disabled.</description>  
</property>
```


The NameNode will periodically clean up files in the recycle bin based on the configured value. In a compute\-storage separation architecture, after using object storage, EMR becomes a stateless compute engine. Therefore, there is no resident recycle bin management service, and users need to manage it themselves. You can control the lifecycle of the recycle bin using the following two methods.

<span id="_3-1-禁用回收站"></span>
### Disable the recycle bin

If there is no need for a recycle bin, modify the fs.trash.interval parameter in core\-site under EMR's service list \- hdfs \- configuration management, and set its value to 0.

<span id="_3-2-配置对象存储生命周期管理方案"></span>
### Configure object storage lifecycle management

To retain the recycle bin functionality, go to the corresponding bucket on the object storage page and create the appropriate lifecycle management rule:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_31efb4924557b9e659e7b6310b38f496.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e701002cb599eb270baab4c04a908a4.png) </span>

Select the specified prefix method, and based on the current bucket and user, determine the address of the corresponding recycle bin and configure its lifecycle. For more usage methods, please refer to: [Set lifecycle rules](https://www.volcengine.com/docs/6349/75028)

<span id="_4-开发指导"></span>
## Development guidance

If you are developing similar code locally and need to debug or test TOS using Committer, download the corresponding Job committer bundle dependency package, place it in the project root directory, and add the following to pom.xml:

```javascript
<dependency>
    <groupId>io.proton/groupId>
    <artifactId>proton-hadoop您的Hadoop版本-bundle</artifactId>
    <version>1.1</version>
    <scope>system</scope>
    <systemPath>${project.basedir}/Name_Your_JAR.jar</systemPath>
</dependency>
```
