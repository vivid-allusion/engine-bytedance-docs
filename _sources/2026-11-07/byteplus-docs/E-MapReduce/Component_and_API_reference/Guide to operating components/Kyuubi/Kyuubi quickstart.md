---
title: "Kyuubi quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Kyuubi_quickstart"
---

This article introduces two typical ways to use Kyuubi: connecting to Kyuubi for interactive analytics via the Beeline client, and programmatic access through standard JDBC/ODBC interfaces.

<span id="_1-前提条件"></span>
## 1 Prerequisites


* A Volcano Engine E\-MapReduce (EMR) Hadoop cluster has been created, and the Kyuubi service has been added to the cluster. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456), [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409).


<span id="_2-使用-beeline-客户端连接-kyuubi"></span>
## 2 Connect to Kyuubi using the Beeline client

You can use the beeline tool to connect to the Kyuubi service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The hostname naming convention in the following example applies to EMR 3.5.0 and later cluster versions. For the naming convention of older versions, see <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.</div>


<span id="_2-1-通过-zookeeper-连接到-kyuubi（推荐）"></span>
### 2.1 Connect to Kyuubi via ZooKeeper (recommended)

You need to specify a particular user to connect to the Kyuubi service. For username and password information, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).

```bash
beeline -n user1 -p user1_password -u "jdbc:hive2://master-1-1:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=kyuubi"
```


<span id="_2-2-直连-kyuubi-thrift-端口"></span>
### 2.2 Directly connect to the Kyuubi Thrift port

You can also connect directly to the Kyuubi service via the Thrift port.

```bash
beeline -n user1 -p user1_password -u "jdbc:hive2://master-1-1:10009"
```


<span id="_3-使用-jdbc-对-kyuubi-服务进行编程访问"></span>
## 3 Programmatic access to the Kyuubi service using JDBC

This section provides a Maven project example that uses the Hive JDBC Driver to connect to Kyuubi.

<span id="_3-1-依赖引入"></span>
### 3.1 Add dependencies

```bash
<dependency>
    <groupId>org.apache.hive</groupId>
    <artifactId>hive-jdbc</artifactId>
    <version>2.3.9</version>
</dependency>
```


<span id="_3-2-代码示例"></span>
### 3.2 Code sample

```bash
import java.sql.*;

public class JDBCTest {
    private static String driverName = "org.apache.hive.jdbc.HiveDriver";
    private static String kyuubiJdbcUrl = "jdbc:hive2://master-1-1:10009/default;";

    public static void main(String[] args) throws Exception {
        Class.forName(driverName);
        Connection conn = DriverManager.getConnection(kyuubiJdbcUrl);
        Statement st = conn.createStatement();
        ResultSet res = st.executeQuery("show databases");
        while (res.next()) {
            System.out.println(res.getString(1));
        }
        res.close();
        st.close();
        conn.close();
    }
}
```
