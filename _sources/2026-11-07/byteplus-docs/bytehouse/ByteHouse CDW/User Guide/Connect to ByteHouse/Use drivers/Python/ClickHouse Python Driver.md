---
title: "ClickHouse Python Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-ClickHouse-Python-Driver"
---

The ClickHouse Python driver enables you to connect Python applications to the ByteHouse Cloud Data Warehouse. This is essential for leveraging Python's rich data science ecosystem to perform complex analysis, build data\-driven applications, or automate data processing tasks. This tutorial will guide you through installing the driver, establishing a connection, and executing fundamental data operations like querying and inserting records.

<span id="110800fb"></span>
# Environment requirements

We recommend using Python 3.12 or a later version.

<span id="db09b9fb"></span>
# Recommended version

It is recommended to use Python driver version 0.2.9 or later.

<span id="65a365cc"></span>
# Restrictions


* The ClickHouse\-Driver has high serialization overhead in Python when importing data chunks. This makes it unsuitable for large\-scale data ingestion or for benchmarking ByteHouse's write throughput.

* The JSONB and Bitmap64 data types of ByteHouse are not supported.

* Currently supported data types:

   
   |Data type |Insert Type |Select Type |
   |---|---|---|
   |[U]Int8/16/32/64/128/256 |int, long |int |
   |Float32/64 |float, int, long |float |
   |Date/Date32 |date, datetime |date |
   |DateTime |datetime, int, long |datetime |
   |String/FixedString(N) |str, bytes |str, bytes |
   |Enum8/16 |Enum, int, long, str |str |
   |Array(T) |list, tuple |list |
   |Bool |bool |bool |
   |UUID |str, UUID |str |
   |Decimal |Decimal, float, int, long |Decimal |
   |IPv4/IPv6 |IPv4Address/IPv6Address, int, long, str |IPv4Address/IPv6Address |
   

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="f65748a6"></span>
# Install ClickHouse Python driver

<span id="a8942633"></span>
## Install dependencies

You may need to install the following dependency:

```Bash
apk add gcc musl-dev
```


<span id="8036b29d"></span>
## Install the driver from PyPI

To obtain the latest release version of clickhouse\-driver, use the following command.

```Python
pip3 install clickhouse-driver
```


<span id="755dfdf4"></span>
## Install the driver from GitHub

