---
title: "Operation Logs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Operation_Logs"
---

The operation log feature of Intelligent Data Insight supports multi\-dimensional search and auditing, making it easy to track user actions and system changes. This article provides a detailed introduction to the methods for searching, viewing, downloading, and managing permissions for operation logs.

<span id="d51edd7f"></span>
# Feature overview

Intelligent Data Insight provides an operation log feature that records user actions on the platform, making it convenient for administrators to trace user behavior and related issues. It supports searching logs by time period, operator, module, action, resource type, resource ID, and more, and also supports downloading operation logs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2094ce43acca4857a57025ab69b0ce17~tplv-goo7wpa0wc-image.image) </span>

<span id="bf5dd698"></span>
# Feature introduction

<span id="d173f529"></span>
## Search operation logs

Users can search logs by operator, operation time, module, action, resource type, resource ID, and more. The search results are displayed in a list, and resetting filter criteria is also supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7020b0d8549a48309f495bde1a209cc6~tplv-goo7wpa0wc-image.image) </span>


|Filter criteria |Description |
|---|---|
|Operation time |The default is the last 3 days, and a custom operation time range is supported.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89a0aaed1404081b318cddc786bef80~tplv-goo7wpa0wc-image.image) </span> |
|Resource type |Single selection. The available options include: access statistics, data links, monitoring, projects, datasets, charts, dashboards, large screens, visual modeling tasks, permissions, users, user groups, ad hoc queries, push records, and more. |
|Search resources |Supports searching by resource ID or resource name. The resource ID is the unique identifier for each resource. For details on how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625e4). |
|Operator |Supports searching by the operator's username, name, or email address. |
|Module/submodule |Modules available for selection include dashboards, visual modeling, visual queries, large screens, scheduled task execution, data connections, datasets, and project center. The project center module can also be further filtered by submodules, such as broadcast management, data permissions, and data connections. |
|Action |Supports searching by action, for example, uploading files, modifying dashboards, creating data connections, and more. |
|Log details |Supports filtering by keywords in the log details, for example, "同步状态(Sync Status)". |


<span id="07611123"></span>
## View operation logs

On the operation log page, enter the search criteria to view the logs in the list below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Due to the large number of [chart] type resources, they are not displayed by default. Please specify the resource name or ID to obtain the operation logs for charts.</div>


* <div data-tips="true" data-tips-type="warning">For private deployment environments version V2.87.0 and above, the operation log list and downloaded logs include department information.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f62651bc2ab4446989e710b590a1cb8~tplv-goo7wpa0wc-image.image) </span>

Click "Log details" on the right side of a log entry to view specific log content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc8d5e7cedb24532baffaccbdb99eb11~tplv-goo7wpa0wc-image.image) </span>

<span id="deb8bdbe"></span>
## Download operation logs

Operation logs can be downloaded. Click "Download logs" on the right side of the interface to download. Supported file formats: XLSX, CSV with GBK encoding, CSV with UTF\-8 encoding.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ab116afadac4efb92a24b4dce1c2acd~tplv-goo7wpa0wc-image.image) </span>

<span id="81c55cb2"></span>
## Log permission management

Users can manage permissions for operation logs. This feature is disabled by default. When enabled, only project administrators and users with higher permissions can view operation logs. Regular users cannot access them, providing hierarchical security protection for operation log access.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5836af9fb6a4c358b9e5b01d543adc4~tplv-goo7wpa0wc-image.image) </span>


* Feature effect diagram:

   * When the switch is off:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/730cb093d96f4185bf1380bdf4769bd2~tplv-goo7wpa0wc-image.image) </span>

   * When the switch is on:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e92c6a2a66ee4c339fde2264cb6aa407~tplv-goo7wpa0wc-image.image) </span>
