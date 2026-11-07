---
title: "Deleting or unsubscribing an instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_or_unsubscribing_an_instance"
---

This topic describes how to manually release pay\-as\-you\-go PostgreSQL instances or unsubscribe from PostgreSQL yearly/monthly subscription instances according to your service requirements.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Once an instance is deleted or unsubscribed from, its associated read\-only nodes are also deleted or unsubscribed from.

* Deleted or unsubscribed instances are removed from the instance list. The backup file is displayed in the **Backups of deleted instances** list and retained for seven days.


<span id=".5Yig6Zmk5a6e5L6L"></span>
## Deleting an instance


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. Go to the **Instances** page, click  **…**  \> **Delete instance** in the **Actions** column of the target instance.

5. Enter the name of the instance to delete and click **OK** in the pop\-up dialog box.


<span id=".6YCA6K6i5a6e5L6L"></span>
## Unsubscribe instance


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. Go to the **Instances** page, click  **…**  \> **Unsubscribe instance** in the **Actions** column of the target instance.

5. On the **Unsubscribe management** page, select the target instance to unsubscribe.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Deleting a pay\-as\-you\-go instance does not involve unsubscription, with no refund involved.</div>


* <div data-tips="true" data-tips-type="tip">Subscription instances support unconditional unsubscription within seven days. For detailed refund rules, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management">Unsubscription Management</a>.</div>
