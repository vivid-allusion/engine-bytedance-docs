---
title: "Switching primary node"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/switching_primary_nodes"
---

RDS for PostgreSQL supports switching between primary and secondary nodes. When the system detects an instance failure, it immediately triggers a switch between the primary and secondary nodes to restore normal operations and ensure instance high\-availability. This topic describes the steps to manually switch the primary node.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

* No migration tasks are ongoing.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the instance has read\-only nodes mounted, the data on the read\-only nodes may experience several minutes of latency after the primary node switch.

* Switching the primary node generally takes 30 to 60 seconds, during which the database will experience 1 to 2 brief disconnections. Operate carefully. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

4. Click the **Connectivity** tab. In the **Instance topology** area, hover over the **Secondary node**, click **Switch to primary node** in the pop\-up window, and then click **OK** in the dialog box to complete the switch of the primary and secondary nodes.
