---
title: "StarRocks Multi-Warehouse best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_Multi-Warehouse_best_practices"
---

<span id="e26e97ba"></span>
## Multi\-Warehouse overview

In a storage\-compute separated cluster, a Warehouse is a group of compute nodes (CN) that provides the computing resources (CPU, memory, and temporary storage) required to execute queries, imports, and data processing tasks. Each Warehouse acts as an independent pool of computing resources, enabling physical isolation of compute resources.

In a storage\-compute separated cluster, data is shared across multiple Warehouses, but different Warehouses maintain physical isolation of compute and memory resources. Therefore, you can create multiple Warehouses for different business requirements, such as Ad hoc Query Warehouse, ETL Warehouse, and Compaction Warehouse, and easily assign specific tasks to their respective Warehouses.

<span id="4dfec127"></span>
### Advantages


* **Resource isolation**


Multi\-Warehouse allows more granular scheduling of compute nodes. You can assign different tasks to different Warehouses, ensuring physical isolation of compute resources.


* **Data sharing**


Multiple Warehouses can share the same data storage, and authorized users can seamlessly access cluster data through any Warehouse.


* **Vertical scalability**


Multi\-Warehouse allows you to group compute nodes as needed, providing greater flexibility to handle workload fluctuations. You can dynamically start or stop Warehouses, or scale by adding or removing stateless compute nodes.


* **Horizontal scalability**


You can easily create new Warehouses to meet the needs of new business scenarios without affecting existing Warehouses. Because data does not need to be redistributed, tasks on existing Warehouses are not affected by new Warehouses. You can build a centralized large cluster to support multiple concurrent services, thereby avoiding the complexity and increased costs associated with maintaining multiple independent clusters.

<span id="bcfc0490"></span>
### Use cases


* **Diverse business workloads**


You can assign different types of workloads to different Warehouses to physically isolate compute resources. For example, you can allocate one Warehouse for query analysis and another for ETL processing, optimizing resource utilization for each Warehouse.


* **Centralized large cluster**


Database administrators can maintain a shared large cluster and create separate Warehouses for each business unit, effectively reducing the need to establish numerous small StarRocks clusters and thereby lowering maintenance overhead.


* **Separation of background tasks**


You can isolate and execute background tasks, such as Compaction tasks, within dedicated Warehouses to prevent interference with normal business operations. You can also adjust Warehouse resources as needed to balance cost and performance.

<span id="f7127609"></span>
### best practices


* **Online\-offline hybrid analytics**


Multi\-Warehouse provides excellent resource isolation and data sharing capabilities for businesses that combine online and offline operations. By storing data from multiple business lines in a unified manner, you reduce storage costs and simplify cluster management.


* **Ad hoc Query**


You can flexibly scale Warehouses up or down based on the requirements of Ad hoc Query requests.


* **Offline tasks**


When offline tasks have strict time requirements, you can quickly allocate resources to ensure urgent tasks are completed within the required timeframe.

<span id="41cbc531"></span>
## Create instances

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2a1c30ce39a432fa18c6edc052bae4e~tplv-goo7wpa0wc-image.image) </span>

When creating multi\-warehouse instances, you need to select **instance type** and choose **multi\-warehouse edition (storage\-compute separation)** .

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Unlike other types of instances, multi\-Warehouse instances allow separate selection of billing cycles for FE and compute Warehouses. It is recommended to use FE with Subscription billing, and configure the payment method for compute Warehouses according to your needs.</div>


* <div data-tips="true" data-tips-type="tip">You can use a compute Warehouse with Subscription billing to execute the cluster's permanent jobs, and use Pay\-As\-You\-Go Warehouses to handle burst queries.</div>


* <div data-tips="true" data-tips-type="tip">On the creation page, you must create a Default Warehouse as the cluster's default Warehouse. Other Warehouses need to be created from the console page.</div>



All queries that do not specify a warehouse will be routed to default_Warehouse. At the same time, default_Warehouse also executes certain instance background tasks, including:


* Compaction

* SUBMIT TASK

* Pipe

* Statistics collection

* Dynamic partition creation and deletion

* Schema Change

* AutoVacuum (that is, garbage file recycling performed after Compaction)

* Garbage Collection (garbage file recycling)

* Statistics report for SHOW DATA

* Asynchronous materialized view refresh

* ANALYZE TABLE


<span id="e574453e"></span>
### Create warehouses

