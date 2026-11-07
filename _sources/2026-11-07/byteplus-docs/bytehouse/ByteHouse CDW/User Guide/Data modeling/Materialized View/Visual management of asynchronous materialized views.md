---
title: "Visual management of asynchronous materialized views"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/visually-manage-asynchronous-materialized-view"
---

ByteHouse supports managing asynchronous materialized views visually, and supports asynchronously refreshing data according to synchronization frequency, making it suitable for complex scenarios that consume significant computing resources. This tutorial introduces how to create and delete asynchronous materialized views.

<span id="1f332423"></span>
# Prerequisite

**Before use, be sure to check whether the view definition is appropriate for the recommended scenarios for using asynchronous views:** 


1. The base tables used in the view definition SQL should preferably be **offline tables updated daily**. **Real\-time tables are not recommended**, as they may cause frequent refresh task triggers, increasing refresh costs and system load.

2. The view definition SQL **must ensure partition alignment**. The target table's partitions should be computed from the partition data of one base table. Otherwise, changes to any base table will trigger a costly **full refresh**.

3. The optimal scenario for joins is: **fact tables updated daily offline** and **dimension tables that are rarely updated**. If fact tables lack partition alignment or dimension tables change frequently, it will cause frequent full refreshes, significantly increasing system load.

4. Views **lack a retry mechanism** upon refresh failure. Failed refreshes will only be retried at the next scheduled interval. Therefore, it is **recommended to set the scheduling interval to minutes** to increase retry opportunities.

5. The actual execution timing **is not guaranteed to strictly adhere to the set interval** and depends on task execution duration. If a task's execution exceeds the interval, it will be deferred to the next cycle. **Do not strictly rely on the scheduling interval for precise timing**.

6. Configuring parameters for asynchronous views in ByteHouse CDW is complex, involving various **Virtual Warehouse (VW) settings**. Failure to configure correctly will route tasks to the default VW, potentially overloading servers. Configure the dedicated vw when you [Create asynchronous materialized view](https://docs.byteplus.com/docs/bytehouse/visually-manage-asynchronous-materialized-view#0b67f56b).


<span id="5589c5ee"></span>
# **Usage restrictions**

Before use, please confirm that your engine version is v2.3 or above. You can view your current engine version on the **Tenant management** \> **Basic information** page in the ByteHouse Console.

<span id="0b67f56b"></span>
# Create asynchronous materialized view


1. Log in to the ByteHouse Console, click on the target database under the **Database** tab, click  **+ View**, and click **Create Materialized View**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/653051c7a16f4ac79088f8e8c6966e33~tplv-goo7wpa0wc-image.image) </span>

2. On the create materialized view page, enter the query SQL, then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8be82f779ffd4ca9a8be0cf5c1df0a7d~tplv-goo7wpa0wc-image.image) </span>

