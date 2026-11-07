---
title: "Query Gateway"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query-gateway"
---

<span id="简介"></span>
# Introduction

ByteHouse CE provides a gateway component for users, serving as the load balancer and unified search entry point of the cluster. The enterprise edition search gateway supports multiple access methods like community Clickhouse Client, Clickhouse Java JDBC, Clickhouse GO Driver, and can also connect using tools such as DataGrip and DBeaver.

The enterprise edition search gateway perceives the node health status, evenly distributing the search load to healthy ByteHouse nodes; clients need not be aware of changes in cluster nodes or maintenance operations such as scaling.

The functions implemented by the gateway are as follows:


* Distributes requests evenly across replicas and nodes using `round robin` technology.

* Supports checking node health status, circuit breaking faulty nodes to prevent sending requests to unhealthy nodes.

* Supports proxying requests to multiple ClickHouse clusters. Specifies clusters or automatically judges the routing cluster based on the user and the search.

* Supports different modes, including automatic assignment of any node, selection of specified nodes, or all nodes, replacing `on cluster` syntax.


You can view the private network gateway address and the public network gateway address (if the cluster has a bound external IP) by navigating through `Manage clusters -> Cluster List -> Click to View Details`.

<span id="08bddf7a"></span>
# Support project commands


|SQL Statement |Usage |TCP Protocol |HTTP Protocol |
|---|---|---|---|
|DROP |DATABASE |✅ |✅ |
||TABLE |✅ |✅ |
|CREATE |NORMAL |✅ |✅ |
| |DATABASE |✅ |✅ |
|SELECT |NORMAL |✅ |✅ |
||WITH CALUSE |✅ |✅ |
|INSERT INTO |NORMAL |✅ |✅ |
||INSERT INTO SELECT |✅ |✅ |
|ALTER |COLUMN |✅ |✅ |
||DELETE |✅ |✅ |
||UPDATE |✅ |✅ |
|SHOW |CREATE TABLE |✅ |✅ |
| |SHOW DATABASES |✅ |✅ |
| |SHOW TABLES |✅ |✅ |
|GRANT |PRIVILEGE |✅ |✅ |
| |ROLE |✅ |✅ |
|EXPLAIN |AST |✅ |✅ |
|REVOKE |PRIVILEGE |✅ |✅ |
|ATTACH | |✅ |✅ |
|CHECK TABLE | |✅ |✅ |
|DESCRIBE TABLE | |✅ |✅ |
|DETACH | |✅ |✅ |
|EXISTS | |✅ |✅ |
|KILL |QUERY |✅ |✅ |
|OPTIMIZE | |✅ |✅ |
|RENAME | |✅ |✅ |
|EXCHANGE | |✅ |✅ |
|SET | |✅ |✅ |
|SET ROLE | |✅ |✅ |
|TRUNCATE | |✅ |✅ |
|USE | |✅ |✅ |


<span id="897cc5ae"></span>
# Gateway function

<span id="80c3ae63"></span>
## HTTP connection

```powershell
curl --location --request POST '<gateway-address>:8123/?password=<password>&user=<user_name>&query_id=<query_id>&custom_gw_force_all_nodes=<true/false>&custom_gw_force\_ck_node=<node_ip>' \
--data-raw '<SQL>'
```


Parameters:


* `gateway-address`: Address of the gateway;

* `user`: ByteHouse Cluster Username;

* `password`: Password for the ByteHouse Cluster User;

* `query_id`: Specify the query ID, with a business identifier prefix recommended (e.g., “bi\-xxxxx”) for easy filtering of all queries under a business in the history later. Example: “bi\-xxxxx”;

* `Custom_gw_force_all_nodes`: [Optional] Send the query to all nodes, true/false (default is false); and `custom_gw_force_ck_node` can only choose one to fill in. The return value is the data from the last node, suitable for DDL statements.

* `custom_gw_force_ck_node`: [Optional] Send the query to a specified node, fill in the node's IP. and `custom_gw_force_all_nodes` can only choose one to fill in.

* `data-raw`: SQL statement sent to the cluster.


<span id="5ed505c1"></span>
## TCP connection

The following is an example using clickhouse\-client:

```shell
clickhouse-client -h <gateway-address> -p 9000 --user <Username> --password <Password>
```


Parameters:


* Gateway\-address: Gateway address.

* User: ByteHouse Cluster Username.

* Password: ByteHouse Cluster User Password;


After establishing the connection, you can use the `set` command to configure the following parameters:


* `custom_gw_force_all_nodes`: [Optional] Sends the query to all nodes, true/false (default false); and `custom_gw_force_ck_node` can only choose one setting.

* `custom_gw_force_ck_node`: [Optional] Sends the query to a specified node, fill in the node's IP. and `custom_gw_force_all_nodes` can only choose one setting;