After you create an instance, go to the console and find the option to create a warehouse on the "Compute Warehouse" page. Each warehouse can have different compute and cache sizes. You can also set different billing methods for each warehouse. Pay\-as\-you\-go billing can be converted to Subscription, but Subscription cannot be converted to Pay\-as\-you\-go billing.

Pay\-As\-You\-Go warehouses offer greater flexibility in elasticity (supporting scaling up, scaling down, and time\-based elasticity). During the testing phase, we recommend prioritizing Pay\-As\-You\-Go warehouses. Once your business is stable, you can switch to Subscription warehouses.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f56a78be3c48768f4a7a63c1a36b6f~tplv-goo7wpa0wc-image.image" width="4096px" /></div>


After clicking Create, the system will provision computing resources and create the warehouse. When the warehouse is 'Running', it means the warehouse has been created, and you can Submit Job to this warehouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00604e43a1b74d4c98bf15eaaf8b20af~tplv-goo7wpa0wc-image.image) </span>

<span id="703dcaa1"></span>
### Warehouse start/stop and scaling

For Pay\-As\-You\-Go warehouses, the multi\-warehouse version supports the start/stop functionality for individual warehouses (default_Warehouse does not support start/stop). After stopping, computing resources are no longer billed; only cache resource fees are charged. You can stop the warehouse during periods of low business activity to save costs.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0decf0a77e3843d5a5e76b46bacaeccb~tplv-goo7wpa0wc-image.image" width="4096px" /></div>


On the warehouse page, you can select **Elasticity Settings** to configure warehouse elasticity:


* For Subscription warehouses, **manual elastic scaling** is supported. You can scale the warehouse to the target resources to meet business requirements.

* For Pay\-As\-You\-Go warehouses, **manual elastic scaling** and **time\-based elasticity** are supported. You can flexibly adjust the warehouse size or set elasticity rules to meet business needs.


<span id="3f7469d5"></span>
### Connect to the warehouse

On the **Network Connection** page, you can find the instance's connection information, enable public access, and configure the allowlist.

You need to create a public IP in advance and bind it to the instance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/603449d6244a42d4bf5dca69afb5a0f2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d182e75bd7244a8a2fb211196d43a06~tplv-goo7wpa0wc-image.image) </span>

<span id="0ed9d24b"></span>
## Monitoring

On the monitoring page, we provide commonly used monitoring information for Overview, FE, and warehouse (CN).

Warehouse monitoring can be viewed by warehouse or by node, making it easier to monitor the health status of instances for operations and maintenance.

You can configure instance alerts in the Volcano Engine **Cloud Monitoring** product.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5daa157eaf1b41fcbafe344998f358ff~tplv-goo7wpa0wc-image.image" width="4096px" /></div>


<span id="cc53f4ac"></span>
## User management

StarRocks adopts both role\-based access control (RBAC) and identity\-based access control (IBAC) to manage permissions within the cluster, enabling cluster administrators to easily restrict permissions at different levels of granularity.

In a StarRocks cluster, you can grant permissions to users or roles. A role is a set of permissions that can be granted to users or roles within the cluster as needed. A user or role can be granted one or more roles, and these roles determine their permissions on different objects.

You can manage user and role permissions on the "User Management" page in the console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the StarRocks 3.X permission system update, the roles assigned to users are not active by default. You need to use the SET ROLE command or enable active_all_roles_on_login. You can enable this feature with one click from the banner on the page.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d08d3fd2134e6c862746ec6de9b561~tplv-goo7wpa0wc-image.image" width="4096px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40b5823c0aa146fd9e52e02056b257fb~tplv-goo7wpa0wc-image.image" width="4096px" /></div>


<span id="b836bf4e"></span>
## Use Warehouse to perform common operations such as query and load

If the Warehouse to be used is not explicitly specified in the operation, all operations are executed by default in the built\-in `default_Warehouse`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If there are no nodes in default_Warehouse, background tasks such as compaction, schema change, materialized view (MV), and statistics table creation will fail.</div>


<span id="6e0c7ca7"></span>
### Specify a default Warehouse for a user

You can specify the default Warehouse to be used when a user connects by setting user attributes.

Specify the default Warehouse as `wh1` for user `jack`.

```SQL
ALTER USER 'jack' SET PROPERTIES ("session.Warehouse" = "wh1");
```


<span id="b5dd0a3b"></span>
### Specify a Warehouse for queries

Query only supports specifying the Warehouse to use by setVar or by manually switching the Warehouse in the current session.


* Specify by setVar:


```SQL
select /*+SET_VAR(Warehouse="aaa")*/ * from my_db.my_table;
```



