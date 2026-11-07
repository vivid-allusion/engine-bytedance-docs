---
title: "Viewing parameter modification history"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/view-parameter-modification-history"
---

This topic introduces how to view parameter modification history of MongoDB instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Parameters** tab.

6. Click **Parameter modification history** sub\-tab to view the parameter modification details, such as the parameter name, parameter values before and after modification, and modification time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can filter the parameter modification history information within a specific time period using the time settings in the upper\-right corner.   </div>
   

<span id=".55u45YWzYXBp"></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameterslog) |Call the DescribeDBInstanceParametersLog API to query parameter modification history of target MongoDB instance within specified time. |
