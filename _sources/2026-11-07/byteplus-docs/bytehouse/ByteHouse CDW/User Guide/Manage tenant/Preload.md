---
title: "Preload "
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-query-acceleration-preload"
---

This tutorial introduces the usage process and features of the preloading function, as well as the procedures for creating, viewing, editing, and deleting preloading tasks.

<span id="94fea963"></span>
# Introduction

The preload function is a data cache optimization mechanism in the ByteHouse Cloud Data Warehouse (CDW), designed to improve query performance. It proactively preloads data from remote object storage to the local cloud disk of the virtual warehouse. Preloading is divided into three steps:


* **Data prefetch**: Data is preloaded into the cache according to the caching strategy. ByteHouse supports three strategies: offline, real\-time, and once.

   * Offline strategy: ByteHouse periodically refreshes existing data into the cache.

   * Real\-time strategy: ByteHouse will automatically retrieve the latest written data and load it into the cache.

   * Single\-preloading strategy: ByteHouse loads data from the specified date range into the cache.

* **Cache management**: ByteHouse CDW monitors and manages cached data. When cache space is insufficient, some less frequently used data is automatically evicted based on usage and importance, freeing up space for new data that needs to be cached.

   * Offline caching strategy: Data is cached by default according to the TTL (Time To Live) you set when creating a cache loading task. When the size of data within the TTL is greater than the cache space size, the LRU (Least Recently Used) eviction strategy is applied.

   * By default, data use the LRU (Least Recently Used) eviction policy.

* **Query acceleration**: When a user executes an SQL query, the data is already cached on the local cloud disk of the virtual warehouse, allowing for fast and direct data access without retrieving it from object storage. This greatly reduces data read time, improves query performance, and enables query results to be returned to the user more quickly.


<span id="1dad5090"></span>
# Usage process

From the perspective of business scenarios, preloading and local disk ([Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache)) are generally used together to ensure sufficient cache space when loading data into the cache. The overall preloading process is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db3e191b747143f4a919963a0fa00b02~tplv-goo7wpa0wc-image.image) </span>

<span id="39be490b"></span>
# Application scenarios


|**Industry** |**Business scenarios** |**Applicability analysis of scenarios and functions** |
|---|---|---|
|**Internet and e\-commerce** |You need to monitor user behavior, goods sales trends, promotional activity effectiveness, and more in real time, and generate analysis reports in real time. |* **Real\-time data dashboard**: By caching frequently accessed sales data in real time (such as transaction records from the past 30 days), the timeliness of BI report analysis is improved from hourly to second\-level.<br><br>* **TEA Event Analysis**: Pre\-cache user behavior logs (such as click and add\-to\-cart data) to support real\-time path analysis and retention rate calculations, and optimize marketing strategy.<br><br>* **High\-concurrency query during major promotions**: By using real\-time local cache to reduce remote storage access, you can handle the real\-time analysis requirements arising from sudden high loads.<br><br>* **Temporary specialized analysis**: Use a single preloading strategy with a specified date range (such as recent 7\-day activity data, or quarterly data) to load the cache, to avoid repeated reads from remote storage, which improves short\-term high\-frequency review efficiency and supports temporary and non\-periodic analysis needs. |
|**Gaming** |Real\-time processing of gaming logs and player behavioral data to support operation decision\-making and user experience optimization |* **Gaming log real\-time analysis**: Preloading frequently queried player online duration, item use, and other data enables the operation team to quickly respond to abnormal situations, such as cheat detection.<br><br>* **Live interaction analysis**: Preloading live streaming room user interaction data (such as bullet comments and virtual gifts) can accelerate the generation of real\-time popularity rankings.<br><br>* **Advertising performance evaluation**: By caching historical advertising campaign data, you can quickly analyze the ROI of different channels and optimize advertising budget allocation.<br><br>* **Version update effect analysis**: Accurately preloading gaming data for specific time frames (such as the version update window period) can improve effect evaluation efficiency. |
|**Automobile** |Connected vehicle devices, such as sensors, GPS, cameras, and others, generate vehicle status, driving behavior, and environmental information in real time. Rapid processing and analysis of these data support real\-time monitoring, fault diagnosis, and user services. |* **Historical data acceleration**: By using an offline caching strategy, frequently accessed historical data (such as driving behavior data from the Last 30 days) is preloaded to accelerate the generation of driving reports or TEA Event Analysis.<br><br>* **Query acceleration**: When generating driving scores, vehicle health reports, or user behavior analysis, data is read directly from the local cache to reduce latency caused by remote storage access.<br><br>* **New functions validation analysis**: After new functions are launched, data from the first two months of use by initial car owners is centrally analyzed through a single preloading. This validates user acceptance and actual performance of new car functions, assisting automakers in rapidly iterating and optimizing functions. |