* Manually switch in the current session:


<span id="ed229f7c"></span>
#### **Specify a Warehouse to use**

```SQL
set [session] Warehouse [=] xxx 
```


Among them, `session` and `=` are optional and do not affect the semantics.

<span id="48123b1a"></span>
#### **View the current Warehouse in use**

```SQL
Show variables like "%warehouse%";
```


The specified Warehouse only takes effect in the current session. If not explicitly specified, `default_Warehouse` is used. Asynchronous tasks such as compaction, asynchronous materialized view refresh, and statistics all use `default_Warehouse`. To avoid impacting performance, it is recommended to keep some alive compute nodes in default_Warehouse.

<span id="88b9d746"></span>
#### Execute query or other SQL

Example:

```SQL
select * from my_db.my_table;
```


<span id="94e1a08e"></span>
### Specify a Warehouse for import

<span id="12079b24"></span>
#### **Specify the Warehouse to use for streamLoad**

Add Warehouse information to the header of the HTTP request.

Example:

```Bash
curl --location-trusted -u root: \
    -H "label:test_labe56"  -H "timeout:100" -H "max_filter_ratio:1" \
    -H "Warehouse:xxx" \
    -T example1.csv -XPUT http://xxx/api/test/test11/_stream_load
```


<span id="eef7a884"></span>
#### **Specify a Warehouse for external transaction import**

<span id="b9125f7a"></span>
##### **Start a transaction**

Add Warehouse information to the header of the HTTP request.

Example:

```Bash
curl --location-trusted -u root: \
    -H label:stream_load_trans_e3cd0c18_14c1_11ee_bee7_00163e135cd7 \
    -H db:stream_load_test_db_e3c600ee_14c1_11ee_bee7_00163e135cd7 \
    -H table:duplicate_table_with_null \
    -H Warehouse:xxx \
    -XPOST http://127.0.0.1:38032/api/transaction/begin
```


There is no need to specify the load, prepare, or commit parameters.

<span id="0efd1b59"></span>
#### Specify the Warehouse to use for the Flink connector \*\*\*\*

Add Warehouse information to the parameters.

Flink SQL example:

```Bash
CREATE TABLE `score_board` (
    `id` INT,
    `name` STRING,
    `score` INT,
    PRIMARY KEY (id) NOT ENFORCED
) WITH (
    'connector' = 'starrocks',
    'jdbc-url' = 'jdbc:mysql://127.0.0.1:9030?sessionVariables=Warehouse=xxx',
    'load-url' = '127.0.0.1:8030',
    'sink.properties.Warehouse' = 'wh1',
    'database-name' = 'test',
    'table-name' = 'score_board',
    'username' = 'root',
    'password' = ''
);

INSERT INTO `score_board` VALUES (1, 'starrocks', 100), (2, 'flink', 100);
```


Flink DataStream example:

```SQL
/**
 * Generate CSV-format records. Each record has three values separated by "\t". 
 * These values will be loaded to the columns `id`, `name`, and `score` in the StarRocks table.
 */
String[] records = new String[]{
        "1\tstarrocks-csv\t100",
        "2\tflink-csv\t100"
};
DataStream<String> source = env.fromElements(records);

/**
 * Configure the Flink connector with the required properties.
 * You also need to add properties "sink.properties.format" and "sink.properties.column_separator"
 * to tell the Flink connector the input records are CSV-format, and the column separator is "\t".
 * You can also use other column separators in the CSV-format records,
 * but remember to modify the "sink.properties.column_separator" correspondingly.
 */
StarRocksSinkOptions options = StarRocksSinkOptions.builder()
        .withProperty("jdbc-url", jdbcUrl)
        .withProperty("load-url", loadUrl)
        .withProperty("database-name", "test")
        .withProperty("table-name", "score_board")
        .withProperty("username", "root")
        .withProperty("password", "")
        .withProperty("sink.properties.Warehouse", "wh1")
        .withProperty("sink.properties.format", "csv")
        .withProperty("sink.properties.column_separator", "\t")
        .build();
// Create the sink with the options.
SinkFunction<String> starRockSink = StarRocksSink.sink(options);
source.addSink(starRockSink);
```


In `jdbcUrl`, you need to specify the Warehouse through sessionvariables, as shown below:

```SQL
jdbc:mysql://127.0.0.1:9030?sessionVariables=Warehouse=xxx
```


<span id="6073e5f8"></span>
#### Specify the Warehouse to use for Broker Load

