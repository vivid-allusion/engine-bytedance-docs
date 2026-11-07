---
title: "Metadata Connection and Application"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Metadata_Connection_and_Application"
---

<span id="_1-产品概述"></span>
# 1. Product overview

As DataWind is used more extensively and promoted within the company, it becomes increasingly important to monitor and manage the resources created by each user in the product. To address this, DataWind provides metadata connection and template application features, enabling all data assets in your DataWind environment to form a data center. This allows you to quickly view relevant information, monitor and manage resources, prevent misuse and abuse of resources, and also build core monitoring for certain key dashboards and datasets to ensure effective management of data output and dashboard applications.

<span id="_2-快速入门"></span>
# 2. Quick start


* For members of the IT or operations department responsible for on\-premises deployment within the enterprise, metadata can be used to understand and analyze how analysts or business users are using DataWind, and to further carry out operations\-related tasks.

* For members of the IT or operations department, or departments responsible for security monitoring or information security auditing within the enterprise, metadata can be used to build a security monitoring and information security audit mechanism, effectively protecting the security of enterprise data assets.


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-使用流程"></span>
## 3.1 Usage process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f8550bd5a0649d494a4d3feb39c9b90~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-功能说明"></span>
## 3.2 Feature description

<span id="_3-2-1-元数据连接"></span>
### 3.2.1 Metadata connection

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41740cc629e84286bcca576ca1f7ccd3~tplv-goo7wpa0wc-image.image) </span>

In the data connection section of "Data Preparation," project administrators can select "DataWind metadata" and click to create DataWind metadata. After creation, system metadata that the user has permission to access can be queried based on project permissions.

Metadata has two statuses:


1. Available status: Click to create DataWind metadata. After creation, system metadata that the user has permission to access can be queried based on project permissions.

2. Disabled status: The system contains all metadata, and only project administrators or group administrators are allowed to perform operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/998a8534e7fe44c48879295fb623eacf~tplv-goo7wpa0wc-image.image) </span>

After clicking Test Connection, the interface will indicate that the connection is successful. Then click Save to enter the details page for this data connection.

<span id="_3-2-2-元数据的数据连接详情"></span>
### 3.2.2 Metadata data connection details

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6653759775843daa9dedda74838c45d~tplv-goo7wpa0wc-image.image) </span>

Currently, DataWind provides you with the following four main categories of metadata:


1. Behavior event data: Records all user operation logs within different projects on the platform, including user behavior auditing, user activity analysis, resource popularity, and other analytical content. The fields such as resource ID, name, and creation time mainly include information about visualization modeling, datasets, charts, and dashboard resources. If there is no event information, it means the resource has not been accessed or operated.

2. Asset detail data: Records asset detail data for datasets, visualization modeling, charts, and dashboards. Datasets and visualization modeling provide information such as scheduling tasks, instance tasks, and underlying table TTL resources, enabling asset statistics, task management, resource management, and other analyses.

3. Asset relationship data: Records the interdependencies among datasets, visualization modeling, charts, and dashboards, which can be used for asset analysis, asset queries, and lineage viewing, among other analyses.

4. User data: Records user data under different projects, used for analyzing project changes, user changes, and other analytical data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/484d05e4a2f54773935e29db1ce3b075~tplv-goo7wpa0wc-image.image) </span>

On the metadata data connection details page, you can view basic information and perform the following operations:


* Lineage view: View downstream resources, such as visualization modeling and datasets. Detailed information includes the name, ID, type, owner, creation time, and update time of these resources.

* Permission assignment: Grant permissions to users, user groups, roles, departments, and so on by searching for users, user groups, roles, departments, and so on.

* Edit: Modify the data connection name.

* Apply: Further use metadata to create datasets or visualization modeling tasks.

* Delete.


<span id="_3-2-3-元数据应用"></span>
### 3.2.3 Metadata application

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/992c268a90ff48b88addcdf53cfcf4b6~tplv-goo7wpa0wc-image.image) </span>

You can further use metadata to create datasets and visualization modeling tasks, and then build dashboards and more.


* Application entry: On the data connection details page, click "Application" in the upper right corner.

