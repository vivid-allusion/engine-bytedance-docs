---
title: "ClickHouse Go Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-clickhouse-go-driver"
---

The open\-source ClickHouse Go driver enables you to connect Go applications to ByteHouse Cloud Data Warehouse for data writing and querying. It serves as the recommended solution while the native ByteHouse Go driver is under maintenance, ensuring stable integration for your projects. This is ideal for developers building data pipelines or analytics tools in Go that need to interact with ByteHouse. This document guides you through installing the driver, establishing a connection, and executing basic operations.

<span id="713f4766"></span>
# Background

Because the native Go driver for ByteHouse is currently being upgraded, you can use the open\-source ClickHouse Go driver to connect to ByteHouse. The open\-source ClickHouse driver supports the following APIs and protocols.


|Detailed items |Capability description |
|---|---|
|API interface |The following interfaces are supported:<br><br><br>* (Recommended) ClickHouse Client interface: Provides the best performance, and supports some special ClickHouse capabilities, such as column writing.<br><br>* database/sql interface: To connect to multiple databases, or to use tools and libraries based on the standard database/sql interface, you can use this interface. |
|Protocol |The following protocols are supported:<br><br><br>* (Recommended) TCP/Native protocol: We recommend using the `TCP/Native` protocol for better performance.<br><br>* HTTP protocol: The HTTP protocol, which is only supported by the database/sql interface, can be used to ensure compatibility with firewalls and proxies. |


<span id="09f48a2b"></span>
# Environment requirements

It is recommended to use the following versions:


|Driver |Verified version |
|---|---|
|ClickHouse Go driver |2.30.0 |
|Go |Golang 1.21 |


<span id="ae135fc2"></span>
# Restrictions


* Currently, ByteHouse JSONB and Bitmap64 data types are not supported.

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="053801cc"></span>
# Install drivers

<span id="e06e15b9"></span>
## Download drivers

Click [this link](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.30.0) to download the ClickHouse Go basic driver.

<span id="a07aa995"></span>
## Install drivers

You can install via `go get`.

```Go
go get github.com/ClickHouse/clickhouse-go/v2@v2.30.0
```


<span id="45c37d04"></span>
# Obtain ByteHouse connection information

You can connect to ByteHouse with the ClickHouse Go driver using either an IAM user or a database user. The differences between IAM users and database users are as follows. Choose the option that best fits your use case.


* An **IAM user** is a user created in BytePlus Identity and Access Management (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. ByteHouse also supports access through the CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database users** are database\-level users created in ByteHouse who can be granted environment, resource, and data permissions. Database users cannot access the ByteHouse Console, but database users can access ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="dd4941fc"></span>
## Use IAM users to connect

Please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) to learn how to connect to ByteHouse using the IAM user method.

General parameter descriptions are as follows:


