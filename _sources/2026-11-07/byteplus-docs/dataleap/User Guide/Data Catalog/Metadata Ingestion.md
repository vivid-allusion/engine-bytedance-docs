---
title: "Metadata Ingestion"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Metadata_Ingestion"
---

Data Catalog provides you with **Metadata Ingestion** functionality. This function allows you to unify and manage metadata from different systems and view the aggregated metadata from various data sources in Data Catalog. This article introduces how to ingest metadata.

<span id="ad45e60a"></span>
## Overview

This feature uses a unified template to create collectors that connect to each data source, completing the ingestion of various types of cluster metadata through the ingestion operation. DataLeap currently supports ingesting the following types of metadata. For detailed ingestion operations of each type, please refer to [Create a New Collector](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion#_2-%E6%96%B0%E5%BB%BA%E9%87%87%E9%9B%86%E5%99%A8).


|Source type |Metadata ingestion execution method |Supported regions |
|---|---|---|
|ByteHouse CDW |Update in real time<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After creating the collector, perform a full collection manual sync once to synchronize the corresponding historical metadata. After the first successful acquisition, the collector automatically updates the metadata in real time.</div><br> |Southeast Asia Pacific (Johor) |
|ByteHouse CE |* Scheduled execution<br><br>* Manual Execution |Southeast Asia Pacific (Johor) |
|LAS Catalog |* Scheduled execution<br><br>* Manual execution |Southeast Asia Pacific (Johor) |


<span id="_1-约束限制"></span>
## Constraints


* The tenant main account has full operation permissions for all collectors. The tenant sub\-account has full operation permissions only for the collectors it created and has view and synchronization execution permissions for collectors created by others.

* Only one collector can be created per cluster.

* ByteHouse CE supports real\-time automatic synchronization of metadata between the console and Data Catalog without collector ingestion, while Data Development and Data Catalog require collector ingestion to synchronize data.


<span id="b21db8ee"></span>
## Prerequisites

The corresponding engine is activated, and the matching type of cluster or instance is created in the engine console. For engine activation operations, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

<span id="_2-新建采集器"></span>
## Create a New Collector


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Metadata Ingestion** to enter the metadata ingestion page.

3. Click the metadata type in the left navigation bar to enter the corresponding data type ingestion page.

4. Click the **New collector** button to open the new collector window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/353347a33f1a4854aeb44f4d1500ac2d~tplv-goo7wpa0wc-image.image) </span>

5. Follow the page prompts to set ingestion information, click the **Next** button step by step, and after setting is complete, click the **Complete** button to create the collector.

   The following table describes the parameters for creating a new collector. Parameters marked with \* before the name are required; those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |\*Acquisition type |Support **ByteHouse CDW**, **ByteHouse CE**, and **LAS Catalog**, click to select. |
   |**Ingestion Target** ||
   |\*Collector name |The name of the data collector; set as needed.<br><br>Only Chinese characters, English letters, numbers, or underscores are allowed, with a maximum length of 100 characters. |
   |Collector description |Description of the collector, limited to 500 characters. |
   |Acquisition type |Displays the currently selected type; not editable. |
   |\*collection method |Only **direct connection** is supported. |
   |\*cluster |Cluster information to connect the data source.<br><br><br>* When **Acquisition type** is **ByteHouse CDW**, or **ByteHouse CE**, the dropdown shows the corresponding running clusters.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Collectors already created or clusters not running normally appear grayed out in the dropdown list and cannot be selected.   </div><br>   <br><br>* When **Acquisition type** is **LAS Catalog**, it is the default cluster and cannot be edited. |
   |**Authorization** ||
   |Authorization check |Select authorization information to allow the Data Catalog to use metadata from the chosen cluster.<br><br>The authorization information states: “I agree that the Dataleap \- Data Catalog product will obtain the metadata of the selected cluster and use it for account queries under the current tenant.” |
   |**Ingestion** **Config** ||
   |Table filter rules |Set data table filtering rules by entering regular expressions.<br><br>After setting the rules, only target data matching the filter rules will be collected during metadata ingestion. |
   |DB filtering rules |Set database filtering rules by entering regular expressions. After setting the rules, only target data matching the filter rules will be collected during metadata ingestion.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be set when <strong>acquisition type</strong> is <strong>ByteHouse CDW</strong>.</div><br> |
   |**Scheduling Configuration** ||
   |\*Execution method |Method for synchronizing metadata.<br><br><br>* ByteHouse CE and LAS Catalog support both **scheduled execution** and **manual execution** options.<br><br>   * Scheduled execution: automatically perform synchronization based on the set frequency and time.<br><br>   * Manual execution: manually perform synchronization.<br><br>* ByteHouse CDW only supports real\-time updates; the collector will automatically update incremental metadata in real time.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After creating the collector, you must manually perform a full synchronization of historical metadata once. See the <a href="https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion#_3-%E6%89%8B%E5%B7%A5%E5%90%8C%E6%AD%A5%E5%85%83%E6%95%B0%E6%8D%AE">Manual Metadata Ingestion</a> for related instructions.   </div><br>    |
   |\*Scheduling frequency |Frequency of scheduled metadata synchronization. Supports daily and hourly execution options.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be configured when <strong>execution method</strong> is set to <strong>scheduled execution</strong>.</div><br> |
   |\*Execution time |Time for scheduled metadata synchronization.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be configured when <strong>execution method</strong> is set to <strong>scheduled execution</strong>.</div><br> |
   


