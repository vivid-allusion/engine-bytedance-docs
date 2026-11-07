---
title: "JOIN clause"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/JOIN-clause-2"
---

The JOIN clause combines data from two or more tables. Torch Log Service (TLS) allows you to query data across projects, and query data from topics and external MySQL data sources. This topic describes the syntax of the JOIN clause and offers typical examples.

<span id="01fe3932"></span>
## **Syntax format**

TLS allows you to use the JOIN clause to combine data from two or more tables. You can query data from multiple topics of the same project at the same time, or from specific topics and external MySQL data sources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use the JOIN clause, when specifying a table name in JOIN_CONDITION or other parameters, type the column alias specified in the AS clause instead of the original table name.</div>


The syntax format of the JOIN clause is as follows:

```SQL
* |
SELECT 
  Key
FROM table1 AS alias1 
JOIN_TYPE table2 AS alias2
  ON JOIN_CONDITION
```


Parameter description


|Parameter |Description |
|---|---|
|Key |A column name or an expression. If you set it to the name of a column, the format is `table.key`, that is `TABLE_ALIAS.FIELD_NAME`, indicating a log field in a topic or database table. |
|JOIN_TYPE |The JOIN type. The following table describes the JOIN types supported by TLS. |
|table |The table name, which is the name of a topic or an external data source.<br><br>If the right table table2 and the left table table1 belong to different projects, specify the corresponding project name for both tables, such as `project1.table1`.<br><br>The name of the table preceding the JOIN keyword must be the name of a topic. The name of the table following the JOIN keyword can be the name of a topic or an external data source. For example, the name of table1 must be the name of a topic, and the name of table2 can be the name of a topic or an external data source. |
|alias |The alias of the table. |
|JOIN_CONDITION |The condition to join tables. Specify a field to join two tables preceding and following JOIN, such as `alias1.key1=alias2.key2`. |


The JOIN types are described as follows:


|JOIN Type |Description |
|---|---|
|LEFT JOIN |Returns all values that meet the conditions specified in the SELECT statement from the left table table1 regardless of whether matching values exist in the right table table2. |
|RIGHT JOIN |Returns all values that meet the conditions specified in the SELECT statement from the right table table2 regardless of whether matching values exist in the left table table1. |
|[INNER] JOIN |Returns the intersection result of matching values in both the left and right tables. INNER can be omitted. |
|FULL JOIN |Returns the union result of matching values in the left and right tables. |


<span id="942864a9"></span>
## **Examples**

<span id="5c160959"></span>
### **Example 1: Query data across topics**

Analyze the age distribution of active users. Count the number of page views in topic1 and calculate the age distribution of visitors in topic2 by userid and uid.


* Query and analysis statement:

   ```SQL
   * | 
   select 
     count(*) as pv
     t2.age  as age_group
   from project.topic1 as t1 left join project.topic2 as t2 on t1.userid = t2.uid 
   group by t2.age 
   order by pv desc
   ```
   

* Return result:

   
   |age_group |pv |
   |---|---|
   |10~20 |8000 |
   |20~30 |5000 |
   |30~40 |2000 |
   


<span id="53e7eb0d"></span>
### **Example 2: Query data across projects**

Analyze the age distribution of active users. Count the number of page views in topic1 and count the age distribution of visitors in topic2 of project2 by userid and uid.


* Query and analysis statement:

   ```SQL
   * | 
   select 
     count(*) as pv
     t2.age  as age_group
   from project.topic1 as t1 left join project2.topic2 as t2 on t1.userid = t2.uid 
   group by t2.age 
   order by pv desc
   ```
   

* Return result:

   
   |age_group |pv |
   |---|---|
   |10~20 |8000 |
   |20~30 |5000 |
   |30~40 |2000 |
   


<span id="da7209bb"></span>
### **Example 3: Query data from a topic and a MySQL data source**

Analyze the age distribution of active users. Query data from a topic named topic1 and an external data source named tls_external_store. The two data sources are joined by the userid and uid fields. Count the number of page views in topic1 and calculate the age distribution of visitors in tls_external_store by userid and uid.


* Query and analysis statement:

   ```SQL
   * | 
   select 
     count(*) as pv
     t2.age  as age_group
   from project.topic1 as t1 left join tls_external_store as t2 on t1.userid = t2.uid 
   group by t2.age 
   order by pv desc
   ```
   

* Return result:

   
   |age_group |pv |
   |---|---|
   |10~20 |8000 |
   |20~30 |5000 |
   |30~40 |2000 |
