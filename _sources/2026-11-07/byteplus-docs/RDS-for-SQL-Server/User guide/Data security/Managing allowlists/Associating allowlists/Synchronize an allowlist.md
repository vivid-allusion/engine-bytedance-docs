---
title: "Synchronize an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Synchronize_allowlist"
---

If you modify the allowlist when the instance is not running, its synchronization status will show as out of sync **.**  To complete allowlist synchronization immediately, you can manually perform the sync operation. This topic explains how to manually synchronize allowlists.

<span id="WxU5u7LQ"></span>
## **Prerequisites**


* The instance has been [created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and is not running.

* In the list of associated instances, the synchronization status shows out of sync.


<span id="6op9r4LH"></span>
## Precautions

The service automatically synchronizes allowlist information every 30 minutes. You can wait for automatic synchronization in non\-urgent cases. In urgent situations, follow the steps below to manually synchronize the allowlist.

<span id="fnwvA4Em"></span>
### Operation Steps


1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the target project and region.

3. There are two entries to **Synchronize allowlist**:

   * Entry 1:

      1. In the left\-side navigation bar, click **Allowlists**.

      2. Click the target allowlist to open the allowlist details panel.

      3. In the allowlist details panel, under **List of associated instances**, click **Synchronize allowlist** in the **Actions** column to manually synchronize the allowlist.

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Note         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If the instance has already synchronized the latest allowlist IP information, the <strong>Synchronize allowlist</strong> option will be unavailable.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The allowlist synchronization has an automatic mechanism that syncs the allowlist information of instances every 30 minutes.         </div>
         

   * Entry 2: **Instances ** \> Click the target instance name \> Click the **Security** tab \> Click the **Allowlist** sub\-tab \> Click the target allowlist name \> Under **List of associated instances**, click **Synchronize allowlist** in the **Actions** column.
