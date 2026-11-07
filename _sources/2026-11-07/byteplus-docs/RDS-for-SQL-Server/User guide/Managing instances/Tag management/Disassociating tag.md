---
title: "Disassociating tag"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-tag"
---

After binding the tag for the specified instance, the instance tag can be untied at any time according to the business requirements. This document describes the steps to disassociate tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Support batch disassociating of instances and tags, up to 20 tags per batch.</div>


<span id="untagging-a-single-instance"></span>
## **Untagging a single instance**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance List** page, locate the target SQL Server instance and click the Edit icon in its corresponding **Tag** column. You can also click the name of the target instance and click the edit icon in the tab line of the basic infor area.

4. In the pop\-up **Edit tag** window, locate the specified tag key and click **Delete**.

5. Click **OK**.


<span id="untagging-multiple-instances"></span>
## **Untagging multiple instances**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Select all instances that need to be taged in the **instance list**, and click **Disassociate tags** in the lower left corner of the page.

4. Select the tag key to delete in the drop\-down list in the pop\-up **Disassociate tag** window, or enter the tag key to filter.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page displays the number of selected instances corresponding to the specified tag, that is, how many instances in the selected instance list are bound to the tag key. When Disassociateing tags, all tags corresponding to the specified tag key in the selected instance list are unbound, and instance tags that are not in the selected list do not involve adjustment.   </div>
   

5. Click **OK**.
