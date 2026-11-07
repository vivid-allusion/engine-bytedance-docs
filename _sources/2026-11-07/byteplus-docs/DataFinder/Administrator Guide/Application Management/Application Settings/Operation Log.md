---
title: "Operation Log"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Operation_Log_"
---

<span id="_1-概述"></span>
# 1. Overview

The operation log is the basic capability of the system. This function records the user's operation on the platform. Administrators can make clear the user's changes to the system through the operation log, so as to ensure the data security of the system and meet the IT audit requirements.

**Scene example**:


1. Troubleshooting: When the user finds that the Dashboard or event tracking data is missing in the system, the administrator can give priority to clarifying whether the corresponding asset has been disabled, deleted or modified through the operation log, and troubleshoot the problems caused by the user's operation.

2. Security audit: operation log can be directly in the interface to search, filter and download, administrators can regularly through the operation log moderation operation whether there are non\-compliant data export, high frequency download or unexpected API calls and other sensitive operations.

3. Misoperation recovery: When a user makes a misoperation, the administrator can locate the operator's operation record through the operation, find the difference between the new/old value, and restore the historical configuration by himself.


**Release Notes** : SaaS versions are supported after 2023.6.15; privatized versions are supported after 4.5 (inclusive).

<span id="_2-功能说明"></span>
# 2. Function description

<span id="_2-1-功能入口"></span>
## 2.1 Function entrance

**Function level**: application management \- \> application settings \- \> operation log.

**Record scope**: all users with application permissions in the application of the operation, the specific operation of this table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36eb12791773454183a0096ea5000504~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-功能权限"></span>
## 2.1 Functional permissions

This function is only open to `group administrators`by default, and other roles can assign the permissions of this function by themselves through `Permission Management - > Role Management - > Function Permissions`Configuration.

**Legacy permission entry** : Group Management \- \> Role Management \- \> Enter the corresponding role \- \> Configure function permissions \- \> Check [operation log] \- \> OK

**New version permission entry** : Project Center \- \> Permission Management \- \> Role Management \- \> Enter the corresponding role \- \> Function Permissions \- \> Configuration \- \> Check [operation log] \- \> Save

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c8d01415d0e4fbf811a47bdd23a444d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-管理界面"></span>
## 2.3 Management interface

**Filtering**: Supported operators, operation time, projects/applications, modules.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6294bf5f6e3b45b9bd2929ef631daf5f~tplv-goo7wpa0wc-image.image) </span>

**Table**: Support operator, operation time, product, project, module, operation behavior, log details (including specific operation objects and comparison of old and new values). Default sort is in reverse chronological order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07448b11151a48f19d4e22f0cc2a1ed2~tplv-goo7wpa0wc-image.image) </span>

**Download**: Click on the `download log`in the upper right corner of the form to start the download.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0068e45363724bd887ef8a0faec5e8d1~tplv-goo7wpa0wc-image.image) </span>


* File name: The default is operation log \- date, which can be edited by yourself.

* File format: Support XLSX/GBK encoding CSV/UTF\-8 encoding CSV.

* Content: Display content in the same table

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a7a7efe63874ec79d2589823d625655~tplv-goo7wpa0wc-image.image) </span>


<span id="附：操作日志记录明细"></span>
# Attachment: operation log record details


