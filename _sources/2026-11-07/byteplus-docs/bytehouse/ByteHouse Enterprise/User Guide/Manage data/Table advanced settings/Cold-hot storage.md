---
title: "Cold-hot storage"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cold-hot-storage"
---

ByteHouse supports hot and cold storage to reduce storage costs.

<span id="f213a428"></span>
# Basic concepts


* Hot data: frequently accessed data stored in hot disk storage (i.e., PLX cloud disk chosen at cluster creation) to meet high performance access needs.

* Cold data: infrequently accessed data stored in cheaper cold storage options to satisfy cost\-effective storage needs.


In ByteHouse, hot data uses SSD disks, which are costlier; whereas cold data, less frequently accessed, may use cheaper, lower performance storage media, specifically differing as follows:


|Data type |Storage method |Creation method |Billing method |
|---|---|---|---|
|Hot data |Local storage |When creating a cluster, choose storage space with SSD cloud disk as the medium layer. |Annual and monthly billing |
|Cold data |Cold storage |Requires additional activation, with object storage ToS as the underlying medium. |Post\-payment |


<span id="4c04b651"></span>
# Hot and cold storage strategy

According to the scenes, three cold and hot data movement strategies are supported.


* **TTL tiered storage**: Add a TTL statement to automatically transfer all data before the interval to the cold storage disk (requires that the storage strategy is activated in the cluster).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e7429c4372a450491362bd2d2e769d9~tplv-goo7wpa0wc-image.image) </span>