<span id="2c7cd480"></span>
## Connection example

<span id="563a09c8"></span>
### Sent to any node

According to the load balancing strategy, select the optimal node for distribution.

**HTTP Direct Connection Example:** 

```bash
curl --location --request POST 'http://<gateway-address>:8123/?user=<user_name>&password=<password> \
--data-raw '<SQL>'
```


**ClickHouse Client connection example:** 

```bash
clickhouse client --host <HOST>.bytehouse-ce.bytepluses.com --user <USER> --password <PASSWORD>
```


**JDBC connection example:** 

If using the official website JDBC driver for Clickhouse: `https://github.com/ClickHouse/clickhouse-jdbc`

ClickHouse JDBC version:

```xml
<dependency>
    <groupId>com.clickhouse</groupId>
    <artifactId>clickhouse-jdbc</artifactId>
    <version>0.4.1<</version>
    <classifier>http</classifier>
</dependency>
```


Java example:

```java
package org.example;

import java.sql.*;

public class Main {

    static String jdbcUrl = "jdbc:clickhouse://<URL>:8123/default";
    static String user = "<USER>";
    static String password = "<PASSWORD>";

    public static void main(String[] args) throws ClassNotFoundException {
        try {
            Connection con = DriverManager.getConnection(jdbcUrl,user,password);
            Statement stmt = con.createStatement();
            ResultSet resultSet = stmt.executeQuery("select * from system.clusters");
            while (resultSet.next()) {
                System.out.println("host_name: " + resultSet.getString("host_name") + " is_local: " + resultSet.getInt("is_local"));
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```


**Golang example:** 

Clickhouse Go Driver version: [v2.7.0](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.7.0)

Code example:

```go
func TestSpecifyNode(t *testing.T) {
   ctx := context.Background()

   conn, err := clickhouse.Open(&clickhouse.Options{
      Addr: []string{"<URL>.bytehouse-ce.bytepluses.com:9000"},

      Auth:     clickhouse.Auth{Database: "default", Username: "<USER>", Password: "<USER>"},
      Debug:    true,
   })
   if err != nil {
      fmt.Printf("error----->: %v", err)
      return
   }

   defer conn.Close()

   rows, err := conn.Query(ctx, "select host_name, is_local from system.clusters")
   if err != nil {
      fmt.Printf("error-----:%v", err)
      return
   }

   var result struct {
      Col1 string `ch:"host_name"`
      Col2 uint8  `ch:"is_local"`
   }

   for {
      if rows.Next() {
         err := rows.ScanStruct(&result)
         if err != nil {
            fmt.Printf("error-----:%v", err)
            return
         }
         fmt.Printf("----> %s %d\n", result.Col1, result.Col2)
      } else {
         break
      }
   }
}
```


<span id="eaa91985"></span>
### Deploy to a specific node

**HTTP Direct connection example:** 

```bash
curl --location --request POST 'http://<gateway-address>:8123/?user=<user_name>&password=<password>&custom_gw_force_ck_node=<node_ip>' \
--data-raw '<SQL>'
```


**ClickHouse Client connection example:** 

```bash
clickhouse client --host <HOST> --user <USER> --password <PASSWORD>                     

ByteHouse Gateway :) set custom_gw_force_ck_node='<node_ip>'
```


**JDBC connection example:** 

