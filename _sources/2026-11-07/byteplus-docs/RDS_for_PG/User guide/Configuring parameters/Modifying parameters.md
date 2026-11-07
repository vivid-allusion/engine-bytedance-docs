---
title: "Modifying parameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters"
---

This topic describes the procedure for modifying parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To ensure instance stability, the console only allows modification of certain parameters. If the parameter you want to modify is unavailable, [submit a ticket](https://console.byteplus.com/workorder/create) for processing.

* Modify parameter values by referring to the **Modifiable parameter value** column on the **PostgreSQL parameter** tab.

* Some parameters require restarting the instance after modification. For details, refer to the "restart or not" column on the modifiable parameters page in the console. If parameters requiring restart are changed, the instance restart usually completes within 30 to 60 seconds. There may be 1 to 2 disconnections during this process; operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.

* Support batch modification of the running values of multiple parameters at the same time.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more information about creating instances, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click the **Parameters** tab at the top of the page.

5. Modify parameter **values** by referring to the **Modifiable parameter value** column on the **PostgreSQL parameter** tab.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Click <strong>Undo</strong> previous step to cancel the current parameter modification. You can click <strong>Undo</strong> previous step multiple times to undo the previous modifications.</div>



6. After modifications, click **Submit** at the top left of the page, and in the pop\-up dialog **Are you sure to submit the following parameter configuration?**  Click **OK** in the dialog.
