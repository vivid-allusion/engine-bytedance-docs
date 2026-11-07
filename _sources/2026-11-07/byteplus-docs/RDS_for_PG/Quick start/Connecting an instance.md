---
title: "Connecting an instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/connect_instance"
---

After adding the PostgreSQL instance's IP allowlist, you can successfully connect to the instance. This topic describes the procedure to connect to a PostgreSQL instance via a client or command line.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* For more information, refer to [Creating databases and accounts](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts).

* [An allowlist has been configured](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_an_allowlist).

* If you are using an ECS instance for connection, please associate a private network and subnet to the instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


* Method 1: Connect to an instance with a client. For more information, refer to [Connecting to an jnstance via client program](https://docs.byteplus.com/en/docs/RDS_for_PG/connecting_to_an_instance_via_a_client_application).

* Method 2: Connect the instance via the command line.

1. Log on to the server that needs to connect to PostgreSQL, such as an ECS instance or local server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on how to log on to an ECS, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance">Log on to an ECS instance</a>.   </div>
   

2. Use the command line to establish a connection.


Once PostgreSQL is installed on the server, you can connect to the PostgreSQL database with the command line tool in the following method:

```Plain Text
psql -h <连接地址> -p <端口> -U <用户名> -d <数据库名称>
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Please use lower\-case letters for ports (\-p).</div>


Refer to the following table for a description of addresses and ports for PostgreSQL instances.


|Option |Note |Example |
|---|---|---|
|\-h |The private or public network address of the PostgreSQL instance. For information on how to get the private or public address, refer to [Connecting to an instance via private network](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_access_address_and_port) and [Applying for or releasing a public network address](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access). |postgresbcc087e73689\*\*\*\*.rds\-pg.ivolces.com |
|\-p |Port number of the PostgreSQL instance. You can connect to PostgreSQL instances after adding IP address allowlists to the PostgreSQL instances. This topic describes how to connect to a PostgreSQL instance via the client and command line tool. You can connect to PostgreSQL instances after adding IP address allowlists to the PostgreSQL instances. This topic describes how to connect to a PostgreSQL instance via the client and command line tool. |5432 |
|\-U |Account name in the PostgreSQL instance. |testuser |
|\-d |Name of the database to log on to. Note: you can omit "\-d" and enter the database name only. |db01 |


Example command:

```Plain Text
psql -h postgresbcc087e73689****.rds-pg.ivolces.com -p 5432 -U testuser -d db01
    
```
