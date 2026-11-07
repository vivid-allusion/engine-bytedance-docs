---
title: "Viewing ArkClaw audit logs"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_audit_logs"
---

Audit logs record historical ArkClaw operations performed by enterprise employees. Intended for administrators, security and compliance officers, and auditors, these logs enable action traceability and accountability, while meeting platform compliance control and external audit requirements. This topic describes how to view audit logs.

<span id="PrDrT8VR"></span>
## Background information

Audit logs record operations (such as creation, deletion, and modification) on ArkClaw\-related resources. Currently, login logs and query logs are not captured. The specific audit items are as follows:


|Resource type |Audit event |
|---|---|
|Managing users |* Create user/Batch create user/Update user/Batch update user/Delete user/Batch delete user/Batch synchronize user<br><br>* Create department/Batch create department/Delete department/Add department member/Batch add department member/Remove department member/Update department<br><br>* Create user group/Delete user group/Add user group member/Remove user group member/Update user group<br><br>* Create user pool/Delete user pool/Update user pool/Update IDP<br><br>* Obtain sensitive user information in plaintext / Enable user information masking / Disable user information masking |
|Claw management |* Create / Creating<br><br>* Start / Starting / Stop / Stopping / Restart / Restarting / Reset / Resetting / Update / Updating<br><br>* Delete / Deleting / Deleted successfully / Deletion failed / Permanently deleting / Permanently deleted / Permanent deletion failed / Move to recycle bin / Restore from recycle bin / Reclaiming due to expiration / Expiration\-caused reclaim failed / Reclaimed due to expiration<br><br>* Recovering after renewal / Recovery failed after renewal / Recovery succeeded after renewal / Suspending due to arrears / Suspension due to arrears failed / Suspension due to arrears succeeded<br><br>* Bind tags / Unbind tags<br><br>* Backup creation in progress / Backup created successfully / Backup creation failed / Enable or disable automatic backup<br><br>* Auto repair in progress / Repair succeeded / Repair failed<br><br>* Change seat editions / Enable or disable observability data masking |
|Claw spaces |* Create / Creating<br><br>* Update / Updating<br><br>* Delete / Deleting / Deletion failed |
|Skills |Create skills / Delete skills / Download skills |
|O&M |Create version upgrade job / Create O&M tasks |


<span id="aJy557Ab"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Administrators or enterprise employees have created ArkClaw instances and performed management operations on them. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).


<span id="Jpubntku"></span>
## Limits

Audit logs are retained by default for 30 days.

<span id="0xnimSi7"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **O&M \> Audit Logs** to view audit logs.



|Item |Description |
|---|---|
|Viewing logs |Each log records critical information, such as event name, resource name, resource ID, result, operator ID, operator email address, and operation time. |
|Searching for logs |* You can filter log records for the following time ranges: last 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 3 days, 7 days, or a custom timeframe.<br><br>* You can search for logs by event name and resource ID. |


&nbsp;
