---
title: "ID - Mapping Operations and Management"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/ID_-_Mapping_Operations_and_Management"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

The system provides ID\-Mapping operations and management\-related functions, mainly including: task information, lineage view, data exploration analysis, and advanced configurations (such as authorization ID Mapping configuration permissions, management ID Mapping online service configurations, etc.

<span id="581aae51"></span>
# 2. Usage Restrictions

Only group administrators (i.e., admin accounts) can configure the ID graph.

<span id="8166d28f"></span>
# 3. Operation Guide

<span id="57d9d1ba"></span>
## 3.1 ID\-Mapping Task Information

Click **Data Fusion \- ID Graph Construction** to access the **task information** page. On this page, all ID\-Mapping task details will be displayed, allowing users to view corresponding task database table names, identity ID, creation time, operating status, etc.


* The header displays an overview of tasks in the current environment, including total number of tasks, success/failure counts, and more.

* Support filtering by "Subject OneID Task" or "Multi\-Subject Relationship Task".

* Support filtering by task type, subject, multi\-subject relationship, and running status.

* Task types include:

   * OneID generation task: one subject, one task, controlling the overall logic of OneID generation, the most core and first task to run, landing in the Hive table.

   * ID data synchronization task: dependent on the OneID generation task, synchronizes the data of each ID mapped BaseID (OneID) to Clickhouse, a task directly relied upon by downstream label applications, and others.

   * Multi\-subject relationship generation: dependent on the OneID generation task, builds the mapping relationship data between subjects to BaseID (OneID) to BaseID (OneID), landing in the Hive table.

   * Multi\-subject relationship data synchronization: dependent on the multi\-subject relationship generation task, synchronizes the data of BaseID mapping relationships between subjects from the Hive table to Clickhouse, a task directly relied upon by downstream subject transformation relationship applications.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/430b4808b8114e1bb0f24bc3b20556ca~tplv-goo7wpa0wc-image.image" width="1901px" /></div>


Support viewing the operation view and records of a single task, and support individually rerunning this task.


* The "Operation View" page will display the upstream DAG dependency of the task and the operating status of each dependent task.

* "Rerun" will restart that task.

* "Operation Records" page will display the task execution status for the last 30 days.


Click the **Run** button in the upper right corner to manually run **all** ID\-Mapping tasks (may cause OneID changes).

<span id="6131f2c2"></span>
## 3.2 Lineage Management

<span id="ac324fe9"></span>
### 3.2.1 Lineage View

In the Lineage View, you can view the upstream and downstream lineage of tags, segments, datasets, asset outputs, IDM online imports, and multi\-subject transformation relationships, facilitating operation and maintenance troubleshooting, and improving abnormal task handling efficiency.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e1f67d870d8489496538084550efee0~tplv-goo7wpa0wc-image.image" width="1902px" /></div>


<span id="a77209ed"></span>
### 3.2.2 **View ID Lineage and Downstream**

In the OneID graph, you can click on an ID to view its details and downstreams, and view the downstream dependency lineage view.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44bf51faca6043aaa6a970a853631278~tplv-goo7wpa0wc-image.image" width="1896px" /></div>


<span id="ae224dc1"></span>
## 3.3 **Data Exploration Analysis**

Supports querying the mapping relationship from ID to OneID, and OneID change records.

<span id="74911b83"></span>
### 3.3.1 OneID Mapping

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instructions</div>


<div data-tips="true" data-tips-type="tip"><strong>Purpose:</strong> View the OneID corresponding to each specific ID value and whether different OneIDs exist under different query environments.</div>


<div data-tips="true" data-tips-type="tip"><strong>Recommendation:</strong> If multiple ID values have different OneIDs in different environments, it does not meet the expected OneID generation. Please check if the offline or real\-time tasks are updating normally. If some ID values have multiple different OneID results, it may be due to delays in data import. It is recommended to wait and query again.</div>


<span id="2390d635"></span>
### 3.3.2 OneID reorganization changes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instructions</div>


<div data-tips="true" data-tips-type="tip"><strong>Purpose:</strong> View the change process of OneID, which can be used to troubleshoot OneID reorganization caused by IDM configuration changes or reference relationship changes.</div>


<div data-tips="true" data-tips-type="tip"><strong>Recommendation:</strong> If the OneID corresponding to the ID changes frequently, you can check the reference relationship configuration or relationship data related to the ID to avoid frequent changes in reference relationships.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d41797cab364c6bbb2a4557e58a3f36~tplv-goo7wpa0wc-image.image) </span>

<span id="d4bed78f"></span>
## **3.4 IDM Advanced Configuration**

<span id="64d55d95"></span>
### 3.4.1 **Authorize IDM configuration permissions**

Click the **Advanced Configuration\-Authorize IDM configuration permissions** button in the upper right corner to jump to the Project Center, supporting the configuration of ID Mapping administrators where authorized individuals will have permission to edit the ID graph.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d32be5613d446b98a6322e8ba3d8bb8~tplv-goo7wpa0wc-image.image" width="1888px" /></div>


<span id="d2d7a5b3"></span>
### 3.4.2 **Manage ID Mapping online service configurations**

