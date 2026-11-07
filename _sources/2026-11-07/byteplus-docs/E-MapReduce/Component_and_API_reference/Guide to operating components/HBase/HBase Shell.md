---
title: "HBase Shell"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/HBase_Shell"
---

In Volcano Engine E\-MapReduce (EMR) clusters, you can use HBase Shell commands to enter interactive command mode. This article introduces commonly used HBase Shell commands.

<span id="_1-前提条件"></span>
## 1 Prerequisites

An EMR cluster with HBase component services has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-基本命令"></span>
## 2 Basic commands

<span id="_2-1-ddl-shell-命令"></span>
### **2.1 DDL Shell commands**


1. Create

   Create a table. Provide a table name and a set of column family specifications (at least one), as well as table configuration (optional).

   The column specification can be a simple string (name) or a dictionary, and must include the NAME attribute.

   For example:

   ```javascript
   创建一个 namespace=ns1 和表限定符=t1的表
   hbase> create 'ns1:t1', {NAME => 'f1', VERSIONS => 5}
   
   指定配置项
   hbase> create 't1', 'f1', {NUMREGIONS => 15, SPLITALGO => 'HexStringSplit', REGION_REPLICATION => 2, CONFIGURATION => {'hbase.hregion.scan.loadColumnFamiliesOnDemand' => 'true'}}
   ```
   

2. List

   List all tables.

   ```javascript
   hbase> list
   ```
   

3. enable/disable

   Enable or disable a table.

   ```javascript
   hbase> enable 't1'
   hbase> disable 't1'
   ```
   

4. Drop

   Delete a table. The table must be disabled before deletion.

   ```javascript
   hbase> drop 't1'
   ```
   


<span id="_2-2-general-shell命令"></span>
### **2.2 General Shell commands**


1. Status

   View the current status of HBase.

   ```javascript
   hbase> status
   ```
   

2. Version

   View the current version of HBase.

   ```javascript
   hbase> version
   ```
   

3. Whoami

   View the current user.

   ```javascript
   hbase> whoami
   ```
   


<span id="_2-3-dml-shell-命令"></span>
### **2.3 DML Shell commands**


1. Get

   Retrieve the content of a row or cell; provide the table name, row, and an optional dictionary consisting of columns, timestamp, time range, and version.

   ```javascript
   hbase> get 'ns1:t1', 'r1'
   hbase> get 't1', 'r1', {COLUMN => 'c1', TIMESTAMP => ts1, VERSIONS => 4}
   ```
   

2. Put

   Place a cell value at the specified table/row/column and timestamp coordinates.

   ```javascript
   将一个单元格值放入表“ns1:t1”或“t1”的“r1”行的“c1”列，并标记为“ts1”的时间戳，执行
   hbase> put 'ns1:t1', 'r1', 'c1', 'value'
   ```
   

3. Delete

   Delete the cell value at the specified table/row/column and (optional) timestamp coordinates. The deletion must precisely match the coordinates of the cell to be deleted.

   ```javascript
   要从't1'表的'r1'行的'c1'列中删除一个单元格，执行以下操作
   hbase> delete 'ns1:t1', 'r1', 'c1', ts1
   ```
   


<span id="_3-其他命令"></span>
## 3 Other commands

In addition to the above commands, HBase Shell also supports a wide range of other functional commands, such as tools commands, namespace commands, and more. For specific command usage, refer to [http://xueai8.com/course/191/article](http://xueai8.com/course/191/article).
