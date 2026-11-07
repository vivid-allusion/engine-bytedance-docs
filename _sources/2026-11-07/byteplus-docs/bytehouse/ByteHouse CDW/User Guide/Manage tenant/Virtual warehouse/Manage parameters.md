---
title: "Manage parameters"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-virtual-warehouse-parameters"
---

ByteHouse provides different levels of parameter management, supporting global parameters, user parameters, and virtual warehouse parameters to meet various business scenario configuration needs. This tutorial explains how to configure and manage different types of parameters.

<span id="4bccf515"></span>
# Feature overview

ByteHouse currently supports setting global parameters, user parameters, and virtual warehouse parameters, distinguished as follows:


|Parameter |Description |
|---|---|
|Global Parameters |Parameters that take effect globally in the environment, supporting the configuration of the default write virtual warehouse and statistics feature.<br><br><br>* **Default write virtual warehouse**: ByteHouse supports setting the default write virtual warehouse for the current environment. If you have purchased multiple virtual warehouses, you can also specify different default write virtual warehouses for different databases in the current environment.<br><br>* **Statistics**: This feature enables the optimizer CBO optimization capability, which can improve query and write performance. Enabling this feature can improve query performance and will consume part of the resources of the default write virtual warehouse. |
|User Parameters |Parameters which are effective at the user level. ByteHouse supports setting the default virtual warehouse, default database, and default language for the current user. |
|Virtual Warehouse parameters |For parameters effective for a single virtual warehouse, you can modify the parameter values in the fixed parameter template of the virtual warehouse based on business needs, or set custom parameters as required. For the currently supported custom parameter list, please refer to [Reference: Custom parameter list](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#c0855d50). |


In ByteHouse, virtual warehouse parameters require setting both the default write virtual warehouse and the default virtual warehouse. This is because ByteHouse natively supports storage\-compute separation (read\-write separation). By configuring the default write virtual warehouse and the default virtual warehouse, you can assign data writing and query operations to different virtual warehouses, enabling resource isolation and improving operational stability. This approach is especially suitable for production environments where both read and write operations are busy, and for business scenarios that demand high real\-time performance for data writing and fast query response times.

In addition to supporting the configuration of the default virtual warehouse and default write virtual warehouse, ByteHouse also allows you to specify the required virtual warehouse when performing operations:


* Console SQL worksheet: Before executing SQL statements in the SQL worksheet, you can select a virtual warehouse as needed. For details, see [Select a virtual warehouse](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet#932edd7d).

* Executing SQL statements in other clients: You can specify the virtual warehouse using relevant parameters. For example,

   ```SQL
   # Query level
   SELECT *
   FROM db.table
   SETTINGS virtual_warehouse='xxx';
   
   # Session level
   SET virtual_warehouse='xxx';
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to set virtual warehouse parameters only at the query level or only at the session level; do not set both at the same time.   </div>
   

<span id="37636c2a"></span>
# Usage restrictions


* Before use, ensure your engine version is v2.3 or above. You can check your current engine version on the ByteHouse console's **Tenant Management** \> **Basic Information** page.

* The following features are in Beta. To use them, submit a ticket or contact the ByteHouse team to request whitelist access.

   * Set database\-level write virtual warehouse

   * Edit virtual warehouse parameters

   * Copy virtual warehouse parameters


<span id="c744315a"></span>
# Set global parameters

<span id="d57e5ece"></span>
## Prerequisites

Only users with SystemAdmin or AccountAdmin roles can configure write virtual warehouses.

<span id="e4ec3478"></span>
## Set the default write virtual warehouse

The default write virtual warehouse is the environment's default virtual warehouse used to write data to the database's underlying storage.

Log in to the ByteHouse console, in **Tenant management**, click the **Parameter settings** tab, under the **Global Parameters** module, click the **Edit** button in the write virtual warehouse row, and select the default write virtual warehouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41c32aedf7e14b0993acde64b253e161~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The write virtual warehouse is a global parameter; changes apply globally across the environment.</div>


* <div data-tips="true" data-tips-type="warning">Frequent changes to this setting are not recommended. Updates take about 5 minutes to take effect and may impact table write performance during that time.</div>


* <div data-tips="true" data-tips-type="warning">You can adjust the virtual warehouse specs as needed to meet your business requirements. For detailed instructions, see <a href="https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f">Edit virtual warehouse configuration</a>.</div>


* <div data-tips="true" data-tips-type="warning">When the write virtual warehouse service expires, the system will notify you that the service is unavailable when you log into the console. You can configure the write virtual warehouse based on the prompt.</div>



<span id="761cc321"></span>
## Set database level write virtual warehouse

ByteHouse supports configuring dedicated write virtual warehouses for databases. After setting a database\-level write virtual warehouse for a database, writing data to that database will use the specified virtual warehouse by default; if none is set, it will use the environment's default write virtual warehouse.


1. Log in to the ByteHouse console, in **Tenant management**, click the **Parameter settings** tab, under the **Global Parameters** module, click **Database Level Write Virtual Warehouse** to enter the configuration page.

2. Click **Edit**, then select the database and its corresponding write virtual warehouse from the dropdown list. Click **Add 1 Row** to configure the default write virtual warehouse for multiple databases

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c356f92f5b64d19923d5853080b868a~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only one write virtual warehouse can be set for each database.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Frequent modifications to the database\-level write virtual warehouse are not recommended. This change takes about 5 minutes to take effect and may affect table write performance during the update.   </div>
   

3. Click **Save** to apply the changes.

4. To delete the database\-level write virtual warehouse, click the **delete** button on the corresponding database row. After deletion, the system will use the default write virtual warehouse set in the current environment.


<span id="eb127ffa"></span>
## Set statistics feature

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only users with the SystemAdmin or AccountAdmin role can configure statistics.</div>


* <div data-tips="true" data-tips-type="warning">This feature requires the engine version to be v2.3.2 or above. Before use, please confirm that your engine version meets the requirements. You can view your current engine version on the ByteHouse Console's <strong>Tenant management</strong> \> <strong>Basic information</strong> page.</div>


* <div data-tips="true" data-tips-type="warning">This feature is disabled by default and must be manually enabled before it can be used.</div>


* <div data-tips="true" data-tips-type="warning">Resource binding rules: This feature occupies part of the resources of the write virtual warehouse. If the default write virtual warehouse is adjusted, statistics will be automatically bound to the new default write virtual warehouse.</div>



Log in to the ByteHouse Console, in **Tenant management**, click the **Parameter settings** tab, under the **Global Parameters** module, toggle the **Statistics Info** button to enable or disable the feature.

<span id="08d78c94"></span>
# Set user parameters

Log in to the ByteHouse console, click **Tenant management**, then the **Parameter settings** tab, under the **User Parameters** module, click the **edit** button in the parameter row and select the corresponding parameter value. The parameter configuration is explained as follows:


* **Default virtual warehouse**: The default virtual warehouse is the user’s default virtual warehouse, used to handle SQL's default compute resources.

* **Default database**: The default database to which the user connects when connecting to ByteHouse.

* **Language**: Default language setting, supports Simplified Chinese or English.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3006980d4da1408b96beb3465fb9b71b~tplv-goo7wpa0wc-image.image) </span>

<span id="9fd5d768"></span>
# Set virtual warehouse parameters

ByteHouse offers two types of virtual warehouses, OLAP and ELT, with corresponding parameter templates. You can choose the virtual warehouse type as needed and customize parameters based on business scenarios. This setup optimizes query performance for OLAP analysis and ensures stability for ELT batch processing tasks. Additionally, ByteHouse supports adding custom SQL parameters to further improve SQL execution efficiency and better adapt to your business scenarios for optimized data processing.

<span id="4bebe4a7"></span>
## Prerequisites

All users can view virtual warehouse parameters, but only users with ALL virtual warehouse privileges can edit parameters or duplicate virtual warehouses.

You can check virtual warehouse privileges by logging into the **ByteHouse Console**, then navigating to **Access control** \> **User** \> **Username** \> \*\*Resource privileges \*\*Path. To obtain permission to edit virtual warehouse parameters, contact your system administrator for configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/317cb78377f94a6a9bfda28505680ba1~tplv-goo7wpa0wc-image.image) </span>

<span id="45e8c736"></span>
## Edit virtual warehouse parameters

ByteHouse provides fixed parameter templates for virtual warehouses, allowing you to configure parameters easily. This helps enhance data warehouse performance and meet specific business scenario requirements.

Besides fixed templates, ByteHouse supports adding custom SQL parameters to better accommodate practical business needs. The custom parameter list is maintained by ByteHouse. For the full list of currently supported custom parameters, please refer to [Reference: Custom parameter list](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#c0855d50). If you have new custom parameter requirements, please contact the ByteHouse team to submit your requests.

**Steps:** 


1. Log in to the ByteHouse console, and navigate to the **Virtual warehouse parameters** module via the path **Tenant management** \> **Parameter settings** \> **Virtual warehouse parameters**. In the virtual warehouse dropdown list, select the virtual warehouse to edit. Then enter the parameter name in the search box and click the **Search** button to find the parameter to modify.

2. Click the **Edit** button to edit the **Current Value**. When editing, refer to the parameter value range to set the parameter. If the parameter value you set exceeds the allowed range, you cannot submit or save it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb438e66793a4bf2b98811d917c29321~tplv-goo7wpa0wc-image.image) </span>

3. (Optional) Add custom parameters.

   1. Click the  **+Custom Parameters** button to enter the add custom parameters page.

   2. Search for the custom parameter to add, check the required parameters, and click **Add**.

   3. View and edit the added custom parameter values in the virtual warehouse parameter list.

   4. If you need to delete a custom parameter, click the **Delete** button on the corresponding parameter row.

4. After confirming the details, click **Save**.

5. (Optional) Some parameters take effect after the virtual warehouse restarts. You can restart the virtual warehouse according to the on\-screen instructions. A prompt box with the “Restart virtual warehouse” button will appear. After clicking the button, the virtual warehouse status changes to “Restarting” and returns to “Running” when the restart is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b499049bf8d14ca0a99754de0c962721~tplv-goo7wpa0wc-image.image) </span>

6. Confirm that the parameter values have been updated in the parameter list on the current page.


<span id="925ca61a"></span>
## Copy virtual warehouse parameters

ByteHouse supports copying current virtual warehouse parameters to other virtual warehouses of the same type, helping you improve configuration efficiency and consistency. After copying, the new parameters will overwrite the existing ones.


1. In the virtual warehouse parameter module, select the virtual warehouse as the source, then click **Copy Parameters**.

2. Select the target virtual warehouse to copy parameters to, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a4b24a8a94404fad8191df565ccc5b~tplv-goo7wpa0wc-image.image) </span>

3. Switch to the target virtual warehouse to check if the parameters have been copied successfully.

4. (Optional) Some parameters take effect after restarting the virtual warehouse. You can restart the virtual warehouse following the on\-screen instructions. After restarting, verify that the parameter values have been updated in the target virtual warehouse’s parameter list.

   When restarting, a prompt with a “Restart virtual warehouse” button will appear. Click this button to change the virtual warehouse status to “Restarting.” The restart is complete once the status returns to “Running.”


<span id="c0855d50"></span>
# Reference: Custom parameter list

The following describes custom parameters supported by ByteHouse:


|Parameter Name (SQL Parameter) |Current Value |Range |Parameter Description |
|---|---|---|---|
|optimize_unique_table_write |false |true/false |It is used for unique key table insert select import optimization. It is recommended to enable only when the staging area is not enabled, dedup_impl_version='dedup_in_txn_commit'. |
|max_insert_threads |0 |positive integer |Size of the write thread pool for worker executing insert select requests. |
|min_insert_block_size_bytes |1,073,710,080 |positive integer |Minimum size of the batch block for insert select. |
|min_insert_block_size_rows |1,048,545 |positive integer |Minimum rows for the batch block insert select. |
|max_partitions_per_insert_block |100 |positive integer |The maximum number of parts allowed to write within each block for a single Insert operation, usually limited by the number of partitions \* buckets in data distribution. |
|lake_commit_in_worker |true |true/false |Whether to use worker to submit when writing tables. |
|lake_write_threads |4 |Positive integer |Thread pool size for table writing. |
|lake_write_max_file_size |1,073,741,824 |Positive integer |Max size of a single file for table writing. |
|input_format_parquet_use_native_reader |false |true/false |Whether to use the native reader when reading parquet files. |
|input_format_parquet_use_footer_cache |false |true/false |Whether to cache the parquet file footer in memory. |
|output_format_parquet_row_group_size |1,000,000 |positive integer |Parquet file row group size. |
|dynamic_adjust_squash_for_write |false |true/false |Whether to optimize memory usage during the squash process in the write procedure. |
|enable_implicit_arg_type_convert |false |true/false |whether to enable implicit function argument conversion. |
|enable_plan_cache |false |true/false |Whether to enable in\-memory query plan cache. |
|match_name_ignore_case |false |true/false |whether to ignore case sensitivity in SQL statements. |
|wait_runtime_filter_timeout |1000 |Positive integer |Wait time for building the runtime filter, default is 1 second; if timed out, the runtime filter result will be ignored. |
