---
title: "Connecting to an instance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connecting_to_an_instance"
---


NDB for MySQL supports connecting to instances via both connection addresses and IP addresses. This article describes how to use the client to connect to the NDB for MySQL instance.

<span id="PVYlCXZG"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The database and account have been created. For specific operations, refer to [Creating a database](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_database) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The cloud server ECS has been prepared, and it has been confirmed that the ECS instance and the NDB for MySQL instance belong to the same private network.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This prerequisite only applies when connecting instances over a private network.   </div>
   

* The [allowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist) is configured.

   * If you are accessing through a public network, you need to add the IP address of the local device or public server to the whitelist.

   * If you access the server through a private network, you need to add the IP address of the cloud server ECS to the whitelist.


<span id="4AIephvE"></span>
## Connection method


1. Install the MySQL client. The client version must be consistent with the NDB for MySQL instance version.

   * If you access it through a private network, you need to install the MySQL client on the cloud server ECS. For more information about logging into Cloud as a Service, see [Logging on to an ECS Instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   * For access through the public network, you need to install the MySQL client side on the local device or the public network Cloud as a Service.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If MySQL client side is installed, execute the <code>mysqladmin -V</code> command to confirm the client side version.      </div>
      

2. Execute the following command to connect to the NDB for MySQL database.

   ```sql
   mysql-h<Connection address or IP address> -P<Port> -u<Username> -p-D<Database name>
   ```
   

   
   |Option |example |Description |
   |---|---|---|
   |\-h |* Connection address: vedbm\-5nvxrkj0\*\*\*\*.default.mysql.vedb.ivolces.com<br><br>* IP：192.168.\*\*\*.\*\*\* |The connection address or IP of the private or public network connecting the endpoint.<br><br>For information on how to obtain the connection address and IP, see [Viewing connection endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_connection_endpoints). |
   |\-P |3306 |The port number of the connection address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">P needs to be capitalized. The default port is 3306.</div><br> |
   |\-u |vedbMySQLUser |The name of the account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It can be a super account or a normal account. For more details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts">Creating an account</a>.</div><br> |
   |\-p |passWord123 |Password of the account above. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure password security, don't fill in the password after \-p. When you are prompted to enter the password after executing the whole line of commands, enter it and press Enter to log in. If this parameter is filled in, a space is not allowed between \-p and password.</div><br> |
   |\-D |vedbmysqlDB |The name of the database to log in to.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required. You can enter the database name without entering \-D.</div><br> |
