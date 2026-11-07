---
title: "Hive connection methods"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_connection_methods"
---

This article introduces three methods for submitting Hive SQL in an E\-MapReduce cluster.

<span id="_1-前提条件"></span>
## 1. Prerequisites


1. Log in to the cluster primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).


<span id="_2-连接方式"></span>
## 2. Connection methods

<span id="_2-1-方式一：通过-hive-客户端"></span>
### 2.1 Method 1: Using the Hive client


1. Run the following command to switch to the hive user.


```shell
su hive
```



2. Run the following command to enter the Hive command line.


```shell
hive
```


If the following information is returned, you have entered the Hive command line.

> Hive Session ID = aaa9c23d\-4975\-4c10\-bb9a\-1817c5fa36e6

> Logging initialized using configuration in file:/etc/emr/hive/conf/hive\-log4j2.properties Async: true

> Hive Session ID = 258437d2\-f601\-42c9\-bab3\-731b975b0642


<span id="_2-2-方式二：通过-beeline"></span>
### 2.2 Method 2: Using beeline

Use the beeline command

```shell
beeline -u "jdbc:hive2://<HiveServer2地址>:10000/" -n <username> -p <password>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For how to obtain the HiveServer2 address, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109261">Determine the HiveServer2 address</a>.</div>


* <div data-tips="true" data-tips-type="tip">The username and password parameters passed from the command line are obtained from the <strong>EMR Console \> Cluster Details \> User Management</strong> page, either imported via IAM user or manually added. For more information, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105426">User management</a>.</div>



After entering the password, you will receive the following information:

> Connecting to jdbc:hive2://<HiveServer2地址\>:10000/

> Connected to: Apache Hive (version 3.1.3\-ve\-2)

> Driver: Hive JDBC (version 3.1.3\-ve\-2)

> Transaction isolation: TRANSACTION_REPEATABLE_READ

> Beeline version 3.1.3\-ve\-2 by Apache Hive

> 0: jdbc:hive2://<HiveServer2地址\>:10000/\>


This indicates that you have successfully connected to Hive.

<span id="_2-3-方式三：通过-jdbc"></span>
### 2.3 Method 3: Using JDBC


1. Create a Maven project


```shell
mvn archetype:generate -DgroupId=com.example -DartifactId=hivejdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```



2. Add POM dependencies


```xml
<dependency>
      <groupId>org.apache.hive</groupId>
      <artifactId>hive-jdbc</artifactId>
      <version>3.1.2</version>
</dependency>
```



3. Use Hive JDBC to connect to the database


```java
package com.example;

import java.sql.*;

/** * Hello world! * */
public class App
{
    private static String driverName = "org.apache.hive.jdbc.HiveDriver";

    public static void main(String[] args) throws SQLException {

        try {
            Class.forName(driverName);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }

        // Username in LDAP
        String user = "hive";

        // User password in LDAP,
        String password = "*******";

        Connection con = DriverManager.getConnection(
                "jdbc:hive2://<HiveServer2地址>:10000", user, password);

        Statement stmt = con.createStatement();

        String sql = "show databases";
        ResultSet res = stmt.executeQuery(sql);

        while (res.next()) {
            System.out.println(res.getString(1));
        }

    }
}
```