Install the development version using the following command. You can obtain the latest documentation and release information on [the project's GitHub homepage](https://github.com/mymarilyn/clickhouse-driver).

```Python
pip3 install git+https://github.com/mymarilyn/clickhouse-driver@master#egg=clickhouse-driver
```


<span id="8beaf8cc"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to the ClickHouse Python Driver through IAM users or database users. The following content describes the differences between IAM and database users to help you choose the right option for your needs.


* **IAM user** is a user created in BytePlus Access Control (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. Access to ByteHouse is also supported through CLI, connection drivers, ecosystem tools, API, and so on.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="04dd51ac"></span>
## Use IAM users to connect

Please refer to [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity) to learn how to connect to ByteHouse using an IAM user.

The following table describes the general parameters.


|Parameter |Connect using an IAM user |
|---|---|
|host |The public/private domain name configured for ByteHouse can be viewed and copied in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it as the fixed value 19000. |
|user & password |* user: Fixed configuration is bytehouse<br><br>* password: ByteHouse API Key. You can obtain the API Key in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|database |The database name configured to connect to ByteHouse. |


<span id="e5420054"></span>
## Use a database user connection

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using database user credentials.

General parameter description as follows:


|Parameter |Connect using a database user |
|---|---|
|host |For the public or private domain name configured for ByteHouse, you can view and copy the corresponding network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it to the default value 19000. |
|user & password |* User: Instructions for filling in parameters are as follows. For details, please refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Depending on your connection method, the user format varies:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For Client object connections: <code>{accountID_or_accountName}::{username}[::{envID}]</code>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For URL connections: <code>{accountID_or_accountName}%3A%3A{username}[%3A%3A{envID}]</code>.   </div><br>   <br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username used to log in to the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional configuration. It refers to the name of the environment where the database is located. Configuration is not required when using the default environment. To use another environment, you must specify the environment name without adding `[]` during configuration. You can log in to the **ByteHouse** **Console** and obtain the required information from**Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Usage examples are as follows:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv` or `21xxxxxxxx%3A%3Ademouser%3A%3Ademoenv`<br><br>      * Environment ID not configured: `21xxxxxxxx::demouser` or `21xxxxxxxx%3A%3Ademouser`<br><br>* Password: Contact your administrator to obtain the password for the database account. If the password is lost or forgotten, you can contact your administrator to reset the password. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|database |The name of the database to connect to. |


<span id="fe5fde74"></span>
# Basic usage

You can use the following code to connect to ByteHouse and start using standard statements to develop on ByteHouse for querying, writing, and reading data. Caution: Replace the connection information fields `{Host}`, `{Password}`, `{User}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other related fields in the connection statement. For information on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-ClickHouse-Python-Driver#8beaf8cc).


* Timeout configuration: The default value for connect_timeout is 10 seconds, and the default value for send_receive_timeout is 300 seconds.

* Default support for `keepAlive` enables connection reuse and avoids short\-lived connections.


<span id="4e36a8fa"></span>
## Connect ByteHouse

ByteHouse supports connecting through a Client object or through URL configuration.

<span id="a13eff67"></span>
### Client object connection configurations

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False,
    settings={"virtual_warehouse": virtual_warehouse_id},
)
```


<span id="41f1d741"></span>
### Connect through a URL configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When configuring a connection using a database account through a URL, the user must fill in according to the <code>{accountID_or_accountName}%3A%3A{username}[%3A%3A{envID}]</code> format. For example:</div>



* <div data-tips="true" data-tips-type="warning">Configuration environment ID: <code>21xxxxxxxx%3A%3Ademouser%3A%3Ademoenv</code></div>


* <div data-tips="true" data-tips-type="warning">No environment ID configured: <code>21xxxxxxxx%3A%3Ademouser</code></div>



```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"


uri = f"clickhouse://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}"
client = Client.from_url(uri)
```


<span id="c484bbd5"></span>
## Custom query ID

You can use Context to set the query ID.

```Python
client.execute("DROP DATABASE IF EXISTS bhpythontest", query_id=f"customized_{uuid.uuid4()}")
```


<span id="6f2df2ef"></span>
## Custom query settings

<span id="23380805"></span>
### Global settings

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False,
    settings={
        'max_execution_time': 450,
        'max_block_size': 10000
    },
)

try:
    # This query automatically uses the parameters set during connection
    result = client.execute("SELECT getSetting('max_execution_time')")
    setting_value = result[0][0]
    print(f"Global setting value: {setting_value}")
except Exception as e:
    print(f"Global setting example error: {e}")
finally:
    client.disconnect()
```


<span id="ca8eb6de"></span>
### SQL level setting

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False
)

try:
    settings = {
        'max_execution_time': 450
    }
    query = """
            SELECT 
                getSetting('max_execution_time')
            """
    result = client.execute(query, settings=settings)
    if result:
        max_execution = result[0][0]
        print(f"max_execution_time: {max_execution}")
        assert max_execution == 450
        print(f"Setting value: {max_execution}")
except Exception as e:
    print(f"Setting example error: {e}")

client.disconnect()
```


<span id="e0c225d0"></span>
## Complete connection and query examples

You can use the following code to connect to ByteHouse and manage data. Replace the fields in the connection configuration in the code with the information provided in [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-ClickHouse-Python-Driver#8beaf8cc).

```Python
import uuid
import time
from datetime import datetime
from clickhouse_driver import Client

host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

# client = Client(
#     host=host,
#     port=port,
#     user=user,
#     password=password,
#     database=database,
#     secure=True,
#     verify=False,
#     settings={"virtual_warehouse": virtual_warehouse_id},
# )

uri = f"clickhouse://{user}:{password}@{host}:{port}/{database}?secure=True&verify=False&virtual_warehouse={virtual_warehouse_id}"
client = Client.from_url(uri)

client.execute("DROP DATABASE IF EXISTS bhpythontest", query_id=f"customized_{uuid.uuid4()}")
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

Prepare to insert data
values_list = []
for i in range(1000):
    value = (
        42,  # uint8(42)
        'ClickHouse',
        'Inc',
        str(uuid.uuid4()),
        {'key': 1},  # Map(String, UInt8)
        ['Q', 'W', 'E', 'R', 'T', 'Y'],  # Array(String)
        ('String Value', 5, [{'key': 'value'},{'key': 'value'},{'key': 'value'}]),  # Tuple
        datetime.now()
    )
    values_list.append(value)

