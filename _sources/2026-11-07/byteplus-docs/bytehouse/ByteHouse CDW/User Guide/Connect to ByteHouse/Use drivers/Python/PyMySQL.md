---
title: "PyMySQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/pymysql"
---

PyMySQL is a Python driver that enables applications to connect to the ByteHouse Cloud Data Warehouse. This allows you to leverage Python's powerful libraries for data analysis, machine learning, and application development directly with your data in ByteHouse. This document will guide you through installing the driver and using it to connect to and interact with ByteHouse.

<span id="ac958e5a"></span>
# Environment requirements

Requires Python 3.12 or higher.

<span id="01715534"></span>
# Recommended version

Use the latest version of PyMySQL Driver [v1.1.2](https://github.com/PyMySQL/PyMySQL/releases/tag/v1.1.2).

<span id="c0eac089"></span>
# Restrictions


* Setting a query ID is not supported yet.

* Setting a virtual warehouse at the connection level is not supported yet.

* ByteHouse JSONB and Bitmap64 data types are not supported.

* Currently, the ByteHouse MySQL protocol does not support the ComPrepare protocol.

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="c1f10ceb"></span>
# Install PyMySQL driver

<span id="a7f20c00"></span>
## Install the driver from PyPI

The latest version of PyMySQL can be obtained using the following command.

```Plain
python3 -m pip install PyMySQL
```


<span id="e2eed906"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to PyMySQL through IAM users or database users. The differences between IAM users and database users are described as follows. Choose the method that best suits your needs.


* **IAM user** is a user created in BytePlus Access Control (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. They can also access ByteHouse through the CLI, connection drivers, ecosystem tools, and APIs.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="2f626c05"></span>
## Connect using an IAM user

For instructions on connecting to ByteHouse with an IAM user, see [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity).

The following table describes the parameters:


|Param |Connect using IAM user |
|---|---|
|host |When configured as ByteHouse's public or private domain name, you can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Configured as a fixed value of 3306. |
|user & password |* User: The fixed configuration is bytehouse<br><br>* password: ByteHouse API Key. You can obtain the API Key in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|database |The name of the database to connect to. |


<span id="d8cea018"></span>
## Use database user connections

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using database user credentials.

The general parameter description is as follows:


|Param |Use a database user to connect |
|---|---|
|host |When configured as ByteHouse's public or private domain name, you can view and copy the network information in the ByteHouse Console under **Tenant Management** \> **Basic Information** \> **Network Information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it to the fixed value 3306. |
|user & password |* User is configured as `{accountID_or_accountName}::{username}[::{envID}]`. For details, please refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse Console, click the Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username used to log in to the ByteHouse database. You can find it in the **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional configuration. It refers to the name of the environment where the database is located. If using the default environment, configuration is not required; to use another environment, specify the environment name, and do not add `[]` during configuration. You can log in to the **ByteHouse** **Console** and obtain the required information from**Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Usage examples are as follows:<br><br>      * Environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Do not configure environment ID: `21xxxxxxxx::demouser`<br><br>* Password: You can contact your administrator to obtain the password for the database account. If the password is lost or forgotten, you can contact your administrator to reset it. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|database |The database name configured to connect to ByteHouse. |


<span id="82a4a922"></span>
# Basic usage

This section introduces how to connect to ByteHouse using PyMySQL. You can find the latest documentation and release information on the program's [Github homepage](https://github.com/PyMySQL/PyMySQL). Caution: When using the connection statement, make sure to replace connection information fields such as `{Host}`, `{Password}`, `{User}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and many other fields. For information on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/pymysql#e2eed906).


* Timeout configuration: The default value for connect_timeout is 10s, the default value for read_timeout is none, and the default value for write_timeout is none.

* By default, `keepAlive` is not supported. To use this feature, you need to configure the relevant parameters. You can refer to [Configure KeepAlive](https://docs.byteplus.com/docs/bytehouse/pymysql#444a37e9) for details.


<span id="2d9c4542"></span>
## Connect to ByteHouse

You can refer to the example below to set the ByteHouse connection information.

```PHP
host = "{Host}"
port = 3306
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

db_config = {
    'host': host,  
    'port': port,
    'user': user,
    'password': password,  
    'database': database,  
    'charset': 'utf8mb4',
}
```


<span id="2024324f"></span>
## Set a specific virtual warehouse

After creating each connection, set the virtual warehouse configuration.

```Python
    connection.cursor().execute(f"set virtual_warehouse = '{virtual_warehouse_id}'")
```


<span id="444a37e9"></span>
## Configure KeepAlive

If you need to use the `keepAlive` feature at the connection level, perform the following configuration and enable it.

```Bash
def get_conn():
    conn = pymysql.connect(
        host=bytehouse_host,
        user=bytehouse_username,
        port=3306,
        password=bytehouse_password,
        database=bytehouse_db,
        connect_timeout=10
    )
    return conn
sock = mysql_conn._sock
sock.setsockopt(socket.SOL_SOCKET, socket.SO_KEEPALIVE, 1)
if sys.platform == "darwin":
    # macOS uses TCP_KEEPALIVE for idle time
    sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_KEEPALIVE, 60)
else:
    # Linux and others
    sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_KEEPIDLE, 60)
sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_KEEPINTVL, 30)
sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_KEEPCNT, 60)
```


<span id="b6aeff15"></span>
## Complete connection and query example

```Python
import uuid
from datetime import datetime

import pymysql

host = "{Host}"
port = 3306
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

db_config = {
    'host': host,  # Fill in HOST URL
    'port': port,
    'user': user,
    'password': password,  # API key secret
    'database': database,  # Database name
    'charset': 'utf8mb4',
}
try:
    connection = pymysql.connect(**db_config)
    connection.cursor().execute(f"set virtual_warehouse = '{virtual_warehouse_id}'")
    with connection:
        with connection.cursor() as client:
            client.execute("DROP DATABASE IF EXISTS bhpythontest")
            client.execute('DROP DATABASE IF EXISTS bhpythontest')
            client.execute('CREATE DATABASE IF NOT EXISTS bhpythontest')
            client.execute(
            """
            CREATE TABLE IF NOT EXISTS bhpythontest.example (
                    Col1 UInt8
                , Col2 String
                , Col3 FixedString(3)
                , Col4 UUID
                , Col5 Map(String, UInt8)
                , Col6 Array(String)
                , Col7 Tuple(String, UInt8, Array(Map(String, String))) KV
                , Col8 DateTime
            ) Engine = CnchMergeTree() ORDER BY tuple()
            """)

            # Prepare to insert data
            values_list = []
            for i in range(1):
                value = (
                    42,  # uint8(42)
                    'ClickHouse',
                    'Inc',
                    str(uuid.uuid4()),
                    "{'key': 1}",  # Map(String, UInt8)
                    "['Q', 'W', 'E', 'R', 'T', 'Y']",  # Array(String)
                    "('String Value', 5, [{'key': 'value'},{'key': 'value'},{'key': 'value'}])",  # Tuple
                    datetime.now().strftime('%Y-%m-%d %H:%M:%S')
                )
                values_list.append(value)

            # Insert data in batches
            insert_sql = "INSERT INTO bhpythontest.example (Col1, Col2, Col3, Col4, Col5, Col6, Col7, Col8) VALUES(%s, %s, %s, %s, %s, %s, %s, %s)"
            client.executemany(insert_sql, values_list)
            print("Successfully inserted 1000 records")

            # Query a record
            select_sql = "SELECT * FROM bhpythontest.example LIMIT 1"
            result = client.execute(select_sql)
            result = client.fetchone()

            if result:
                print("Query result:")
                print(f"Col1: {result[0]}")
                print(f"Col2: {result[1]}")
                print(f"Col3: {result[2]}")
                print(f"Col4: {result[3]}")
                print(f"Col5: {result[4]}")
                print(f"Col6: {result[5]}")
                print(f"Col7: {result[6]}")
                print(f"Col8: {result[7]}")

            # Delete a table
            drop_sql = "DROP TABLE IF EXISTS bhpythontest.example"
            client.execute(drop_sql)
            print("Table deleted")
            client.close()
except Exception as e:
    print(f"Operation failed: {e}")
```


&nbsp;