```SQL
LOAD LABEL [<database_name>.]<label_name>
(
    data_desc[, data_desc ...]
)
WITH BROKER
(
    StorageCredentialParams
)
[PROPERTIES
(
    opt_properties
)
]
```


Add the `Warehouse` parameter to opt_properties in the statement for creating the import task. The default value is the Warehouse of the current session.

Example:

```SQL
LOAD LABEL test_broker_load_e2a81a1e_674e_11ee_8013_00163e135cd7.path_extra_fields_e50c557c_674e_11ee_8013_00163e135cd9 
(DATA INFILE( "hdfs://172.26.194.238:9000/starrocks_test_data/system_data/hdfs_data/nose-ut-data/broker_load_data/orc_files/hive_hdfs_test_10827_orc/*")
 INTO TABLE `tbl_sr_10827` FORMAT AS "orc" )  
 WITH BROKER hdfs_broker 
 () 
 PROPERTIES("Warehouse"="aaa");
```


<span id="0516180d"></span>
#### Specify the Warehouse to use for routine load

Add the `Warehouse` parameter to job_properties. The default value is the Warehouse of the current session.

```SQL
CREATE ROUTINE LOAD <database_name>.<job_name> ON <table_name>
[load_properties]
[job_properties]
FROM data_source
[data_source_properties]
```


Example:

```SQL
CREATE ROUTINE LOAD routine_load_basic_types_fe824e00_680a_11ee_81d7_00163e135aa9 
on primary_table_types_load 
COLUMNS (k1,k2,k3,k4,k5,k6,v1,v2,v3,v4,v5,v6,v7,v8), 
COLUMNS TERMINATED BY '\t',where v1 != 0 
PROPERTIES (
    "desired_concurrent_number"="1",
    "max_error_number"="1000",
    "max_batch_interval"="7",
    "Warehouse"="ccc"
) 
FROM KAFKA (
    "kafka_broker_list"="ip:port",
    "kafka_topic"="xxx",
    "kafka_partitions"="0",
    "kafka_offsets"="OFFSET_BEGINNING"
);
```


<span id="f934c50c"></span>
### Specify the Warehouse to use for materialized views

Add the `Warehouse` parameter to PROPERTIES in the create materialized view statement. The default value is the Warehouse of the current session.

```SQL
"Warehouse" = "Warehouse_name"
```


For example, to create a materialized view named order_mv and specify that subsequent rewrite operations run in the Warehouse named `aaa`, use the following statement:

```SQL
CREATE MATERIALIZED VIEW order_mv
DISTRIBUTED BY HASH(`order_id`)
REFRESH ASYNC EVERY (interval 1 MINUTE) 
PROPERTIES ("Warehouse" = "aaa")
AS SELECT 
    order_list.order_id,
    sum(goods.price) as total
FROM order_list INNER JOIN goods ON goods.item_id1 = order_list.item_id2
GROUP BY order_id;
```


After successful execution, you can see the Warehouse information in the `show materialized views where name="order_mv"` command and `show create materialized view order_mv`. The fe.audit.log also records the execution status of materialized view rewrite statements, which includes the Warehouse field.

<span id="b020b986"></span>
### Compaction uses the specified Warehouse.

By default, compaction is executed in `default_Warehouse`. To specify a different Warehouse, modify the configuration item `lake_compaction_Warehouse` *.* 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Both dynamic modification in the session and modification in fe.conf followed by a restart are supported.</div>


For example, to specify a Warehouse named aaa for compaction.


1. Execute `ADMIN SET FRONTEND CONFIG ("lake_compaction_Warehouse" = "aaa");` in the session, or write `lake_compaction_Warehouse *=* aaa;` \*\* in fe.conf and then restart fe.

2. After modification, use `show proc '/compactions'` to view recent compaction records; the last column displays the Warehouse information.


<span id="67ffd0c9"></span>
### JDBC connection specifies Warehouse.

Add the parameter `sessionVariables=warehouse=xxx` to the JDBC connection string, where `xxx` is the specified Warehouse name.

```Plain
jdbc:mysql://127.0.0.1:9030?sessionVariables=warehouse=xxx 
```


<span id="1b83828f"></span>
### Superset connection specifies Warehouse.

Refer to [支持 Superset | StarRocks](https://docs.starrocks.io/zh/docs/integrations/superset_support/) to install starrocks\-sqlalchemy, and use init_command to set the corresponding Warehouse.

```SQL
starrocks://root:@192.168.100.88:9030/test?init_command=set Warehouse = xxx 
```