* Notes:

   a. When creating a dataset, it is recommended to build one dataset for each subject metadata. The dataset can use either direct connection or extraction mode. For extraction mode, check the data range for backfill; otherwise, the query may return empty results. Direct connection mode allows querying all data in the project up to the present.

   b. Dataset query data permission scope: Controlled by the role permissions of the creator, not the permissions of dashboard users.

   c. If the owner is transferred and no further edits are made, permissions remain unchanged.

   d. Users must have edit permissions for the corresponding project to create a metadata dataset.


<span id="fb09604d"></span>
### 3.2.4 Additional capabilities

Based on system metadata, you can build an operations\-oriented information dashboard. For this purpose, we provide an information dashboard template for enterprise customers. This template is a value\-added module. To use it, contact your company's sales representative or customer success manager for purchase information.

<span id="491122c0"></span>
# 4. Description of the metadata indicator system

<span id="_4-1-行为事件主题数据"></span>
## 4.1 Behavioral event subject data

**Overview:**  Records all user operation logs within different projects on the platform, used for behavioral auditing, user activity analysis, resource popularity analysis, and more. Fields such as resource ID, name, and creation time mainly include information on visualization modeling, datasets, charts, and dashboard resources. If there is no event information, it indicates that the resource has not been accessed or operated.

**Content:** 


|Field name |Expression |Display name |Remarks |
|---|---|---|---|
|p_date |p_date |p_date |Date partition field |
|Event timestamp |event_timestamp |event_timestamp |Event timestamp = p_date, that is, the data table is stored according to incremental logic. |
|Project ID |app_id |app_id | |
|Event user |event_user |Event user | |
|Event occurrence time (date format) |toDate(event_timestamp/1000) |Event occurrence time (date format) | |
|Resource ID |resource_id |Resource ID | |
|Resource name |resource_name |Resource name | |
|Resource owner |resource_owner |Resource owner | |
|Resource creation time |resource_create_time |Resource creation time | |
|Project ID of the resource |resource_app_id |Project ID of the resource | |
|Resource type |resource_type |Resource type | |
|Event occurrence time |to_date(event_timestamp/1000) |Event occurrence time | |
|Event type |event_type |Event type | |
|Event resource ID |event_resource_id |Event resource ID | |
|Event module |event_module |Event module | |
|Event action |event_action |Event action | |
|Event details |event_payload |Event details | |
|Event resource name |event_resource_name |Event resource name | |
|Event resource type name |event_resource_type_name |Event resource type name | |
|Page views |count(event_user) |Page views |Calculated field |
|Unique visitors |count(distinct event_user) |Unique visitors |Calculated field |
|Resource folder |resource_folder_name |Resource folder | |


<span id="_4-2-资产明细主题数据"></span>
## 4.2 Asset details subject data

**Overview:**  Records detailed asset data for datasets, visualization modeling, charts, and dashboards. Datasets and visualization modeling provide information on scheduling tasks, instance tasks, and underlying table TTL resources, enabling asset statistics, task management, resource management, and related analyses.

**Content:** 

> Note: Assets include all asset content and may contain system\-generated tasks.



