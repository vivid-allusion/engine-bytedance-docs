---
title: "When the source database is MySQL, after enabling the binlog and setting the parameter binlog_format to row and binlog_row_image to full, how can I ensure that the parameter format takes effect immediately?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/how_can_I_bring_parameter_format_immediately_effective"
---

You can ensure that the parameter format has taken effect through the following methods to prevent business connections from continuing to use the old format to write.


1. During non\-business periods, interrupt all business connections in the current database.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before the end of this step, do not create or start a migration task, otherwise it will cause the task to fail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the source database is on the slave, you also need to reset the primary\-secondary synchronization SQL thread.   </div>
   

   1. Log in to the source database via the official MySQL client or other tools.

   2. Execute the following command to query all business connections in the current database. This step will display all business connections other than all Binlog Dump connections and the current connection.

      ```shell
      show processlist;
      ```
      

   3. Interrupt all business connections found in the previous step.

2. In order to prevent the format of parameter `binlog_format` and parameter `binlog_row_image` from becoming invalid due to database restarts, please add or modify the configuration parameters `binlog_format` and `binlog_row_image` in the source database's startup configuration file (that is, `my.ini` or `my.cnf`, etc.) and save them. The specific parameter information is as follows.

   ```shell
   binlog_format = row;
   binlog_row_image = full;
   ```
