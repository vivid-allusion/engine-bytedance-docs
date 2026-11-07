---
title: "Monitoring Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Monitoring_Management"
---

<span id="_1-概述"></span>
# 1. Overview

In the "Monitoring Management" module of the project center, project administrators or monitoring creators can view and manage monitoring tasks that have been configured within the current project.

The monitoring alert (also referred to as monitoring alarm) feature can be used to monitor changes in metrics or data within charts, providing monitoring configuration capabilities at the hour, day, and month granularity. Users can configure monitoring by setting monitoring rules and monitoring frequency. The alert methods currently supported by the system include email, Feishu, WeCom, Webex, and DingTalk.


* The specific alert method depends on the office platform integration configuration completed by your company's system administrator. For detailed steps, see [Office platform integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f7).


<span id="_2-功能介绍"></span>
# 2. Features

First, as a project administrator or monitoring creator, you can click "Project Center" and select "Monitoring Management" from the left sidebar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b0a0d99a858468789b8ee04ebcbb36f~tplv-goo7wpa0wc-image.image) </span>

Second, you can view a list of all monitoring tasks for which you have permission in the current project.

Third, you can query monitoring tasks by chart, owner, recipient, and task status, or search by name.

Finally, you can perform operations on one or more monitoring tasks, such as enabling or disabling, copying, viewing alert records, editing, transferring ownership, deleting, and more.

<span id="_3-注意事项"></span>
# 3. Notes

(1) Which users can view or edit monitoring tasks?

Answer: The creator of the monitoring, project administrators, and the owner of the chart associated with the monitoring.

Because monitoring is considered private information, monitoring on personal dashboards cannot be edited by others. To allow others to edit monitoring, the chart associated with the monitoring must be placed on a public dashboard, and then management permissions for that dashboard must be granted to others.


| |**Viewing scope** |**Scope of operations** |
|---|---|---|
|Project administrator |Can view all monitors under the project |Has full permissions |
|Project member |All monitors I created |Has full permissions |
||All monitors created based on the charts I manage |Has full permissions |
||All monitors for which I am the recipient |No permission to operate |


(2) Monitoring and subscriptions support batch transfer of ownership.

(3) If the monitoring recipient is empty, the monitoring cannot take effect.