|Param |Description |
|---|---|
|Host |The Host field differs across protocols, but the format is the same: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.volces.com`, which is the public domain name configured for ByteHouse. Here, `tenant-{TENANT_ID}-{REGION}` represents the account ID of the primary BytePlus account and the region information for ByteHouse, respectively. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |* The TCP protocol uses port 19000.<br><br>* The HTTP protocol uses port 8123. |
|Database |The name of the database in ByteHouse to connect to. |
|username & password |* username: Set to bytehouse.<br><br>* password: Your ByteHouse API key, which you can obtain in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|virtual_warehouse |The name of your virtual warehouse. Log in to the ByteHouse Console, click Virtual warehouse at the top, view and copy the virtual warehouse ID. For example, vw\-{environment_id}{account_id}\-{virtual_warehouse_name}.<br><br>If not configured, your default virtual warehouse set in ByteHouse will be used. |


<span id="66dbd61c"></span>
## Use a database user connection

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using a database user.

General parameter descriptions are as follows:


|Param |Configuration essentials |
|---|---|
|Host |The Host field differs across protocols, but the format remains the same: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.volces.com`, which serves as ByteHouse's public domain name. Here, `tenant-{TENANT_ID}-{REGION}` refers to the account ID of the BytePlus primary account and the region information of ByteHouse, respectively. You can view and copy the network information in the ByteHouse Console under \*\*Tenant management \*\*\> \*\*Basic information \*\*\> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |* The TCP protocol uses port 19000.<br><br>* The HTTP protocol uses port 8123. |
|Database |Database name configured for connecting to ByteHouse. |
|username & password |* username: Follow these instructions to format username. For details, please refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Depending on the connection method you use, the concatenation method for the username will differ:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When using OpenDB connections, the username is configured as <code>{accountID_or_accountName}::{username}[::{envID}]</code>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When connecting using the DSN method, the username configuration is <code>{accountID_or_accountName}%3A%3A{username}[%3A%3A{envID}]</code>.   </div><br>   <br><br>   * {accountID_or_accountName}: It refers to the BytePlus user account ID or name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: The username used to log in to your ByteHouse database account. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users** \> **View database username**.<br><br>   * `{envID}`: It refers to the name of the environment where the database is located. When using the Default environment, configuration is not required; to use another environment, specify the environment name, and do not add `[]` during configuration. You can log in to the **ByteHouse** **Console**, where you can obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Usage examples are as follows:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv` or `21xxxxxxxx%3A%3Ademouser%3A%3Ademoenv`<br><br>      * Do not configure an Environment ID: `21xxxxxxxx::demouser` or `21xxxxxxxx%3A%3Ademouser`<br><br>* Password: The password for the database account is custom\-configured by the administrator during account creation. You can contact the administrator to obtain the password. To reset your password if it is lost or forgotten, contact the administrator. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|virtual_warehouse |Configure it as the virtual warehouse name. Log in to the **ByteHouse Console**, click the **Virtual warehouse** at the top of the page, and view and copy the virtual warehouse ID. For example, `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If not configured, the default virtual warehouse that you set in ByteHouse will be used. |


<span id="26a8576d"></span>
# Basic usage

<span id="29ebb3fd"></span>
## Connect ByteHouse