Insert in batches
insert_sql = "INSERT INTO bhpythontest.example (Col1, Col2, Col3, Col4, Col5, Col6, Col7, Col8) VALUES"
client.execute(insert_sql, values_list)
print("Successfully inserted 1000 records.")

Query a record
select_sql = "SELECT * FROM bhpythontest.example LIMIT 1"
result = client.execute(select_sql)

if result:
    Col1, Col2, Col3, Col4, Col5, Col6, Col7, Col8 = result[0]
    print(f"Query result:")
    print(f"Col1: {Col1}")
    print(f"Col2: {Col2}")
    print(f"Col3: {Col3}")
    print(f"Col4: {Col4}")
    print(f"Col5: {Col5}")
    print(f"Col6: {Col6}")
    print(f"Col7: {Col7}")
    print(f"Col8: {Col8}")

# Drop the table
drop_sql = "DROP TABLE IF EXISTS bhpythontest.example"
client.execute(drop_sql)
print("Table is deleted")

client.disconnect()
```


<span id="4b17d750"></span>
## Insert data from a Pandas DataFrame

`'use_numpy': True` requires support for the `Numpy` / `Pandas` packages; refer to the example below.

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False,
    settings={"virtual_warehouse": virtual_warehouse_id,"use_numpy": True},
)

client.execute(
   'CREATE TABLE test_df (x Int, y String) Engine = CnchMergeTree() ORDER BY tuple()'
)

df_insert = pd.DataFrame({
    'x': [1, 2],
    'y': ['apple', 'banana'],
}, dtype=object)

client.insert_dataframe('INSERT INTO test_df VALUES', df_insert)

df_select = client.query_dataframe('SELECT * FROM test_df')

print(df_select)
```


<span id="a11683fb"></span>
## Insert data from CSV file

Assume your CSV file contains the following data:

```Plain
time,order,qty
2019-08-01 15:23:14,New order1,5
2019-08-05 09:14:45,New order2,3
2019-08-13 12:20:32,New order3,7
```


Data can be inserted into ByteHouse using the following methods:

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False,
    settings={"virtual_warehouse": virtual_warehouse_id},
)

def iter_csv(filename):
    converters = {
        'time': lambda x: datetime.strptime(x, '%Y-%m-%d %H:%M:%S'),
        'order': str,
        'qty': int,
    }
    with open(filename, 'r') as f:
        reader = DictReader(f)
        for line in reader:
            yield {k: (converters[k](v) if k in converters else v) for k, v in line.items()}


client.execute(
    'CREATE TABLE IF NOT EXISTS data_csv (time DateTime, order String, qty Int32) Engine = CnchMergeTree() ORDER BY tuple()'
)
client.execute('INSERT INTO data_csv VALUES', iter_csv('data.csv'))
```


<span id="8d06fa65"></span>
## Retrieve data according to column names

By setting `"with_column_types"=True`, you can use data retrieval by column name.

```Python
host = "{Host}"
port = 19000
password = "{Password}"
user = "{User}"
database = "{Database}"
virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}"

client = Client(
    host=host,
    port=port,
    user=user,
    password=password,
    database=database,
    secure=True,
    verify=False,
    settings={"virtual_warehouse": virtual_warehouse_id},
)

client.execute("""
CREATE TABLE IF NOT EXISTS test_table (
    int_column Int32,
    string_column String,
    array_column Array(Int32)
) ENGINE = CnchMergeTree()
ORDER BY int_column
""")

data_to_insert = [
    (1, 'First', [1, 2, 3]),
    (2, 'Second', [4, 5, 6]),
    (3, 'Third', [7, 8, 9])
]

client.execute(
    "INSERT INTO test_table (int_column, string_column, array_column) VALUES",
    data_to_insert
)

query = "SELECT * FROM test_table"
data, columns = client.execute(query, with_column_types=True)

# Use dictionary comprehension to create a dictionary with column names as keys
column_data = {col_name: [row[i] for row in data] for i, col_name in enumerate([col[0] for col in columns])}

# Access by column names
print("int_column:", column_data['int_column'])
print("string_column:", column_data['string_column'])
print("array_column:", column_data['array_column'])
```
