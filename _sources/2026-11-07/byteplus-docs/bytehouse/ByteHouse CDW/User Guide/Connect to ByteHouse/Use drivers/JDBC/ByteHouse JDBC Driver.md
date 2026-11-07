---
title: "ByteHouse JDBC Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-bytehouse-jdbc-driver"
---

ByteHouse JDBC Driver is a driver that enables Java applications to connect to the ByteHouse cloud data warehouse through the JDBC interface. It supports data querying, insertion, and other operations, helping Java developers quickly integrate ByteHouse and achieve efficient data access. This tutorial introduces how to connect to and access the ByteHouse cloud data warehouse using JDBC.

<span id="035ba1f6"></span>
# Environment requirements

Support Java 1.8.0_261 or later (requires TLS v1.3 support).

<span id="02cfa533"></span>
# Recommended version

It is recommended to use the latest version of ByteHouse JDBC Driver. Go to the [ByteHouse Java Driver index](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) page to obtain the latest version of the ByteHouse JDBC Driver jar file.

<span id="a4fdf462"></span>
# Driver compatibility

Some SQL statements and functions are affected by the driver version. For details, refer to the table below.


|SQL/Function |Driver version |
|---|---|
|replace into |≥1.1.67 |


<span id="3374e87c"></span>
# Install ByteHouse JDBC driver

<span id="9b9ace80"></span>
## Local installation

Please go to the [ByteHouse Java Driver index](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) page. You can obtain the latest version of the ByteHouse JDBC Driver jar file.

After obtaining the jar file, simply add the compiled jar file to your project, or use your chosen dependency management tool to add this project as a dependency. Then, you can import and use classes in a Java program.

<span id="f0ff65d4"></span>
## Add the driver as a Gradle dependency

The following is an example of using the ByteHouse JDBC driver with Gradle:

```Java
repositories {
    // This is public bytedance repository for downloading artifacts
    maven {
        url "https://artifact.bytedance.com/repository/releases"
    }
}

dependencies {
    implementation "com.bytedance.bytehouse:driver-java:1.1.74:all"
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the above example, <code>java:1.1.74</code> is a sample version number. In practice, you need to replace it with the latest version number. Go to the <a href="https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/">ByteHouse Java Driver index</a> page to obtain the latest version of the driver file.</div>


<span id="080071aa"></span>
## Add the driver as a Maven dependency

Examples of using the ByteHouse JDBC driver via Maven are as follows:

```Java
// This is public bytedance repository for downloading artifacts
<repository>
    <id>bytedance</id>
    <name>ByteDance Public Repository</name>
    <url>https://artifact.bytedance.com/repository/releases</url>
</repository>

<dependency>
    <groupId>com.bytedance.bytehouse</groupId>
    <artifactId>driver-java</artifactId>
    <version>1.1.74</version>
    <classifier>all</classifier>
</dependency> 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the above example, <code>java:1.1.74</code> is a sample version number. When using this example, replace the sample version number with the latest version number. Go to the <a href="https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/">ByteHouse Java Driver index</a> page to obtain the latest version of the driver file.</div>


<span id="c9f9f1ac"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to the ByteHouse JDBC Driver using IAM users or database users. The differences between IAM users and database users are described below; you may choose as needed.


* **IAM User** is a user created in BytePlus Identity and Access Management (IAM). The user's privileges are determined by IAM privilege policies and the ByteHouse resource and data privileges you grant. IAM users can access the ByteHouse Console, and ByteHouse also supports access through CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database User** is a database\-level user created in ByteHouse and can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse Console, but access to ByteHouse is supported through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="32e04058"></span>
## IAM users

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using IAM user.

The following table describes the general parameters:


|Param |Configuration description |
|---|---|
|Host |The public or private domain name of your ByteHouse instance. You can view and copy this information from the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**, for details, please see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |Fixed at 19000. |
|User |Fixed to bytehouse. |
|Password |To obtain the ByteHouse API Key, you can get it in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|Database |Configure the ByteHouse database name for connection. You can log in to the ByteHouse Console and view and copy databases on the **Database** page. |
|virtual_warehouse |Optional. The name of the virtual warehouse group. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>Log in to the **ByteHouse Console**, click **virtual warehouse** at the top, and then view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If this parameter is not configured, the default virtual warehouse for your account is used. |