|Module name |Submodule name |Operational behavior |Original value/new value meaning |Record field |
|---|---|---|---|---|
|Dashboard |Dashboard |new build |Empty/Dashboard information |Dashboard ID/name/Dashboard description/owner/whether it is a folder |
| | |authorization |Dashboard information + original authorized person list/Dashboard information + new authorized person list |Dashboard ID/Name/Dashboard Description/Owner/Whether it is a folder permission type (Only I can/Have edit permission User Dashboard ID/Name/Dashboard Description/Owner/Whether to change members for the folder |
| | |edit |Edit pre\-Dashboard information/edit post\-Dashboard information |Dashboard ID/name/Dashboard description/owner/whether it is a folder |
| | |copy |Dashboard Information/Dashboard Information |Dashboard ID/Name/Dashboard Description/Owner |
| | |delete |Dashboard information/empty |Dashboard ID/name/Dashboard description/owner/whether it is a folder |
| | |Create subscription |Empty/subscription information |Dashboard ID/name/Dashboard description/owner/subscription name/push time/push effect/push method |
| | |edit subscription |Subscription information before editing/Subscription information after editing |Dashboard ID/name/Dashboard description/owner/subscription name/push time/push effect/push method |
| | |unsubscribe |Subscription information/empty |Dashboard ID/name/Dashboard description/owner/subscription name/push time/push effect/push method |
| |chart |new build |Empty/chart information |Chart ID/Chart Name/Owner/Icon Type (Event Analysis Save Icon) |
| | |edit |Chart information before editing/Chart information after editing |Chart ID/Chart Name/Owner |
| | |delete |Chart information/empty |Chart ID/Chart Name/Owner |
|Advanced Analytics |Event Analysis/Retention Analysis/Conversion Analysis/Distribution Analysis/Component Analysis/User Path/Attribution Analysis/User Lifecycle/LTV Analysis/Business Object Analysis |query |empty/record field | |
| | |download |empty/record field | |
| | |openAPI request |empty/record field | |
|User analysis |user scrutiny |query |Empty/query condition dsl |Query DSL |
| | |openAPI request |Empty/query condition dsl |Query DSL |
| |user portrait |query |Empty/query condition dsl |Query DSL |
| |user grouping |new build |empty/grouping information |ID/Name/Type/Description |
| | |edit |User grouping information before editing/User grouping information after editing |ID/Name/Type/Description |
| | |View user list |empty/grouping information |ID/Name/Type/Description |
| | |recalculate |empty/grouping information |ID/Name/Type/Description |
| | |download |empty/grouping information |ID/Name/Type/Description |
| | |delete |Cluster information/empty |ID/Name/Type/Description |
| | |openAPI request |empty/grouping information |ID/Name/Type/Description |
|Scenario Analysis \- Mini Program Analysis |QR code management |new build |Empty/QR code information |ID/Name/Mini Program id/Page URL/QR code group |
| | |edit |QR code information before modification/QR code information after modification |ID/Name/Mini Program id/Page URL/QR code group |
| | |delete |QR code information/empty |ID/Name/Mini Program id/Page URL/QR code group |
| | |download |Empty/QR code information |ID/Name/Mini Program id/Page URL/QR code group |
|Data management \- metadata management |event classification |new build |Empty/event classification information |ID/Name/Event List |
| | |edit |Pre\-Modification Event Classification/Post\-Modification Event Classification |ID/Name/Event List |
| | |delete |Event classification information/empty |ID/Name |
| |User Properties/Event Properties/User Properties |new build |Empty/general event |Name/Presentation Name/Description/Status (List) Extra Records when Attributes: Data Type/Whether Public Attributes |
| | |edit |Original General Event/New General Event |Name/Presentation Name/Description/Status (Single or List) Extra Records when Attributes: Data Type/Whether the Attribute is Public |
| | |enable |Original General Event/New General Event |Name/Presentation Name/Description/Status Attribute when extra records: Data Type/Whether Public Attribute |
| | |disable |Original General Event/New General Event |Name/Presentation Name/Description/Status Attribute when extra records: Data Type/Whether Public Attribute |
| | |acceptance |General event information before acceptance/general event information after acceptance |Name/Presentation Name/Description/Status (List) Extra Records when Attributes: Data Type/Whether Public Attributes |
| |Virtual events/virtual properties |new build |Empty/virtual event |Name/Presentation Name/Name/Rule Attribute Extra Records: Data Type/Attribute Type |
| | |edit |Original virtual event/new virtual event |Extra records when name/display name/rule property: data type/property type |
| | |delete |Virtual event/empty |Name/Presentation Name/Name/Rule Attribute Extra Records: Data Type/Attribute Type |
|Data Management \- Data Governance |Data Governance Dashboard |Export event tracking scheme |empty | |
| |Data warehousing details |Download all details |empty | |
| | |download |empty | |
|Data Management \- Open Data |data distribution |new build |empty/data distribution |Name/Distribution/webhook URL/Headers/Status |
| | |open |Original data distribution/new data distribution |Name/Distribution/webhook URL/Headers/Status |
| | |disable |Original data distribution/new data distribution |Name/Distribution/webhook URL/Headers/Status |
| | |edit |Original data distribution/new data distribution |Name/Distribution/webhook URL/Headers/Status |
| | |delete |Data distribution/empty |Name/Distribution/webhook URL/Headers/Status |
|Application Management |general settings |enable |function name + original general settings/function name + new general settings |Function name/status |
| | |disable |function name + original general settings/function name + new general settings |Function name/status |
| | |Configuring crawler rules |The original rules/new rules |Reptile characteristics/reptile characteristics |
| |date annotation |new build |empty/date comment information |Date/Name/Description |
| | |edit |Before the modification date comment information/After the modification date comment information |Date/Name/Description |
| | |delete |Date comment information/empty |Date/Name/Description |
| | |batch deletion |Date comment information/empty |Date/Name/Description |
|Task Management |Monitoring management |new build |Empty/monitoring information |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |enable |Monitoring information/Monitoring information |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |disable |Monitoring information/Monitoring information |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |batch enable |Monitoring information/Monitoring information |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |batch shutdown |Monitoring information/Monitoring information |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |delete |Monitoring information/empty |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| | |batch deletion |Monitoring information/empty |Monitoring name/monitoring rules/monitoring frequency/monitoring period/notification channel |
| |query task management |new build |empty/query task |Task Name/Task ID/Analysis Module |
| | |delete |Query task/empty |Task Name/Task ID/Analysis Module |
|Dashboard Center |Dashboard/chart/folder management |batch deletion |Dashboard, chart, folder list/empty |Dashboard ID/name/Dashboard description/owner/whether it is a folder or chart ID/chart name/owner |
| | |volume licensing |Empty/Dashboard, Charts, Folder Information + List of New Authorizers | |
| | |bulk handover |Empty/Dashboard, chart, folder info + new owner | |
| |webhook management |new build |Empty/webhook information |Name/Address/Enterprise Group Type |
| | |modify |Webhook information before modification/webhook information after modification |Name/Address/Enterprise Group Type |
| | |delete |Webhook information/empty |Name/Address/Enterprise Group Type |
|Scenarios template | |Save scene template |Empty/Scene Template Information |Type/Name |


**Added after version 4.6:** 


|Module name |Submodule name |Operational behavior |Original value/new value meaning |Record field |
|---|---|---|---|---|
|Data management \- metadata management |business object |new build |empty/business object |ID/Name/Presentation Name/Description/Status/Associated Attribute List (Name/Presentation Name/Description/Data Type/Status/Logic) |
| | |edit |Original Business Object/New Business Object |ID/Name/Presentation Name/Description/Status/Associated Attribute List (Name/Presentation Name/Description/Data Type/Status/Logic) |
| | |enable |current business object |ID |
| | |disable |current business object |ID |
| |analysis subject |new build |Empty/Business Principal |Attribute name/unit |
| | |edit |Original business entity/new business entity |Attribute name/unit |
| | |delete |Business entity/empty |Attribute name/unit |
| |Custom Session |new build |Empty/Custom session |Name/display name/event list/time interval/whether to cut the event/whether to cut across time periods |
| | |edit |Original custom session/new custom session |Name/display name/event list/time interval/whether to cut the event/whether to cut across time periods |
| | |delete |Custom session/empty |Name/display name/event list/time interval/whether to cut the event/whether to cut across time periods |
| |session management |edit |Original session/new session |time interval |
|Data Management \- Data Access |Official account access |new build |Empty/new access official account information |Follow name/official account ID/status |
| | |enable |Official account information |Follow name/official account ID/status |
| | |deactivate |Official account information |Follow name/official account ID/status |
| | |edit |Original official account information/new official account information |Follow name/official account ID/status |
| | |delete |Official account information/empty |Follow name/official account ID/status |
|Project Center \- Project Management |Project details |edit |Original project information/new project information |Project ID/Project Name/Project Description/Administrator/Caliber ID |
|Project Center \- Permission Management |Role Management |new build |Empty/Role Information |Role Name/Role Description/Role Owner |
| | |Disable/Enable |Role information + old status/role information + new status |Role Name/Role Description/Role Owner/Status |
| | |delete |Role information/empty |Role Name/Role Description/Role Owner/Status |
| | |Edit Role Information |Old Role Information/New Role Information |Role Name/Role Description/Role Owner/Status |
| | |configure feature permissions |Role information + old function permissions/role information + new function permissions |Role id/permission list |
| | |Modify attribute permission |Role information + old permissions/role information + new permissions |Character id/rules |
| | |Modify event permissions |Role information + old permissions/role information + new permissions |Character id/rules |
| | |Delete event permission |Role information + deleted permissions |Character id/rules |
| | |Add members (privatization needs to be viewed in the portal) |empty/member information |Role Name/Role Description/Role Owner/Status/Member List |
|Project Center \- Permission Management |user management |Invite new users (privatization needs to be viewed in the portal) |empty/user list + role permissions |Invite user/role permissions |
