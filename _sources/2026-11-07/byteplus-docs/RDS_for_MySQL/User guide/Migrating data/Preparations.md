---
title: "Preparations"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/preparations"
---

This topic describes how to prepare for data transfer using DTS to ensure successful configuration and running of the migration task.


|Applicable scenarios |**Network for Data Transfer** |**Preparations** |
|---|---|---|
|The source or destination database is located in the IDC or ECS and plans to use an internet connection. |Internet |Add the IP address of the DTS server to the allowlist of the self\-managed database. |
|The source or destination database is deployed locally but does not have a public address. |Internet (with the help of other servers) |The following preparations must be made:<br><br>Connect a local database or a database on a third\-party cloud to the database gateway.<br><br>Add the IP address of the DTS server to the allowlist of the self\-managed database. |
|The source or destination database is deployed in the ECS. |VPC |None.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In this scenario, the system automatically adds the IP address of the DTS server to the ECS security rules. You do not need to manually add it.</div><br> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">You can click <strong>View DTS IP segment</strong> in the <strong>Source database information</strong> area on the <strong>Configuring source and target database</strong> page to view and copy the CIDR block.</div>


* <div data-tips="true" data-tips-type="tip">You can also check the migration objects in the source database and destination database and make appropriate preparations based on the description in the precheck items. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql">Pre\-check items</a>.</div>
