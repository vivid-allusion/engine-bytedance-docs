---
title: "ClickHouse NodeJS"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ClickHouse-NodeJS"
---

ByteHouse Cloud Data Warehouse supports connecting through the ClickHouse native NodeJS client. This document introduces how to use ClickHouse to connect to ByteHouse Cloud Data Warehouse and perform operations such as creating tables, querying, and more.

<span id="2b23aac8"></span>
# Recommended version

Please ensure that the version of the ClickHouse NodeJS Client you use is v2.4.2 or above.

<span id="8e269f7c"></span>
# Restrictions


* The JSONB and Bitmap64 types in ByteHouse are not currently supported.

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="e7b0dd25"></span>
# Install ClickHouse NodeJS Client

Use npm to install the ClickHouse NodeJS Client.

```JavaScript
npm install clickhouse@2.4.2
```


<span id="b8e5e552"></span>
# Obtain ByteHouse connection information

The following sections describe the differences between IAM and database users to help you choose the appropriate connection method.


* **IAM user** refers to a user created in BytePlus access control (IAM), whose permissions are determined by the IAM privilege policy and by the permissions to ByteHouse resources and data that you grant. IAM users can access the ByteHouse Console and can also access ByteHouse through the CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database user** is a database\-level user created in ByteHouse, which can be granted environment, resource, and data permissions. Database users cannot access the ByteHouse Console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and many other methods.


For more information about IAM users and database users, refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="48eef4a1"></span>
## Use IAM user to connect

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using an IAM user.

The following table describes the parameters.


|Param |Configuration description |
|---|---|
|host |Set this to your ByteHouse public or private domain name. You can view and copy the domain name information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Fixed at 8123. |
|username & Password |Username and password for the ByteHouse Database.<br><br><br>* The username is always `bytehouse`.<br><br>* Password: Set this to the API Key obtained from ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|VIRTUAL_WAREHOUSE_ID |Optional. Set it as the virtual warehouse name. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>You can log in to the **ByteHouse Console**, click **Virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If no configuration is set, the default virtual warehouse you set in ByteHouse will be used. |
|Database |ByteHouse database name. Log in to the ByteHouse Console, then view and copy databases on the **Database** page. |


<span id="5391ae75"></span>
## Use database user connections


|Param |Configuration description |
|---|---|
|host |When configured as ByteHouse's public or private domain name, you can view and copy the domain name information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Fixed at 8123. |
|User & Password |Log in with the username and password of the ByteHouse database.<br><br><br>* User is configured as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: This refers to the BytePlus User Account ID or name. Log in to the ByteHouse Console, and click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: The username used to log in to the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. The name of the environment where the database is located. No configuration is required when using the default environment; to use another environment, you must specify the environment name, and do not include `[]` in the configuration. You can log in to the **ByteHouse** **console** and obtain it from **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      For example:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Do not configure environment ID: `21xxxxxxxx::demouser`<br><br>* password: Contact the administrator to obtain the password for the database account. To reset your password if you have lost or forgotten it, contact the administrator. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|VIRTUAL_WAREHOUSE_ID |Optional. The name of the virtual warehouse. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>Log in to the **ByteHouse Console**, click **virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If no configuration is set, the default virtual warehouse that you set in ByteHouse will be used. |
|Database |ByteHouse database name. You can log in to the ByteHouse Console and view and copy databases on the **Database** page. |


<span id="ab9d9a71"></span>
# Basic usage

<span id="bde22207"></span>
## Connect ByteHouse

You can refer to the code below to connect to ByteHouse. When using the code, make sure to replace the placeholders in the connection statement, such as `{host}`, `{password}`, `{user}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields. For details on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/ClickHouse-NodeJS#b8e5e552).

```JavaScript
const host = '{Host}';
const port = 8123;
const password = '{Password}';
const user = '{User}';
const database = '{Database}';
const virtual_warehouse = '{VIRTUAL_WAREHOUSE_ID}';