<span id="_3-手工同步元数据"></span>
## Manual Metadata Ingestion


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Metadata Ingestion** to enter the metadata ingestion page.

3. Click the metadata type to enter the corresponding data type ingestion page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9c7385ad52143bda5412616c34a87b1~tplv-goo7wpa0wc-image.image) </span>

4. Click the **execute** button in the **action** column of the list to open the execution window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62d2c735fade4715a1c5da474f3cb7ed~tplv-goo7wpa0wc-image.image) </span>

5. After setting the execution scope, click the **OK** button to manually synchronize the metadata to DataLeap.

   * Full Amount: synchronize all metadata in the target source once.

   * Specified Scope: synchronize metadata for specified tables. Select this option and enter the name of the data table to synchronize.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a current task is in progress, this button is grayed out and unavailable.</div>


* <div data-tips="true" data-tips-type="tip">If synchronization fails, perform the following steps:</div>


   1. <div data-tips="true" data-tips-type="tip">Check the <strong>execution log</strong> to find and resolve the problem.</div>


   2. <div data-tips="true" data-tips-type="tip">Use the <strong>execute</strong> function to manually sync metadata that failed to obtain to the Data Catalog.</div>



<span id="_4-查看执行历史"></span>
## View Execution History


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Metadata Ingestion** to enter the metadata ingestion page.

3. Click the metadata type to enter the corresponding data type ingestion page.

4. Click the **execution history** button in the **action** column of the list to view all synchronization metadata execution history records in the pop\-up side window. The following operations can be performed:

   * Set search criteria to view records meeting the conditions for different execution states within different time periods.

   * Click the **execution log** button in the **action** column of a record to view its execution log.


<span id="_5-搜索采集器"></span>
## Manage Collectors


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Metadata Ingestion** to enter the metadata ingestion page.

3. Click a metadata type to enter the corresponding data type ingestion page.

4. The following management operations can be performed on created collectors:

   * Search collectors

      Set search criteria to view the list of collectors matching the conditions.

   * Edit collector

      Click the **Edit** button in the **Action** column of the list to edit information. In the pop\-up collector details side panel, you can modify the collector's information.

   * Delete collector

      Click the **Delete** button in the **Action** column of the list to delete information. In the pop\-up confirm deletion window, you can perform the following delete operations:

      * Click the **Confirm** button to delete the collector and clear the collected metadata. After deletion, the corresponding historical metadata will also be cleared and cannot be recovered.

      * Select **Delete the collector only** and click the **Confirm** button to keep the collected metadata and only delete the collector.

   * Disable/Enable collector

      Click the **Disable/Enable composite** button in the **Action** column of the list to disable or enable the collector.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you lack permission or if a task is currently in progress, the edit and delete buttons are grayed out and unavailable.</div>


* <div data-tips="true" data-tips-type="tip">After creating a collector, it is enabled by default. When enabled, collection runs according to the scheduled frequency; when disabled, collection cannot be performed.</div>



<span id="406770e6"></span>
## Follow\-up Actions

After successful metadata ingestion, you can perform data search, view data lineage, manage tables, and other operations in the **Data Catalog**. You can also go to other modules for operations related to the ingested data, such as managing data permissions and protection in **Data Security**.
