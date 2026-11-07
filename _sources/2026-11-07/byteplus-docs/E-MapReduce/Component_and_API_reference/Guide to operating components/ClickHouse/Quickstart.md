---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/clickhouse_quickstart"
---

This article introduces the detailed procedure and related configuration for creating a ClickHouse cluster.

<span id="_1-创建集群"></span>
## Step 1: Create a cluster

Cluster creation consists of four steps: software settings \-\-\> hardware settings \-\-\> other settings \-\-\> preview and confirmation.


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the top menu bar, select the region and project space from the dropdown as appropriate.

3. On the overview page, click **Create cluster** to enter the cluster creation page.

4. On the cluster creation page, select the analytics scenario as **Interactive query**, set the cluster type to ClickHouse, and choose the appropriate product version as needed. Supported versions include EMR\-3.0.1, EMR\-3.1.0, and later versions.

5. In the first step of software settings for ClickHouse cluster creation, you can choose whether the service is highly available. For high availability, Zookeeper must have 3 nodes, and ClickHouse data must have 2 replicas.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to use high availability mode in production environments to ensure service stability and prevent data loss. Non\-high availability mode is intended for testing scenarios only.   </div>
   

6. In hardware settings, complete the following instance configuration information.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">VPC, subnet, and other network configurations cannot be changed after the cluster is created. Plan the network carefully.   </div>
   

   
   |Configuration items |Note |
   |---|---|
   |Replica and shard configuration |Configure cluster Replica and Shard settings:<br><br><br>* Replica: The number of replicas in ClickHouse<br><br>* Shard: The number of shards in ClickHouse<br><br><br>Once the values of both are determined, the number of Core nodes can be determined. |
   |Node selection and configuration |Instance node types are divided into Master and Core. The Master node deploys Zookeeper, and the Core node deploys the ClickHouse cluster. You can plan computing resources and disk space based on business requirements and data growth.<br><br><br>* Master instance:<br><br>   * Number of Master nodes: The default is 1 for a standard cluster; the default is 3 for a high\-availability cluster.<br><br>   * You can choose from **compute type and general purpose type** instance types and select the appropriate instance specification as needed. Introduction to cloud server instance specifications [.](https://www.volcengine.com/docs/6396/70840)<br><br>   * System disk: Supports ultra\-fast SSD cloud disk, size can be adjusted as needed, capacity range: 60–2048 GB.<br><br>   * Data disk: Supports ultra\-fast SSD cloud disk, size can be adjusted as needed, capacity range: 60–32768 GB.<br><br>      For details on cloud disk performance, see [Cloud disk specifications](https://www.volcengine.com/docs/6396/101839).<br><br>* Core instance:<br><br>   * Number of Core nodes: Adjust according to the number of Replica and Shard configurations.<br><br>   * You can choose from **compute type, local SSD type, general purpose type, memory type, and big data type** instance types and select the appropriate instance specification as needed. Introduction to cloud server instance specifications [.](https://www.volcengine.com/docs/6396/70840)<br><br>   * System disk: Supports ultra\-fast SSD cloud disk, size can be adjusted as needed, capacity range: 60–2048 GB.<br><br>   * Data disk: Supports ultra\-fast SSD cloud disk, size can be adjusted as needed, capacity range: 60–32768 GB.<br><br>      For details on cloud disk performance, see [Cloud disk specifications](https://www.volcengine.com/docs/6396/101839).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use ultra\-fast SSD or higher disks for Core nodes.   </div><br>    |
   

7. After completing hardware settings, click **Next** to configure other cluster information, including cluster name, machine key or password, and more.

8. Finally, preview the relevant parameters set in previous steps. After confirming they are correct, review and check "**Agree to the terms of service**" and then click **Create now** to submit the cluster creation.


For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-配置修改"></span>
## Step 2: Configuration modification

After the cluster is successfully created, you can directly use the ClickHouse service. To modify ClickHouse\-related configurations, select the ClickHouse cluster you want to manage in the cluster list page, then go to **Cluster details \> Service list \> ClickHouse service \> Service parameters** to view or modify the relevant parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After modifying parameters, you need to Save and restart the corresponding component.</div>


<span id="_3-查询数据"></span>
## Step 3: Query data

After the ClickHouse service is started, you can use the ClickHouse client to connect to the cluster and perform operations such as creating databases, tables, inserting, and querying data.

The following is a sample SQL operation.


1. Log in to the Core instance node of the ClickHouse cluster. You can use [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404) or ECS remote login. The example below uses remote login:

   1. Click **Cluster list \> Service list \> ClickHouse \> Deployment topology** tab to enter the deployment topology of the ClickHouse component service.

   2. Click the ECS ID under the component name (emr\-core\-1 host name) to navigate to the cloud server instance page, and click the **Remote connection** button in the upper right corner.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f39c96a2262b9d1e9f467dc067d8afb6.png) </span>

   3. Select a remote connection method (ECS Terminal is recommended), enter the cluster authentication information, and log in to the command\-line environment of the Core instance node of the ClickHouse cluster to execute relevant command\-line operations.

2. Use the ClickHouse client to connect to the current node of ClickHouse:


```bash
-- 切换到 ClickHouse 目录
cd /usr/lib/emr/current/clickhouse/
-- 执行客户端命令，连接 ClickHouse 集群
./clickhouse-client
```



3. Create a database after logging in:


```sql
CREATE DATABASE IF NOT EXISTS helloworld ON CLUSTER  cluster_emr;
```



4. Create a table under the db:


```sql
-- Create a local data table
CREATE TABLE helloworld.my_first_table ON CLUSTER  cluster_emr
(
    user_id UInt32,
    message String,
    timestamp DateTime,
    metric Float32
)
ENGINE = MergeTree()
PRIMARY KEY (user_id, timestamp);

-- Create a distributed table
CREATE TABLE IF NOT EXISTS helloworld.my_first_table_dist ON CLUSTER  cluster_emr 
(
    user_id UInt32,
    message String,
    timestamp DateTime,
    metric Float32
) ENGINE = Distributed(cluster_emr, helloworld, my_first_table, rand());
```



5. Insert data


```sql
INSERT INTO helloworld.my_first_table_dist (user_id, message, timestamp, metric) VALUES
    (101, 'Hello, ClickHouse!',                                 now(),       -1.0    ),
    (102, 'Insert a lot of rows per batch',                     yesterday(), 1.41421 ),
    (102, 'Sort your data based on your commonly-used queries', today(),     2.718   ),
    (101, 'Granules are the smallest chunks of data read',      now() + 5,   3.14159 )
```



6. Query data:


```sql
select * from helloworld.my_first_table_dist;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6355d5da3b3e60a5f3dd4358723bb0a.png) </span>