const clickhouse = new ClickHouse({
    url: util.format('https://%s', host),
    port: port,
    debug: false,

    basicAuth: {
        username: user,
        password: password,
    },

    isUseGzip: false,
    usePost: false,
    format: 'json',

    config: {
        session_timeout: 60,
        output_format_json_quote_64bit_integers: 0,
        enable_http_compression: 0,
        database: database,
        virtual_warehouse: virtual_warehouse,
    },

});
```


The parameter description is as follows:


|Param |Configuration description |
|---|---|
|debug |Specifies whether to enable debug mode. The default is false. |
|basicAuth.username |The username for the connection. For IAM users, this is always `bytehouse`. |
|basicAuth.password |Set the connection password as the API Key of ByteHouse Cloud Data Warehouse. Log in to the ByteHouse Cloud Data Warehouse Console. Under the **Tenant management** tab, click **Connection information**. Then create and copy an API Key. |
|isUseGzip |Set whether to enable Gzip compression for data transmission. To enable, set to true. The default value is false. |
|usePost |Set whether to use the POST method to send query requests. POST requests are suitable for scenarios where the query content is too large. To enable this feature, set this value to `true`. The default value is `false`. |
|format |It specifies the format of query results or inserted data; JSON, CSV, and TSV formats are supported. The JSONEachRow format is not currently supported. |
|config.session_timeout |Set the session timeout period. The default value is 60 seconds. |
|config.output_format_json_quote_64bit_integers |It controls whether 64\-bit integers are enclosed in quotation marks when output in JSON format. The default value is 0. When set to 0, the value is returned directly as a number; when set to 1, the value is returned as a string (for example, `"12345678"`). |
|config.enable_http_compression |Specifies whether to enable HTTP transport compression. Set to 0 to disable, set to 1 to enable. |
|config.database |Set to the name of the ByteHouse Cloud Data Warehouse database you need to connect to. |
|config.virtual_warehouse |Optional. It specifies the virtual warehouse for ByteHouse Cloud Data Warehouse. Log in to the ByteHouse CDW Console. Under the **Virtual warehouses** tab, view and copy the virtual warehouse ID. |


<span id="709c6bb8"></span>
## Basic database operations

After a successful connection, you can use the following code to create a database, tables, insert data, and query data.

```JavaScript
import { ClickHouse } from 'clickhouse';
import * as util from "node:util";

const host = '{Host}';
const port = 8123;
const password = '{Password}';
const user = '{User}';
const database = '{Database}';
const virtual_warehouse = '{VIRTUAL_WAREHOUSE_ID}';

const clickhouse = new ClickHouse({
    url: util.format('https://%s', host),
    port: port,
    debug: false,

    basicAuth: {
        username: user,
        password: password,
    },

    isUseGzip: false,
    usePost: false,
    format: 'json',

    config: {
        session_timeout: 60,
        output_format_json_quote_64bit_integers: 0,
        enable_http_compression: 0,
        database: database,
        virtual_warehouse: virtual_warehouse,
    },

});

// @ts-ignore
// Complete example
async function run() {
    try {
        await clickhouse.query('DROP DATABASE IF EXISTS bhnodetest').toPromise();
        await clickhouse.query('CREATE DATABASE IF NOT EXISTS bhnodetest').toPromise();
        await clickhouse.query(`
      CREATE TABLE bhnodetest.sample_table (
        id Int32,
        name String
      ) ENGINE = CnchMergeTree()
      ORDER BY id
    `).toPromise();

        await clickhouse.insert(
            'INSERT INTO bhnodetest.sample_table (id, name)',
            [
                [1, 'Alice'],
                [2, 'Bob'],
            ]
        ).toPromise();

        const rows = await clickhouse.query('SELECT * FROM bhnodetest.sample_table FORMAT JSON').toPromise();

        console.log('Query result:', rows);
    } catch (err) {
        console.error('Error running ClickHouse operations:', err);
    }
}

// @ts-ignore
await run();
```


<span id="bab1dd7d"></span>
## Use callback functions to query

This example demonstrates the asynchronous execution method for processing query results via callback functions.

```JavaScript
clickhouse.query('SELECT * FROM bhnodetest.sample_table FORMAT JSON').exec((err, rows) => {
    if (err) {
        console.error('Callback query error:', err);
    } else {
        console.log('Query result (Callback):', rows);
    }
});
```


<span id="1612bd71"></span>
## Stream query

This example demonstrates processing query results using the streaming approach, which is suitable for scenarios where a large amount of data is returned, such as batch reading of data. Data can be processed row by row instead of waiting for all data to be loaded.

```JavaScript
clickhouse.query('SELECT number FROM system.numbers LIMIT 5 FORMAT JSON').stream()
  .on('data', function (chunk) {
    const stream = this;
    process.stdout.write('Stream chunk: ' + chunk.toString());
    stream.pause();
    setTimeout(() => stream.resume(), 1000); // Simulate backpressure scenarios
  })
  .on('error', err => {
    console.error('Stream error:', err);
  })
  .on('end', () => {
    console.log('\nStream ended.');
  });
```


<span id="ae0a0a8d"></span>
## Perform a streaming insertion

This example demonstrates processing query results using the streaming method, which is suitable for scenarios where a large amount of data is returned, such as reading data in batches. Data can be processed row by row instead of waiting for all data to be loaded.

```JavaScript
clickhouse.query('SELECT number FROM system.numbers LIMIT 5 FORMAT JSON').stream()
    .on('data', function (chunk) {
        const stream = this;
        process.stdout.write('Stream chunk: ' + chunk.toString());
        stream.pause();
        setTimeout(() => stream.resume(), 1000); // Simulate backpressure Scenes
    })
    .on('error', err => {
        console.error('Stream error:', err);
    })
    .on('end', () => {
        console.log('\nStream ended.');
    });
```
