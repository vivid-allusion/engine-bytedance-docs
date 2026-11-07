---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hbase_Note"
---

<span id="_1-hbase基本概念"></span>
## 1 HBase basic concepts

HBase is an open\-source, non\-relational distributed database that is modeled after Google’s BigTable and implemented in Java. It is part of the Apache Software Foundation’s Hadoop project, runs on the HDFS file system, and provides BigTable\-like services for Hadoop.

Note on key HBase terminology:


|Noun |Note |
|---|---|
|**Namespace** |Namespaces are logical groupings of tables, similar to databases in relational database systems. This abstraction lays the foundation for upcoming multi\-tenant related features. |
|**Table** |Tables are declared in advance during schema definition. |
|**Row** |The row key is uninterpreted bytes. Rows are sorted lexicographically, with the lowest sequence appearing first in the table. An empty byte array is used to represent the start and end of the table namespace. |
|**Column family** |Columns in Apache HBase are divided into *column families*. All column members of a column family share the same prefix.<br><br>For example, the courses:history column and the courses:math column are both members of the courses column family. The colon (`:`) separates the column family and the column qualifier. The column family prefix must consist of printable characters. The column family qualifier, or qualifier suffix, can consist of any bytes. Column families must be declared in advance during schema definition. Columns do not need to be defined at schema time, but can be conceived dynamically when the table is running.<br><br>In practice, all column family members are stored together in the file system. Because tuning and storage specifications are performed at the column family level, it is recommended that all column family members have similar general access patterns and size characteristics. |
|**Cells** | *{row, column, version}*  tuples in HBase precisely specify a `cell`. The cell content is uninterpreted bytes. |
|**Versions** |There may be countless cells where the row and column are the same, but the cell address differs only in its version dimension.<br><br>HBase stores versions in descending order, so when reading from storage files, the latest value is found first. |


<span id="_2-数据模型操作"></span>
## **2 Data model operations**

The four main HBase data model operations are “**Get**”, “**Put**”, “**Scan**”, and “**Delete**”. Operations are performed using the [Table](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Table.html) instance.

<span id="_2-1-get"></span>
### **2.1 Get**