You can refer to the code below to connect to ByteHouse. When using the code, replace the placeholders `{Host}`, `{Password}`, `{User}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields in the connection statement. For details on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-clickhouse-go-driver#45c37d04).


* Timeout configuration

   * When using the TCP protocol: dial_timeout defaults to 30s, and read_timeout defaults to 300s.

   * When using the HTTP protocol: the default value of dial_timeout is 30s, and the default value of read_timeout is 300s.

* The driver enables `keepAlive` by default to support connection reuse and avoid creating short\-lived connections.


<span id="32673c3a"></span>
### Use the TCP/Native protocol


* Use ClickHouse Driver's OpenDB to create a connection

   ```Go
   import (
       "context"
       //"crypto/tls"
       "database/sql"
       "fmt"
       "github.com/ClickHouse/clickhouse-go/v2"
       "github.com/google/uuid"
       "time"
   )
   
   func main() {
       host := "{Host}"
       port := 19000
       password := "{Password}"
       user := "{User}"
       database := "{Database}"
       virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"
   
       db := clickhouse.OpenDB(&clickhouse.Options{
        Addr: []string{fmt.Sprintf("%s:%d", host, port)},
        Auth: clickhouse.Auth{
           Database: database,
           Username: user,
           Password: password,
        },
        Protocol: clickhouse.Native,
        TLS: &tls.Config{
           InsecureSkipVerify: true,
        },
        Settings: clickhouse.Settings{
           "virtual_warehouse": virtual_warehouse_id,
        },
       })
   ```
   

* Create a connection using a Go Database DSN (Data Source Name)

   ```Go
   import (
       "context"
       //"crypto/tls"
       "database/sql"
       "fmt"
       "github.com/ClickHouse/clickhouse-go/v2"
       "github.com/google/uuid"
       "time"
   )
   
   func main() {
       host := "{Host}"
       port := 19000
       password := "{Password}"
       user := "{User}"
       database := "{Database}"
       virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"
   
       db, err := sql.Open(
          "clickhouse",
          fmt.Sprintf("clickhouse://%v:%v@%v:%v/%v?secure=true&virtual_warehouse=%v", user, password, host, port, database, virtual_warehouse_id),
       )
      if err != nil {
         log.Fatal(err)
      }
   ```
   


<span id="d8442976"></span>
### Use the HTTP protocol

When creating a global connection with the HTTP protocol, you must add the `describe_query_with_data_type_flags=0` parameter.


* Use ClickHouse Driver's OpenDB to create a connection

   ```Go
   import (
       "context"
       //"crypto/tls"
       "database/sql"
       "fmt"
       "github.com/ClickHouse/clickhouse-go/v2"
       "github.com/google/uuid"
       "time"
   )
   
   func main() {
       host := "{Host}"
       port := 8123
       password := "{Password}"
       user := "{User}"
       database := "{Database}"
       virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"
   
       db := clickhouse.OpenDB(&clickhouse.Options{
        Addr: []string{fmt.Sprintf("%s:%d", host, port)},
        Auth: clickhouse.Auth{
           Database: database,
           Username: user,
           Password: password,
        },
        Protocol: clickhouse.HTTP,
        TLS: &tls.Config{
           InsecureSkipVerify: true,
        },
        Settings: clickhouse.Settings{
           "virtual_warehouse":                   virtual_warehouse_id,
           "describe_query_with_data_type_flags": "0",
        },
       })
   ```
   

* Create a connection using a Go database DSN (Data Source Name)

   ```Go
   import (
       "context"
       //"crypto/tls"
       "database/sql"
       "fmt"
       "github.com/ClickHouse/clickhouse-go/v2"
       "github.com/google/uuid"
       "time"
   )
   
   func main() {
       host := "{Host}"
       port := 8123
       password := "{Password}"
       user := "{User}"
       database := "{Database}"
       virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"
   
       db, err := sql.Open(
          "clickhouse",
          fmt.Sprintf("https://%v:%v@%v:%v/%v?secure=true&describe_query_with_data_type_flags=0&virtual_warehouse=%v", user, password, host, port, database, virtual_warehouse_id),
       )
       if err != nil {
          log.Fatal(err)
       }
   ```
   


<span id="98a804cd"></span>
## Custom query ID

You can use Context to set the query ID.

```Go
func UseContextSendQueryId(db *sql.DB) {
    queryId, _ := uuid.NewUUID()
    ctx := clickhouse.Context(context.Background(), clickhouse.WithQueryID(fmt.Sprintf("customer_%v", queryId.String())))
    _, err := db.ExecContext(ctx, "DROP DATABASE IF EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }
}
```


<span id="df6bf02b"></span>
## Custom query settings

```Go
func UseContextSendQuerySetting(db *sql.DB) {
// Use a context to pass settings for a specific API call
    ctx := clickhouse.Context(context.Background(), clickhouse.WithSettings(clickhouse.Settings{
       "max_execution_time": 450,
    }))

    var settingValue uint16
    if err := db.QueryRowContext(ctx, "SELECT getSetting('max_execution_time')").Scan(&settingValue); err != nil {
       log.Fatal(err)
    }
    fmt.Printf("settingValue: %v\n", settingValue)
    if settingValue != 450 {
       panic(fmt.Sprintf("expected setting value to be 450, got %d", settingValue))
    }
}
```


<span id="395219e8"></span>
## Complete connection and query example

You can use the following code to connect to ByteHouse and manage data.

```Go
import (
    "context"
    //"crypto/tls"
    "database/sql"
    "fmt"
    "github.com/ClickHouse/clickhouse-go/v2"
    "github.com/google/uuid"
    "time"
)

func main() {
    host := "{Host}"
    port := 8123 // Set the port based on the protole: 8123 for HTTP or 19000 for TCP
    password := "{Password}"
    user := "{User}"
    database := "{Database}"
    virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"

    //db := clickhouse.OpenDB(&clickhouse.Options{
    // Addr: []string{fmt.Sprintf("%s:%d", host, port)},
    // Auth: clickhouse.Auth{
    //    Database: database,
    //    Username: user,
    //    Password: password,
    // },
    // Protocol: clickhouse.Native,
    // TLS: &tls.Config{
    //    InsecureSkipVerify: true,
    // },
    // Settings: clickhouse.Settings{
    //    "virtual_warehouse": virtual_warehouse_id,
    // },
    //})
    db, err := sql.Open(
       "clickhouse",
       fmt.Sprintf("clickhouse://%v:%v@%v:%v/%v?secure=true&virtual_warehouse=%v", user, password, host, port, database, virtual_warehouse_id),
    )
    if err != nil {
       log.Fatal(err)
    }

    defer db.Close()

    if err := db.Ping(); err != nil {
       log.Fatal(err)
    }

    UseContextSendQueryId(db)
    UseContextSendQuerySetting(db)

    _, err = db.Exec("DROP DATABASE IF EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }

    _, err = db.Exec("CREATE DATABASE IF NOT EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }

    _, err = db.Exec(`
CREATE TABLE IF NOT EXISTS bhgotest.example (
        Col1 UInt8
    , Col2 String
    , Col3 FixedString(3)
    , Col4 UUID
    , Col5 Map(String, UInt8)
    , Col6 Array(String)
    , Col7 Tuple(String, UInt8, Array(Map(String, String))) KV
    , Col8 DateTime
) Engine = CnchMergeTree() ORDER BY tuple()
`)
    if err != nil {
       log.Fatal(err)
    }

    batchInsert, err := db.Begin()
    if err != nil {
       log.Fatal(err)
    }
    batchInsertPrepare, err := batchInsert.Prepare("INSERT INTO bhgotest.example")
    if err != nil {
       log.Fatal(err)
    }
    for i := 0; i < 1000; i++ {
       _, err := batchInsertPrepare.Exec(
          uint8(42),
          "ClickHouse", "Inc",
          uuid.New(),
          map[string]uint8{"key": 1},             // Map(String, UInt8)
          []string{"Q", "W", "E", "R", "T", "Y"}, // Array(String)
          []any{ // Tuple(String, UInt8, Array(Map(String, String)))
             "String Value", uint8(5), []map[string]string{
                {"key": "value"},
                {"key": "value"},
                {"key": "value"},
             },
          },
          time.Now(),
       )
       if err != nil {
          log.Fatal(err)
       }
    }
    batchInsert.Commit()

    row := db.QueryRow("SELECT * FROM bhgotest.example  limit 1")
    var (
       col1             uint8
       col2, col3, col4 string
       col5             map[string]uint8
       col6             []string
       col7             interface{}
       col8             time.Time
    )
    if err := row.Scan(&col1, &col2, &col3, &col4, &col5, &col6, &col7, &col8); err != nil {
       log.Fatal(err)
    }
    print(col1, col2, col3, col4, col5, col6, col7)

    db.Exec("DROP TABLE IF EXISTS bhgotest.example")

}

func UseContextSendQueryId(db *sql.DB) {
    queryId, _ := uuid.NewUUID()
    ctx := clickhouse.Context(context.Background(), clickhouse.WithQueryID(fmt.Sprintf("customer_%v", queryId.String())))
    _, err := db.ExecContext(ctx, "DROP DATABASE IF EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }
}

func UseContextSendQuerySetting(db *sql.DB) {
    // we can use context to pass settings to a specific API call
    ctx := clickhouse.Context(context.Background(), clickhouse.WithSettings(clickhouse.Settings{
       "max_execution_time": 450,
    }))

    var settingValue uint16
    if err := db.QueryRowContext(ctx, "SELECT getSetting('max_execution_time')").Scan(&settingValue); err != nil {
       panic(err)
    }
    fmt.Printf("settingValue: %v\n", settingValue)
    if settingValue != 450 {
       panic(fmt.Sprintf("expected setting value to be 450, got %d", settingValue))
    }
}
```