<span id="7337519b"></span>
## Database users

Please refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889) to learn how to connect to ByteHouse using a database user account.

General parameter descriptions are as follows:


|Param |Configuration description |
|---|---|
|Host |The public or private domain name of your ByteHouse instance. You can view and copy this from the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |Fixed at 19000. |
|User |Username format is `{accountID_or_accountName}::{username}[::{envID}]`. For details, see [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90):<br><br><br>* `{accountID_or_accountName}`: This refers to the BytePlus User Account ID or Name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the Account ID or Name.<br><br>* `{username}`: Refers to the username of the ByteHouse database account used to log in. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users** \> **View Database username**.<br><br>* `{envID}`: Optional configuration, the name of the environment where the database is located. If you use the default environment, you do not need to specify it; to use other environments, specify the environment name, and do not add `[]` during configuration. You can log in to the **ByteHouse** **Console**, where you can obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>   Usage examples are as follows:<br><br>   * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>   * No environment ID configured: `21xxxxxxxx::demouser` |
|Password |The database account password is set by the administrator when the account is created. Contact the administrator to obtain the password. If your password is lost or forgotten, you can contact the administrator to reset it. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|Database |Configure the ByteHouse database name for connection. Log in to the ByteHouse Console. On the **Database** page, you can view and copy databases. |
|virtual_warehouse |Optional configuration. Configure as the virtual warehouse name. To specify a virtual warehouse for query and write operations, configure this parameter.<br><br>Log in to the **ByteHouse Console**, click the virtual warehouse at the top, and view and copy the virtual warehouse ID. Example: `vw-{environment_id}{account_id}-{virtual_warehouse_name}`.<br><br>If this parameter is not configured, the default virtual warehouse for your account is used. |


<span id="749eec7f"></span>
# Basic usage

You can use the following code to connect to ByteHouse and start using standard statements to query, write, and read data in ByteHouse.


* Timeout configuration: The default value of ping_timeout is 10s, query_timeout is 0s, and connect_timeout is 0s. The send_timeout and receive_timeout parameters do not take effect currently.

* The driver supports `keepAlive` by default, which enables connection reuse and helps avoid creating short\-lived connections.


<span id="50813f0c"></span>
## Connect to ByteHouse

You can refer to the code below to connect to ByteHouse. When using the code below, be sure to replace the following fields in the connection statement: `{host}`, `{Password}`, `{User}`, `{Database}`, `{VITUAL_WAREHOUSE_ID}`, and other connection information fields. For information on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-jdbc-driver#c9f9f1ac).

<span id="4a35946e"></span>
### Use Properties to configure a connection

```Java
import com.bytedance.bytehouse.jdbc.statement.ByteHouseStatement;

import java.sql.*;
import java.util.Properties;
import java.util.UUID;

public class BHJDBC {
    public static void main(String[] args) {
        String host = "{Host}";
        int port = 19000;
        String password = "{Password}";
        String user = "{User}";
        String database = "{Database}";
        String virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";

        // Use properties to set basic connection parameters
        String url = String.format("jdbc:bytehouse://%s:%d", host, port);
        Properties properties = new Properties();
        // Different virtual warehouses can be set as needed
          properties.setProperty("virtual_warehouse", virtual_warehouse_id);
          properties.setProperty("secure", "true");
          properties.setProperty("user", user);
          properties.setProperty("password", password);
          properties.setProperty("database", database);

        Connection conn = null;
        try {
            conn = DriverManager.getConnection(url, properties);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="daa6c97e"></span>
### Use a URL parameter configuration to connect

```Java
import com.bytedance.bytehouse.jdbc.statement.ByteHouseStatement;

import java.sql.*;
import java.util.Properties;
import java.util.UUID;