Click the **Advanced Configuration\-Manage ID Mapping online service configurations** button in the upper right corner to jump to the Project Center, supporting the construction of online services for ID Mapping subjects and conversion relationships for quick query interfaces with high QPS and low latency.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40a51bcf30cf425485e96e78d1028a10~tplv-goo7wpa0wc-image.image" width="1890px" /></div>


<span id="293eec38"></span>
### 3.4.3 **Manage subjects and visibility scope**

Click the **Advanced Configuration\-Manage subjects and visibility scope** button in the upper right corner to jump to the Project Center, supporting the **subjects and IDs** for **reverse disablement** (default all available, selectively disable in batches after checking specific objects).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0798aff2cc7542ba9eeafb766d11a351~tplv-goo7wpa0wc-image.image" width="1876px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Attention: This configuration is at the group level. Disabling it will take effect on the user accessing various projects.</strong></div>



* Configure subject resource permissions. After selecting resources, click "Batch Disable" and choose the objects to disable in the pop\-up window. (Only support filtering by user)


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95e9cc3173bb4de6932023b64aacedbe~tplv-goo7wpa0wc-image.image" width="2878px" /></div>



* Configure ID type resource permissions. After selecting resources, click "Batch Disable" and choose the object to disable in the pop\-up window. (Support filtering by user, user group, role)


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2aa56cdb62c4b6fbdb17b6097f1232c~tplv-goo7wpa0wc-image.image" width="2872px" /></div>


<span id="041b4e69"></span>
### 3.4.4 Set the lifecycle of the **base table**

The IDMapping task involves data production and data synchronization processes at the underlying level. Users can set the lifecycle days of the base table to save storage resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instructions</div>



* <div data-tips="true" data-tips-type="tip">Duration: minimum 14 days, maximum 365 days, only integer input supported</div>


* <div data-tips="true" data-tips-type="tip">If there is a OneID change and a backfill requirement, a reasonable period can be set according to the backfill requirement.</div>


* <div data-tips="true" data-tips-type="tip">On\-demand configuration: Currently only applicable to the underlying tables of Hive, CK, and Tendis are not supported temporarily.</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1944c299a1b34f708b0b99c676586bc6~tplv-goo7wpa0wc-image.image" width="1886px" /></div>


<span id="f5b27274"></span>
### 3.4.5 **Offline Full ID Count Logic Management**

IDMapping is based on the generation of graphs from the full ID, with data from multiple sources supporting the definition of statistical logic for full ID data. When activated, OneID will integrate all offline IDs and historical real\-time IDs, suitable for scenarios where offline data warehouse data is incomplete and multiple channel data is needed to build a complete full ID.

> \*Note: This feature is turned off by default. To enable it, please inform us during deployment and switch on the corresponding feature toggle.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4ce2fad0b874c06b4b3981809a165eb~tplv-goo7wpa0wc-image.image" width="1915px" /></div>


<span id="6ee13722"></span>
### 3.4.6 **Full Management ID Data Fusion Cycle**

To ensure consistency in the generation of OneID, the same ID is maintained during the process, supporting the setting of a reference period for historical OneID so that new data can seamlessly connect with historical data. The default fusion cycle is set to 7 days but can be customized as needed.

> \*Attention: This feature is off by default. To enable it, please inform and activate the corresponding feature switch during deployment.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7feda42312f546d195f7d871bae01f7b~tplv-goo7wpa0wc-image.image" width="1906px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Attention:</div>



1. <div data-tips="true" data-tips-type="tip">If the data source of a certain ID is only real\-time, the real\-time data will be stored every day. Only when it's both offline and real\-time, choose to believe that the offline dataset contains the complete ID. However, configure this feature to avoid scenarios where users are left in the dark.</div>


2. <div data-tips="true" data-tips-type="tip">It is suggested that the offline ID includes all historical IDs every day. If confirmed to be included, this function can be ignored</div>



<span id="16727de5"></span>
## 3.5 **Delete ID**

On the ID configuration page, ID deletion is supported.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfe308a2f3d3468cb52c712c03a1404a~tplv-goo7wpa0wc-image.image" width="1559px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Attention</div>



1. <div data-tips="true" data-tips-type="tip">Group and project administrators, as well as ID Mapping administrators, have the authority to delete IDs</div>


2. <div data-tips="true" data-tips-type="tip">The ID linked by the system cannot be deleted, such as the ID linked by Finder products.</div>


3. <div data-tips="true" data-tips-type="tip">After deleting the ID, the OneID data bound to that ID will be cleared during the next task update, and once deleted, it cannot be undone.</div>


4. <div data-tips="true" data-tips-type="tip">When deleting an ID, you can view the lineage information of that ID. After the deletion of the ID, downstream tasks may execute abnormally.</div>


