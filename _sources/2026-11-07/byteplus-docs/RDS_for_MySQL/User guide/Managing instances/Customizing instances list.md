---
title: "Customizing instances list"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/customizing_instances_list"
---

This topic introduces the operation steps for customizing the columns of the custom instance list.

<span id="background"></span>
## Background

The instance list displays information about instances in columns, including instance name, instance ID, running status, availability zone of the primary node, private network address, private network port, public network address, public network port, private network, instance type, label, specification of the primary node, number of nodes, CPU usage (%), memory usage (%), disk usage (%), database version, billing type, creation time, project to which it belongs, and supported operations. The "Instance Name/ID" column and the "Operation" column are always displayed. Except for the "Instance Name/ID" and "Operation" columns, the display of other columns can be customized.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The custom settings for the instance list are persistent within the same browser. After changing accounts or refreshing the page, the settings will still be maintained. You can clear the browser cache to clear the persistent settings. After clearing, only the default display columns will be shown, and the public network address/port, CPU usage (%), memory usage (%), or disk usage (%) will not be displayed.</div>


<span id="steps"></span>
## Procedure


1. Log on to the [RDS for MySQL Console](https://console.byteplus.com/db/rds-mysql).

2. In the upper \- left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs has not been set, for this operation, you should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** on the left navigation bar to enter the instance list.

4. Click **Custom table columns** <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46cb83b1bf62ee62266d3c9e5cf0f036.jpg) </span> in the upper \- right corner of the instance list to customize the display of columns in the instance list.