|Field name |Expression |Display name |Remarks |
|---|---|---|---|
|p_date |p_date |p_date | |
|Base table creation time |data_table_create_time |Base table creation time | |
|Base table storage size |data_table_table_size |Base table storage size | |
|Base table update time |data_table_update_time |Base table update time | |
|Base table lifecycle |data_table_ttl |Base table lifecycle | |
|Base table row count |data_table_line_num |Base table row count | |
|Visual modeling update type |prep_schedule_type |Visual modeling update type |* 0 self\-scheduling<br><br>* 1 dorado scheduling<br><br>* 2 real\-time task scheduling type<br><br>* 3 no scheduling |
|Visual modeling task type |prep_task_type |Visual modeling task type |* \-1 all types (offline + real\-time)<br><br>* 0 offline type<br><br>* 1 real\-time type<br><br>* 2 tag import type |
|Visual modeling task routine information |prep_schedule_conf |Visual modeling task routine information | |
|Visual modeling task execution status |prep_execute_status |Visual modeling task execution status |* \-1 initialization status<br><br>* 0 all statuses<br><br>* 1 non\-existent status<br><br>* 2 scheduling status<br><br>* 3 running status<br><br>* 4 success status<br><br>* 5 failure status<br><br>* 6 pending scheduling status<br><br>* 7 terminated status<br><br>* 8 other status |
|Visual modeling total count |uniq(case when resource_type= '可视化建模' then resource_id end) |Visual modeling total count |Calculated field |
|Visual modeling latest sync end time |prep_last_sync_end_time |Visual modeling latest sync end time | |
|Visual modeling latest sync start time |prep_last_sync_time |Visual modeling latest sync start time | |
|Task count (visual modeling/dataset) |uniq(case when instance_schedule_time is not null then resource_id end ) |Task count (visual modeling/dataset) |Calculated field |
|Instance ID |instance_id |Instance ID | |
|Instance creation time |instance_create_time |Instance creation time | |
|Instance queue |instance_queue |Instance queue | |
|Instance end time |instance_end_time |Instance end time | |
|Instance start time |instance_start_time |Instance start time | |
|Instance name |instance_name |Instance name | |
|Instance configuration information |instance_conf |Instance configuration information | |
|Instance task execution time |instance_task_time |Instance task execution time | |
|Number of instances |uniq(instance_id) |Number of instances | |
|Instance scheduling time |instance_schedule_time |Instance scheduling time | |
|Instance execution waiting time (s) |dateDiff('second', toDateTime(instance_schedule_time), toDateTime(instance_start_time)) |Instance execution waiting time (s) |Calculated field |
|Instance execution duration (s) |dateDiff('second', toDateTime(instance_start_time), toDateTime(instance_end_time)) |Instance execution duration (s) |Calculated field |
|Instance status |instance_status |Instance status | |
|Dataset lifecycle |dataset_ttl |Dataset lifecycle | |
|Dataset synchronization type |dataset_sync_type |Dataset synchronization type | |
|Total number of datasets |uniq(case when resource_type= '数据集' then resource_id end) |Total number of datasets |Calculated field |
|Total number of charts |uniq(case when resource_type= '图表' then resource_id end) |Total number of charts |Calculated field |
|Project ID |app_id |Project ID | |
|Project creation time |app_create_time |Project creation time | |
|Project update time |app_update_time |Project update time | |
|Project name |app_name |Project name | |
|Project status |app_status |Project status | |
|Total number of projects |uniq(app_id) |Total number of projects | |
|Total number of dashboards |uniq(case when resource_type= '仪表盘' then resource_id end) |Total number of dashboards |Calculated field |
|Resource ID |resource_id |Resource ID | |
|Resource creation time |resource_create_time |Resource creation time | |
|Resource update time |resource_update_time |Resource update time | |
|Resource type |resource_type |Resource type | |
|Resource name |resource_name |Resource name | |
|Resource deletion time |resource_delete_time |Resource deletion time | |
|Resource owner |resource_owner |Resource owner | |
|Dataset type |data_set_type |data_set_type | |


<span id="_4-3-资产关系主题数据"></span>
## 4.3 Asset relationship subject data

**Overview:**  Records the interdependencies among datasets, visual modeling, charts, and dashboards, which can be used for asset analysis, asset queries, and lineage analysis.

**Content:** 

> \*Note: Because the relationships are stored as many\-to\-many mappings, please perform deduplication when conducting statistics.