[Get](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Get.html) returns the attributes of a specified row. Get is executed using [Table.get](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Table.html#put-org.apache.hadoop.hbase.client.Put-).

<span id="_2-2-put"></span>
### **2.2 Put**

[Put](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Put.html) can add a new row to the table (if the key is new) or update an existing row (if the key already exists). Executed via [Table.put](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Table.html#batch-java.util.List-java.lang.Object:A-) (non\-writeBuffer) or [Table.batch](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Table.html#delete-org.apache.hadoop.hbase.client.Delete-) (non\-writeBuffer).

<span id="_2-3-scan"></span>
### **2.3 Scan**

[Scan](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Scan.html) allows iteration over multiple rows for specified attributes.

The following is an example of a “scan table” instance. Suppose a table is populated with rows keyed as “row1”, “row2”, and “row3”, then another set of rows with keys “abc1”, “abc2”, and “abc3”. The following example shows how to configure a Scan instance to return rows starting with “row”.

```Plain
public static final byte[] CF = "cf".getBytes();
public static final byte[] ATTR = "attr".getBytes();
...

Table table = ...      // instantiate a Table instance

Scan scan = new Scan();
scan.addColumn(CF, ATTR);
scan.setRowPrefixFilter(Bytes.toBytes("row"));
ResultScanner rs = table.getScanner(scan);
try {
  for (Result r = rs.next(); r != null; r = rs.next()) {
    // process result...
  }
} finally {
  rs.close();  // always close the ResultScanner!
}
```


<span id="_2-4-delete"></span>
### **2.4 Delete**

[Delete](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Delete.html) removes a row from the table. Deletion is performed using [Table.delete](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/client/Table.html#version.delete).

HBase does not modify data in place; therefore, delete operations are handled by creating new markers called tombstones. These delete markers are cleaned up during compaction.

<span id="_3-hbase-snapshot-迁移"></span>
## 3 HBase snapshot migration

<span id="_3-1-生成快照"></span>
### 3.1 Create a snapshot

Use the HBase Shell command to enter interactive mode and execute the following command to create a snapshot for the table named t1.

```Plain
snapshot 't1','t1_snapshot'
```


<span id="_3-2-查看快照生成结果"></span>
### 3.2 View snapshot creation results

```Plain
list_snapshots

SNAPSHOT                              TABLE + CREATION TIME                                                                                      
 t1_snapshot                          t1 (Thu Nov 03 21:20:51 +0800 2022)                                                                        
1 row(s) in 0.0080 seconds

=> ["t1_snapshot"]
```


<span id="_3-3-查看快照文件"></span>
### 3.3 View snapshot files

Exit HBase Shell using quit, then use the hdfs command to view the snapshot. You will see a snapshot file named `.hbase-snapshot`.

```Plain
hadoop fs -ls /apps/hbase/data


SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/hadoop-2.10.2/share/hadoop/common/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-log4j12-1.7.30.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
log4j:WARN custom level class [Relative to Yarn Log Dir Prefix] not found.
SLF4J: Actual binding is of type [org.slf4j.impl.Reload4jLoggerFactory]
Found 9 items
drwxr-xr-x   - hbase hdfs          0 2022-11-03 21:24 /apps/hbase/data/.hbase-snapshot
drwxr-xr-x   - hbase hdfs          0 2022-11-03 10:58 /apps/hbase/data/.tmp
drwxr-xr-x   - hbase hdfs          0 2022-11-03 21:15 /apps/hbase/data/MasterProcWALs
drwxr-xr-x   - hbase hdfs          0 2022-11-03 10:58 /apps/hbase/data/WALs
drwxr-xr-x   - hbase hdfs          0 2022-11-03 10:58 /apps/hbase/data/corrupt
drwxr-xr-x   - hbase hdfs          0 2022-11-03 10:58 /apps/hbase/data/data
-rw-r--r--   2 hbase hdfs         42 2022-11-03 10:54 /apps/hbase/data/hbase.id
-rw-r--r--   2 hbase hdfs          7 2022-11-03 10:54 /apps/hbase/data/hbase.version
drwxr-xr-x   - hbase hdfs          0 2022-11-03 21:17 /apps/hbase/data/oldWALs
```


<span id="_3-4-使用-snapshot-工具迁移快照文件"></span>
### 3.4 Use the snapshot tool to migrate snapshot files

<span id="_3-4-1-方式一"></span>
#### 3.4.1 Method 1

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If Ranger permission management is enabled on the EMR cluster, you need to set the relevant HDFS path permissions and Yarn submission permissions for the HBase user (the following commands are executed by the HBase user by default) in the Ranger UI. For details, see <a href="https://docs.byteplus.com/docs/undefined/69aa3969c85d87051aff3ed8">HDFS integration</a>, <a href="https://docs.byteplus.com/docs/undefined/69aa39638252b50542cbf57b">YARN integration</a>.</div>


Migrate to the local directory /tmp/20221103

```Plain
hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot t1_snapshot -copy-from hdfs:///apps/hbase -copy-to hdfs:///tmp/20221103
```


Check the migration results. There are two files: one is the snapshot, and the other is the metadata verification file.

```Plain
hadoop fs -ls /tmp/20221103

SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/hadoop-2.10.2/share/hadoop/common/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-log4j12-1.7.30.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
log4j:WARN custom level class [Relative to Yarn Log Dir Prefix] not found.
SLF4J: Actual binding is of type [org.slf4j.impl.Reload4jLoggerFactory]
Found 2 items
drwxr-xr-x   - root hdfs          0 2022-11-03 21:26 /tmp/20221103/.hbase-snapshot //快照文件
drwxr-xr-x   - root hdfs          0 2022-11-03 21:26 /tmp/20221103/archive //元数据校验文件
```


<span id="_3-4-2-方式二"></span>
#### 3.4.2 Method 2

Send the snapshot file directly to the hdfs directory of another HBase cluster.

For example, for another HBase cluster with the master node **emr\-4dh2cu897xxxxxxx\-master\-1**, execute the following command:

```Plain
hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot t1_snapshot -copy-to hdfs://emr-4dh2cu897xxxxxxx-master-1:8020/apps/hbase/data
```


Then log in to the **emr\-4dh2cu897xxxxxxx\-master\-1** node and use the HDFS command to check. For login instructions, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

```Plain
hadoop fs -ls /apps/hbase/data
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/hadoop-2.10.2/share/hadoop/common/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-reload4j-1.7.36.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/emr/2.0.0/tez-0.10.1/lib/slf4j-log4j12-1.7.30.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
log4j:WARN custom level class [Relative to Yarn Log Dir Prefix] not found.
SLF4J: Actual binding is of type [org.slf4j.impl.Reload4jLoggerFactory]
Found 10 items
drwxr-xr-x   - root  hdfs          0 2022-11-04 10:46 /apps/hbase/data/.hbase-snapshot //快照文件
drwxrwxrwx   - hbase hdfs          0 2022-11-03 16:46 /apps/hbase/data/.tmp
drwxrwxrwx   - hbase hdfs          0 2022-11-04 10:36 /apps/hbase/data/MasterProcWALs
drwxrwxrwx   - hbase hdfs          0 2022-11-02 11:19 /apps/hbase/data/WALs
drwxr-xr-x   - root  hdfs          0 2022-11-04 10:46 /apps/hbase/data/archive  //元数据校验文件
drwxrwxrwx   - hbase hdfs          0 2022-11-02 11:18 /apps/hbase/data/corrupt
drwxrwxrwx   - hbase hdfs          0 2022-11-02 11:19 /apps/hbase/data/data
-rwxrwxrwx   2 hbase hdfs         42 2022-11-01 20:12 /apps/hbase/data/hbase.id
-rwxrwxrwx   2 hbase hdfs          7 2022-11-01 20:12 /apps/hbase/data/hbase.version
drwxrwxrwx   - hbase hdfs          0 2022-11-04 10:42 /apps/hbase/data/oldWALs
```


<span id="_3-5-从快照恢复表"></span>
### 3.5 Restore a table from a snapshot


1. Copy the snapshot file from the HDFS directory to the data directory:


```Plain
hadoop fs -cp /tmp/20221103/* /apps/hbase/data
```



2. Enter HBase Shell:


```Plain
hbase shell
```



3. First, check whether the snapshot exists:


```Plain
list_snapshots


SNAPSHOT                                       TABLE + CREATION TIME                                                                                                                  
 t1_snapshot                                   t1 (Thu Nov 03 11:06:10 +0800 2022)                                                                                                    
1 row(s) in 0.1360 seconds

=> ["t1_snapshot"]
```



4. Restore the table from the snapshot:


```Plain
restore_snapshot 't1_snapshot'
```



5. Use list to view:


```Plain
list


TABLE                                                                                                                                                                                 
t1                                                                                                                                                                                    
1 row(s) in 0.0040 seconds

=> ["t1"]
```



6. Query the data and check whether it is consistent with the previously inserted data:


```Plain
get 't1','rowkey001', {COLUMN=>'f1:col1'}
COLUMN                                         CELL                                                                                                                                   
 f1:col1                                       timestamp=1667444472819, value=value01                                                                                                 
1 row(s) in 0.0510 seconds
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The migration method of approach two also follows the same verification process. You need to execute the same HBase commands on another cluster.</div>


<span id="_4-example"></span>
## 4 Example

Create, modify, and delete tables using Java:

The JDK can be 1.8, and the HBase version is 2.3.7.

```java
package com.example.hbase.admin;

import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HConstants;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Connection;
import org.apache.hadoop.hbase.client.ConnectionFactory;
import org.apache.hadoop.hbase.io.compress.Compression.Algorithm;

public class Example {

  private static final String TABLE_NAME = "MY_TABLE_NAME_TOO";
  private static final String CF_DEFAULT = "DEFAULT_COLUMN_FAMILY";

  public static void createOrOverwrite(Admin admin, HTableDescriptor table) throws IOException {
    if (admin.tableExists(table.getTableName())) {
      admin.disableTable(table.getTableName());
      admin.deleteTable(table.getTableName());
    }
    admin.createTable(table);
  }

  public static void createSchemaTables(Configuration config) throws IOException {
    try (Connection connection = ConnectionFactory.createConnection(config);
         Admin admin = connection.getAdmin()) {

      HTableDescriptor table = new HTableDescriptor(TableName.valueOf(TABLE_NAME));
      table.addFamily(new HColumnDescriptor(CF_DEFAULT).setCompressionType(Algorithm.NONE));

      System.out.print("Creating table. ");
      createOrOverwrite(admin, table);
      System.out.println(" Done.");
    }
  }

  public static void modifySchema (Configuration config) throws IOException {
    try (Connection connection = ConnectionFactory.createConnection(config);
         Admin admin = connection.getAdmin()) {

      TableName tableName = TableName.valueOf(TABLE_NAME);
      if (!admin.tableExists(tableName)) {
        System.out.println("Table does not exist.");
        System.exit(-1);
      }

      HTableDescriptor table = admin.getTableDescriptor(tableName);

      // Update existing table
      HColumnDescriptor newColumn = new HColumnDescriptor("NEWCF");
      newColumn.setCompactionCompressionType(Algorithm.GZ);
      newColumn.setMaxVersions(HConstants.ALL_VERSIONS);
      admin.addColumn(tableName, newColumn);

      // Update existing column family
      HColumnDescriptor existingColumn = new HColumnDescriptor(CF_DEFAULT);
      existingColumn.setCompactionCompressionType(Algorithm.GZ);
      existingColumn.setMaxVersions(HConstants.ALL_VERSIONS);
      table.modifyFamily(existingColumn);
      admin.modifyTable(tableName, table);

      // Disable an existing table
      admin.disableTable(tableName);

      // Delete an existing column family
      admin.deleteColumn(tableName, CF_DEFAULT.getBytes("UTF-8"));

      // Delete a table (Need to be disabled first)
      admin.deleteTable(tableName);
    }
  }

  public static void main(String... args) throws IOException {
    Configuration config = HBaseConfiguration.create();

    //Add any necessary configuration files (hbase-site.xml, core-site.xml)
    config.addResource(new Path(System.getenv("HBASE_CONF_DIR"), "hbase-site.xml"));
    config.addResource(new Path(System.getenv("HADOOP_CONF_DIR"), "core-site.xml"));
    createSchemaTables(config);
    modifySchema(config);
  }
}
```
