---
title: "Connecting to an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/connect_instance"
---

Adding an allowlist for the MySQL instance IP addresses enables a successful connection to the instance. This topic describes how to connect to a MySQL instance by using a client or the command line.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and is in the **Running** state. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A database and an account have been created. For details, refer to [Creatig a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database) and [an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account).

* An allowlist has been associated with the instance. For details, refer to [Associating an instance with an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_instances_to_allowlists).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


* Method 1: Connect to an instance with a client. For more information, refer to [Connecting to an jnstance via client program](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_client_application).

* Method 2: Connect the instance via the command line. The operation steps are as follows.

1. Install MySQL. The following method uses a Linux system as an example:

   * CentOS: Run `yum install mysql`.

   * Ubuntu: Run `apt-get update` and then run `apt install mysql-server`.

2. Log on to the server from which you want to connect to MySQL, for example, an ECS server or a local server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on how to log on to an ECS, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance">Log on to an ECS instance</a>.   </div>
   

3. Use the command line to establish a connection.

   ```Plain Text
   mysql -h<连接地址> -P<端口> -u<用户名> -p -D<数据库名称>
   ```
   

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Note that \-P (uppercase) is used for the port, and \-p (lowercase) is for the password.   </div>
   

Refer to the following table for a description of connection addresses and ports for MySQL instances.


|Option |Note |Example |
|---|---|---|
|\-h |The private or public address of the MySQL instance. For information on how to get the private or public address, refer to [Connecting to an instance via private network](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port) and [Applying for or releasing a public address](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access). |rds\-mysql\-hb3c8a96e9119\*\*\*.rds.ivolces.com |
|\-P |The port number of the MySQL instance. If you connect via private network, enter the private network address port of the MySQL instance. If you connect via public network, enter the Port for the MySQL instance. P must be uppercase, and the default Port is 3306. If the port number is the default port, this parameter is optional. |3306 |
|\-u |The account name in the MySQL instance. |testuser |
|\-p |Password for the account above. Note: To ensure password security, do not enter the password after \-p. You will be prompted to enter the password after running the entire command. After entering the password, press Enter to log on. If you specify this parameter, do not add a space between \-p and the password. |PassWord123 |
|\-D |The name of the database to log on to. This parameter is optional. You can omit \-D and only enter the database name. |mysql |


Example command:

```Plain Text
mysql -hrds-mysql-hb3c8a96e9119****.rds.ivolces.com -P3306 -utestuser -p
```


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBInstanceEndpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints) |Call the DescribeDBInstanceEndpoints API to query the list of connection addresses of the instance. |
