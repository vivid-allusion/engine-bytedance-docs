---
title: "How to view the log_reuse_wait_desc attribute value of a database?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/log_reuse_wait_desc_attribute_value"
---

This topic describes how to view the `log_reuse_wait_desc` attribute value of a database. There are two methods:


* **Method 1**: View in the BytePlus console.

   1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

   3. In the **Instances**, click the name of the target instance.

   4. Go to the **Summary** page and click the **Database management** tab at the top of the page.

   5. Click **View properties** in the **Actions** column of the target database.

   6. View the value of the `log_reuse_wait_desc` attribute.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <code>log_reuse_wait_desc </code> attribute value is <code>NOTHING</code>, then you can shrink the transaction log.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <code>log_reuse_wait_desc</code> attribute value is <code>LOG_BACKUP</code>, wait for the next log backup to finish and the attribute value to change to <code>NOTHING</code> before shrinking the transaction log.      </div>
      

* **Method 2**: View in SQL Server Management Studio (SSMS).

   1. Create a new query window and enter the following SQL statement. For example, to view the `log_reuse_wait_desc` attribute value for testDB, replace testDB with the target database name in the SQL statement.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1be0c60b7f417869613a11d9dc2c801c.png) </span>

      ```SQL
      SELECT log_reuse_wait_desc, name FROM sys.databases WHERE name = N'testDB'
      ```
      

   2. Click **Execute**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d60ea8a66307629298ae0b6ecf76e2f2.png) </span>

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <code>log_reuse_wait_desc</code> attribute value is <code>NOTHING</code>, then you can shrink the transaction log.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <code>log_reuse_wait_desc</code> attribute value is <code>LOG_BACKUP</code>, wait for the next log backup to finish and the attribute value to change to <code>NOTHING</code> before shrinking the transaction log.      </div>
