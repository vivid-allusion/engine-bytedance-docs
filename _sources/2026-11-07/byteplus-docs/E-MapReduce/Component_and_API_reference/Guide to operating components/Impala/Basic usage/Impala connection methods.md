---
title: "Impala connection methods"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala_connection_methods"
---

This article introduces several methods for connecting to Impala.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An E\-MapReduce (EMR) cluster with the Impala component service has been created.

2. Currently, the Impala component is open via allowlist. You can apply for access using the method described in [Impala connection methods](https://docs.byteplus.com/docs/E-MapReduce/109296).


<span id="_2-使用-impala-shell-连接-impala"></span>
## 2 Connect to Impala using impala\-shell

To connect to Impala using impala\-shell, see: [Impala-shell tool](https://docs.byteplus.com/docs/E-MapReduce/109294) **。** 

<span id="_3-使用-jdbc-连接-impala"></span>
## 3 Connect to Impala using JDBC

You can connect to Impala using Hive's JDBC Driver.


1. Add Hive JDBC Driver dependency


```xml
<dependency>
    <groupId>org.apache.hive</groupId>
    <artifactId>hive-jdbc</artifactId>
    <version>2.3.9</version>
</dependency>
```



2. Obtain the Impala connection string


```java
package com.example;

import java.sql.*;

public class App 
{
    public static void main( String[] args ) throws Exception {
        String driverName = "org.apache.hive.jdbc.HiveDriver";
        Class.forName(driverName);

        // 1. If Impala has enabled LDAP authentication, you also need to provide a username and password
        // 2. Connection conn = DriverManager.getConnection("jdbc:hive2://<Impala deployment node>:21050/;auth=noSasl");

        Connection conn = DriverManager.getConnection("jdbc:hive2://180.xxx.xx.xx:21050/default;auth=noSasl");

        Statement stmt = conn.createStatement();
        stmt.executeUpdate("drop table if exists my_table");
        stmt.close();

        stmt = conn.createStatement();
        stmt.executeUpdate("CREATE TABLE my_table ( id INT) STORED AS PARQUET");
        stmt.close();

        stmt = conn.createStatement();
        stmt.executeUpdate("insert into my_table values(1)");
        stmt.close();

        stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("select * from my_table");

        while (rs.next()) {
            System.out.println("id=" + rs.getLong("id"));
        }

        rs.close();
        stmt.close();
        conn.close();
    }
}
```


<span id="_4-本地使用工具连接-impala"></span>
## 4 Connect to Impala locally using tools

The following describes how to use database tools locally to connect to Impala in the cloud.

<span id="_4-1-开启公网访问"></span>
### 4.1 Enable public network access


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, select and enter the **Cluster List \> Cluster Name \> Service List \> Impala** page.

3. Expand the deployment topology, click the ECS instance where StateStore is located, and enter the ECS instance details page.

4. On the ECS instance details page, bind the **public IP**. For details, see: [Bind public IP](https://www.volcengine.com/docs/6401/68687)

5. After binding the public IP to the cluster's master\-1 node, record the public IP address.

6. On the master\-1 ECS instance details page, click the 【**Security Group**】 tab at the top to enter the page for modifying security group access rules.

7. Click 【**Configure Rules**】 in the **Actions** column on the left to enter the security group list page.

8. Click **Access Rules \> Inbound Rules \> Add Rule**, add the IP address of your local machine (which can be viewed via [Impala connection methods](https://docs.byteplus.com/docs/E-MapReduce/109296)), and the port range **21050**.

9. Click the **Confirm** button to complete the security group addition.


<span id="_4-2-使用数据库工具连接-impala"></span>
### 4.2 Connect to Impala using database tools

The following uses DBeaver as an example to illustrate how to connect to Impala.

**Edit the connection configuration**

Details:


* JDBC URL: jdbc:hive2://xxx.xx.xx.xx(public IP):21050

* Host: The public IP of master\-1.

* Port: 21050.

* Add the driver property auth=noSasl


After connecting, you can view the corresponding Impala database information.
