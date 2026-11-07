---
title: "Serverless Spark access Kerberos cluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/access_Kerberos_cluster"
---

Serverless Spark access to Kerberos cluster refers to securely accessing clusters protected by Kerberos authentication in a serverless Spark environment. This addresses the need to access secure clusters in serverless scenarios and is suitable for scenarios such as handling Kerberos\-authenticated HDFS or Hive data. This article will guide you through the configuration and usage steps.

<span id="ba36a261"></span>
# Prerequisites


* An EMR on ECS cluster has been created, and **Kerberos authentication** has been enabled. For detailed instructions, refer to: [Use a Kerberos-authenticated cluster](https://docs.byteplus.com/docs/E-MapReduce/Use_a_Kerberos-authenticated_cluster).

* An exclusive EMR Serverless queue has been created, and you have permission to operate this queue.

* [Object Storage TOS](https://console.byteplus.com/tos) has been enabled.


<span id="58a67b40"></span>
# Limits


1. Access to the Kerberos cluster is only supported under the default compute group of the exclusive queue.

2. The system only supports Serverless Spark accessing storage\-compute separated Kerberos clusters, and does not support Spark Streaming job access.

3. A single Serverless queue only supports access to one Kerberos cluster.

4. In Spark jobs accessing Kerberos\-authenticated clusters, the **Driver cannot use the queue's elastic resources**; only the **Executor can schedule elastic resources normally**. Ensure that there are available fixed resources under the default compute group to support Driver startup and subsequent job execution, as the Driver is a prerequisite for job startup (it must occupy resources to complete initialization first).


<span id="35b19acf"></span>
# Configure external HMS

<span id="637e117a"></span>
## Configure external HMS


1. Log in to [EMR Serverless Console](https://console.byteplus.com/emr/serverless/queue_manage?projectName=default), click the queue name, and enter the queue details page.

2. Click **Compute Group \> default** in the left navigation bar in sequence to enter the compute group details page.

3. On the **Metadata and Network Connection** tab, click **Change Configuration**. Refer to the following for configuration instructions:



|Parameter name |Description |
|---|---|
|Metadata |Select external HMS |
|VPC |This parameter must be consistent with the network configuration of the EMR on ECS cluster. |
|Availability Zone C subnet |This parameter must be consistent with the network configuration of the EMR on ECS cluster. |
|Security group |This parameter must be consistent with the network configuration of the EMR on ECS cluster. |
|HMS connection |thrift://:9083<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, HMS connections only support domain name mode. The DNS query method for nodes is as follows:</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/334060ca0db54f75a0fb137e0211ef01~tplv-goo7wpa0wc-image.image" /></div><br> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to configure multiple HMS addresses to ensure high availability. Separate addresses with a comma (',').</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26c700ab232e4179ada4f15f6852a102~tplv-goo7wpa0wc-image.image) </span>


4. After configuration is complete, click **Save**. You can click **Test Connection** in the lower right corner to check whether the connection is successful.


<span id="2e6819c8"></span>
## Kerberos authentication parameter configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Parameter configuration must be consistent with the <code>krb5.conf</code> file configuration in Kerberos in the EMR on ECS cluster.</div>


Use the `vim /etc/krb5.conf` command on [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_log_in_to_the_cluster) to view the `krb5.conf` file. Copy its content to the configuration box on the **Queue Details** \> **Kerberos Authentication Configuration** page.

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
            admin_server = master-1-1.*****
        }

     [domain_realm]
      .xxxxxxxxxxxxxxxxxx.EMR.COM = xxxxxxxxxxxxxxxxxx.EMR.COM
      xxxxxxxxxxxxxxxxxx.EMR.COM = xxxxxxxxxxxxxxxxxx.EMR.COM
```


<span id="7a62d93e"></span>
# Submit job

<span id="28e1a8de"></span>
## Scenario 1: Submit Spark task

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When there is no need to access the external HMS during task execution, add the following configuration to disable HMS access.</div>


<div data-tips="true" data-tips-type="tip">```SQL
-- Disable external metadata access and cross-VPC access
set emr.serverless.external.catalog=false;
set las.cross.vpc.access.enabled=false;
```
</div>


<span id="8faa4842"></span>
### SparkSQL

To access Kerberos, specify the following parameters:

```SQL
-- Specify the principal used for Kerberos access. The format must be <username>@<REALM>
set spark.kerberos.principal=username@A873A71EE5D115874738.EMR.COM;
-- The TOS path of the keytab file for the corresponding user. You need to upload it in advance to your account's TOS.
set serverless.spark.kerberos.keytab.path=tos://nyc-fns/xxxxx.keytab;
-- Add for sparksql; not required for sparkjar
set tqs.query.engine.type = sparkcli;
-- Enable Kerberos authentication for HMS
set spark.hive.metastore.sasl.enabled=true;
-- The format is hive/_HOST@<REALM>. The first part does not need to be modified; just replace <REALM> with your own Kerberos cluster's <REALM>
set spark.hive.metastore.kerberos.principal=hive/_HOST@A873A71EE5D115874738.EMR.COM; 
-- Only enable cross-VPC access for the spark driver to avoid large jobs consuming a large number of subnet IP addresses
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
```


<span id="cf36bf5a"></span>
#### Read table

Example

```SQL
set spark.kerberos.principal=<user>@<REALM>;-- Specify the principal used for Kerberos access; the format must be <username>@<REALM>
set serverless.spark.kerberos.keytab.path=tos://bucketname/<user>.keytab;-- The TOS path of the keytab file for the corresponding user. You need to generate the keytab file in advance and upload it to your account's TOS.
-- Only enable cross-VPC access for the Spark driver to avoid large tasks consuming a significant number of subnet IPs
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
set tqs.query.engine.type = sparkcli;-- Add to sparksql; not required for sparkjar
set spark.hive.metastore.sasl.enabled=true;
set spark.hive.metastore.kerberos.principal=hive/_HOST@<REALM>;-- The format is hive/_HOST@<REALM>; the preceding part does not need to be modified, just replace <REALM> with your own Kerberos cluster's <REALM>

show tables; -- View all tables in the current database
show create table xxx;-- View the specified table
select * from xxx limit 10;-- Query the first 10 records of the specified table
```


<span id="242e2f29"></span>
#### Write table

Example

```SQL
-- Define the default data warehouse directory TOS path for Spark SQL, used to store data files for managed tables (Managed Tables)
set spark.sql.warehouse.dir=tos://bucketname/managed;
-- Parameters that must be added as described above
set spark.kerberos.principal=<user>@<REALM>;-- Specify the principal used for Kerberos access; the format must be <username>@<REALM>
set serverless.spark.kerberos.keytab.path=tos://bucketname/<user>.keytab;-- The TOS path of the corresponding user's keytab file, which must be uploaded in advance to the account's TOS
-- Only enable cross-VPC access for the Spark driver to avoid large tasks consuming a significant number of subnet IPs
set serverless.cross.vpc.driver.only.enabled = true;
set serverless.cross.vpc.dns.resolve.enabled = true;
set tqs.query.engine.type = sparkcli;-- Add to sparksql; not required for sparkjar
set spark.hive.metastore.sasl.enabled=true;
set spark.hive.metastore.kerberos.principal=hive/_HOST@<REALM>;-- The format is hive/_HOST@<REALM>; the preceding part does not need to be modified, just replace <REALM> with your own Kerberos cluster's <REALM>

create table if not exists serverless.employees_serverless as select * from employees;-- Create a managed table (if it does not exist) and insert data from the source table (employees)
```


<span id="32f0c27f"></span>
#### Read external Catalog and write table

```SQL
-- Define the default data warehouse directory TOS path for Spark SQL, used to store data files for managed tables (Managed Tables)
set spark.sql.warehouse.dir=tos://bucketname/managed;
-- Parameters that must be added as described above
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


<span id="5b0e2871"></span>
### SparkJar

Refer to [SparkJar job](https://docs.byteplus.com/docs/E-MapReduce/SparkJar_jobs), and fill in the Kerberos\-related configuration in the Spark parameters (Spark Conf) to enable access.

<span id="5070eda5"></span>
## Scenario 2: Connect to Kyuubi Gateway to submit job

<span id="cd6a7cdf"></span>
### Create keytab file


1. On the machine in the cluster where Kerberos is located, execute the following command to enter the Kerberos admin.local tool.

   ```Plain
   kadmin.local
   ```
   

2. Create principal. The format of the principal is `kyuubi/<fqdn>@<REALM>`. Here, the `<fqdn>` domain name can be customized.

   ```Plain
   addprinc -randkey kyuubi/serverless-spark-jdbc.emr.cn-beijing.volces.com@E159E9BE5E120****.EMR.COM
   ```
   

3. Export the keytab file.

   ```Plain
   xst -k /etc/krb5/keytab/serv/kyuubi.keytab kyuubi/serverless-spark-jdbc.emr.cn-beijing.volces.com@E159E9BE5E120****.EMR.COM
   ```
   

4. Upload the exported keytab file to TOS.

   ```Plain
    hdfs dfs -put /etc/krb5/keytab/serv/kyuubi.keytab tos://emr-autotest/azmn/kyuubi/
   ```
   


<span id="0b7a5ce4"></span>
### Create Gateway and configure Kerberos\-related parameters

For general instructions on creating and connecting Gateway, see [Create and manage Kyuubi Gateway](https://docs.byteplus.com/docs/undefined/6a69df3d2d357f0506fa932e). The following introduces the key configuration parameters for enabling Kerberos.


1. Select external HMS for metadata.

2. Configure the Kerberos\-related parameters in the Engine Configuration of Gateway.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea54f567cf9449f39738ed45ba207e00~tplv-goo7wpa0wc-image.image) </span>

   The configuration example is as follows.

   ```JSON
   kyuubi.authentication=KERBEROS,custom
   kyuubi.kinit.principal=kyuubi/serverless-spark-jdbc.emr.cn-beijing.volces.com@E159E9BE5E120CAC4ECA.EMR.COM
   kyuubi.kinit.keytab=tos://emr-autotest/azmn/kyuubi/kyuubi.keytab
   hadoop.security.authentication=kerberos
   hive.metastore.sasl.enabled=true
   hive.metastore.kerberos.principal=hive/_HOST@E159E9BE5E120CAC4ECA.EMR.COM
   ```
   

   You need to modify the following parameters according to your situation. Keep the other parameters consistent with the example values.

   
   |Parameter |Note |
   |---|---|
   |`kyuubi.kinit.principal` |Specify the principal used by Kyuubi Gateway for Kerberos authentication. The format is `<user>/<host>@<realm>`, and it must be configured as the principal created in the above 'Create keytab file' step. |
   |`kyuubi.kinit.keytab` |The TOS path where the keytab file is uploaded. |
   |`hive.metastore.kerberos.principal` |The principal corresponding to HMS in the Kerberos environment. |
   


<span id="c00430ec"></span>
### Connect to Kyuubi and submit job

The following uses Beeline to connect to Kyuubi as an example.


1. Run the kinit command to initialize.

2. Connect to Kyuubi and submit job.

   ```Bash
   beeline -u "jdbc:hive2://192.168.**.1**:10009/;principal=kyuubi/serverless-spark-jdbc.emr.cn-beijing.volces.com@E159E9BE5E120CAC4ECA.EMR.COM?kyuubi.session.iam.credential.ak=AKLTNGExZjEyMWVlMGQ2NDllOGI2ZDE4M2Y5****;kyuubi.session.iam.credential.sk=TVRWaE5UUXlZVFZoWVdZNU5ESm1NV0U1TURZME9EUTFOalk1Tl****;queue_name=doctest;kyuubi.engine.share.level=connection"
   ```
   

   Details:

   
   |Parameter |Note |
   |---|---|
   |`-u` |Must be configured as the Endpoint (including port number) of the Kyuubi Gateway service. You can obtain the Endpoint information on the details page of the corresponding Gateway. |
   |`principal` |Specify the principal used by Kyuubi Gateway for Kerberos authentication. The format is `<user>/<host>@<realm>`, and it must be configured as the principal created in the above 'Create keytab file' step. |
   |`kyuubi.session.iam.credential.ak`、`kyuubi.session.iam.credential.sk` |Volcano Engine IAM account AK and SK information used for authentication. |
   |`queue_name` |The name of the queue or compute group resource where the job runs. |
   

   After connecting to Kyuubi, you can Submit Job.
