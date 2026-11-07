---
title: "MySQL JDBC Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-jdbc-driver"
---

This document explains how to connect to ByteHouse Cloud Data Warehouse using the open\-source MySQL JDBC driver. This method allows you to leverage the familiar MySQL protocol and existing Java tools for seamless data interaction, ideal for developers building Java applications that need to query or manage data in ByteHouse. This guide will walk you through installing the driver, configuring connection parameters, and performing basic data operations.

<span id="9589e584"></span>
# Environment requirements

JDK version: Java v1.8.0_261 or higher (requires TLS v1.3 support).

<span id="65377834"></span>
# Recommended version

MySQL JDBC driver version: It is recommended to use v8.3.0 or later.

<span id="84f14674"></span>
# Restrictions


* Currently, ByteHouse's JSONB and BitMap64 types are not supported.

* Setting query ID is not supported.

* To address any other unknown restrictions encountered during use, contact the ByteHouse team for assistance.


<span id="65ccbec8"></span>
# Install MySQL JDBC driver

<span id="7a04f56b"></span>
## Local installation

Click the [MySQL Connector Page](https://mvnrepository.com/artifact/com.mysql/mysql-connector-j/8.3.0) to download MySQL JDBC Driver v8.3.0.

<span id="66cd3a2a"></span>
## Add the driver as a Maven dependency

The following is an example of using the MySQL JDBC driver with Maven:

```Java
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.3.0</version>
</dependency>
```


<span id="e8f1a56a"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to MySQL using the MySQL JDBC Driver through IAM users or database users. The differences between IAM users and database users are as follows. You can choose according to your needs.


* **IAM User** is a user created in BytePlus Identity and Access Management (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. ByteHouse also supports access through the CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database users** are database\-level users created in ByteHouse who can be granted environment, resource, and data permissions. Database users cannot access the ByteHouse Console, but database users can access ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="cc87e41f"></span>
## IAM users


|Parameter |Configuration description |
|---|---|
|host |When configured as ByteHouse's public or private domain name, you can view the corresponding information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it to the fixed value 3306. |
|user & password |Use the API Key as both the username and password. For how to obtain the API key, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* user: The first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, then the user is `xxxx`.<br><br>* password: The second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, then the password is `yyyy`. |
|database |Configure the ByteHouse database name for connection. Log in to the ByteHouse Console, and on the **Database** page, view and copy the database name. |
|virtual_warehouse_id |Optional configuration: set as the virtual warehouse name. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>Log in to the **ByteHouse Console**, click **Virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If no configuration is specified, the system will use the default virtual warehouse you set in ByteHouse. |


<span id="12b01c23"></span>
## Database users


|Parameter |Configuration description |
|---|---|
|host |For ByteHouse's public/private domain name configuration, you can view and copy the domain name information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set it to the fixed value 3306. |
|user & password |* User should be configured as the format `{accountID_or_accountName}::{username}[::{envID}]`. For more information, please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username used to log in to the ByteHouse Database. You can view the database username in **ByteHouse Console** \> \*\*Access control \*\*\> **User** \> **View database username**.<br><br>   * `{envID}`: Optional configuration. It refers to the name of the environment where the database is located. When using the Default environment, configuration is not required; to use another environment, specify the environment name, and do not add `[]` during configuration. You can log in to the **ByteHouse** **Console**, where you can obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Usage examples are as follows:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Environment ID not configured: `21xxxxxxxx::demouser`<br><br>* password: Contact your administrator to obtain the password for the database account. To reset a lost or forgotten password, contact the administrator. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|database |Configure the ByteHouse database name for connection. You can log in to the ByteHouse Console and, on the **Database** page, view and copy databases. |
|virtual_warehouse_id |Optional configuration. Set it as the virtual warehouse name. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>Log in to the **ByteHouse Console**, click **Virtual warehouse** at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If no configuration is set, the default virtual warehouse that you set in ByteHouse will be used. |


<span id="3c73bd3e"></span>
# Basic usage

Use the following code to connect to ByteHouse. Once connected, you can use standard SQL statements to query, write, and read data.


* Timeout configuration: The default value of connect_timeout is 0s, and the default value of socketTimeout is 0s.

* By default, `keepAlive` is not supported. To use this feature, you need to create a new KeepAliveMysqlSocketFactory class. For details, refer to [Configure KeepAlive](https://docs.byteplus.com/docs/bytehouse/mysql-jdbc-driver#2ecb2966). This feature requires the use of JDK11.


<span id="4496085a"></span>
## Connection information

You can refer to the code below to connect to ByteHouse. Caution: When connecting, make sure to replace the fields `{Host}`, `{Password}`, `{User}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection parameters in the connection string. For information on how to obtain these fields, please refer to [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/mysql-jdbc-driver#e8f1a56a).

<span id="dd696106"></span>
### Use Properties to configure the connection

```Java
import java.sql.*;
import java.util.Properties;
import java.util.UUID;

public class MysqlJDBC {
    public static void main(String[] args) {
        String host = "{Host}";
        int port = 3306;
        String virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";
        String password = "{Password}";
        String user = "{User}";
        String database = "{Database}";

        // Set some basic parameters of the link by using properties
        String url = String.format("jdbc:mysql://%s:%d", host, port);
        Properties properties = new Properties();
        properties.setProperty("useSSl", "true");
        properties.setProperty("verifyServerCertificate", "false");
        properties.setProperty("enabledTLSProtocols", "TLSv1.2");
        properties.setProperty("user", user);
        properties.setProperty("password", password);
        properties.setProperty("database", database);
        // It is recommended to add the following parameters to improve performance
        // By default, MySQL's prepared statement splits batch data into individual records and executes each insert statement row by row when performing an insert batch.
        // After adding the following parameters, the driver will concatenate batch data into a single SQL statement and execute it to improve query efficiency
        properties.setProperty("rewriteBatchedStatements", "true");
        properties.setProperty("useServerPrepStmts", "false");
        
        Connection conn = null;
        Statement initStatement = null;
        try {
            conn = DriverManager.getConnection(url, properties);
            initStatement = conn.createStatement();
            initStatement.execute(String.format("SET virtual_warehouse='%s'", virtual_warehouse_id)); // Specify a particular virtual warehouse
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (initStatement != null) initStatement.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="60ae052c"></span>
### Use URL parameters to configure the connection

```Java
import java.sql.*;
import java.util.Properties;
import java.util.UUID;

public class CKJDBC {
    public static void main(String[] args) {
        String host = "{Host}";
        int port = 3306;
        String virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";
        String password = "{Password}";
        String user = "{User}";
        String database = "{Database}";
        
        String url = String.format("jdbc:mysql://%s:%d/?useSSl=true&verifyServerCertificate=false&enabledTLSProtocols=TLSv1.2&user=%s&password=%s&database=%s&rewriteBatchedStatements=true&useServerPrepStmts=false", // It is recommended to use rewriteBatchedStatements=true&useServerPrepStmts=false to improve batch insert efficiency
                host, port, user, password, database);

        Connection conn = null;
        Statement initStatement = null;
        try {
            conn = DriverManager.getConnection(url, properties);
            initStatement = conn.createStatement();
            initStatement.execute(String.format("SET virtual_warehouse='%s'", virtual_warehouse_id)); // Specify a particular virtual warehouse
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (initStatement != null) initStatement.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="2ecb2966"></span>
## Configure KeepAlive

To use the `keepAlive` feature, use JDK 11 and run the following code to configure and enable it.


1. Inherit the MySQL StandardSocketFactory class.

   ```Java
   package com.bytehouse.factory;
   
   import com.mysql.cj.conf.PropertySet;
   import com.mysql.cj.protocol.StandardSocketFactory;
   import jdk.net.ExtendedSocketOptions;
   import java.net.Socket;
   import java.util.logging.Level;
   import java.util.logging.Logger;
   
   public class KeepAliveMysqlSocketFactory extends StandardSocketFactory {
   
       private static final Logger LOG = Logger.getLogger(KeepAliveMysqlSocketFactory.class.getName());
   
       // TCP Keep-Alive parameter (unit: second)
       private static final int KEEPALIVE_IDLE = 60;
       private static final int KEEPALIVE_INTERVAL = 30;
       private static final int KEEPALIVE_COUNT = 60;
   
       @Override
       public Socket createSocket(PropertySet props)  {
           Socket sock = super.createSocket(props);
           configureKeepAlive(sock);
           return sock;
       }
   
       private void configureKeepAlive(Socket sock) {
           try {
               // Enable Keep-Alive
               sock.setKeepAlive(true);
   
               // Set TCP_KEEPIDLE (for example, 60 s)
               sock.setOption(ExtendedSocketOptions.TCP_KEEPIDLE, KEEPALIVE_IDLE);
   
               // Set TCP_KEEPINTVL (for example, 30 s)
               sock.setOption(ExtendedSocketOptions.TCP_KEEPINTERVAL, KEEPALIVE_INTERVAL);
   
               // Set TCP_KEEPCNT (for example, 5 probes)
               sock.setOption(ExtendedSocketOptions.TCP_KEEPCOUNT, KEEPALIVE_COUNT);
   
               LOG.info("TCP keep-alive options set successfully.");
           } catch (Exception e) {
               LOG.log(Level.WARNING, "can not configure Keep-Alive", e);
           }
       }
   
   }
   ```
   

2. Add the custom parameter named Factory to the connection URL.

   ```Java
   jdbc:mysql://<host>:3306/<database>?socketFactory=com.bytehouse.factory.KeepAliveMysqlSocketFactory
   ```
   


<span id="980bf3cd"></span>
## Create databases and tables

After establishing a connection with ByteHouse, you can use the following code to create databases and tables.

```Java
    public static void dropDatabase(Connection connection) {
        Statement stmt = null;
        try {
            stmt = connection.createStatement();
            String dropDbQuery = "Drop DATABASE IF EXISTS bhjdbctest";
            stmt.execute(dropDbQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void createDatabase(Connection connection) {
        Statement stmt = null;
        try {
            stmt = connection.createStatement();
            String createDbQuery = "CREATE DATABASE IF NOT EXISTS bhjdbctest";
            stmt.execute(createDbQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void createTable(Connection connection) {
        Statement stmt = null;
        try {
            stmt = connection.createStatement();
            String createTableQuery = "CREATE TABLE IF NOT EXISTS bhjdbctest.orders\n (" +
                    "OrderID String, OrderName String, OrderPriority Int8)" +
                    " engine = CnchMergeTree() partition by OrderID order by OrderID";
            stmt.execute(createTableQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="f5a8e3f2"></span>
## Write data

You can use the following code to write data.

```Java
    public static void insertTable(Connection connection) {
        Statement stmt = null;
        try {
            stmt = connection.createStatement();
            String insertQuery = "INSERT INTO bhjdbctest.orders VALUES ('54895','Apple',12)";
            stmt.executeUpdate(insertQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="e9944195"></span>
## Write data in batches

Use PreparedStatement for batch data insertion

```Java
    public static void insertBatch(Connection connection) {
        PreparedStatement pstmt = null;
        String insertQuery = "INSERT INTO bhjdbctest.orders (OrderID, OrderName, OrderPriority) VALUES (?,'Apple',?)";
        try {
            pstmt = connection.prepareStatement(insertQuery);
            int insertBatchSize = 10;
            for (int i = 0; i < insertBatchSize; i++) {
                pstmt.setString(1, "ID" + i);
                pstmt.setInt(2, i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (pstmt != null) pstmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="9778963d"></span>
## Query write results

You can use the following code to query data.

```Java
    public static void selectTable(Connection connection) {
        Statement stmt = null;
        try {
            stmt = connection.createStatement();
            String selectTableQuery = "SELECT * FROM bhjdbctest.orders";
            ResultSet rs = stmt.executeQuery(selectTableQuery);
            ResultSetMetaData rsmd = rs.getMetaData();
            int columnsNumber = rsmd.getColumnCount();
            while (rs.next()) {
                for (int i = 1; i <= columnsNumber; i++) {
                    if (i > 1) System.out.print(", ");
                    String columnValue = rs.getString(i);
                    System.out.print(columnValue);
                }
                System.out.println();
            }
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```


<span id="8e601271"></span>
# FAQs

<span id="e933f8c9"></span>
## Unsupported or unrecognized SSL message error

If you encounter the `Unsupported or unrecognized SSL message` error during use, it is caused by an outdated Java version. This error occurs in Java versions earlier than v1.8.0_261.

You can resolve this using the following methods:


* Upgrade the Java version to Java 11.

* To retain the Java 1.8 environment, upgrade to Java 1.8.0_261 or a higher patch version to resolve this issue.


<span id="384eeee9"></span>
## DB::Exception: No local available worker group for vw\-xxxx

To resolve the `DB::Exception: No local available worker group for vw-xxxx` error encountered during use, start the virtual warehouse.

You can resolve this using the following methods:

Log in to the ByteHouse Cloud Data Warehouse console, go to the **Virtual warehouse** page, and check whether the virtual warehouse you are using is in the `running` status.

<span id="3e140d2f"></span>
## Code: **UNAUTHENTICATED**

If you encounter the `Exception: unknown error: Code: UNAUTHENTICATED` error during use, this may be caused by incorrect `user` and `password` configuration.

You can resolve this using the following methods:

Ensure that the `user` and `password` you configured are correct.

<span id="177dad01"></span>
## DB::Exception: Database `xxx.yyy` doesn't exist

If you encounter the `DB::Exception: Database xxx.yyy doesn't exist` error during use, this may be caused by an incorrect database name configuration.

You can resolve this using the following methods:

Please confirm whether the database name configured in the connection information is correct.

<span id="96e84fec"></span>
## Exception: No appropriate protocol

If you encounter the error `Caused by: javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)` during use, this may be caused by TLS version incompatibility.

You can resolve this in the following ways:

Please add a parameter to the end of the connection URL: `enabledTLSProtocols=TLSv1.2,TLSv1.3`.

Examples are as follows:

```Java
String url = String.format("jdbc:mysql://%s:%d/%s?enabledTLSProtocols=TLSv1.2,TLSv1.3", host, port, database);
```
