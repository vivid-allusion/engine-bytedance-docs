---
title: "Serverless Spark access to Kerberos clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Spark_access_to_Kerberos_clusters"
---

Serverless Spark access to Kerberos clusters refers to securely accessing clusters protected by Kerberos authentication in a serverless Spark environment. This addresses the need to access secure clusters in serverless scenarios and is suitable for handling Kerberos\-authenticated HDFS or Hive data and similar use cases. This article will guide you through the configuration and usage steps.

<span id="4ee63863"></span>
## Prerequisites


* An EMR on ECS cluster has been created, and **Kerberos authentication** is enabled. For detailed instructions, refer to: Using Kerberos authentication clusters.

* An exclusive EMR Serverless queue has been created, and you have permission to operate this queue.

* Object storage TOS has been enabled.


<span id="e1115a03"></span>
## Limits


1. Access to Kerberos clusters is only supported under the default compute group of exclusive queues.

2. The system only supports Serverless Spark accessing storage\-compute separated Kerberos clusters, and does not support Spark Streaming job access.

3. A single Serverless queue only supports access to one Kerberos cluster.

4. In Spark jobs accessing Kerberos authentication clusters, the **Driver cannot use the queue's elastic resources**; only the **Executor can schedule elastic resources normally**. Because the Driver is a prerequisite for job startup (it must occupy resources to complete initialization first), you must ensure that there are available fixed resources under the default compute group to support Driver startup and subsequent job execution.


<span id="6335d02c"></span>
## Procedure

<span id="740d3f3b"></span>
### Configure external HMS


1. Log in to the [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default), click the queue name, and enter the queue details page.

2. Click **Compute group \> default** in the left navigation bar in sequence to enter the compute group details page.

3. On the **Metadata and network connection** tab, click **Change configuration**. Configuration instructions are as follows:



|Parameter name |Description |
|---|---|
|Metadata |Select external HMS |
|VPC |This parameter must be consistent with the EMR on ECS cluster network configuration. |
|Availability zone C subnet |This parameter must be consistent with the EMR on ECS cluster network configuration. |
|Security group |This parameter must be consistent with the EMR on ECS cluster network configuration. |
|HMS connection |thrift://:9083 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to configure multiple HMS addresses to ensure high availability. Separate addresses with a comma (',').</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26c700ab232e4179ada4f15f6852a102~tplv-goo7wpa0wc-image.image) </span>


4. After configuration is complete, click **Save**. You can click **Test connection** in the lower right corner to check whether the connection is successful.


<span id="c2bc96c4"></span>
### Kerberos authentication parameter configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Parameter configuration must be consistent with the configuration of the <code>krb5.conf</code> file in Kerberos within the EMR on ECS cluster.</div>


On the **Queue details** \> **Kerberos authentication configuration** page, fill in the contents of the krb5.conf file and Save.


1. Log in to the primary node, use the `vim /etc/krb5.conf` command to view the `krb5.conf` file, and copy the file contents into the **Kerberos authentication configuration** box.

2. Modify the KDC server domain name in the file to the internal IP address of the EMR on ECS cluster primary node. After completion, click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5fc26e76f2a49fcad95e280c0243b51~tplv-goo7wpa0wc-image.image) </span>

**Example**

```YAML
    [libdefaults]
        default_realm = xxxxxxxxxxxxxxxxxx.EMR.COM
        udp_preference_limit = 4096
        ticket_lifetime = 24h
        renew_lifetime = 7d
        forwardable = true
        rdns = false
        dns_lookup_realm = false
        dns_lookup_kdc = false
        kdc_timeout = 3s
        max_retries = 2

    [realms]
        xxxxxxxxxxxxxxxxxx.EMR.COM = {
            kdc = 192.168.1.36:88
            kdc = 192.168.1.36:88
            admin_server = 192.168.1.36:749
        }

     [domain_realm]
      .xxxxxxxxxxxxxxxxxx.EMR.COM = xxxxxxxxxxxxxxxxxx.EMR.COM
      xxxxxxxxxxxxxxxxxx.EMR.COM = xxxxxxxxxxxxxxxxxx.EMR.COM
```


<span id="0f14300a"></span>
### Submit Spark tasks

<span id="82ec7e15"></span>
#### SparkSQL

<span id="8fd2fd73"></span>
##### Read table

Example

```SQL
set spark.kerberos.principal=<user>@<REALM>;-- 指定访问kerberos使用的principal，格式必须为 <username>@<REALM>
set serverless.spark.kerberos.keytab.path=tos://bucketname/<user>.keytab;-- 对应用户的keytab文件的TOS路径，需提前生成keytab文件并上传到账号的TOS下
-- 只打开 spark driver 的跨vpc访问，避免大任务消耗大量的子网ip
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
set tqs.query.engine.type = sparkcli;-- sparksql添加，sparkjar不需要
set spark.hive.metastore.sasl.enabled=true;
set spark.hive.metastore.kerberos.principal=hive/_HOST@<REALM>;-- 格式为 hive/_HOST@<REALM>，前面部分无需修改，替换自身 kerberos 集群的<REALM>即可

show tables; --查看当前数据库下的所有表
show create table xxx;--查看指定表
select * from xxx limit 10;--查询指定表的前10条数据
```


<span id="d64234dd"></span>
##### Write table

Example

```SQL
-- 定义 Spark SQL 的默认数据仓库目录TOS路径，用于存储托管表（Managed Tables）的数据文件
set spark.sql.warehouse.dir=tos://bucketname/managed;
-- 上述必须添加的参数
set spark.kerberos.principal=<user>@<REALM>;-- 指定访问kerberos使用的principal，格式必须为 <username>@<REALM>
set serverless.spark.kerberos.keytab.path=tos://bucketname/<user>.keytab;-- 对应用户的keytab文件的TOS路径，需要提前上传到账号的TOS下
-- 只打开 spark driver 的跨vpc访问，避免大任务消耗大量的子网ip
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
set tqs.query.engine.type = sparkcli;-- sparksql添加，sparkjar不需要
set spark.hive.metastore.sasl.enabled=true;
set spark.hive.metastore.kerberos.principal=hive/_HOST@<REALM>;-- 格式为 hive/_HOST@<REALM>，前面部分无需修改，替换自身 kerberos 集群的<REALM>即可

create table if not exists serverless.employees_serverless as select * from employees;--创建托管表（若不存在），并从源表（employees）插入数据
```


<span id="33efb5c3"></span>
##### Read external catalog and write table

```SQL
-- 定义 Spark SQL 的默认数据仓库目录TOS路径，用于存储托管表（Managed Tables）的数据文件
set spark.sql.warehouse.dir=tos://bucketname/managed;
-- 上述必须添加的参数
set spark.kerberos.principal=<user>@<REALM>;
set serverless.spark.kerberos.keytab.path=tos://bucketname/<user>.keytab;
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
set tqs.query.engine.type = sparkcli;
set spark.hive.metastore.sasl.enabled=true;
set spark.hive.metastore.kerberos.principal=hive/_HOST@<REALM>;

-- paimon catalog
set spark.sql.catalog.paimon_catalog=org.apache.paimon.spark.SparkCatalog;
set spark.sql.catalog.paimon_catalog.warehouse=tos://paimon-emr-test/user/paimon/warehouse/;
set spark.sql.storeAssignmentPolicy=ansi;

create table serverless.test as select * from paimon_catalog.paimon_db.veh_2k where dt = '20251117';
```


<span id="86bbc7e8"></span>
#### SparkJar

Refer to SparkJar task submission Note, and fill in the Kerberos\-related configuration in the Spark Conf parameters to enable normal access.
