---
title: "What should I do if I encounter the error error 1054 (42s22): unknown column 'my_row_id' in 'field list' when synchronizing data from Volcano Engine MySQL 8.0 to 5.7?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_should_I_do_if_I"
---

What should I do if I encounter the error error 1054 (42s22): unknown column 'my_row_id' in 'field list' when synchronizing data from BytePlus MySQL 8.0 to BytePlus MySQL 5.7?


* **Possible cause**: BytePlus MySQL 8.0 automatically adds the Primary key` my_row_id` to tables without Primary keys. However, BytePlus MySQL 5.7 does not have this column. Therefore, when synchronizing data from BytePlus MySQL 8.0 to BytePlus MySQL 5.7, the error message `Error 1054 (42s22): unknown column 'my_row_id' in 'field list'` might occur. When synchronizing data from BytePlus MySQL 5.7 to BytePlus MySQL 8.0, the `Error 1054 (42s22): unknown column 'byte_rds_ai_uk_row_id' in 'field list'` might occur.

* **Solution**: When creating a BytePlus MySQL 8.0 synchronization data to BytePlus MySQL 5.7 task or creating a BytePlus MySQL 5.7 synchronization data to BytePlus MySQL 8.0 task, you need to enable etl and configure the corresponding etl filter function to filter hidden primary keys. The ETL filter function is as follows:

   ```lisp
   (defn main []
     (case (car (dts/pk))
           "my_row_id" (dts/drop-column "my_row_id")
           "byte_rds_ai_uk_row_id" (dts/drop-column "byte_rds_ai_uk_row_id")))
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about etl, refer to <a href="https://docs.byteplus.com/en/docs/DTS/brief_introduction_to_etl">ETL introduction</a>.   </div>
