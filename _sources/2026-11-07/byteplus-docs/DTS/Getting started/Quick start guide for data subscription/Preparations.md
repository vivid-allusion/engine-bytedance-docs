---
title: "Preparations"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Preparations"
---

This topic introduces the preparations required before using DTS for data subscription to ensure smooth configuration and operation of data subscription tasks.


|Applicable scenarios |Network used for data subscription |Preparations to be executed |
|---|---|---|
|The source database or target database is located in the IDC and plans to connect via the public network. |Public network |Add the IP address of the DTS server to the allowlist of the self\-managed database. |
|The source or target database is deployed locally but does not have a public IP address. |Public network (via other servers) |The following preparations are required:<br><br><br>* Connect the local or third\-party cloud database to the database gateway.<br><br>* Add the IP address range of the DTS server to the allowlist of the self\-managed database. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can view and copy the CIDR block by clicking View <strong>DTS IP segment</strong> in the <strong>Source database information</strong> area on the <strong>Configuring source and target database</strong> page.</div>


* <div data-tips="true" data-tips-type="tip">You can also prepare the subscription objects in the source and target databases according to the instructions in the Pre\-check items. For details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items</a>.</div>


* <div data-tips="true" data-tips-type="tip">When the instance type is <strong>RDS for MySQL</strong> and the access method is a <strong>MySQL connected over public network </strong>(such as the source database being an instance of a third\-party cloud service), you need to retain logs (e.g., Binlog) for at least 24 hours. Retaining logs for more than 7 days is recommended. Otherwise, the DTS task may fail because it can not obtain logs, potentially causing the task to fail and sometimes resulting in inconsistent or lost data.</div>
