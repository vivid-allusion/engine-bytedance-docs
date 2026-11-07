---
title: "Enabling or disabling overload protection"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_overload_protection"
---

This article describes how to enable or disable the overload protection feature.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL provides an overload protection feature to prevent system breakdowns caused by sudden traffic surges to the primary node when read\-only or secondary nodes collectively fail.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the connection endpoint for your instance does not have the overload protection feature, upgrade the instance's kernel minor version. For information about how to upgrade the kernel minor version of the instance, refer to [Manually upgrading instance kernel minor versions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).

* The overload protection feature takes effect only when the Read/Write separation feature is enabled for the connection endpoint, and the primary node is not the only node in the endpoint.

* Only proxy endpoints support the overload protection feature.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Required

An instance has been created and the state of the instance is **Running**. For specific steps, refer to [Create instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, choose MySQL \\> Instance list.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click the **Connectivity** tab.

6. On the **Connectivity** page, in the **Endpoints** list, click **Edit** in the **Actions** column for the target connection endpoint to open the **Modify endpoint** page.

7. In the **Advanced configuration** area on the **Modify endpoint** page, enable or disable overload protection and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When enabling overload protection, you must set a protection duration. After the set protection duration, the overload limit on the Primary node is removed. The overload protection duration ranges from 60 to 7,200s.   </div>