5. <div data-tips="true" data-tips-type="tip">After deleting the ID, the impacts on OneID, multi\-subject relationships, and online services are as follows:</div>


   1. <div data-tips="true" data-tips-type="tip">OneID Configuration: The reference relationships of this ID with other IDs will be deleted, and the OneID generation logic will change.</div>


   2. <div data-tips="true" data-tips-type="tip">Multi\-Subject Relationships: The conversion relationships dependent on this ID will be deleted.</div>


   3. <div data-tips="true" data-tips-type="tip">OneID Online Services: If online services are enabled for this ID, calling the interface services associated with this ID will fail. The interfaces of open services will not be displayed in the lineage. Please verify internally if this ID has been called.</div>



<span id="d80987d5"></span>
## 3.6 **OneID Data Correction**

> \*Attention: This feature is off by default. To enable it, please inform and activate the corresponding feature switch during deployment.


Based on a complete ID lineage system, the ID Graph Construction module provides the capability for automated data correction, allowing the correction of historical OneID to the latest OneID.

<span id="238fe1d7"></span>
### 3.6.1 **Data Correction Scope**


* Visual modeling tasks: tasks containing IDM operators with the backflush switch enabled, registered as data files, and tasks containing IDM operators

* Data File: Behavioral/Detail Data File

* Label: No support for backflush correction. For tasks involving weekly/monthly granular cycles, it is recommended to change to daily granularity instead

* Segment: No support for backflush correction. For tasks involving weekly/monthly granular cycles, it is recommended to change to daily granularity instead

* DataFinder Behavioral Data: includes Finder behavioral data and attribute data

   * Attention: When DataFinder is deployed independently, OneID data correction is not supported


<span id="54d2473b"></span>
### 3.6.2 **Application Scenarios**

**Scenario 1:**  Users exist, anonymously log in on the first day, change to real\-name login on the second day, and it is necessary to link the user's behavioral trajectory at this point


* ID\-Mapping Configuration: Mobile number/device number, mobile number priority \> device number, device number refers to mobile number

* Situation on the first day: Anonymous login, only device number 1 information is available, corresponding to **Device number 1 = OneID1**

* The situation on the second day: Real\-name login. At this point, there is mobile phone number 1 + device number 1 information. The device number refers to the mobile number, so at this time mobile number 1 = device number 1 = OneID2

* Issue: The behaviors on the first day are recorded around **OneID1**. The behaviors on the second day are recorded around **OneID2**, resulting in the inability to analyze the user's behaviors for two days in sequence for conversion behavior paths


**Scene 2**: ID\-Mapping configuration change. Based on Scene 1, the device number should now take priority as the business ID. IDM configuration is updated accordingly


* Before the ID\-Mapping configuration change: Mobile number/device number, mobile number takes precedence over the device number, with the device number referencing the mobile number

* After the ID\-Mapping configuration change: Mobile number/device number, mobile number takes precedence below the device number, with the mobile number referencing the device number

* Before change: Mobile number = device number = OneID1, OneID1 generated based on the mobile number

* After change: Mobile number = device number = OneID2, OneID2 generated based on the device number

* Issue: As above, historical data such as behavioral data/business details cannot be linked with the latest data


**Solution based on the above scenarios:**  Based on a complete ID lineage system, IDM provides a product feature for automatic data correction, allowing the correction of historical OneIDs to the latest OneIDs **Solution logic:**  Daily scheduled tasks for data update backfilling.

Instructions

**1. Functional Limitations:** 


* Resource Risk: Daily timed wake\-up tasks will increase the task volume, which may lead to increased resource consumption.

* Correction Cycle Risk: Supports data correction for up to 3 days. Longer correction cycles will increase resource consumption and task stability risks, requiring consultation for operational changes.


**2. Data Correction Scope:** 


* Visual Modeling Tasks: Tasks containing IDM operators with the backflush switch enabled, registered as data archives with IDM operators.

* Data Archive: Behavioral/Detail Data Archives

* Labels: Do not support retroactive corrections. For tasks involving weekly/monthly granular large cycle tasks, it is recommended to change to daily granularity.

* Segments: Do not support retroactive corrections. For tasks involving weekly/monthly granular large cycle tasks, it is recommended to change to daily granularity.

* DataFinder Behavioral Data: Includes DataFinder behavioral and attribute data

   * When deploying DataFinder independently, OneID data correction is not supported.


<span id="224dff9a"></span>
### 3.6.3 **Operation Steps**


|Steps |Functional Entry |Operating Instructions |Operation Screenshots |
|---|---|---|---|
|1\-Mandatory |ID Graph Construction \- OneID Configuration |Click the 'More' button on the main entity name, click on "Set OneID Correction Scope" to summon the configuration entrance to enter the pop\-up configuration window, set the cycle for refreshing, supporting up to 3 days. Extra manpower and resource cost evaluation will be required if it exceeds 3 days and needs to be assessed separately. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0602c9ca8de64c859aa93e2dc997c791~tplv-goo7wpa0wc-image.image) </span> |
||||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d51667ce850446a58198f592cf5fba08~tplv-goo7wpa0wc-image.image) </span> |
|2 \- Optional |Visual modeling (offline) \- IDMapping operator |When using the IDMapping operator to build offline tasks, you can configure whether to backflush, thereby deciding whether the task needs to be backflushed regularly to correct OneID data |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8e038e6225b43758da42ed2db43c260~tplv-goo7wpa0wc-image.image) </span> |
