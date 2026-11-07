---
title: "Statistics information and execution plan"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-statistics-information-and-execution-plan"
---

<span id="69520c53"></span>
## Statistics information

The current ByteHouse self\-developed query optimizer uses statistical information to enhance query performance. Currently, it supports users manually creating stats to collect statistics from tables or change query designs to enhance query performance. Future support for automatic collection and update capabilities will be provided. The supported syntax is as follows:


1. Create Statistics


```SQL
CREATE STATS [IF NOT EXISTS] (<db>.* | ALL | [<db>.]<table>['(' <col1>, <col2>, ..., <coln> ')']) 
        [WITH (FULLSCAN | SAMPLE [<rows> ROWS] [<ratio> RATIO])] 
```



2. Show Statistics


```SQL
SHOW (STATS|COLUMN_STATS) (<db>.* | ALL | [<db>.]<table>'('<col1>, <col2>, ..., <coln> ')' )
```



3. Delete Statistics


```SQL
DROP STATS (<db>.* | ALL | [<db>.]<table>['(' <col1>, <col2>, ..., <coln> ')' ])
```


<span id="0918ed2c"></span>
## Execution plan

For data engineers, diagnosing issues through execution plans is a crucial troubleshooting method. For example, problems such as Join order, whether the statistical information is missing, whether the estimation is reasonable, and whether the pushdown is activated. ByteHouse provides the capability to display physical execution plans. It uses the Explain + Query method for performing analyses, which facilitates a more intuitive analysis and optimization of queries alongside the visualization of Enquiry Details via Query Profiler.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, statistical information needs to be manually collected before generating execution plans.</div>


Generate physical execution plan:

```SQL
EXPLAIN (QUERY Statement) ;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, EXPLAIN semantics only support the analysis of DQL SELECT syntax.</div>


<span id="55aa7d3e"></span>
## Example


1. Create a database table.

   ```SQL
   CREATE DATABASE sampledb;
   CREATE TABLE sampledb.t1 
   (
     id Int64,
     name Int64
   ) ENGINE = CnchMergeTree()
   ORDER BY id;
   CREATE TABLE sampledb.t2
   (
     uid Int64,
     name Int64
   ) ENGINE = CnchMergeTree()
   ORDER BY uid;
   ```
   

2. Insert sample data.

   ```SQL
   INSERT INTO sampledb.t1 VALUES (1,'bob'),(2,'alice'),(3,'peter'),(4,'jay'),(5,'yiyang'),(6,'aurora');
   INSERT INTO sampledb.t2 VALUES (1,'smith'),(2,'parker'),(3,'taylor'),(4,'davis'),(5,'joines');
   ```
   

3. Collect statistical information of the table.

   ```SQL
   CREATE stats sampledb.t1;
   CREATE stats sampledb.t2;
   ```
   

   The results are as follows:

   
   |table_name |row_count |elapsed_time |
   |---|---|---|
   |t1 |6 |0.026777215 |
   

4. Show the statistical information of the table.

   ```SQL
   SHOW stats sampledb.t1;
   ```
   

5. Generate an execution plan for the table.

   ```SQL
   USE sampledb;
   EXPLAIN SELECT * FROM t1 JOIN t2 ON (t1.id = t2.uid);
   ```
   

   The results are as follows:

   ```Plain
   Gather Exchange est. 6 rows
   └─ Projection est. 6 rows
   │ Expressions: [id, name, uid], t2.name:=name_1
   └─ Inner Join est. 6 rows
   │ Condition: id == uid
   ├─ Local Exchange est. 6 rows
   │ └─ ReadFromStorage 2100069045.sampledb.t1 est. 6 rows
   │ Outputs: [id, name]
   └─ Broadcast Exchange est. 5 rows
   └─ ReadFromStorage 2100069045.sampledb.t2 est. 5 rows
   Outputs: [uid], name_1:=name
   ```
   

6. Delete the statistical information of the table.

   ```SQL
   DROP stats sampledb.t1;
   DROP stats sampledb.t1;
   ```
