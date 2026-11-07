---
title: "MySQL Go Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-go-driver"
---

The MySQL Go driver enables Go applications to interact with the ByteHouse Cloud Data Warehouse, allowing you to leverage Go's performance for high\-throughput data analysis. This is ideal for building backend services or data pipelines that query and manage large datasets stored in ByteHouse. This guide walks you through setting up your environment, establishing a connection, and performing basic data operations.

<span id="0c21b6c0"></span>
# Environment requirements


|Driver |Verified version |
|---|---|
|MySQL Go driver |1.8.1+, [Driver download link](https://github.com/go-sql-driver/mysql/releases) |
|Go |Golang 1.20+ |


<span id="9e107170"></span>
# Restrictions


* ByteHouse does not support the JSONB and Bitmap64 data types.

* Currently, the ByteHouse MySQL protocol does not support the ComPrepare protocol, so the insert batch logic cannot use prepared statements in the MySQL Go driver and can only construct SQL statements by string concatenation.

* Currently, authentication of database accounts is not supported.

* Setting query ID is not supported.

* Setting a virtual warehouse at the connection level (sql.Open) is not supported.

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="d4bdbc6a"></span>
# Install dependencies

You can find the latest documentation and release information in the [driver's GitHub repository](https://github.com/go-sql-driver/mysql).

```Go
go get -u github.com/go-sql-driver/mysql

-- Below is the dependency
go get -u github.com/stretchr/testify
```


After installation, add the following import statements to your Go code.

```Go
import (
        "database/sql"

        _ "github.com/go-sql-driver/mysql"
)
```


<span id="2c06f968"></span>
# Obtain ByteHouse connection information

You can connect to ByteHouse using IAM users. Here's how to obtain the required connection information. For more connection operations, please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).


|Param |Configuration description |
|---|---|
|host |This is the public or private domain name of your ByteHouse instance. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |The port is fixed at 3306. |
|user & password |Use the API Key as the user and password. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* user: The first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, then the user should use `xxxx`.<br><br>* password: The part after the dot in the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the user should enter `yyyy`. |
|database |The name of the database to connect to in ByteHouse. |


<span id="158ad38d"></span>
# Basic usage

You can use the following code to connect to ByteHouse and start using standard SQL statements to query, write, and read data.


* Timeout configuration: The default value for timeout is 0s, the default value for readTimeout is 0s, and the default value for writeTimeout is 0s.

* By default, `keepAlive` is enabled to allow connection reuse and prevent numerous short\-lived connections.


<span id="30a8b29f"></span>
## Connect to ByteHouse

Use the following code example, filling in your ByteHouse connection information. Caution: Replace the placeholder values for fields like `{Host}`, `{Password}`, and `{User}` with your actual credentials. For details on how to obtain this information, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/mysql-go-driver#2c06f968).

```Go
host := "{Host}"
port := 3306
password := "{Password}"
user := "{User}"
database := "{Database}"
virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"

db, err := sql.Open(
   "mysql", 
   fmt.Sprintf("%v:%v@(%v:%v)/%v", user, password, host, port, database),
)
if err != nil {
   log.Fatal(err)
}
```


<span id="31a28ac0"></span>
## Set a specific virtual warehouse (connection level)

After creating each connection, set the virtual warehouse configuration.

```Go
    _, err = conn.ExecContext(ctx, fmt.Sprintf("set virtual_warehouse = '%v'", virtual_warehouse_id))
    if err != nil {
        log.Fatal(err)
    }
```


<span id="114b5d1e"></span>
## Basic usage examples

```Go
package main

import (
    "context"
    "database/sql"
    "fmt"
    "github.com/go-sql-driver/mysql"
    _ "github.com/go-sql-driver/mysql"
    "github.com/google/uuid"
    "log"
    "strconv"
    "strings"
    "time"
)

func main() {
    host := "{Host}"
    port := 3306
    password := "{Password}"
    user := "{User}"
    database := "{Database}"
    virtual_warehouse_id := "{VIRTUAL_WAREHOUSE_ID}"

    db, err := sql.Open(
       "mysql", 
       fmt.Sprintf("%v:%v@(%v:%v)/%v", user, password, host, port, database),
    )
    if err != nil {
       log.Fatal(err)
    }

    if err := db.Ping(); err != nil {
       log.Fatal(err)
    }
    ctx := context.Background()
    conn, err := db.Conn(context.Background())
    if err != nil {
       log.Fatal(err)
    }
    defer conn.Close()
    defer db.Close()
    
    _, err = conn.ExecContext(ctx, fmt.Sprintf("set virtual_warehouse = '%v'", virtual_warehouse_id))
    if err != nil {
        log.Fatal(err)
    }
    
    _, err = conn.ExecContext(ctx, "DROP DATABASE IF EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }

    _, err = conn.ExecContext(ctx, "CREATE DATABASE IF NOT EXISTS bhgotest")
    if err != nil {
       log.Fatal(err)
    }

    _, err = conn.ExecContext(ctx, `
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

    values_list := make([]string, 0)
    for i := 0; i < 1000; i++ {
       value := fmt.Sprintf("(%v,%v,%v,'%v',%v,%v,%v,'%v')", uint8(42),
          "'ClickHouse'", "'Inc'",
          uuid.New(),
          "{'key': 1}",                     // Map(String, UInt8)
          "['Q', 'W', 'E', 'R', 'T', 'Y']", // Array(String)
          "('String Value', 5, [{'key': 'value'},{'key': 'value'},{'key': 'value'}])",
          time.Now().Format("2006-01-02 15:04:05"))
       values_list = append(values_list, value)
    }

    sql := fmt.Sprintf("INSERT INTO bhgotest.example VALUES %s",
       strings.Join(values_list, ", "))
    _, err = conn.ExecContext(ctx, sql)
    if err != nil {
       log.Fatal(err)
    }

    row := conn.QueryRowContext(ctx, "SELECT * FROM bhgotest.example  limit 1")
    var (
       col1             uint8
       col2, col3, col4 string
       col5             string
       col6             string
       col7             string
       col8             string
    )
    if err := row.Scan(&col1, &col2, &col3, &col4, &col5, &col6, &col7, &col8); err != nil {
       log.Fatal(err)
    }
    print(col1, col2, col3, col4, col5, col6, col7, col8)

    conn.ExecContext(ctx, "DROP TABLE IF EXISTS bhgotest.example")

}
```
