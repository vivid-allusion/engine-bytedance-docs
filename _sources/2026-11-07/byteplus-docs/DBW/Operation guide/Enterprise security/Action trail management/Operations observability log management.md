---
title: "Operations observability log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Operation_observability_log_management"
---

The Database Workshop (DBW) provides the operations observability log management function, which can record all operation behaviors, including SQL throttling and KILL sessions. This topic describes how to view operations observability log information in the Database Workshop (DBW) console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* DBW Administrators can view all operation behaviors.

* Non\-DBW roles, i.e., normal users or non\-DBW roles, only support viewing their own operation behaviors.

* Operations observability logs are retained for 30 days. For other requirements, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Enhanced data security**: All operations observability operations can be monitored in real time, covering SQL throttling, KILL sessions, and other content, enabling timely detection and prevention of abnormal behavior. In addition, it can prevent and track all illegal data tampering behaviors.

* **Track user operations**: The operations observability logs record the historical operations of all operators in detail. This ensures that all operations are traceable, increases the transparency of system operations, and helps ensure compliance with security policies and regulatory requirements.

* **Quickly locate issues**: When system faults or exceptions occur, you can quickly trace the operation history with the Operations Observability logs to determine the root cause of the problem and take timely measures to solve it.


<span id=".5p-l55yL6L-Q57u06KeC5rWL5pel5b-X5L-h5oGv"></span>
## View operation observability log information


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. In the left navigation bar, choose **Corporate security** \> **Operation audit**.

4. On the **Operation audit** page, click **Operation observability log**.

5. On the **Operation observability log** tab, view the following information:

   
   <Tabs>
   <Tab zoneid="pu0L3savxf" title="View SQL throttling related operation records">
   <TabTitle>View SQL throttling related operation records</TabTitle>
   
   1. Click **SQL throttling**.
   
   2. In the **SQL throttling** sub\-tab, view the operation records of SQL throttling, including **Create SQL rate limiting task**, **Delete SQL rate limiting task**, **Terminate SQL throttling task**, and **Modify SQL rate limiting task** for **Operation time**, **Username**, **Operation type**, **Database type**, **Instance ID**, and **Execution status**.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also click <strong>View details</strong> in the <strong>Task details</strong> column of the target operation record to view the specific information of the SQL throttling task in the <strong>SQL rate limiting task details</strong> dialog box.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Database type includes RDS for MySQL and veDB for MySQL.   </div>
      
   
   
   </Tab>
   <Tab zoneid="hWnJJY5jQU" title="View KILL session-related operation records">
   <TabTitle>View KILL session-related operation records</TabTitle>
   
   1. Click **KILL sessions**
   
   2. In the **KILL session** dialog box, view the operation records of KILL sessions, including **Manually kill selected session**, **Create persistent KILL tasks**, **Delete persistent KILL task**, and **Terminate persistent KILL task** for **Operation time**, **Username**, **Operation type**, **Database type**, **Instance ID**, and **Execution status**.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also click <strong>View details</strong> in the <strong>Task details</strong> column of the target operation record to view the specific information of the KILL task in the <strong>Persistent KILL task details</strong> dialog box.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Database type includes RDS for MySQL, veDB for MySQL, RDS for PostgreSQL, and Document Database for MongoDB.   </div>
      
   
   
   </Tab>
   </Tabs>
   

&nbsp;
