---
title: "How to obtain the instance's GTID_EXECUTED?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance"
---

You can obtain the instance's GTID_EXECUTED through the following actions.


1. Log on to the server that needs to connect to MySQL, such as an ECS server or a local server.

   For the operation steps on how to log on to an ECS, refer to [Log on to an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to connect to the target instance.

   ```shell
   mysql -h<Connection URL> -P<Port> -u<UserName> -p -D<DataName>
   ```
   

   Parameter description

   
   |**Parameter** |**Description** |
   |---|---|
   |\-h |The internal or external network connection address of the MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For information on how to get the private or public address, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port">Connecting to an instance via private network</a> and <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access">Applying for or releasing a public address</a>.</div><br> |
   |\-P |The port number of the MySQL instance. The port number varies depending on the connection address, as follows:<br><br><br>* When using an internal network connection, you must enter the internal network port of the MySQL instance.<br><br>* When using an external network connection, you must enter the external network port of the MySQL instance. `P` must be capitalized, and the default port is 3306. If the port number is the default port, this parameter can be left blank. |
   |\-u |The account name in the MySQL instance. |
   |\-p |The password of the account in the MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure password security, do not enter the password after <code>-p</code>. You are prompted to enter the password after the command is run. Press Enter after entering the password to log on. If this parameter is filled in, a space is not allowed between <code>-p</code> and password.</div><br> |
   |\-D |The name of the database to log on to. This parameter is optional. You can omit `-D` and enter only the database name. |
   

3. Execute the following command to obtain the instance's GTID_EXECUTED.

   ```shell
   show master status
   ```
   

   Execution result example

   ```shell
   +---------------+------------------+--------------+------------------+---------------------------------------------------+
   | File          | Position         | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set.                                |
   +---------------+------------------+--------------+------------------+---------------------------------------------------+
   | binlog.000992 | 302355           |              |                  |  5d3ffd44-9614-11ed-aaf2-5254ac13e820:1-3514674   |
   +-------------+--------------------+--------------+------------------+---------------------------------------------------+
   1 row in set (0.01 sec)
   ```
   


You can view the execution results in `Executed_Gtid_Set.` Get the GTID_EXECUTED of the instance from 中, that is, the value of this example is `5d3ffd44-9614-11ed-aaf2-5254ac13e820:1-3514674`.