<span id="7a526dd1"></span>
# Function description

The ByteHouse preloading task will preload data stored in the database into each virtual warehouse, as shown in the following diagram.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb1080a516fb4d5eac6133d6f4c0bfa6~tplv-goo7wpa0wc-image.image) </span>

Preloading tasks are divided into three modes: real\-time preloading tasks, periodic preloading tasks, and single\-preloading tasks. Contrasts are introduced as follows.


|Contrast items |Real\-time preloading tasks |Periodically preloading tasks |Single\-preloading tasks |
|---|---|---|---|
|Preloading task description |Preload the latest written data to the virtual warehouse cache in real time. Each table only supports real\-time loading to one virtual warehouse. |Data can be loaded into the virtual warehouse cache periodically, and a single table can be loaded into multiple virtual warehouses. |One\-time task. Preload data within the specified date range into the cache of the virtual warehouse. A single table can be loaded into multiple virtual warehouses. |
|Data preloading logic |When data is written to the table, a preloading task is immediately triggered, and the newly written data is immediately loaded into the cache. |It runs every day on a schedule:<br><br><br>* Partition table:<br><br>   * Date\-partitioned table: Refresh incremental data in partitions within the TTL period during each run.<br><br>   * Non\-date type partition tables: The entire table is refreshed on each run.<br><br>* Non\-partitioned table: Refresh the entire table on each run. |It runs only on the specified date:<br><br><br>* Partition table:<br><br>   * Date type partition table: Preload data within the specified date range into cache.<br><br>   * Non\-date\-type partitioned table: Preload all table data each time it runs.<br><br>* Non\-partitioned table: The entire table is refreshed on each run. |


<span id="e0013473"></span>
# Limitations


* The preloading function requires engine version 2.3 or above, and the materialized view preloading function requires engine version 2.3.2 or above. You can view the current engine version in use on the **Tenant management** \> **Basic information** page.

* Materialized view preloading is a Beta feature. To use this feature, please submit a ticket or contact the ByteHouse team to obtain whitelist access.


<span id="ff746dfa"></span>
# Cautions

Preloading tasks will load table data into the cache resources of the virtual warehouse. The virtual warehouse allocates a default amount of cache space for you, and you can also enable the virtual warehouse local disk feature (a value\-added function) to obtain a larger cache space. For details, see [Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache).

<span id="5649cab2"></span>
# Create a preloading mission


1. After logging in to and entering the ByteHouse CDW Console, click the top **Tenant management**. On the **Preload** page, click the **Create Preload Task** in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2b930397a334607a49eee40776200a4~tplv-goo7wpa0wc-image.image) </span>

2. Configure the preloading task on the pop\-up page.

   1. Configure basic information. Configure alert name and description in the interface.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff3b603d74748c69795acb66aef3754~tplv-goo7wpa0wc-image.image) </span>

   2. Configure preload type. Select the task type for preloading and configuring task details.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c6e2e3652444f9a9795ff28a3cfbe32~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Configuration description |
      |---|---|
      |Task type |Currently, three task types are supported: **real\-time preloading, periodic preloading**, and **single** **preloading**.<br><br><br>* **Real\-time preloading**: It preloads the latest written data in real time into the virtual warehouse cache. Each table can only be real\-time loaded into one virtual warehouse.<br><br>* **Periodic preloading**: It preloads data periodically into the virtual warehouse cache. For non\-day\-partitioned tables, the full table data will be preloaded. It supports preloading a single table into multiple virtual warehouses. The periodic loading task also requires further configuration of the following task parameters, such as preload range, preload time, and others.<br><br>* **Single preloading**: It preloads data within the specified date range into the virtual warehouse cache. For non\-day\-partitioned tables, the full table data will be preloaded. It supports preloading a single table into multiple virtual warehouses. The one\-time preloading task still needs to be configured with the date range parameter below. |
      |Preload range |The data loaded by the periodic preloading task consists of tasks from the last N days. |
      |Preload time |Configure the scheduled time for the periodic loading task to run every day. |
      |Timezone |Configure the timezone used for periodic Mission loading. |
      |Load immediately |Select whether to start a loading task immediately after the periodic task is created. |
      |Date range |Configure the date range for a single preloading task. |
      

   3. Configure preloading objects. Select the databases, tables, and materialized views to be preloaded, as well as the virtual warehouse where the preloaded data will be written, from the dropdown menu.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Real\-time preloading tasks only support selecting one virtual warehouse, that is, one table can only be preloaded to a single virtual warehouse.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fc69d3f4bdc4478b2d498aafde67e97~tplv-goo7wpa0wc-image.image) </span>

