---
title: "JDBC"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/jdbc"
---

JAVA App can interact with ClickHouse through the ClickHouse JDBC Driver.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75efeb351b88e5e977e3470e316c8cf7.png) </span>

<span id="d87ce4b3"></span>
# Preparation


1. System is installed with a Java Environment.

2. Download official [ClickHouse JDBC Driver](https://github.com/ClickHouse/clickhouse-java).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This document has been verified under version v0.6.0\-patch4 of the driver.</div>


* <div data-tips="true" data-tips-type="warning">When using the ByteHouse <code>BitMap64</code> Data type, you need to install a dedicated ByteHouse JDBC patch. For details, see the later document.</div>


3. You can refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information) to view the connection information for the relevant cluster.


<span id="148a8953"></span>
# Connect to ByteHouse

Create a **`HelloClickHouse.java`**, paste the following code into it to connect to ByteHouse and perform a simple query:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

/**
 */
public class SimpleQuery {

  public static void main(String[] args) throws Exception {
    Class.forName("com.clickhouse.jdbc.ClickHouseDriver");
    Connection connection = DriverManager.getConnection("jdbc:clickhouse://<host>:<ip>", <username>, <password>);
    //Replace <host>:<ip> with the address and port of the service of the ByteHouse node, replace <username> with the username, and replace <password> with the password.
    Statement stmt = connection.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT (number % 3 + 1) as n, sum(number) FROM numbers(10000000) GROUP BY n");

    while (rs.next()) {
      System.out.println(rs.getInt(1) + "\t" + rs.getLong(2));
    }
  }
}  
```


The following example concatenates a series of complex SQL:

```java
package examples;

import java.sql.*;

/**
 * BatchQuery
 */
public class BatchQuery {
    public static void main(String[] args) throws Exception {
        try (Connection connection = DriverManager.getConnection("jdbc:clickhouse://<host>:<port>", username, password)) {
         //<Replace <host>:<ip> with the address and port of the service of the ByteHouse node, replace username with the actual username, and replace password with the actual password.
            try (Statement stmt = connection.createStatement()) {
                try (ResultSet rs = stmt.executeQuery("drop table if exists test_jdbc_example")) {
                    System.out.println(rs.next());
                }
                try (ResultSet rs = stmt.executeQuery("create table test_jdbc_example(day Date, name String, age UInt8) Engine=Log")) {
                    System.out.println(rs.next());
                }
                try (PreparedStatement pstmt = connection.prepareStatement("INSERT INTO test_jdbc_example VALUES(?, ?, ?)")) {
                    for (int i = 1; i <= 200; i++) {
                        pstmt.setDate(1, new Date(System.currentTimeMillis()));
                        if (i % 2 == 0)
                            pstmt.setString(2, "Zhang San" + i);
                        else
                            pstmt.setString(2, "Zhang San");
                        pstmt.setByte(3, (byte) ((i % 4) * 15));
                        System.out.println(pstmt);
                        pstmt.addBatch();
                    }
                    pstmt.executeBatch();
                }

                try (PreparedStatement pstmt = connection.prepareStatement("select count(*) from test_jdbc_example where age>? and age<=?")) {
                    pstmt.setByte(1, (byte) 10);
                    pstmt.setByte(2, (byte) 30);
                    printCount(pstmt);
                }

                try (PreparedStatement pstmt = connection.prepareStatement("select count(*) from test_jdbc_example where name=?")) {
                    pstmt.setString(1, "Zhang San");
                    printCount(pstmt);
                }
                try (ResultSet rs = stmt.executeQuery("drop table test_jdbc_example")) {
                    System.out.println(rs.next());
                }
            }
        }
    }

    public static void printCount(PreparedStatement pstmt) throws SQLException {
        try (ResultSet rs = pstmt.executeQuery()) {
            System.out.println(pstmt);
            if (rs.next())
                System.out.println(rs.getInt(1));
        }
    }
}
```


<span id="b93d8137"></span>
# BitMap64 JDBC Driver Patch

When using the official JDBC 0.3.2\-patch11 to connect to ByteHouse Enterprise Version 2.1.0, an error may occur: `java.sql.SQLException: Unknown data type: BitMap64`. In this case, a driver patch must be installed to ensure the program runs normally:


1. Download the ByteHouse JDBC patch:

   * Complete Package (contains JDBC + CLI + gRPC + HTTP Modules)

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cecebc1f3354df18ab6d283c5ef4e31~tplv-goo7wpa0wc-image.image" name="clickhouse-jdbc-0.3.3-SNAPSHOT-ce-patch-v1-all.jar">clickhouse-jdbc-0.3.3-SNAPSHOT-ce-patch-v1-all.jar</Attachment>
      

   * Individual Package (JDBC Module only)

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87dfea2c43f9466da3c35c8ede5ecd29~tplv-goo7wpa0wc-image.image" name="clickhouse-jdbc-0.3.3-SNAPSHOT-ce-patch-v1.jar">clickhouse-jdbc-0.3.3-SNAPSHOT-ce-patch-v1.jar</Attachment>
      

2. Copy the file to the `src/main/resources/lib` Folder in the project.

3. Using Maven, add the following dependencies in the project's pom.xml file.


```YAML
<dependencies>
    <dependency>
        <groupId>0.3.2-patch11-ce-patch-v1</groupId>
        <artifactId>0.3.2-patch11-ce-patch-v1</artifactId>
        <version>0.3.2-patch11-ce-patch-v1</version>
        <scope>system</scope>
        <systemPath>${project.basedir}/src/main/resources/lib/clickhouse-jdbc-0.3.3-SNAPSHOT-ce-patch-v1-all.jar</systemPath>
        <classifier>all</classifier>
        <exclusions>
            <exclusion>
                <groupId>*</groupId>
                <artifactId>*</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <!-- 0.3.3-SNAPSHOT-ce-patch-v1 dependency -->
        <groupId>org.roaringbitmap</groupId>
        <artifactId>RoaringBitmap</artifactId>
        <version>0.9.36</version>
    </dependency>
</dependencies>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Fill in the absolute <code>Path</code>, which can be partially obtained through the <code>${project.basedir}</code> function.</div>


<span id="9ae6f3b8"></span>
# FAQ

<span id="70f9b0a3"></span>
## When connecting to ByteHouse using JDBC, an error occurs: `Driver class 'org. not found roaringbitmap. longlong. Roaring64NavigableMap'`


* Possible reasons: The above error may occur if you are not using a dedicated BitMap64 driver.

* Solution: You can refer to the document, download, and use the BitMap64 driver patch, then connect to ByteHouse. For details, refer to [BitMap64 JDBC Driver Patch](https://docs.byteplus.com/docs/bytehouse/jdbc#b93d8137).
