---
title: "Python Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/python-driver"
---

This article explains how to use ClickHouse Connect in the Python development environment to connect to and access ByteHouse Enterprise Edition.

<span id="0ae7d973"></span>
# Install ClickHouse Connect

Run the following command to install ClickHouse Connect.

```Plain
pip install clickhouse-connect
```


Refer to the [ClickHouse Connect official documentation](https://clickhouse.com/docs/zh/integrations/python#installation) for more installation methods.

<span id="85de2e3b"></span>
# Obtain ByteHouse connection information

Before connecting with ClickHouse Connect, you need to obtain ByteHouse connection information. Refer to the following sections to get the required details.


* Host address: cluster connection address, see [Cluster connection address](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#6ab9e6d0) for details.

* Port: port number, use 8123. For more port information, see [Cluster connection address](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#6ab9e6d0).

* Username: the username for the ByteHouse service. For details, see [Retrieve account and password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#c697cd0c).

* Password: the password for the ByteHouse service. For details, see [Retrieve account and password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#c697cd0c).


<span id="ce4a68f1"></span>
## Obtain the network domain name

The cluster connection address is the cluster’s gateway information. Log in and enter the ByteHouse console, then click the top **Cluster Management**. Navigate via **Cluster List \> Cluster Details \> Basic Information** to view the **Network Information** module’s gateway configuration. Copy the private or public address according to your environment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8e9c93f7c484e18b7675b49619cc9a0~tplv-goo7wpa0wc-image.image) </span>

<span id="5eefd938"></span>
## Obtain account and password

The ByteHouse service username is the BytePlus IAM account. You can view the username through **Cluster Management \> Cluster List \> Cluster \> Connect Cluster**.

When you first log in to BytePlus with the IAM account password, the system automatically generates the initial ByteHouse service password. If you forget or lose the password, you can reset and set a new password in **Cluster Management** \> **Cluster List** \> **Cluster** \> **Connect Cluster**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ea21b7204bb4d2db43a31b4b3259b54~tplv-goo7wpa0wc-image.image) </span>

<span id="fc9da12e"></span>
# Connect and use with ClickHouse Connect

<span id="d8b5d7fa"></span>
## Connect to ByteHouse

Refer to the code example below to set ByteHouse connection information. Replace the `host`, `port`, `username`, `password` parameters in the command with the connection details obtained from [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/python-driver#85de2e3b).

```Python
import clickhouse_connect

client = clickhouse_connect.get_client(host='xxxxxxx-public.bytehouse-ce.bytepluses.com', port=8123, username='{user}', password='{password}', secure=False)
```


Parameter description:


* `secure`: indicates whether to use an encrypted connection (HTTPS/TLS).


<span id="a3939e4f"></span>
## Basic usage example

After connecting to ByteHouse via ClickHouse Connect, you can perform operations such as creating tables, querying data, and inserting records.

<span id="2450fb87"></span>
### Create table

Use the `client.command` command to execute SQL commands.

```SQL
client.command('CREATE TABLE new_table (key UInt32, value String, metric Float64) ENGINE HaMergeTree ORDER BY key') 
```


<span id="ba1d08e0"></span>
### Insert data

Use `client.insert` to batch insert data.

```SQL
row1 = [1000, 'String Value 1000', 5.233]
row2 = [2000, 'String Value 2000', -107.04]
data = [row1, row2]
client.insert('new_table', data, column_names=['key', 'value', 'metric'])
```


<span id="2aae9137"></span>
### Query data

Use `client.query` to query data.

```SQL
result = client.query('SELECT max(key), avg(metric) FROM new_table')
result.result_rows
Out[13]: [(2000, -50.9035)]
```


<span id="e9b850a4"></span>
### Insert data using InsertContexts

All insert operations in ClickHouse Connect are executed through InsertContext. InsertContext includes all parameter values inserted via `client.insert`. Additionally, when creating InsertContext, ClickHouse Connect retrieves column data type information required for Native format inserts. Reusing InsertContext for multiple inserts avoids repeated pre\-query operations, significantly improving insertion efficiency and execution speed.

You can obtain InsertContext information using `client.create_insert_context`. Note that when reusing InsertContext, only its data property can be modified.

```SQL
test_data = [[1, 'v1', 'v2'], [2, 'v3', 'v4']]
ic = test_client.create_insert_context(table='test_table', data='test_data')
client.insert(context=ic)
assert client.command('SELECT count() FROM test_table') == 2
new_data = [[3, 'v5', 'v6'], [4, 'v7', 'v8']]
ic.data = new_data
client.insert(context=ic)
qr = test_client.query('SELECT * FROM test_table ORDER BY key DESC')
assert qr.row_count == 4
assert qr[0][0] == 4
```
