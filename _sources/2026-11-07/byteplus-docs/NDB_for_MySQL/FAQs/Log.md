---
title: "Log"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Log_faq"
---

<span id=".YmlubG9nLeeahOS_neeVmeaXtumXtOaYr-WQpuWPr-S7peaJi-WKqOS_ruaUue-8nw=="></span>
### Can the Binlog retention period be manually modified?

Manual binlog retention modification is supported for MySQL 8.0 compatible instances, but not for MySQL 5.7 compatible instances.

The Binlog retention period (`vedb_binlog_expire_logs_seconds`) defaults to 432,000 seconds (5 days) and can be modified in the **Parameters** tab. For steps, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).

<span id=".dmVkYi1teXNxbC3lj6ror7voioLngrnkuIrmnIktYmlubG9nLeaXpeW_l-WQl--8nw=="></span>
### Are there Binlog files on read\-only nodes in NDB for MySQL?

Yes. Connect to the read\-only endpoint and execute the `show binary logs;` command to view existing binary file lists and sizes.

<span id=".5aaC5L2V5L2_55So5pmu6YCa6LSm5Y-35p-l55yLLWJpbmxvZy3ml6Xlv5fvvJ8="></span>
### How to view Binlog with a normal account?

By default, normal accounts do not have Binlog read access. A super account can grant permissions with these steps.


1. Log on to the NDB for MySQL database using a super account. For steps, refer to [Connecting to an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connecting_to_an_instance).

2. Execute the following SQL to grant Binlog access permissions to a normal account.

   ```sql
   GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'username'@'%';
   FLUSH PRIVILEGES;
   ```
   

3. Execute the `show binary logs;` command to view existing binary file lists and sizes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For downloading and parsing Binlog, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Download_and_parse_Binlog_logs">Download and parse Binlog</a>.   </div>
   

<span id="lw00F75D"></span>
### How to query operation records for tables in an instance and operation records for a specific IP.

You can view the operations performed on database tables and the operation records of specific IPs through audit logs. For more information about audit logs, refer to [Database audit management](https://docs.byteplus.com/en/docs/DBW/Database_audit_management) and [SQL insights and auditing management](https://docs.byteplus.com/en/docs/DBW/Full_SQL_insight_management).

<span id="iejORRJD"></span>
### How do I clean up the Binlog of NDB for MySQL instance?

NDB for MySQL controls the Binlog retention period with the `vedb_binlog_expire_logs_seconds` parameter. The default retention period is 432,000 seconds (5 days), and you can adjust it based on your business needs. For operation steps, see [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).
