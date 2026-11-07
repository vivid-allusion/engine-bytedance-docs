---
title: "Spark uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_uses_Proton"
---

<span id="_1-火山-emr"></span>
## Volcano EMR

<span id="_1-1-认证配置"></span>
### Authentication configuration

For details on authentication configuration for Volcano Engine E\-MapReduce (EMR), see [Hadoop 使用 Proton - 认证配置](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE).

By default, as long as EMR and TOS services are enabled by the same user, manual configuration for accessing TOS is not required on the EMR cluster. Otherwise, manual AK/SK configuration is required.

<span id="_1-2-hdfs-配置"></span>
### HDFS configuration

The EMR cluster has already been configured with the relevant HDFS settings, so no additional configuration is needed.

<span id="_1-3-spark-配置"></span>
### Spark configuration

The EMR cluster has already been configured with the relevant Spark settings, so no additional configuration is needed.

<span id="_2-自建-hadoop-集群"></span>
## Self\-built Hadoop cluster

<span id="_2-1-认证配置"></span>
### Authentication configuration

Please refer to the [Hadoop 使用 Proton - 认证配置](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE) section for authentication configuration.

<span id="_2-2-sdk-部署"></span>
### SDK deployment


1. In the [Proton release version](https://docs.byteplus.com/docs/E-MapReduce/109371), download the corresponding SDK tar package according to the Proton version and extract it.

2. Place `plugins/hadoop${hadoop.major.version}/proton-hadoop${hadoop.major.version}-bundle-{proton.version}.jar` in the following two directories. Here, `hadoop.major.version` can be `2` or `3`, corresponding to Hadoop 2.x or Hadoop 3.x, and `proton.version` is the Proton version.

   * `$HADOOP_HOME/share/hadoop/hdfs/`

   * `$SPARK_HOME/jars/`


<span id="_2-3-hdfs-配置"></span>
### HDFS configuration

Configure Hadoop's `core-site.xml` so that the HDFS client uses Proton's FileSystem when accessing TOS:

```XML
<configuration>
   <property>
        <name>fs.tos.access-key-id</name>
        <value>{iam.role.access.key}</value>
        <!--TOS authentication configuration: EMR cluster does not need to configure this item-->
   </property>
   <property>
        <name>fs.tos.secret-access-key</name>
        <value>{iam.role.access.val}</value>
        <!--TOS authentication configuration: EMR cluster does not need to configure this item-->
    </property>
    <property>
        <name>fs.tos.impl</name>
        <value>io.proton.fs.ProtonFileSystem</value>
    </property>
    <property>
        <name>fs.tos.endpoint</name>
        <value>http://tos-cn-{region}.volces.com</value>
        <!--If you are in the Volcano ECS environment (including Volcano EMR), you can use the internal endpoint: http://tos-cn-{region}.ivolces.com-->
    </property>
</configuration>
```


<span id="_2-4-spark-配置"></span>
### Spark configuration


1. Download and install the Spark committer based on Proton

   First, download [proton-spark-3.5.1-2.2.jar](https://emr-manager-repository.tos-cn-beijing.volces.com/releases/SPARK/spark/3.5.1/proton-spark-3.5.1-2.2.jar) (corresponding to Spark 3.5.1 version) and place it under `${SPARK_HOME}/jars` on each node. If the `spark.yarn.archive` parameter is configured, ensure that this jar is included in the archive.

   For other versions of the committer jar, you can obtain them from [JobCommitter version](https://docs.byteplus.com/docs/E-MapReduce/109372).

2. Configure spark

   Configure Spark's `spark-default.conf` so that Spark uses Proton's JobCommitter when using Submit Job:

   * Spark 3.x:

   ```plain
   spark.sql.extensions io.proton.spark.ProtonSparkSessionExtension
   ```
   

   * Spark 2.x:

   ```plain
   spark.hadoop.mapreduce.outputcommitter.class io.proton.commit.Committer
   spark.sql.sources.commitProtocolClass org.apache.spark.internal.io.cloud.EMROutputCommitProtocol
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For self\-built clusters, ensure that Spark can load Hadoop's <code>core-site.xml</code>. This can be achieved by setting <code>spark-env.sh</code> with <code>export HADOOP_CONF_DIR=/your/hadoop/conf/dir</code>.</div>


<span id="94949c00"></span>
## Serverless Spark uses the s3 scheme

When metadata is stored using s3/s3a or other non\-TOS schemes, and data files are on TOS, it is recommended to use Proton in serverless scenarios. Refer to the following for configuration.

```Python
spark.hadoop.fs.{scheme}.endpoint=http://tos-{region}.ivolces.com
spark.hadoop.fs.{scheme}.impl=io.proton.fs.ProtonFileSystem
spark.hadoop.fs.AbstractFileSystem.{scheme}.impl=io.proton.fs.ProtonFS
spark.hadoop.proton.objectstorage.{scheme}.impl=io.proton.common.object.tos.TOS
spark.hadoop.fs.{scheme}.access-key-id=xxxxxx
spark.hadoop.fs.{scheme}.secret-access-key=xxxxxx

//如果是s3a，proton有重名配置的兼容性问题，需要额外加下面两个参数覆盖core-default.xml中的默认值：
spark.hadoop.fs.s3a.multipart.size=67108864
spark.hadoop.fs.s3a.multipart.threshold=134217728
```


Example: region: North China, scheme: s3a, storage location: tos

```Python
spark.hadoop.fs.s3a.endpoint=http://tos-cn-beijing.ivolces.com
spark.hadoop.fs.s3a.impl=io.proton.fs.ProtonFileSystem
spark.hadoop.fs.AbstractFileSystem.s3a.impl=io.proton.fs.ProtonFS
spark.hadoop.proton.objectstorage.s3a.impl=io.proton.common.object.tos.TOS
spark.hadoop.fs.s3a.access-key-id=xxxxxx
spark.hadoop.fs.s3a.secret-access-key=xxxxxx
spark.hadoop.fs.s3a.multipart.size=67108864
spark.hadoop.fs.s3a.multipart.threshold=134217728
```


<span id="_3-测试"></span>
## Testing


1. Open Spark SQL and create a test table:


```SQL
CREATE TABLE testProton(id INT, name STRING) USING parquet LOCATION "tos://<your_bucket>/path/to/table";
```



2. Insert some data into the table:


```SQL
INSERT INTO testProton VALUES (1, 'zhangsan'), (2, 'lisi');
```



3. Open the TOS console, locate the table directory, and confirm that there is a `_SUCCESS` file. Download and open this file. If it contains the following text, it indicates that the Proton committer was used:


```JSON
{
  "name" : "io.proton.commit.SuccessData",
  "success" : true,
  "timestamp" : 1679043015429,
  "date" : null,
  "hostname" : "xdesktop/127.0.0.1",
  "committer" : "io.proton.commit.Committer",
  "description" : "Task committer attempt_20230317165012_0000_m_000000_0",
  "jobId" : "job_25d10e1f-e315-4403-8acc-7adada1f1ed0",
  "filenames" : [ "spark-tables/1679042998827/testProton/part-00000-f9917923-a220-49fb-a2dd-626535a7a6d7-c000.snappy.parquet" ],
  "diagnostics" : {
    "fs.job.committer.threads" : "10"
  }
}
```
