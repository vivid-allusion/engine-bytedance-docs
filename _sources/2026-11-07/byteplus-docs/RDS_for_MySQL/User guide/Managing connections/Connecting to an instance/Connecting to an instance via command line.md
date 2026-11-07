---
title: "Connecting to an instance via command line"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_command_line"
---

Adding an allowlist for the MySQL instance IP addresses enables a successful connection to the instance. This topic describes how to connect to a MySQL instance via the command line.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A database and an account have been created. For details, refer to [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3).

* An allowlist has been configured. For details, refer to [Associating an allowlist with an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).

* If you are using an ECS instance for connection, ensure that the ECS and the MySQL instance belong to the same virtual private cloud and a subnet.

* (Optional) If the verification method for the database account is IAM verification, you need to [create an IAM authentication policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_IAM_authentication_policy).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the server from which you want to connect to MySQL, for example, an ECS server or a local server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance">Log on to an ECS instance</a>.   </div>
   

2. Install MySQL. The following method uses a Linux system as an example:

   * CentOS: Run `yum install mysql`.

   * Ubuntu: Run `apt-get update` and then run `apt install mysql-server`.

3. Use the command line to establish a connection.



<Tabs>
<Tab zoneid="RKFYtECkhp" title="The verification method for the database account is IAM verification">
<TabTitle>The verification method for the database account is IAM verification</TabTitle>

<span id="ePB7dssd"></span>
### Syntax

```Shell
mysql -h<连接地址> -P<端口> --enable-cleartext-plugin -u<数据库账号> -p'<临时 Token>'
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Use the uppercase `\-P` for the port and the lowercase `\-p` for the password.</div>


<span id="NIaPOa9D"></span>
### Parameter description


|Options |Description |Sample |
|---|---|---|
|\-h<br><br> |The private or public address of the MySQL instance. For information on how to get the private or public address, refer to [Connecting to an instance via private network](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port) and [Applying for or releasing a public address](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access). |rds\-mysql\-hb3c8a96e9119\*\*\*.rds.ivolces.com |
|\-P |The port number of the MySQL instance. If you connect via private network, enter the private network address port of the MySQL instance. If you connect via public network, enter the Port for the MySQL instance. P must be uppercase, and the default Port is 3306. If the port number is the default port, this parameter is optional. |3306 |
|\-u |The database account name in the MySQL instance. |testuser |
|\-p |The temporary token of the database account. For the method to acquire a temporary token, refer to [Generating a temporary token](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Generating_a_temporary_token?lang=en). Since the generated temporary token contains the ampersand (&), you must enclose the token with single quotation marks ('') to prevent parsing errors. |Action=ConnectDatabase&DBUser=yzh&InstanceId=mysql\-41186f538XXXX |


<span id="8uxzdd13"></span>
### Sample

```Shell
mysql -hrds-mysql-hb3c8a96e9119****.rds.ivolces.com -P3306 --enable-cleartext-plugin -utestuser -p'Action=ConnectDatabase&DBUser=yzh&InstanceId=mysql-41186f538XXXX'
```



</Tab>
<Tab zoneid="dTNmBpg1af" title="The verification method for the database account is password">
<TabTitle>The verification method for the database account is password</TabTitle>

<span id="PIKb60VP"></span>
### Syntax

```Plain Text
mysql -h<连接地址> -P<端口> -u<用户名> -p<密码> -D<数据库名称>
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Use the uppercase `\-P` for the port and the lowercase `\-p` for the password.</div>


<span id="W3biTzFh"></span>
### Parameter description


|Options |Description |Sample |
|---|---|---|
|\-h |The private or public address of the MySQL instance. For information on how to get the private or public address, refer to [Connecting to an instance via private network](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port) and [Applying for or releasing a public address](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access). |rds\-mysql\-hb3c8a96e9119\*\*\*.rds.ivolces.com |
|\-P |The port number of the MySQL instance. If you connect via private network, enter the private network address port of the MySQL instance. If you connect via public network, enter the Port for the MySQL instance. P must be uppercase, and the default Port is 3306. If the port number is the default port, this parameter is optional. |3306 |
|\-u |The database account name in the MySQL instance. |testuser |
|\-p |The password of the database account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To ensure password security, do not enter the password after \-p. You are prompted to enter the password after the command is run. Press Enter after entering the password to log on. If you specify this parameter, do not add a space between \-p and the password.</div><br> |PassWord |
|\-D |The name of the database to log on to. This parameter is optional. You can omit \-D and only enter the database name. |mysql |


<span id="MkZuvQ0c"></span>
### Sample

```Plain Text
mysql -hrds-mysql-hb3c8a96e9119****.rds.ivolces.com -P3306 -utestuser -p
```



</Tab>
</Tabs>


<span id="tWCv2mcM"></span>
## FAQ

**Why can't I connect to the database?** 

If you cannot access a database, please conduct troubleshooting as recommended:


* Confirm that the MySQL instance is **Running**.

* Confirm whether an [account has been created](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3) for the instance.

* Check if an [IP allowlist group](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances) is configured.

* If connecting via a private network, confirm that the ECS instance and the database instance are in the same VPC.


If you still cannot connect to the MySQL instance after troubleshooting, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBInstanceEndpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints) |Call the DescribeDBInstanceEndpoints API to query the list of connection addresses of the instance. |