public class BHJDBC {
    public static void main(String[] args) {
        String host = "{Host}";
        int port = 19000;
        String password = "{Password}";
        String user = "{User}";
        String database = "{Database}";
        String virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";

        String url = String.format("jdbc:bytehouse://%s:%d/?secure=true&user=%s&password=%s&database=%s&virtual_warehouse=%s",
                host, port, user, password, database, virtual_warehouse_id);


        Connection conn = null;
        try {
            conn = DriverManager.getConnection(url);
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            try {
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```


<span id="5fd6edc8"></span>
## Create databases and tables

After establishing a connection with ByteHouse, you can use the following code to create a database and a table.

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
     /*
     * Create database
     */
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
     /*
     * Create table
     */
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


<span id="efcf8e8d"></span>
## Write data

You can use the following code to write data.

```Java
     /*
     * Insert data
     */
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
     /*
     * Batch insert data
     */
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


<span id="bee13e8f"></span>
## Search

You can use the following code to query data.

```Java
     /*
     * Query data
     */
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


<span id="14048103"></span>
## Use Query ID

Setting a query ID helps track query execution status and facilitates subsequent debugging or management of query tasks. You can use the native JDBC method or the ByteHouse\-specific interface to set the query ID for a query.

<span id="9a75c275"></span>
### Custom query IDs

To set a query ID, add the `stmt.setQueryId(String.format("customized_%s", UUID.randomUUID()));` method call as shown in the following code.

```Java
    public static void dropDatabaseWithQueryId(Connection connection) {
        ByteHouseStatement stmt = null;
        try {
            stmt = (ByteHouseStatement)connection.createStatement();
            stmt.setQueryId(String.format("customized_%s", UUID.randomUUID()));
            String createDbQuery = "Drop DATABASE IF EXISTS bhjdbctest";
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
```


<span id="7c1b5bfa"></span>
### Use the ByteHouse\-specific interface

Starting with version v1.1.83, the ByteHouse JDBC driver supports assigning custom Query IDs.

<span id="e3d1308b"></span>
#### Prerequisites

Before using the Query ID feature, please ensure that the following conditions are satisfied:


* The ByteHouse JDBC Driver version is v1.1.83 or later.

* Replace JDBC interfaces with ByteHouse\-specific interfaces:

   * `Connection` → `ByteHouseConnection`

   * `Statement` → `ByteHouseStatement`

   * `PreparedStatement` → `ByteHousePreparedStatement`


If a Query ID is not explicitly specified during use, the ByteHouse JDBC driver will randomly and automatically generate a Query ID and associate it with the query.

<span id="6cbd9b8a"></span>
#### API Overview


|API |Configuration description |
|---|---|
|`ByteHouseConnection.setQueryId(String queryId)` |Set the Query ID only for the next query.<br><br>```Java```<br>```((ByteHouseConnection) connection).setQueryId("next-query-id");```<br>```connection.createStatement().executeQuery("SELECT 1");```<br>```// Query ID: "next-query-id"```<br> |
|`ByteHouseStatement.setQueryId(String queryId)` |Set the Query ID directly in ByteHouseStatement.<br><br>```Java```<br>```ByteHouseStatement statement = (ByteHouseStatement) connection.createStatement();```<br>```statement.setQueryId("next-query-id");```<br>```statement.executeQuery("SELECT 1");```<br>```// Query ID: "next-query-id"```<br> |
|`ByteHousePreparedStatement.setQueryId(String queryId)` |Due to limitations in the interaction between JDBC and ByteHouse, the Query ID must be set before the `PreparedStatement` is created. Therefore, do not directly use `setQueryId()` on `PreparedStatement` to insert data. The correct approach is shown below:<br><br>```Java```<br>```((ByteHouseConnection) connection).setQueryId("first-query-id");```<br>```ByteHousePreparedInsertStatement ps = (ByteHousePreparedInsertStatement) connection.prepareStatement("INSERT INTO demo.tbl VALUES (?)");```<br>```ps.setObject(1, 1);```<br>```ps.execute();```<br>```// Query ID: "first-query-id"```<br>``````<br>```// Set a new query ID for the next query```<br>```((ByteHouseConnection) connection).setQueryId("second-query-id");```<br>```ps.setObject(1, 2);```<br>```ps.execute();```<br>```// Query ID: "second-query-id"```<br> |
|`ByteHouseConnection.getQueryId()` |Returns the Query ID of the last executed statement on the connection.<br><br>```Java```<br>```((ByteHouseConnection) connection).setQueryId("first-query-id");```<br>```assertEquals(((ByteHouseConnection) connection).getQueryId(), "first-query-id");```<br>``````<br>```ByteHousePreparedInsertStatement ps = (ByteHousePreparedInsertStatement) connection.prepareStatement("INSERT INTO demo.tbl VALUES (?)");```<br>```ps.setObject(1, 1);```<br>```ps.execute();```<br>```assertEquals(((ByteHouseConnection) connection).getQueryId(), "first-query-id");```<br> |


<span id="5167ef4d"></span>
#### Use session\-level Query ID prefix

You can use the `session_query_id_prefix` property to set a session\-level prefix for all Query IDs.

```Java
Properties props = new Properties();
props.setProperty("session_query_id_prefix", "my-spark-application-");

Connection connection = new ByteHouseDriver().connect(jdbcUrl, props);
```


<span id="5c38aa72"></span>
#### Example 1: Prefix only (no explicit Query ID)

JDBC automatically adds an incrementing counter to each query's prefix:

```Java
Properties props = new Properties();
props.setProperty("session_query_id_prefix", "my-spark-application-");

Connection connection = new ByteHouseDriver().connect(jdbcUrl, props);

connection.createStatement().executeQuery("DROP DATABASE IF EXISTS demo"); 
// Query ID: "my-spark-application-1"
connection.createStatement().executeQuery("CREATE DATABASE IF NOT EXISTS demo");
// Query ID: "my-spark-application-2"
connection.createStatement().executeQuery("CREATE TABLE demo.tbl(id INT) ENGINE=CnchMergeTree ORDER BY id");
// Query ID: "my-spark-application-3"
```


<span id="afed84bb"></span>
#### Example 2: Prefix + explicit Query ID

The driver program concatenates the prefix with the user\-specified Query ID. It does not increment automatically.

```Java
Properties props = new Properties();
props.setProperty("session_query_id_prefix", "my-spark-application-");

Connection connection = new ByteHouseDriver().connect(jdbcUrl, props);

((ByteHouseConnection) connection).setQueryId("drop-db");
connection.createStatement().executeQuery("DROP DATABASE IF EXISTS demo");
// Query ID: "my-spark-application-drop-db"
((ByteHouseConnection) connection).setQueryId("create-db");
connection.createStatement().executeQuery("CREATE DATABASE IF NOT EXISTS demo");
// Query ID: "my-spark-application-create-db"
```


<span id="40cd04ab"></span>
# Configure connection pools

ByteHouse supports JDBC connections for developing data applications with connection pools like HikariCP and Druid.

<span id="07fc7593"></span>
## JDBC connection through HikariCP

The following example shows how to connect to HikariCP using the ByteHouse JDBC driver.

<span id="84ceebd6"></span>
### Maven dependencies

When using the ByteHouse JDBC driver with Maven, add the following dependencies to the `pom.xml` file to include HikariCP:

```XML
<dependency>
    <groupId>com.zaxxer</groupId>
    <artifactId>HikariCP</artifactId>
    <version>4.0.3</version>
</dependency>
```


<span id="4aca799d"></span>
### Gradle dependencies

When using the ByteHouse JDBC driver with Gradle, add the following dependency to the `build.gradle` file to include HikariCP:

```Groovy
dependencies {
    implementation 'com.zaxxer:HikariCP:4.0.3'
} 
```


<span id="467352b3"></span>
### Class name

When you use HikariCP, the class you interact with most frequently is `HikariDataSource`. You can configure and use HikariCP in a Java application as shown in the following example to create a ByteHouse connection.

<span id="7f5703e5"></span>
### Connections and queries

You can refer to the code below to connect to ByteHouse. When using it, be sure to replace the connection information fields in the connection statement, such as `host`, `port`, `password`, `user`, `database`, `virtual_warehouse_id`, and more. For information on how to obtain these fields, please refer to [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-jdbc-driver#c9f9f1ac).

```Java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

import java.sql.*;

public class HikariConnection {
    public static Connection getConnectionWithHikariConfig(String host, String port, String apiKey) throws Exception {

        HikariConfig config = new HikariConfig();
        String jdbcURL = String.format("jdbc:bytehouse://%s:%s/?api_key=%s", host, port, apiKey);
        
        // Standard Hikari configuration
        config.setJdbcUrl(jdbcURL);
        config.setMinimumIdle(5); // Min number of free connections in the pool
        config.setMaximumPoolSize(20); // Max connections in the pool
        config.setMaxLifetime(4 * 60 * 1000); // The connection will expire (be reclaimed) in 4 minutes, with a maximum allowed lifetime of 5 minutes
        config.setIdleTimeout(2 * 60 * 1000); // After the connection is idle for 2 minutes, it meets the condition for eviction (recycling)

        config.setPoolName("BH-Pool");
        config.addDataSourceProperty("secure", "true");
        // config.addDataSourceProperty("virtual_warehouse", {VIRTUAL_WAREHOUSE_ID});

        HikariDataSource hds = new HikariDataSource(config);
        Connection conn = hds.getConnection();
        return conn;
    }

    public static void main(String[] args) {
        String host = "{HOST}";
        String apiKey = "{API_KEY}";
        String port = "19000"; 
        try {
            Connection connection = getConnectionWithHikariConfig(host, port, apiKey);
            createDatabase(connection);
            createTable(connection);
            insertTable(connection);
            insertBatch(connection);
            selectTable(connection);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void createDatabase(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String createDbQuery = "CREATE DATABASE IF NOT EXISTS inventory";
            stmt.execute(createDbQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void createTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {

            String createTableQuery = "CREATE TABLE IF NOT EXISTS inventory.orders\n (" +
                    "OrderID String, OrderName String, OrderPriority Int8)" +
                    " engine = CnchMergeTree() partition by OrderID order by OrderID";
            stmt.execute(
                    createTableQuery
            );
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void insertTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String insertQuery = "INSERT INTO inventory.orders VALUES ('54895','Apple',12)";
            stmt.executeUpdate(
                    insertQuery
            );
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void insertBatch(Connection connection) {
        String insertQuery = "INSERT INTO inventory.orders (OrderID, OrderName, OrderPriority) VALUES (?,'Apple',?)";
        try (PreparedStatement pstmt = connection.prepareStatement(insertQuery)) {
            int insertBatchSize = 10;

            for (int i = 0; i < insertBatchSize; i++) {
                pstmt.setString(1, "ID" + i);
                pstmt.setInt(2, i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void selectTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String selectTableQuery = "SELECT * FROM inventory.orders";
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
        }
    }
}
```


<span id="f8a0713c"></span>
## Connect to JDBC using Druid

You can also connect to ByteHouse through Alibaba's Druid connection pool.

<span id="a92ce69c"></span>
### Maven dependencies

When using the ByteHouse JDBC driver with Maven, add the following dependencies to the `pom.xml` file to include Druid:

```XML
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.23</version>
</dependency>
```


<span id="782c0b4e"></span>
### Gradle dependencies

Please add the following dependencies to the `build.gradle` file to include Druid:

```Groovy
dependencies {
     implementation 'com.alibaba:druid:1.1.23' 
}
```


<span id="b894e598"></span>
### Class name

When using Druid, the class you interact with most frequently is `DruidDataSource`. You can configure and use Druid in a Java application to create a ByteHouse connection by following the example below.

<span id="a9f25ad8"></span>
### Connections and queries

Refer to the following to connect to ByteHouse. Caution: When connecting, be sure to replace the fields in the connection statement, such as `host`, `port`, `password`, `user`, `database`, `virtual_warehouse_id`, and more. For information on how to obtain these values, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-jdbc-driver#c9f9f1ac).

```Java
import com.alibaba.druid.pool.DruidDataSource;
import java.sql.*;
import java.util.Properties;

public class DruidConnection {
    public static Connection getConnectionWithDruidConfig(String host, String port, String apiKey) throws Exception {

        DruidDataSource druidDataSource = new DruidDataSource();
        String jdbcURL = String.format("jdbc:bytehouse://%s:%s/?api_key=%s", host, port, apiKey);
        druidDataSource.setUrl(jdbcURL);
        druidDataSource.setDriverClassName("com.bytedance.bytehouse.jdbc.ByteHouseDriver");
        druidDataSource.setMaxActive(10); // Max active connections
        druidDataSource.setInitialSize(2); // Initial connection count
        druidDataSource.setMinIdle(2); // Min idle connection count
        druidDataSource.setMaxWait(50000); // Max wait time for obtaining a connection
        Properties properties = druidDataSource.getConnectProperties();
        properties.setProperty("secure", "true");
        // properties.setProperty("virtual_warehouse", {VIRTUAL_WAREHOUSE_ID});

        druidDataSource.setConnectProperties(properties);
        Connection conn = druidDataSource.getConnection();

        return conn;
    }

    public static void main(String[] args) {
        String host = "{HOST}";
        String apiKey = "{API_KEY}";
        String port = "19000"; 
        try {
            Connection connection = getConnectionWithDruidConfig(host, port, apiKey);
            createDatabase(connection);
            createTable(connection);
            insertTable(connection);
            insertBatch(connection);
            selectTable(connection);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void createDatabase(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String createDbQuery = "CREATE DATABASE IF NOT EXISTS inventory";
            stmt.execute(createDbQuery);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void createTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {

            String createTableQuery = "CREATE TABLE IF NOT EXISTS inventory.orders\n (" +
                    "OrderID String, OrderName String, OrderPriority Int8)" +
                    " engine = CnchMergeTree() partition by OrderID order by OrderID";
            stmt.execute(
                    createTableQuery
            );
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void insertTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String insertQuery = "INSERT INTO inventory.orders VALUES ('54895','Apple',12)";
            stmt.executeUpdate(
                    insertQuery
            );
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void insertBatch(Connection connection) {
        String insertQuery = "INSERT INTO inventory.orders (OrderID, OrderName, OrderPriority) VALUES (?,'Apple',?)";
        try (PreparedStatement pstmt = connection.prepareStatement(insertQuery)) {
            int insertBatchSize = 10;

            for (int i = 0; i < insertBatchSize; i++) {
                pstmt.setString(1, "ID" + i);
                pstmt.setInt(2, i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

        } catch (SQLException ex) {
            ex.printStackTrace();
        }
    }

    public static void selectTable(Connection connection) {
        try (Statement stmt = connection.createStatement()) {
            String selectTableQuery = "SELECT * FROM inventory.orders";
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
        }
    }
}
```


<span id="c321ba8b"></span>
# FAQs

<span id="10f66932"></span>
## Unsupported or unrecognized SSL message error

If you encounter the `Unsupported or unrecognized SSL message` error, it is caused by a Java version that is too low. This error occurs in Java versions below 1.8.0_261 \*\*\*\* .

To resolve this issue, do one of the following:


* Upgrade Java version to Java 11.

* To retain the Java 1.8 environment, upgrade to Java 1.8.0_261 or a higher patch version to resolve this issue.


<span id="adb018b0"></span>
## DB::Exception: No local available worker group for vw\-xxxx

If you encounter the error `DB::Exception: No local available worker group for vw-xxxx`, this error occurs because the virtual warehouse has not started.

To resolve this issue, do one of the following:

Log in to the ByteHouse Cloud Data Warehouse console. On the **Virtual warehouse** page, check whether your virtual warehouse is in the `running` status.

<span id="abc47470"></span>
## Code: **UNAUTHENTICATED**

If you encounter the `Exception: unknown error: Code: UNAUTHENTICATED` error, this may be caused by incorrect configuration of `user` and `password`.

To resolve this issue, do one of the following:

Please ensure that the configured `user` and `password` are correct.

<span id="e54266ad"></span>
## DB::Exception: Database `xxx.yyy` doesn't exist

If you encounter the `DB::Exception: Database xxx.yyy doesn't exist` error, this may be caused by a database name configuration error.

To resolve this issue, do one of the following:

Please confirm that the database name configured in the connection information is correct.

<span id="8958ad72"></span>
## Exception: No appropriate protocol

If you encounter the `Caused by: javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)` error, this may be caused by incompatible TLS versions.

To resolve this issue, do one of the following:

Please add the following parameter to the end of the connection URL: `enabledTLSProtocols=TLSv1.2,TLSv1.3`.

For example,

```Java
String url = String.format("jdbc:bytehouse://%s:%d/%s?enabledTLSProtocols=TLSv1.2,TLSv1.3", host, port, database);
```