If you want to use the ClickHouse official website JDBC driver, you can download it [here](https://github.com/ClickHouse/clickhouse-java).

ClickHouse JDBC version:

```xml
<dependency>
    <groupId>com.clickhouse</groupId>
    <artifactId>clickhouse-jdbc</artifactId>
    <version>0.4.1<</version>
    <classifier>http</classifier>
</dependency>
```


Java example:

```java
package org.example;

import java.sql.*;

public class Main {

    static String jdbcUrl = "jdbc:clickhouse://<URL>:8123/default?custom_settings=custom_gw_force_ck_node=<node_ip>";
    static String user = "<USER>";
    static String password = "<PASSWORD>";

    public static void main(String[] args) throws ClassNotFoundException {
        try {
            Connection con = DriverManager.getConnection(jdbcUrl,user,password);
            Statement stmt = con.createStatement();
            ResultSet resultSet = stmt.executeQuery("select * from system.clusters");
            while (resultSet.next()) {
                System.out.println("host_name: " + resultSet.getString("host_name") + " is_local: " + resultSet.getInt("is_local"));
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```


**Golang Example:** 

Clickhouse Go Driver version: [v2.7.0](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.7.0)

Code example:

```go
func TestSpecifyNode(t *testing.T) {
   ctx := context.Background()

   conn, err := clickhouse.Open(&clickhouse.Options{
      Addr: []string{"<URL>.bytehouse-ce.bytepluses.com:9000"},

      Auth:     clickhouse.Auth{Database: "default", Username: "<USER>", Password: "<USER>"},
      Debug:    true,
      Settings: map[string]interface{}{"custom_gw_force_ck_node": "<HOST>"},
   })
   if err != nil {
      fmt.Printf("error----->: %v", err)
      return
   }

   defer conn.Close()

   rows, err := conn.Query(ctx, "select host_name, is_local from system.clusters")
   if err != nil {
      fmt.Printf("error-----:%v", err)
      return
   }

   var result struct {
      Col1 string `ch:"host_name"`
      Col2 uint8  `ch:"is_local"`
   }

   for {
      if rows.Next() {
         err := rows.ScanStruct(&result)
         if err != nil {
            fmt.Printf("error-----:%v", err)
            return
         }
         fmt.Printf("----> %s %d\n", result.Col1, result.Col2)
      } else {
         break
      }
   }
}
```


<span id="9c324eb1"></span>
### Distribute to all nodes

**HTTP Direct connection example:** 

```bash
curl --location --request POST 'http://<gateway-address>:8123/?user=<user_name>&password=<password>&custom_gw_force_all_nodes=true \
--data-raw '<SQL>'
```


**ClickHouse Client example:** 

```java
clickhouse client --host <HOST>.bytehouse-ce.bytepluses.com --user <USER> --password <PASSWORD>

ByteHouse Gateway :) set custom_gw_force_all_nodes=true
ByteHouse Gateway :) CREATE TABLE default.test(`id` Int64,`info` String COMMENT '1') ENGINE = MergeTree ORDER BY id SETTINGS index_granularity = 8192

CREATE TABLE default.test
(
    `id` Int64,
    `info` String COMMENT '1'
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192
```


**JDBC connection example:** 

If you want to use the official website jdbc driver, you can download it [here](https://github.com/ClickHouse/clickhouse-java).

ClickHouse JDBC version:

```xml
<dependency>
    <groupId>com.clickhouse</groupId>
    <artifactId>clickhouse-jdbc</artifactId>
    <version>0.4.1<</version>
    <classifier>http</classifier>
</dependency>
```


Java example:

```java
package org.example;

import java.sql.*;

public class Main {

    static String jdbcUrl = "jdbc:clickhouse://<URL>:8123/default?custom_settings=custom_gw_force_all_nodes=true";
    static String user = "<USER>";
    static String password = "<USER>";

    public static void main(String[] args) throws ClassNotFoundException {
        try {
            Connection con = DriverManager.getConnection(jdbcUrl,user,password);
            Statement stmt = con.createStatement();
            ResultSet resultSet = stmt.executeQuery("select * from system.clusters");
            while (resultSet.next()) {
                System.out.println("host_name: " + resultSet.getString("host_name") + " is_local: " + resultSet.getInt("is_local"));
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```


**Golang connection example:** 

Clickhouse Go Driver version: [v2.7.0](https://github.com/ClickHouse/clickhouse-go/releases/tag/v2.7.0)

```go
func TestAllNodes(t *testing.T) {
   ctx := context.Background()

   conn, err := clickhouse.Open(&clickhouse.Options{
      Addr: []string{"<URL>.bytehouse-ce.bytepluses.com:9000"},

      Auth:     clickhouse.Auth{Database: "default", Username: "<USER>", Password: "<USER>"},
      Debug:    true,
      Settings: map[string]interface{}{"custom_gw_force_all_nodes": true},
   })
   if err != nil {
      fmt.Printf("error----->: %v", err)
      return
   }
   
   defer conn.Close()
   
   err = conn.Exec(ctx, "CREATE TABLE default.test(`id` Int64,`info` String COMMENT '1') ENGINE = MergeTree ORDER BY id SETTINGS index_granularity = 8192")
   if err != nil {
      fmt.Printf("error----->: %v", err)
      return
   }
}
```


<span id="c496d212"></span>
### Asynchronous query

(Only HTTP support) Can be used by adding X\-Async\-Query to the header. After sending, do not immediately receive the results, but use query_id to asynchronously request the query results, commonly used in large query scenes.

Example:

```bash
curl --location --request POST 'http://<gateway-address>:8123/?user=<user_name>&password=<password>&query_id=<queryID>' \
--header 'X-Async-Query: 1' \
--data-raw 'show tables FORMAT JSON;'
```


Response：


* When submitting asynchronously and the query is in progress, the return header contains the following information:

   * `Header：X-Async-Query: running`

* After the query is complete, results will be returned, and the header will include `X-Spend-Time` information (unit: ms):

   * `Header: X-Spend-Time: 100`


<span id="800d9ae4"></span>
# **Feature limitations**

TLS Data Encryption is not supported yet:

```bash
HTTPS & Clickhouse Client --secure
```
