---
title: "Download and parse Binlog logs"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Download_and_parse_Binlog_logs"
---

This article describes how to remotely obtain the Binlog logs of NDB for MySQL instance, and view and parse the Binlog logs using the mysqlbinlog tool.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Install **MySQL 8.0** on your local device or ECS environment.

2. Connect NDB for MySQL instance through the MySQL client side. For detailed steps, see [Connecting to an Instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Connecting_to_an_instance).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Both RW and RO nodes can access Binlog logs. You can view Binlog logs by Primary node endpoint, Default endpoint, and Custom endpoint address.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Super accounts have access to Binlog logs by default. If you use a normal account to obtain Binlog logs, you need to first grant permissions to the normal account using a super account. For detailed steps, see <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Log_faq#如何使用普通账号查看-binlog-日志？">How to view Binlog logs with a normal account</a>.   </div>
   

3. Execute `show binary logs;` and view the Binlog file.

   ```SQL
   MySQL [(none)]> show binary logs;
   +---------------------+-----------+-----------+
   | Log_name            | File_size |  Encrypted|
   +---------------------+-----------+-----------+
   | mysql-binlog.000001 |       156 | No        |
   | mysql-binlog.000002 |      6558 | No        |
   +---------------------+-----------+-----------+
   2 rows in set (0.00 sec)
   ```
   

4. Execute `exit` to exit MySQL. Execute the following statement on the client side to remotely retrieve the Binlog log and save it locally.

   ```bash
   mysqlbinlog -u<usernam> -p -h<connection address> --read-from-remote-server --raw mysql-binlog.**
   ```
   

   Examples:

   ```bash
   mysqlbinlog -utest_user -p -hvedbm-7eukjwtg****.default.mysql.vedb.ivolces.com --read-from-remote-server --raw mysql-binlog.000002
   ```
   

5. Execute the following command to view the Binlog log file content through the mysqlbinlog tool and output the content to the specified file.

   ```bash
   mysqlbinlog -vv --base64-output=decode-rows mysql-binlog.000002 >> binlog2.txt
   ```
   

   Check out the specific content:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3fed0a0c11d1361dbb66f8d4bd7201db.png) </span>

6. Parsing Binlog logs, see [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/mysqlbinlog.html?spm=a2c4g.11186623.2.15.374d5c0cnwMeJd).
