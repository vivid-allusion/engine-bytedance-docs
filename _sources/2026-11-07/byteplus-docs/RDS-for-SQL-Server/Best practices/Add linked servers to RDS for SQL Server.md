---
title: "Add linked servers to RDS for SQL Server"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/adding-linked-server-to-rds-for-sql-server"
---

When you need a database in an RDS for SQL Server instance A to access a database in a SQL Server instance B (an RDS for SQL Server instance or a local SQL Server instance), you can create a linked server on instance A to access instance B. This topic describes how to add a linked server on SQL Server instance A to access SQL Server instance B.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Two instances have been created and are in the Running state. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* You have connected to the instance using SQL Server Management Studio. For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-instance).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* RDS for SQL Server instance A and SQL Server instance B must be in the same VPC.

* The IP addresses of the primary and secondary nodes for both instance A and instance B must be added to the allowlist associated with the instances.

* Ensure that instance B listens on port 1433.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Obtain the IP addresses of the primary and secondary nodes

   1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

   3. In the left navigation bar, click **Instances**.

   4. On the **Instances** page, click the name of the target instance.

   5. On the instance details page, click **Connection management**.

   6. On the **Connectivity** tab, hover over the **Primary node** and **Secondary node** cards to get the IP addresses of the primary and secondary nodes.

2. Create an allowlist

   1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

   3. In the left\-side navigation pane, click **Allowlists**.

   4. On the **Allowlists** page, click **Create allowlist**.

   5. In the **Create allowlist** pane, configure the following information.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Allowlist name** |Custom allowlist name. Naming rules are as follows:<br><br><br>* Must start with a Chinese character, letter, or underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The length must be between 1 and 32 characters, and the name is unique. |
      |**Description** |The description can be used to search for an allowlist in the allowlists. The description cannot exceed 200 characters. |
      |**IP address** |Enter the IP addresses of the primary and secondary nodes for instances A and B. |
      

   6. Click **OK**.

3. Associate allowlist

   1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

   3. In the left\-side navigation pane, click **Allowlists**.

   4. On the **Allowlists** page, click **Associate instance** in the **Actions** column of the target allowlist.

   5. In the **Associate instance** panel, select instance A and instance B, and click **OK**.

4. Add a Linked Server

   1. Connect to the instance using SQL Server Management Studio. For details, see [Connect to instance A](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-instance).

   2. In the top menu bar, click **New Query** and configure the following script to create a linked server.

      ```sql
      USE [master]
      GO
      EXEC master.dbo.sp_addlinkedserver @server = N'BBBB', @srvproduct=N'BBBB', @provider=N'SQLNCLI', @datasrc=N'mssqlc9b90c50****.rds-mssql.ivolces.com,1433'
      EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname = N'BBBB', @locallogin = NULL , @useself = N'False', @rmtuser = N'veyun_user', @rmtpassword = N'********'
      GO
      ```
      

      
      |**Parameter** |**Description** |
      |---|---|
      |`@server` |Linked server name. |
      |`@srvproduct` |Database name. |
      |`@provider` |Use the default value `SQLNCLI`. |
      |`@datasrc` |The private IP address/private domain name and port for instance B.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Ensure that instance B listens on port 1433.</div><br> |
      |`@rmtsrvname` |Linked server name. |
      |`@rmtuser` |The account name, with `veyun_user` as the default. |
      |`@rmtpassword` |Account password. |
      

   3. After you finish writing the script, you can right\-click the target database and select **Test connection**.

   4. If the message "**Test connection to the linked server succeeded**" is displayed in the **Linked Server** dialog box, the linked server is successfully created.