3. Once configured, click **Create now**.


<span id="158cf16a"></span>
# View preloading tasks

For single preloading and periodic preloading tasks, after a task is created, you can go to the preloading task list page and click **View Executions** to view the specific running status of the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0ac431c9068438c80ded1a552bac192~tplv-goo7wpa0wc-image.image) </span>

On the task status details page, you can view whether each task has run successfully each day. You can also view the preloading duration for each table or partition, partition\-level status, and loading status. For partially successful tasks, ByteHouse displays the success percentage. You can expand the table to view the reasons for loading failures. ByteHouse also supports retrying preloading tasks. You can perform retry operations on daily tasks, with options to retry the entire table or select a single partition to retry.

<span id="1eb587bf"></span>
# Edit preloading tasks

You can also edit the existing preloading tasks in the preloading task list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afb28f8742e54cc08abf3b915d33b09a~tplv-goo7wpa0wc-image.image) </span>


|Cache strategy |Important notes for edit and change |
|---|---|
|Real\-time cache strategy |* When you check or uncheck the tables to be preloaded into cache:<br><br>   * After unchecking the table, its data will no longer be cached in the virtual warehouse. Previously preloaded data will be gradually deleted according to the cache eviction strategy (LRU strategy).<br><br>   * The data of the newly selected tables will subsequently be cached in the virtual warehouse according to the current caching strategy.<br><br>* When switching the virtual warehouse for preloaded data:<br><br>   * After switching the virtual warehouse, subsequent data will be cached in the new virtual warehouse, while preloaded data in the previous virtual warehouse will be gradually deleted according to the cache eviction strategy (LRU strategy). |
|Offline cache strategy |* When you check or uncheck the tables that need to be preloaded to cache:<br><br>   * After you uncheck the table, its data will no longer be preloaded to the virtual warehouse. Any previously cached data from this table will be gradually deleted according to the cache eviction strategy (LRU strategy).<br><br>   * Newly selected tables will subsequently follow the current caching strategy, and their historical data will be periodically loaded into the virtual warehouse.<br><br>* When increasing or decreasing virtual warehouses for preloaded data:<br><br>   * After a new virtual warehouse is added, subsequent data will be preloaded in the new virtual warehouse.<br><br>   * After reducing the number of virtual warehouses, no new data will be preloaded in the virtual warehouses, and historical cached data will be gradually deleted according to the cache eviction strategy (LRU strategy). |
|Single preloading strategy |* When checking or unchecking tables to be preloaded into the cache:<br><br>   * After unchecking the table, data from that table will no longer be preloaded to the virtual warehouse. Previously preloaded data will be gradually deleted according to the cache eviction strategy (LRU strategy).<br><br>   * For newly selected tables, the table data will subsequently be preloaded to the virtual warehouse according to the current preloading strategy.<br><br>* When switching the virtual warehouse for preloaded data:<br><br>   * After switching the virtual warehouse, subsequent data will be preloaded in the new virtual warehouse. Preloaded data in the previous virtual warehouse will be gradually deleted according to the cache eviction strategy (LRU strategy). |


<span id="c976bb9c"></span>
# Delete preloading tasks

You can also delete created preloading tasks on the preloading task list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0ee486960024e5fa69f175bb398fd62~tplv-goo7wpa0wc-image.image) </span>

After the preloading task is deleted, preloaded data will not be deleted immediately. Instead, it will be gradually cleared according to the eviction strategy (LRU strategy).

<span id="618be926"></span>
# Manually delete the preloaded date

ByteHouse allows you to manually clear cached data of tables or partitions as needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before clearing the cache, please confirm whether the cached data has been used to avoid accidental deletion.</div>


Click **View Executions** and click **Clear Cache**.

<span id="ac43ddd2"></span>
# View preloading monitoring

After creating a preloading task, you can go to **Tenant management** \> **Cloud monitor** to monitor the local disk. You can view local disk metrics, such as cache utilization, preloaded data read/write counts, and other metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d4a81edddbb4e39929635c2d0ddd98e~tplv-goo7wpa0wc-image.image) </span>

For details on the currently supported local disk monitoring metrics and guidance on how to create monitoring alarms via BytePlus Cloud Monitoring, see [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).