* **Move factor strategy**: Store newly written data in local storage as hot data, providing efficient queries. When the amount of hot data storage reaches the business usage threshold (i.e., the move factor), automatically prioritize moving the large part data to cold storage to free up local storage space. A storage strategy (Storage Policy) needs to be activated in the system file, and this setting must be added when creating a table.

   1. `s3_cold` strategy: By default, it is used for MergeTree family tables other than the HaUniqueMergeTree table. This strategy follows the cluster’s move factor strategy and can also be effective if the user sets TTL to eliminate to cold storage;

   2. `s3_cold_for_unique_table` strategy: Used for HaUniqueMergeTree tables, this strategy does not follow the cluster’s move factor strategy (i.e., it cannot move even if the cluster's capacity is at 100%), but it can still be effective if the user sets TTL to eliminate to cold storage;

* **Manually move partitions**: Move specified partitions to local storage or cold storage.


<span id="dc232f62"></span>
# Usage limitations

Cold storage uses object storage services, which can significantly reduce costs, but its performance is much lower than local storage.

**Please follow the use scenario to determine if cold storage is needed.** 


1. Currently, cold storage only supports HaMergeTree or HaUniuqeMergeTree table engines.

2. Using TTL for tiered storage requires that the partition is a `datetime` type (including `toDate()`, `toMonth()`).

3. When using MaterializeMySQL, it is not supported to select a TTL policy to dump to cold storage, only the movement factor strategy is supported.

4. Using cold storage will significantly reduce efficiency in the following scenarios:

   * Data reading;

   * Partition merging;

   * Master\-slave synchronization.

5. Small tables are not recommended for cold storage, as cold storage queries perform about ten times worse than hot storage queries. It is advisable to consider moving historical partition data to cold storage after the data volume of the table increases.

6. Tables that frequently backtrack historical partition data are not recommended for cold storage (like: toC.ods_chatglm_server_log_local) to avoid data duplication or impact on write\-query performance.

7. When initially creating a table, it is not necessary to specify a cold storage TTL; subsequently, by inspecting the volume of data in various business tables, scenarios suitable for activating cold storage in large tables can be identified.


Incorporating the above restrictions, the best practices for using cold storage are as follows:


* Preferably use cold storage in single\-replica mode, as synchronization between replicas in multi\-replica mode significantly increases time consumption.

* Since data in cold storage merges slowly and does not deduplicate, currently it only supports automatic transference after data cools down, scenarios of directly importing data to cold storage (such as setting data before 2022\-01\-01 to be transferred to cold storage and then directly inserting data of 2021\-12\-01) are not recommended. If there is a need to import a large volume of data with the expectation of certain data directly entering cold storage, please submit a ticket.


<span id="7add5fcc"></span>
# Billing

<span id="df6d9088"></span>
## Billing method

Hot storage and cold storage are billed separately, generating different orders.


1. Hot storage billing: Hot storage space is created upon new cluster creation, prepaid through annual or monthly packages, refer to [Billing introduction](https://docs.byteplus.com/docs/bytehouse/billing-method#%E8%AE%A1%E8%B4%B9%E4%BB%8B%E7%BB%8D).

2. Cold storage billing: After a cluster has activated cold storage, billing starts on an hourly basis according to the storage usage, categorized as a post\-paid resource. Billing prices will be prompted when activating the "Hot and Cold Storage" function, as shown in the figure (the specific price is subject to the actual display of the product interface). For more details, please refer to [Cold storage billing](https://docs.byteplus.com/docs/bytehouse/billing-method#483941f4).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9852bca3ec5448c9b5936172866dad2~tplv-goo7wpa0wc-image.image) </span>


<span id="2a812153"></span>
## Payment arrears explanation

Hot storage is prepaid. If you wish to discontinue the renewal, please refer to [Unsubscribe description](https://docs.byteplus.com/docs/bytehouse/billing-method#5cf260c6).

For cold storage, billing occurs daily, and deductions are made in real\-time once the invoice is issued. If there are any arrears, please refer to [Handling overdue payments](https://docs.byteplus.com/docs/bytehouse/billing-method#0bcba7f4).

<span id="dbaa04b7"></span>
# Usage guide

<span id="14eed730"></span>
## Activate "hot and cold tiered storage"

Ways to enable cold storage for clusters include:


* Activate when creating a cluster

* Activate for an existing cluster


<span id="9f54ce46"></span>
### Activate when creating a cluster

Permission Requirements: BytePlus's BillFullAccess permission (see [Policy Management](https://console.byteplus.com/iam/policymanage/?scope=All));

Activation Steps:


1. Access the ByteHouse Console, click **Create cluster.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c43fbb90ac694f249f14943d0db31d05~tplv-goo7wpa0wc-image.image) </span>

2. Select the billing type, computing resource specifications, replica mode, etc., according to individual needs.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use cold storage in single copy mode, as synchronization between copies will significantly increase the time in multiple copy scenarios.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/483d922f6adb4100b2d9795668bdb873~tplv-goo7wpa0wc-image.image" width="310px" />   </div>
   

3. You can select the "cold\-hot storage" after choosing the size of local data, and fill in the threshold for migration to cold storage.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can choose the "Local Storage Cap" strategy:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When local storage reaches the cap, it will affect functions such as data insertion. It is suggested to set the maximum storage value according to business assessment, as moving cold storage will affect part of IO performance.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After activating the "Local Storage Cap" function, a capacity cap needs to be set. The default value is 90%, and a customizable range is the integers from [1,99].   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbe6b7cbebbf403a8137eafc4f4c6363~tplv-goo7wpa0wc-image.image) </span>

4. Complete the configurations for other Cluster settings and finish creating the cluster.

5. Refer to steps in [Activate when creating a cluster](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage#9f54ce46), and correctly configure when creating a new table to enable cold storage.


<span id="f545e851"></span>
### Existing cluster activation

Permission Requirements: Cluster Administrator, or system Administrator;

Activation Steps:


1. Navigate to Cluster & Operations Management \-\> Manage Clusters \-\> Cluster List \-\> Cluster Details \-\> Storage Management.

2. Select "Activate", and choose a hot\-cold data migration strategy.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9a2a66f6da24aa686810af171b893be~tplv-goo7wpa0wc-image.image" width="2376px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9852bca3ec5448c9b5936172866dad2~tplv-goo7wpa0wc-image.image) </span>

3. (Optional) Users may choose the "Local Storage Limit" strategy at this point.

   1. When local storage reaches its capacity limit, it will affect functions such as data insertion. It is advisable to set the maximum storage capacity based on business assessment, as moving to cold storage may affect some IO performance.

   2. After enabling the "Local Storage Limit" feature, set the capacity limit. The default value is 90%, and the customizable range is an integer from [1,99].

4. Once confirmed, the activation of cold storage is complete.

5. For newly created tables, refer to steps in [Activate when creating a cluster](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage#9f54ce46) to correctly configure the cold storage option when creating a new data table; for existing tables, changing the storage strategy will not immediately take effect. It is recommended to refer to steps in [Move partition](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage#883d4d6e) for manual handling of existing data.


<span id="76d973e2"></span>
## Specify the storage strategy when creating a table

After the cluster has activated cold storage, it is necessary to specify the storage strategy when creating a table so that the data in the table will be moved according to the strategy configured at the time of activation.

<span id="a49eff51"></span>
### Create tables using SQL statements.

Permission required: User with Create permission for the database.

<span id="cf125576"></span>
#### Moving factor configuration

After enabling cold storage and configuring the cold\-hot data shifting rules, the system will automatically add a `s3_cold`/`s3_cold_for_unique_table` storage strategy. When creating a table, specify this storage strategy in settings. Once the table is created, it will shift the data according to the rules configured at the time of activating cold storage. Example:

```SQL
CREATE TABLE example_table on cluster xxxx
(
    d Date,
    a Int
)
ENGINE = HaMergeTree(...)
PARTITION BY d
ORDER BY d
SETTINGS index_granularity = 8192, storage_policy = 's3_cold';
```


If a storage strategy is not specified, the table will still be stored entirely in local storage.

<span id="7c1f233c"></span>
#### TTL strategy configuration

When a storage strategy is configured, multi\-level TTL can be configured.

At time point 1 (as in the example, 2 weeks later), the data will be transferred to cold storage (DISK = 's3').

At time point 2 (as in the example, one month later), the data will be completely deleted.

Example:

```SQL
CREATE TABLE example_table on cluster xxxx
(
    d Date,
    a Int
)
ENGINE = HaMergeTree(...)
PARTITION BY d
ORDER BY d
TTL d + INTERVAL 1 MONTH DELETE,
    d + INTERVAL 2 WEEK TO DISK 's3'
SETTINGS index_granularity = 8192, storage_policy = 's3_cold';
```


If configured this way, multi\-level TTL and mobility factor strategies will take effect simultaneously. Once the data meets the conditions of TTL or the hot and cold mobility factors, it will initiate the movement from hot data to cold data. For more TTL usage instructions, please refer to the document [TTL](https://docs.byteplus.com/docs/bytehouse/ttl).

<span id="59bde393"></span>
#### HaUniqueMergeTree

HaUniqueMergeTree is a proprietary engine of ByteHouse. After activating cold storage, the following points should be noted:


1. Unique tables will not deduplicate data in cold storage during write operations.

2. By default, Unique tables do not perform merge operations on data stored on object storage (i.e., `skip_merge_for_unique_data_in_remote_disk = 1`); if it is necessary to allow merge operations on this data, specify the parameter `skip_merge_for_unique_data_in_remote_disk = 0` when creating the table. Merge performance on cold storage is poor, **please configure cautiously**.


Example:

```SQL
CREATE TABLE example_table on cluster xxxx
(
    d Date,
    a Int
)
ENGINE = HaUniqueMergeTree(...)
PARTITION BY d
ORDER BY d
TTL d + INTERVAL 1 MONTH DELETE,
    d + INTERVAL 2 WEEK TO DISK 's3'
SETTINGS 
    index_granularity = 8192, 
    storage_policy = 's3_cold'
    skip_merge_for_unique_data_in_remote_disk = 1;
```


<span id="c43f4559"></span>
### Visualize table creation

Table creation via visualization automatically generates the SQL without the need to manually specify storage_policy or configuration parameters.

Permission requirements: Data engineers, cluster administrators, or system administrators;

Steps:


1. Go to Data object \-\> Create new table.

2. After completing options for the database, table, and columns, click to expand the "Advanced key".

3. Set the partition key. Note that if you want to enable the TTL function, the partition key should include Date or DateTime type.

4. Set TTL.

   * Move to cold storage: Select Move to Cold Storage, and then set the TTL partition key and date. When the set date is reached, less frequently used data will be moved to cold storage to meet cost\-effective storage needs.

   * Delete data: Select Delete Data, and then set the TTL partition key and date. Unwanted data can be deleted according to the time period, reducing storage costs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The time of cold storage must be less than the deletion.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71eced82055c44c2b0b0474bb2b16409~tplv-goo7wpa0wc-image.image) </span>

5. After setting the remaining parameters, the system will automatically add the corresponding configuration parameters to the generated statements;

6. Click "Create." Then the new table will apply cold storage rules.


<span id="97514f22"></span>
## Change table storage strategy

After activating cold storage, if the storage strategy of the existing tables is not changed, the data within the tables will not move according to the configuration set when cold storage was activated. Therefore, it is necessary to achieve the goal of applying cold storage rules to the data tables by changing the table's storage strategy and TTL settings.

<span id="5b3cba23"></span>
### SQL modification

Description: The storage strategy and TTL of the table can be modified using the Alter command.

Permission required: Users with Alter permission on the table.

SQL Example:

```SQL
ALTER TABLE table_name ON cluster xxxx
MODIFY SETTING storage_policy = 's3_cold'; 
-- Edit the storage policy. Here illustrates how to modify the local table.

ALTER TABLE table_name on cluster cluster_name 
MODIFY TTL toDate(create_date) + toIntervalDay(30) TO DISK 's3';
-- Edit the TTL policy.
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After changing storage strategy / TTL, data will not move immediately; only data inserted afterward will apply the rules. If you wish to adjust existing data, refer to the "Manual Move Partition" section. For more instructions on TTL, refer to <a href="https://docs.byteplus.com/docs/bytehouse/ttl">TTL</a>.</div>


<span id="5c7a9c8b"></span>
### Visualize modification

Edit the storage strategy and TTL settings through the visual interface.

Permission requirements: Data engineer, cluster manager, or system administrator;

Steps:


1. Access Data object \-\> Select the corresponding table \-\> Edit table \-\> Visualization Edit.

2. Change the storage strategy and TTL settings.

3. Confirm and finish editing.


<span id="78a20625"></span>
## View storage usage

Visualize local storage and cold storage usage trends for analysis and decision\-making.

Permission requirements: Cluster manager, system administrator.

Steps:


1. Access Cluster management \> Cluster list \> Cluster details \> Storage & Bandwidth.

2. View chart trends for local storage and cold storage usage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa55eda53c3463f83205c5afed23753~tplv-goo7wpa0wc-image.image) </span>


<span id="883d4d6e"></span>
## Move partition

Use the Alter command to complete the process of moving a partition to cold storage.

Permission requirements: Users with Alter permission on a table.

Basic Syntax

```SQL
ALTER db_name.table_name MOVE PARTITION 'partition_name' TO DISK 's3'
-- Here illustrates how to modify the local table.
```


SQL Example:

```SQL
ALTER TABLE table_name ON cluster xxxx
MODIFY SETTING storage_policy = 's3_cold'; 
-- Before moving, you need to ensure that the storage policy has been set. If it has not been modified, use the above command to change the storage policy. 
-- Note that this illustrates how to modify the local table. If you modify the distributed tables, an error will occur.

SELECT partition FROM system.parts WHERE table = 'table_name' GROUP BY partition
-- Retrive the partition name

ALTER db_name.table_name MOVE PARTITION 'partition_name' TO DISK 's3';
-- Move the partition to the cold storage
```


<span id="29babde2"></span>
# FAQ

**Q**: When setting up cold storage, the SQL statements for creating, modifying, and moving partitions all involve Local tables. If operations are performed on Distributed tables, errors will occur. For example:

```SQL
Code: 48, e.displayText() = DB::Exception: There was an error on [HOST:PORT]: Code: 48, e.displayText() = DB::Exception
Setting storage_policy cannot be modified SQLSTATE: HY000 (versicon 21.9.1) SQLSTATE: HY000 (version 21.9.1)
```


**A**: Set the storage strategy and TTL on the Local table. If it is a distributed table, you can find its underlying table through the `show create table` statement and then execute the cold storage SQL statement.
