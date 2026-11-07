---
title: "Go Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/go-driver"
---

This article explains how to connect and access ByteHouse CE via [ClickHouse Go Driver](https://github.com/ClickHouse/clickhouse-go/).

<span id="743472be"></span>
## Prerequisites

Click [here](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.3.0) to download the v2.3.0 version of the driver.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Recommended to use version 2.3.0 drivers to connect to ByteHouse CE, other versions of the drivers may cause compatibility issues.</div>


<span id="53eca270"></span>
## Connect to ByteHouse

Please refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information) for the Cluster Connection address, user name, and Password.

<span id="3245d119"></span>
## Basic usage

<span id="8e1ca560"></span>
### Connect to cluster

You can refer to the following code to connect to ByteHouse CE. When using, please replace the verification information.

```Go
import (
  "context"
  "fmt"
  "github.com/ClickHouse/clickhouse-go/v2"
)

conn, _ := clickhouse.Open(&clickhouse.Options{
Addr: []string{"<HOST>:<PORT>"},
Auth: clickhouse.Auth{Database: "default", Username: "<USERNAME>", Password: "<连接密码>"},
})

// test connection
if err := conn.Ping(context.Background()); err != nil {
fmt.Printf("error %s", err)
}

defer conn.Close()
```


Parameter description:


|Parameter |Configuration |
|---|---|
|`<HOST>` |Configure as the gateway address of ByteHouse Enterprise Edition.<br><br>You can log in to the ByteHouse Enterprise console, go to **Cluster management \> Cluster list \> Target cluster \> Basic information**, and view/copy the public or private network gateway address. |
|`<PORT>` |Fixed configuration: **9000**. |
|`Database` |Configure as **default**. To connect to other databases, set this to the desired database name. |
|`Username` |Configure with your username.<br><br>You can log in to the ByteHouse Enterprise console, go to **Access control \> User \> User List**, and view/copy the username. |
|`Password` |Configure with the password corresponding to the username above.<br><br>You can log in to the ByteHouse Enterprise console, click **Personal Center** in the top\-right corner, then click **Account management**, and copy the connection password from the **Cluster connection account**. |


You can also view the connection command for the Golang driver on the **Cluster management \> Cluster list \> Cluster \> Connect** tab, and obtain it by clicking the copy button.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd450fc185a446d8433690e146f7999~tplv-goo7wpa0wc-image.image) </span>

<span id="78f9f56d"></span>
### Official examples

Additionally, you can refer to the following SQL use cases to connect and use ByteHouse CE.


* [batch with release connection](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/batch_release_connection.go)

* [async insert](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/async.go)

* [batch struct](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/append_struct.go)

* [columnar](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/columnar_insert.go)

* [scan struct](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/scan_struct.go)

* [query parameters](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/query_parameters.go)

* [client info](https://github.com/ClickHouse/clickhouse-go/blob/main/examples/clickhouse_api/client_info.go)