3. Configure the materialized view info, and click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ad87cb3fa074ba0a37802c23702113e~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Parameter description |
   |---|---|
   |Materialized view type |Select asynchronous materialized view. |
   |Database |Select the database in which to create the materialized view and target table. |
   |Name |Customize the name of the materialized view. Naming rules are as follows:<br><br><br>* The name can only contain letters, numbers, and underscores "_".<br><br>* Up to 128 characters. |
   |Order by key |The system will recommend an appropriate order by key based on the SQL command you have entered; you can select and confirm from the drop\-down list. After creation, changing the order by key is not supported. |
   |Partition key |The system will recommend an appropriate partition key based on the SQL command you have entered; you can select and confirm from the drop\-down list. After creation, changing the partition key is not supported. |
   |Virtual warehouse |Select the virtual warehouse resources that the materialized view depends on. |
   |Refresh frequency |Select the data refresh frequency. Supports refresh by day, hour, minute, or second. |
   |Execution time zone |Select the time zone that data refresh depends on. |
   |Execution period |You can set it to all day or customize the execution period.<br><br>When selecting a custom execution period, you need to configure the specific execution date, start time, and end time. You can click the  **+**  button to define multiple execution times. |
   |Parameter configuration |Configure security optimization parameters for the materialized view as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To use this feature, contact the ByteHouse team to enable it and configure the required parameters. You need to specify the exact parameters you require. The system will only display the parameters that have been configured for you.</div><br><br><br>The currently supported full custom parameter descriptions are as follows:<br><br><br>* **max_memory_usage**: The maximum memory usage limit (in bytes) for a single execution task of an asynchronous materialized view. If the limit is exceeded, the task will be interrupted and an error will be reported, preventing a single task from occupying excessive memory resources. The default value is 68,719,476,736.<br><br>* **max_memory_usage_for_user**: The total memory usage cap (in bytes) for all asynchronous materialized view execution tasks under this user, controlling user\-level resource usage and balancing resource allocation among multiple users. The default value is 242,292,621,312.<br><br>* **max_threads**: The maximum number of concurrent threads for asynchronous materialized view execution, used to control CPU resource usage. The more threads, the higher the execution efficiency (should be configured reasonably according to cluster resources). Default value is 4.<br><br>* **max_execution_time**: The maximum timeout for a single execution of an asynchronous materialized view (unit: seconds). If this time is exceeded, the task will automatically terminate to prevent prolonged occupation of cluster resources. Default value is 3600.<br><br>* **max_query_cpu_seconds**: The maximum CPU usage time during asynchronous materialized view execution (unit: seconds), used to control CPU resource consumption and prevent tasks from excessively occupying computing resources. Default value is 3600.<br><br>* **max_joined_block_size_rows**: When the materialized view includes a JOIN operation, this sets the maximum number of rows per data block during association, optimizing join query performance and preventing excessive memory pressure caused by large data blocks. Default value is 65505.<br><br>* **distributed_max_parallel_size**: In a distributed cluster environment, this sets the maximum number of parallel tasks for asynchronous materialized view execution, controlling the concurrency of distributed tasks and adapting to cluster node resource configuration. Default value is 10.<br><br>* **bsp_mode**: Whether to use BSP (Bulk Synchronous Parallel) mode. This mode operates in stages and can effectively reduce resource usage. Supports setting to 0 or 1. Default value is 1. 0 means disabled, 1 means enabled. For more information, see [BSP (Bulk Synchronous Parallel) Execution Mode](https://docs.byteplus.com/docs/bytehouse/Asynchronous_Materialized_View#bc623105).<br><br>* **enable_intermediate_result_cache**: Intermediate result cache switch. Supports setting to 0 or 1. Default value is 0. 0 means disabled, 1 means enabled. When enabled, intermediate results during materialized view execution are cached, accelerating subsequent incremental updates or recalculation procedures. |
   

4. Preview the system\-generated create SQL and confirm whether it meets your requirements. After confirming, click **Create,**  and the system will automatically create an asynchronous materialized view. To modify the information, click **Previous**.

5. After the system prompts "Created successfully", under the **Materialized View** tab, click **Materialized View Name** to view the materialized view details.


<span id="86c7dee2"></span>
# Edit asynchronous materialized view

After the asynchronous materialized view is created, you can edit the virtual warehouse, refresh frequency, and execution period.


1. In the ByteHouse console, under the **Database** tab, click on the target database, click on the materialized view tab, then click on **target materialized view name**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9359c6af1c14a929959ce6b935d21f5~tplv-goo7wpa0wc-image.image) </span>

2. On the materialized view page, click the \*\*Synchronization Tasks \*\*tab and click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/204bfc21de7c4e328388420455c06cc7~tplv-goo7wpa0wc-image.image) </span>

3. On the edit refresh configuration interface, you can adjust the virtual warehouse, refresh frequency, execution time zone, refresh cycle, refresh time(s), and other information as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20bfb9b81e7341d7af744d3e0c76cd94~tplv-goo7wpa0wc-image.image) </span>

4. After adjusting the configuration, click **Save**.

   When the system prompts "Edit materialized view successful", you can view the adjusted virtual warehouse and refresh configuration under the asynchronous sync task tab.

5. (Optional) If you have contacted the ByteHouse team to enable the parameter setting feature, you can also click **Synchronization Tasks** on the page and then click **Parameter settings** to adjust the parameter value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64d72b45131c4237bda4359d4ca3b696~tplv-goo7wpa0wc-image.image) </span>


<span id="c856657d"></span>
# Manually execute asynchronous materialized view sync task

After the asynchronous materialized view is created, you can manually run asynchronous sync tasks as needed.


1. In the ByteHouse console, click the target database under the **Database** tab, click the materialized view tab, and click on the **target materialized view name**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9359c6af1c14a929959ce6b935d21f5~tplv-goo7wpa0wc-image.image) </span>

2. On the materialized view page, click the asynchronous sync task tab, and click **Manually Start**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8de9564b4814ab8af4ebda447e22661~tplv-goo7wpa0wc-image.image) </span>

   The system will prompt "Manual execution successful", and you can view the task list to check the task execution status.


<span id="6190b37f"></span>
# Delete asynchronous materialized view


1. In the ByteHouse console, click the target database under the **Database** tab, click the materialized view tab, and click on the **target materialized view name**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9359c6af1c14a929959ce6b935d21f5~tplv-goo7wpa0wc-image.image) </span>

2. Click  **...**  in the upper right corner of the materialized view interface. Click the **Delete materialized view** button, and in the popup window, click **Delete**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6e457b6b8304832a61d19d0197455b6~tplv-goo7wpa0wc-image.image) </span>
