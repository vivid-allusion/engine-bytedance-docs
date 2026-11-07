---
title: " ClickHouse Rust (HTTP) Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/clickhouse-rust-http-driver"
---

The ClickHouse Rust (HTTP) driver is a library that enables your Rust applications to interact with the ByteHouse Cloud Data Warehouse. This document guides you through installing the driver, establishing a connection to ByteHouse, and performing basic data operations.

<span id="c2212bfd"></span>
# Environment requirements

It is recommended to use Rustc 1.84.1 or later.

<span id="8d2cdccc"></span>
# Recommended version


|**Items** |**Validated versions/notes** |
|---|---|
|ClickHouse driver version |Verified version: 0.13.1. For version details, see: [clickhouse v0.13.1](https://crates.io/crates/clickhouse/0.13.1) |


<span id="1b2b6a60"></span>
# Restrictions


* Currently, the BitMap64 and JSONB data types are temporarily not supported.

* If you encounter any other limitations, please contact the ByteHouse team.


<span id="07c76b57"></span>
# Install drivers

After obtaining the ClickHouse driver, you can install it using `cargo`:

```Bash
# Install ClickHouse with native-tls feature
cargo add clickhouse@0.13.1 --features native-tls
# Install tokio with full features (required for async operations)
cargo add tokio@1.0.1 --features full
# Install anyhow for error handling (optional but recommended)
cargo add anyhow
# Install serde with derive features (required for Row trait)
cargo add serde --features derive
```


Alternatively, add the following to `Cargo.toml`:

```TOML
[dependencies]
anyhow = "1.0.95"
clickhouse = { version = "0.13.1", features = ["native-tls"] }
serde = { version = "1.0.217", features = ["derive"] }
tokio = { version = "1.0.1", features = ["full"] }
```


<span id="ff86ee42"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to the ClickHouse Rust (HTTP) Driver through IAM users or database users. The differences between IAM users and database users are described as follows; you can choose one option according to your needs.


* **IAM user** is a user created in BytePlus Access Control (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. The IAM user can also access to ByteHouseusing CLI, connection drivers, ecosystem tools, APIs, and so on.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="6db6019a"></span>
## Connect using IAM user

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse as an IAM user.


|Parameters |Description |
|---|---|
|url |When connecting to ByteHouse, the URL must use HTTPS and be set to ByteHouse's public or private domain name. You can view the relevant information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it to a fixed value of 8123. |
|user & password |* user: Configured as bytehouse<br><br>* password: ByteHouse's API Key. You can obtain the API Key in the ByteHouse console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|database |The name of the database to connect to ByteHouse. |
|option |(Optional) Configure the virtual warehouse to be used after connecting to ByteHouse. If you have multiple virtual warehouses and want to use a specified virtual warehouse for subsequent ByteHouse data queries, or wish to set other specified parameters, you can configure these settings in `option`.<br><br>To find the virtual warehouse ID, navigate to the **Virtual warehouse** page in the ByteHouse console. |


<span id="ad21a821"></span>
## Connect using a database user

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using a database user account.

The parameters are as follows:


|Parameters |Parameter description |
|---|---|
|url |When connecting to ByteHouse, the URL must use HTTPS and be set to ByteHouse's public or private domain name. You can view the relevant information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set to a fixed value of 8123. |
|user & password |* The user is configured as `{accountID_or_accountName}::{username}[::{envID}]`. For more information, refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: Refers to the Volcano Engine user account ID or name. Log in to the ByteHouse console, and click the Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: Refers to the username used to log in to the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional configuration. The name of the environment where the database is located. No configuration is required when using the default environment; to use another environment, you must specify the environment name, and do not add `[]` when configuring. You can log in to the **ByteHouse** **console** and obtain it from **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Example usage is as follows:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Do not configure environment ID: `21xxxxxxxx::demouser`<br><br>* Password: Contact your administrator to get the database account password. To reset a lost or forgotten password, contact the administrator. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|database |The name of the database configured for connecting to ByteHouse. |
|option |(Optional) Configure the virtual warehouse to be used after connecting to ByteHouse. If you have multiple virtual warehouses and want to use a specified virtual warehouse for subsequent ByteHouse data queries, or want to set other specified parameters, you can configure these in the `option`.<br><br>How to get a virtual warehouse ID: You can view the ID of the corresponding virtual warehouse on the **Virtual warehouse** page in the ByteHouse console. |


<span id="b5533b78"></span>
# Basic usage

You can use the following code to connect to ByteHouse and start developing on ByteHouse using standard statements for querying, writing, and reading data.


* Timeout configuration: send_timeout defaults to None, end_timeout defaults to None.

* Supports `keepAlive` by default, enabling connection reuse and preventing short\-lived connections.


<span id="e8e613db"></span>
## Connect to ByteHouse

Refer to the code below to connect to ByteHouse. When using it, make sure to replace the connection information fields in the connection statement, such as `{Host}`, `{Username}`, `{Password}`, `{Database}`, and `{VIRTUAL_WAREHOUSE_ID}`. For information on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/clickhouse-rust-http-driver#ff86ee42).

```Python
const host: &str = "{Host}";
const port: i32 = 8123;
const password: &str = "{Password}";
const user: &str = "{User}";
const database: &str = "{Database}";
const virtual_warehouse_id: &str = "{VIRTUAL_WAREHOUSE_ID}";

pub fn create_client() -> Client {
    let client = Client::default()
        .with_url(format!("https://{}:{}", host, port))
        .with_database(database)
        .with_user(user)
        .with_password(password)
        .with_option("virtual_warehouse", virtual_warehouse_id)
        .with_compression(Compression::None);
    return client;
}
```


<span id="d94e355c"></span>
## Custom query IDs

You can use with_option to set the query ID.

```Rust

pub async fn query_id_example() -> Result<()> {
    let client = create_client();

    // Use a simple string as query ID
    let query_id = format!("customized_{}", Uuid::new_v4());
    println!("Query ID: {}", query_id);
    // Execute a simple query with the query ID
    let result = client
        .query("SELECT 1")
        .with_option("query_id", query_id)
        .fetch_one::<u8>()
        .await?;
    println!("Result: {}", result);

    Ok(())
}
```


<span id="2efdcd25"></span>
## Custom query settings

<span id="2f790531"></span>
### Global settings

You can set using `.with_option("virtual_warehouse", virtual_warehouse_id)`. For example,

```Rust
const host: &str = "{Host}";
const port: i32 = 8123;
const password: &str = "{Password}";
const user: &str = "{User}";
const database: &str = "{Database}";
const virtual_warehouse_id: &str = "{VIRTUAL_WAREHOUSE_ID}";

pub fn create_client() -> Client {
    let client = Client::default()
        .with_url(format!("https://{}:{}", host, port))
        .with_database(database)
        .with_user(user)
        .with_password(password)
        .with_option("virtual_warehouse", virtual_warehouse_id)
        .with_compression(Compression::None);
    return client;
}
```


<span id="dfa68d1a"></span>
### SQL level settings

For each SQL execution, you can set the option using `.with_option("virtual_warehouse", virtual_warehouse_id)`. For example

```Rust
let all_users = client
    .query("SELECT ?fields FROM bhrusttest.users")
    .with_option("virtual_warehouse", virtual_warehouse_id)
    .fetch_all::<User>()
    .await?;
```


<span id="8314be48"></span>
## Connections and queries

After connecting to ByteHouse, you can perform operations such as creating tables, reading or writing data, and other operations using the ClickHouse Rust (HTTP) Driver. The following examples show some basic operations.

```Rust
use clickhouse::{Client, Compression, Row};
use anyhow::Result;
use serde::{Deserialize, Serialize};
use uuid::Uuid;

#[derive(Debug, Row, Serialize, Deserialize)]
struct AdjFactorInsertRow<'a> {
    id: u32,
    name: String,
    age: u8,
    active: bool,
    ts_code: &'a str,
    #[serde(with = "clickhouse::serde::time::date")]
    trade_date: Date,
    adj_factor: f64,
}
const host: &str = "{Host}";
const port: i32 = 8123;
const password: &str = "{Password}";
const user: &str = "{User}";
const database: &str = "{Database}";
const virtual_warehouse_id: &str = "{VIRTUAL_WAREHOUSE_ID}";

pub fn create_client() -> Client {
    let client = Client::default()
        .with_url(format!("https://{}:{}", host, port))
        .with_database(database)
        .with_user(user)
        .with_password(password)
        //.with_option("virtual_warehouse", virtual_warehouse_id)
        .with_compression(Compression::None);
    return client;
}

pub async fn quickstart_example() -> Result<()> {
    let client = create_client();

    // Drop table if exists and create a new one
    client
        .query("DROP DATABASE IF EXISTS bhrusttest")
        .execute()
        .await?;
    client
        .query("CREATE DATABASE IF NOT EXISTS bhrusttest")
        .execute()
        .await?;


    client
        .query(
            "
            CREATE TABLE bhrusttest.users (
                id       UInt32,
                name     String,
                age      UInt8,
                active   Bool
            ) ENGINE = CnchMergeTree()
            ORDER BY id
            "
        )
        .execute()
        .await?;

    println!("Table created successfully");

    // Insert some sample data
    let mut insert = client.insert("bhrusttest.users")?;

    let users = vec![
        User {
            id: 1,
            name: "Alice".to_string(),
            age: 25,
            active: true,
        },
        User {
            id: 2,
            name: "Bob".to_string(),
            age: 30,
            active: true,
        },
        User {
            id: 3,
            name: "Charlie".to_string(),
            age: 35,
            active: false,
        },
    ];

    for User in users {
        insert.write(&User).await?;
    }

    insert.end().await?;
    println!("Data inserted successfully");

    // Select all users
    let all_users = client
        .query("SELECT ?fields FROM bhrusttest.users")
        .with_option("virtual_warehouse", virtual_warehouse_id)
        .fetch_all::<User>()
        .await?;

    println!("\nAll users:");
    for User  in all_users {
        println!("{:?}", User);
    }

    Ok(())
}

#[tokio::main]
async fn main() {
    quickstart_example().await.expect("TODO: panic message");
    query_id_example().await.expect("TODO: panic message");
}


pub async fn query_id_example() -> Result<()> {
    let client = create_client();

    // Use a simple string as query ID
    let query_id = format!("customized_{}", Uuid::new_v4());
    println!("Query ID: {}", query_id);
    // Execute a simple query with the query ID
    let result = client
        .query("SELECT 1")
        .with_option("query_id", query_id)
        .fetch_one::<u8>()
        .await?;
    println!("Result: {}", result);

    Ok(())
}
```
