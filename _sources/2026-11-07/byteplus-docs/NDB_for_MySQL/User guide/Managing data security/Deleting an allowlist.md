---
title: "Deleting an allowlist"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_an_allowlist"
---

This article describes how to delete an allowlist that is no longer needed through the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

All instances in the allowlist are disassociated from the allowlist. For information about how to disassociate an instance from an allowlist, see [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Disassociating_instance_and_allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the allowlist.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, select the target allowlist actions column for  **...**  \> **Delete**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the allowlist is associated with an instance, deletion is not allowed. You need to click the target allowlist name first, disassociate the instance in the <strong>Allowlist information</strong>, and then delete it. After instances are disassociated from the allowlist, IP addresses in the allowlist can no longer be used to access the instances in the database. Please proceed with caution.   </div>
   

5. Click **OK** in the pop\-up dialog box.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteAllowList) |Call the DeleteAllowList to delete the allowlist. |
