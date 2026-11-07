---
title: "Restarting an instance or a readonly node"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance"
---

When an instance experiences full connections or performance issues, you can restart the instance manually. This article describes the steps for restarting a RDS for PostgreSQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The time to restart the instance depends on the load state of the instance, which will cause the business to flash out once or twice. Please operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Instances** page, click  **… \> Restart the instance** in the **Actions** column of the target instance,

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also enter the target instance and click <strong>Restart Instance</strong> in the upper right corner of the page.   </div>
   

4. Confirm the instance information in the pop\-up dialog box and select the **Restart scope** as **All nodes** (default) or **Specify read\-only node**. After confirming that everything is correct, click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you choose to <strong>Specify read\-only node</strong>, you need to check the read\-only node that needs to be restarted in the drop\-down list of Read\-only node. You can select up to all read\-only nodes of the instance.</div>


* <div data-tips="true" data-tips-type="tip">Return to the instance list page, refresh the current list, and the instance status changes to <strong>Restarting</strong>. After the restart is complete, the instance status changes to <strong>Running</strong>.</div>