|Field name |Expression |Display name |Remarks |
|---|---|---|---|
|p_date |p_date |p_date | |
|Number of visual modeling resources |uniq([visual modeling resource ID]) |Number of visual modeling resources |Calculated field |
|Visual modeling resource ID |prep_resource_id |Visual modeling resource ID | |
|Visual modeling resource creation time |prep_resource_create_time |Visual modeling resource creation time | |
|Visual modeling resource name |prep_resource_name |Visual modeling resource name | |
|Visual modeling resource owner |prep_resource_owner |Visual modeling resource owner | |
|Number of dataset resources |uniq([数据集资源ID]) |Number of dataset resources |Calculated field |
|Dataset resource ID |dataset_resource_id |Dataset resource ID | |
|Dataset resource creation time |dataset_resource_create_time |Dataset resource creation time | |
|Dataset resource name |dataset_resource_name |Dataset resource name | |
|Project ID of dataset resource |dataset_resource_app_id |Project ID of dataset resource | |
|Owner of dataset resource |dataset_resource_owner |Owner of dataset resource | |
|Chart creation time |report_create_time |report_create_time | |
|Chart update time |report_update_time |report_update_time | |
|Number of charts |uniq([Chart resource ID]) |Number of charts |Calculated field |
|Chart owner email prefix |report_owner_email_prefix |report_owner_email_prefix | |
|Chart status |report_status |report_status | |
|Chart resource ID |report_resource_id |Chart resource ID | |
|Chart resource creation time |report_resource_create_time |Chart resource creation time | |
|Chart resource name |report_resource_name |Chart resource name | |
|Owner of chart resource |report_resource_owner |Owner of chart resource | |
|Project ID |coalesce(app_id,dashboard_resource_app_id,report_resource_app_id,dataset_resource_app_id,prep_resource_app_id) |Project ID |Calculated field |
|Dashboard ID |dashboard_id |dashboard_id | |
|Dashboard update time |dashboard_resource_update_time |dashboard_resource_update_time | |
|Number of dashboards |uniq([Dashboard resource ID]) |Number of dashboards |Calculated field |
|Dashboard resource ID |dashboard_resource_id |Dashboard resource ID | |
|Dashboard resource creation time |dashboard_resource_create_time |Dashboard resource creation time | |
|Dashboard resource name |dashboard_resource_name |Dashboard resource name | |
|Owner of dashboard resource |dashboard_resource_owner |Owner of dashboard resource | |


<span id="_4-4-用户主题数据"></span>
## 4.4 User topic data

**Overview:**  Records user data under different projects, used for analyzing project changes, user changes, and other analytical data.

**Content:** 

> \*Note: Different projects have different configurations, so user information content may vary.



|Field name |Expression |Display name |Remarks |
|---|---|---|---|
|p_date |p_date |p_date |Date partition field |
|Project ID |app_id |app_id | |
|Project creation time |app_create_time |app_create_time | |
|Project update time |app_update_time |app_update_time | |
|Project name |app_name |Project name | |
|Project status |app_status |app_status | |
|User ID |user_id |user_id | |
|User email prefix |user_email_prefix |User email prefix | |
|User creation time |user_create_time |user_create_time | |
|User update time |user_update_time |user_update_time | |
|User name |user_name |user_name | |
|User status |user_status |user_status |* SUBJECT_STATUS_NORMAL = 0, indicates the user status is normal<br><br>* SUBJECT_STATUS_TERMINATED = 1, indicates the user has left the company<br><br>* SUBJECT_STATUS_DISABLED = 2, indicates the user is disabled<br><br>* SUBJECT_STATUS_DELETED = 3, indicates the user is deleted |
|Total number of users |uniq(user_id) |Total number of users |Calculated field |
|User department |department_name |department_name | |


<span id="_5-faq"></span>
# 5.FAQ

(1) **After importing the template, if you do not select to replace the dataset, the dashboard query will not work properly after import. How should this be resolved?** 


* **Cause:**  After importing the template, if you do not replace the dataset, the template dataset will still use the historical permission configuration, which may not be effective in the new environment. You need to re\-edit and update the permission information.



|Import configuration |Issue description |Solution |
|---|---|---|
| | |1. Locate the imported dataset and see an abnormal permission prompt<br><br>2. Click Edit Dataset, update the dataset configuration, and save |


(2) **After importing the template and selecting to replace the dataset, you will see many field names in both Chinese and English. How should this be resolved?** 


* **Cause:**  The imported template is a standardized dataset, and the dataset names have been optimized and modified. The original dataset uses English field names. At this point, both will exist simultaneously. To avoid information interference, you can delete all English field names to improve readability.


(3) What is the data lifecycle of system metadata?

The TTL (data lifecycle) of data connected to metadata is 7 days by default. When deploying the product, you can set the TTL. For specific operations, please consult customer service personnel.
