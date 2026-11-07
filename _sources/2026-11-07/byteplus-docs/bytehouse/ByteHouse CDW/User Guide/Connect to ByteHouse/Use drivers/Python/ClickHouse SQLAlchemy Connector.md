---
title: "ClickHouse SQLAlchemy Connector"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/clickhouse-sqlalchemy-connector"
---

This tutorial introduces how to use ClickHouse SQLAlchemy Connector to connect to and access the ByteHouse Cloud Data Warehouse.

<span id="42980168"></span>
# Environment requirements

Python 3.12 or higher is recommended.

<span id="bed25a21"></span>
# Recommended version


|**Detailed items** |**Verified versions/Important notes** |
|---|---|
|SQLAlchemy version |[2.0.38](https://pypi.org/project/SQLAlchemy/2.0.38/) |
|ByteHouse clickhouse\-connect support package version |[0.3.2+bytehouse](https://github.com/bytehouse-docs/ecosystem/tree/main/dist/clickhouse-sqlalchemy)<br><br>Note: Because ByteHouse does not natively support the open\-source ClickHouse SQLAlchemy Connector, you also need to use the ByteHouse clickhouse\-connect support package to modify the open\-source connector for compatibility. |
|Python version |Python 3.10 |


<span id="c6ced23c"></span>
# Restrictions


* FixString is not supported. Use String instead.

* ByteHouse does not support the JSONB and Bitmap64 data types.

* For any other restrictions you encounter, contact the ByteHouse team for assistance.


<span id="518b3225"></span>
# Cautions

By default, SQLAlchemy sends transaction control commands like `ROLLBACK` and `COMMIT`. Because ByteHouse does not support these commands, you must add the following code to override the relevant methods and prevent them from being sent.

```Python
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Get the MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define rollback function for a null operation (does not perform any operation)
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original rollback and commit methods on the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---
```


<span id="e01e8985"></span>
# Install SQLAlchemy


1. Install SQLAlchemy and its dependencies. For more SQLAlchemy installation instructions, see the [SQLAlchemy official documentation](https://www.sqlalchemy.org/).

   ```Python
   pip install SQLAlchemy
   ```
   

2. Install SQLAlchemy database\-related drivers.

   * Install PyMySQL: Use the PyMySQL driver for MySQL as the protocol layer for communication with ByteHouse.

      ```Python
      pip install pymysql
      ```
      

   * Install cryptography: for encryption and decryption.

      ```Python
      pip install cryptography
      ```
      


<span id="332b15a2"></span>
# Obtain the ByteHouse connection information

ByteHouse supports connecting to the ClickHouse SQLAlchemy Connector through IAM users or database users. The differences between IAM users and database users are described as follows; you may choose according to your needs.


* **IAM user**: An **IAM user** is created in BytePlus Access Control (IAM). Their privileges are determined by IAM policies and the permissions you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console and connect to ByteHouse via the CLI, connection drivers, ecosystem tools, and APIs.

* **Database user**: A **database user** is created in ByteHouse at the database level. You can grant these users privileges for environments, resources, and data. Database users cannot access the ByteHouse console, but they can connect to ByteHouse using the CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="c925b4c9"></span>
## Connect using an IAM user

Please refer to [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity)to learn how to connect to ByteHouse using an IAM user.

The following table describes the general parameters.


|Parameter |Description |
|---|---|
|Host |The public domain name of your ByteHouse instance. The format is `tenant-{TENANT_ID}-{REGION}-public.bytehouse.volces.com`, where `tenant-{TENANT_ID}-{REGION}` represents the account ID of the primary BytePlus account and the ByteHouse region, respectively. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |* The TCP protocol uses port 19000.<br><br>* The HTTP protocol uses port 8123. |
|Database |The name of the database to connect to. |
|user & password |* User: Set to ByteHouse.<br><br>* password: ByteHouse API Key. You can obtain the API Key in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|virtual_warehouse |The name of the virtual warehouse. Log in to the **ByteHouse Console**, click the **Virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If no configuration is set, the default virtual warehouse specified in your ByteHouse settings will be used. |


<span id="6ed8cd11"></span>
## Connect using a database user

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using database user credentials.

General parameter description


|Parameter |Description |
|---|---|
|Host |The Host field varies across different protocols, but the format remains the same: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.volces.com`, which is configured as ByteHouse's public domain name. In this format, tenant\-{TENANT_ID}\-{REGION} refers to the Account number ID of the BytePlus primary account and the Region information of ByteHouse, respectively. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |Fixed at 19000. |
|Database |The name of the database to connect to. |
|user & password |* user is configured as `{accountID_or_accountName}%3A%3A{username}[%3A%3A{envID}]`. For details, please refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: Refers to the BytePlus User Account ID or Name. You can log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the Account ID or Name.<br><br>   * `{username}`: The username for the ByteHouse database account. Go to **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. The name of the environment where the database is located. If you use the default environment, configuration is not required; to use another environment, you must specify the environment name, and do not add `[]` during configuration. You can log in to the **ByteHouse** **Console**, then obtain information in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Usage examples are as follows:<br><br>      * Configuration Environment ID: `21xxxxxxxx%3A%3Ademouser%3A%3Ademoenv`<br><br>      * Environment ID not configured: `21xxxxxxxx%3A%3Ademouser`<br><br>* Password: The password for the database account is set by the administrator during database account creation. You can contact the administrator to obtain the password. To reset the password if it is lost or forgotten, contact the Administrator. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|virtual_warehouse |The name of the virtual warehouse. Log in to the **ByteHouse Console**, click the **Virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If not configured, the default virtual warehouse you set in ByteHouse will be used. |


<span id="9daa9170"></span>
# Basic usage

You can use the following code to connect to ByteHouse and execute standard statements for querying, writing, and reading data. When using, make sure to replace the connection information fields in the connection statement, such as `{Host}`, `{Password}`, `{User}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields. For information on how to obtain these fields, see [Obtain the ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/clickhouse-sqlalchemy-connector#332b15a2).


* By default, `keepAlive` is supported, allowing connection reuse and avoiding short\-lived connections.


<span id="959df7d7"></span>
## Connect to ByteHouse

Refer to the code example below to connect to ByteHouse.

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}'
engine = create_engine(connection_string)
session = make_session(engine)
```


<span id="0172ceb7"></span>
## Custom query ID

Use the **execution_options** method to set the query ID.

```Python
global_settings = session.query(text("getSetting('max_execution_time')")).execution_options(query_id=f"customized_{uuid.uuid4()}")
```


<span id="b9452af9"></span>
## Custom query settings

<span id="1c66f163"></span>
### Global settings

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}&max_execution_time=450'
engine = create_engine(connection_string)
session = make_session(engine)

try:
    global_settings = session.query(text("getSetting('max_execution_time')")).execution_options(query_id=f"customized_{uuid.uuid4()}")
    global_settings_value = global_settings.scalar()
    assert global_settings_value == 450
    print(f"Result: {global_settings_value}")
finally:
    session.close()
```


<span id="6f03c836"></span>
### SQL level setting

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}&max_execution_time=450'
engine = create_engine(connection_string)
session = make_session(engine)

try:
    settings = {'max_execution_time': 400}
    query_settings = session.query(text("getSetting('max_execution_time')")).execution_options(settings = settings,query_id=f"customized_{uuid.uuid4()}")
    query_settings_value = query_settings.scalar()
    assert query_settings_value == 400
    print(f"Result: {query_settings_value}")
finally:
    session.close()
```


<span id="204a08b6"></span>
## Connection with query examples

```Python
import uuid
from datetime import datetime
from typing import Type

from sqlalchemy import create_engine, text, MetaData, Column, func
from clickhouse_sqlalchemy import make_session, get_declarative_base, types, engines, Table, select
from sqlalchemy.sql.ddl import DropSequence, DropSchema, CreateSchema, DropTable
from sqlalchemy.testing.provision import drop_db

host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}&max_execution_time=450'
engine = create_engine(connection_string)
session = make_session(engine)

global_settings = session.query(text("getSetting('max_execution_time')")).execution_options(query_id=f"customized_{uuid.uuid4()}")
global_settings_value = global_settings.scalar()
assert global_settings_value == 450
print(f"Result: {global_settings_value}")
settings = {'max_execution_time': 400}
query_settings = session.query(text("getSetting('max_execution_time')")).execution_options(settings = settings,query_id=f"customized_{uuid.uuid4()}")
query_settings_value = query_settings.scalar()
assert query_settings_value == 400
print(f"Result: {query_settings_value}")
result = session.execute(text('SELECT 1'))
value = result.scalar()
print(f"Result: {value}")

# Define metadata
metadata = MetaData()

try:
    # Delete database (if it exists)
    with engine.connect() as conn:
        drop_db = DropSchema('bhpythontest', if_exists=True)
        conn.execute(drop_db)
        create_db = CreateSchema('bhpythontest', if_not_exists=True)
        conn.execute(create_db)
        print("数据库创建成功")
        metadata.schema = 'bhpythontest'
        # Define table structure
        example_table = Table(
            'bhpythontest', metadata,
            Column('Col1', types.UInt8),
            Column('Col2', types.String),
            Column('Col3', types.String),
            Column('Col4', types.UUID),
            Column('Col5', types.Map(types.String, types.UInt8)),
            Column('Col6', types.Array(types.String)),
            # Map type is not supported under types.Tuple. Catching up with the KV flag is required. You can choose to create using the DDL method.
            Column('Col7', types.Tuple(types.String, types.UInt8, types.Array(types.String))),
            Column('Col8', types.DateTime),
            engines.CnchMergeTree(order_by=func.tuple())
        )

        Create a table
        metadata.create_all(engine)
        print("表创建成功")

        # Prepare to insert data
        data_to_insert = []
        for i in range(1000):
            record = {
                'Col1': 42,
                'Col2': 'ClickHouse',
                'Col3': 'Inc',
                'Col4': str(uuid.uuid4()),
                'Col5': {'key': 1},
                'Col6': ['Q', 'W', 'E', 'R', 'T', 'Y'],
                'Col7': ('String Value', 5, ['String1', 'String2']),
                'Col8': datetime.now()
            }
            data_to_insert.append(record)

    # Insert data in batches
    with engine.connect() as conn:
        # Method 1: Use execute to insert multiple times (suitable for small batches)
        # for data in data_to_insert:
        #     conn.execute(example_table.insert(), data)

        # Method 2: Batch insert (REC.)
        conn.execute(example_table.insert(), data_to_insert)

        print(f"Successfully inserted {len(data_to_insert)} records")

    # Query data
    with engine.connect() as conn:
        # Query records
        query = select(example_table).limit(1)
        result = conn.execute(query).fetchone()

        if result:
            print("Query result:")
            print(f"Col1: {result.Col1}")
            print(f"Col2: {result.Col2}")
            print(f"Col3: {result.Col3}")
            print(f"Col4: {result.Col4}")
            print(f"Col5: {result.Col5}")
            print(f"Col6: {result.Col6}")
            print(f"Col7: {result.Col7}")
            print(f"Col8: {result.Col8}")

    # Delete table
    with engine.connect() as conn:
        conn.execute(DropTable(example_table))
        print("Table deleted")

except Exception as e:
    print(f"Operation failed: {e}")
    raise
finally:
    session.close()
    # Close engine
    engine.dispose()
```


<span id="dbf8608a"></span>
## Define data models

Use the following code to replace the corresponding `connection_string` in the connection string:

```Python
# Create connection
connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


The updated code is as follows:

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


<span id="a10d98f8"></span>
## Use different data types

Use the following code to replace the corresponding `connection_string` in the connection string:

```Python
# Create connection
connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


The replaced code is as follows:

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


<span id="d776e404"></span>
## Read data

Use the following code to replace the corresponding `connection_string` in the connection string:

```Python
# Create connection
connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


The replaced code is as follows:

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


<span id="e00578f2"></span>
## Write data

Use the following code to replace the corresponding `connection_string` in the connection string:

```Python
# Create connection
connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


The replaced code is as follows:

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

connection_string = f'clickhouse+native://{user}:{password}@{host}:{port}/{database}?secure={secure}&verify={verify}'
engine = create_engine(connection_string)
```


<span id="6539e567"></span>
# Related references

For details about using SQLAlchemy, please refer to the [official documentation](https://www.sqlalchemy.org/).
