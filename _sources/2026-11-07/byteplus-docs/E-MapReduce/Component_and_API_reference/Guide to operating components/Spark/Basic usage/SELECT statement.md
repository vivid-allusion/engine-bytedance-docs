---
title: "SELECT statement"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/SELECT_statement"
---

In Apache Spark, the SELECT statement is used to retrieve data from one or more tables.

<span id="_1-普通查询"></span>
## 1 Basic queries

Suppose we have a table named employees with the following structure:

```sql
CREATE TABLE employees (
  id INT,
  name STRING,
  salary FLOAT,
  department STRING
)
```


This table contains the following data:


|id |name |salary |department |
|---|---|---|---|
|1 |Alice |70000 |HR |
|2 |Bob |80000 |IT |
|3 |Carol |75000 |HR |
|4 |Dave |85000 |IT |


<span id="_1-1-查询所有列"></span>
### 1.1 Query all columns


* Example statement


```sql
SELECT * FROM employees;
```



* Result



|id |name |salary |department |
|---|---|---|---|
|1 |Alice |70000 |HR |
|2 |Bob |80000 |IT |
|3 |Carol |75000 |HR |
|4 |Dave |85000 |IT |


<span id="_1-2-查询特定列"></span>
### 1.2 Query specific columns


* Example statement


```sql
SELECT name, salary FROM employees;
```



* Result



|name |salary |
|---|---|
|Alice |70000 |
|Bob |80000 |
|Carol |75000 |
|Dave |85000 |


<span id="_1-3-带条件的查询"></span>
### 1.3 Query with conditions


* Example statement


```sql
SELECT * FROM employees WHERE department = 'IT';
```



* Result



|id |name |salary |department |
|---|---|---|---|
|2 |Bob |80000 |IT |
|4 |Dave |85000 |IT |


<span id="_1-4-排序查询结果"></span>
### 1.4 Sort query results


* Example statement


```sql
SELECT * FROM employees ORDER BY salary DESC;
```



* Result



|id |name |salary |department |
|---|---|---|---|
|4 |Dave |85000 |IT |
|2 |Bob |80000 |IT |
|3 |Carol |75000 |HR |
|1 |Alice |70000 |HR |


<span id="_1-5-排序并限制结果数量"></span>
### 1.5 Sort and limit the number of results


* Example statement


```sql
SELECT * FROM employees ORDER BY salary DESC LIMIT 2;
```



* Result



|id |name |salary |department |
|---|---|---|---|
|4 |Dave |85000 |IT |
|2 |Bob |80000 |IT |


<span id="_1-6-使用-spark-sql-的-dataframe-api"></span>
### 1.6 Use the DataFrame API of Spark SQL

In PySpark, you can use the DataFrame API to perform similar queries:


* Example statement


```sql
df = spark.sql("SELECT * FROM employees WHERE salary > 75000")
df.show()
```



* Result



|id |name |salary |department |
|---|---|---|---|
|4 |Dave |85000 |IT |


<span id="_2-join"></span>
## 2 Join

In Spark SQL, the JOIN clause is used to combine data from two or more tables. Depending on the relationship between the data, there are several different types of JOIN:


1. INNER JOIN: Returns only the rows that match the join condition in both tables.

2. LEFT OUTER JOIN or LEFT JOIN: Returns all rows from the left table, even if there are no matching rows in the right table. Rows in the right table that do not match will be NULL in the result.

3. RIGHT OUTER JOIN or RIGHT JOIN: Opposite to LEFT JOIN, returns all rows from the right table, even if there are no matching rows in the left table.

4. FULL OUTER JOIN or FULL JOIN: Returns all rows from both the left and right tables. If there is no match on one side, the result for that side will be NULL.

5. CROSS JOIN: Returns the Cartesian product of the two tables, combining each row from the left table with every row from the right table.


Suppose we have two tables: employees and departments.

employees table:

```sql
CREATE TABLE employees (employee_id INT, name STRING, department_id INT);
```


The table contains the following data:


|employee_id |name |department_id |
|---|---|---|
|1 |Alice |2 |
|2 |Bob |3 |
|3 |Charlie |2 |
|4 |David |4 |


departments table:

```sql
CREATE TABLE departments (department_id INT, department_name STRING);
```


The table contains the following data:


|department_id |department_name |
|---|---|
|1 |Accounting |
|2 |IT |
|3 |HR |


<span id="_2-1-inner-join"></span>
### 2.1 INNER JOIN


* Example statement


```sql
SELECT e.name, d.department_name 
    FROM employees e 
    [INNER] JOIN departments d ON e.department_id = d.department_id;
```



* Result



|name |department_name |
|---|---|
|Alice |IT |
|Bob |HR |
|Charlie |IT |


<span id="_2-2-left-join"></span>
### 2.2 LEFT JOIN


* Example statement


```sql
SELECT e.name, d.department_name
    FROM employees e
    LEFT JOIN departments d ON e.department_id = d.department_id;
```



* Result



|name |department_name |
|---|---|
|Alice |IT |
|Bob |HR |
|Charlie |IT |
|David |NULL |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because there is no record with department_id 4 in the employees table, the department returned for David by the LEFT JOIN is NULL.</div>


<span id="_2-3-right-join"></span>
### 2.3 RIGHT JOIN


* Example statement


```sql
SELECT e.name, d.department_name
    FROM employees e
    RIGHT JOIN departments d ON e.department_id = d.department_id;
```



* Result



|name |department_name |
|---|---|
|NULL |Accounting |
|Alice |IT |
|Bob |HR |
|Charlie |IT |


The behavior of RIGHT JOIN is similar to LEFT JOIN, but it returns all rows from the right table (departments). Since there is no record in the employees table corresponding to the Accounting department, the name is (null).

<span id="_2-4-full-outer-join"></span>
### 2.4 FULL OUTER JOIN


* Example statement


```sql
SELECT e.name, d.department_name
    FROM employees e
    FULL OUTER JOIN departments d ON e.department_id = d.department_id;
```



* Result



|name |department_name |
|---|---|
|NULL |Accounting |
|Alice |IT |
|Bob |HR |
|Charlie |IT |
|David |NULL |


FULL OUTER JOIN returns all rows from both the left and right tables. Fields missing from unmatched rows are set to NULL.

<span id="_2-5-cross-join"></span>
### 2.5 CROSS JOIN


* Example statement


```sql
SELECT e.name, d.department_name
    FROM employees e
    CROSS JOIN departments d;
```



* Result



|Name |Position |
|---|---|
|Alice |Accounting |
|Alice |IT |
|Alice |HR |
|Bob |Accounting |
|Bob |IT |
|Bob |HR |
|Charlie |Accounting |
|Charlie |IT |
|Charlie |HR |
|David |Accounting |
|David |IT |
|David |HR |


CROSS JOIN combines each row in the employees table with each row in the departments table, forming a Cartesian product. Therefore, the number of rows in the result set is the product of the number of rows in the two tables.

<span id="_3-sortby-子句"></span>
## 3 ORDER BY clause

In Spark SQL, the `SORT BY` clause is used to return result rows sorted within each partition in the order specified by the user. When there are multiple partitions, `SORT BY` returns sorted results within each partition, and then sorts by partition. This is different from the `ORDER BY` clause, which guarantees the overall order of the output.

Suppose we have a table named person with the following structure:

```sql
CREATE TABLE person (zip_code INT, name STRING, age INT);
```


The table contains the following data:


|name |age |zip_code |
|---|---|---|
|Anil K |27 |94588 |
|Dan Li |18 |94588 |
|John V |null |94588 |
|Zen Hui |50 |94588 |
|Aryan B. |18 |94511 |
|David K |42 |94511 |
|Lalit B. |null |94511 |


Now, we sort by name, partitioning all people by zip_code.


* The statement


```sql
[ SORT BY { expression [ ASC | DESC ] [ NULLS { FIRST | LAST } ] [ , ... ] } ]
```



* Example of statement execution


```sql
SELECT /*+ REPARTITION(zip_code) */ name, age, zip_code FROM person SORT BY name;
```



* Execution results



|name |age |zip_code |
|---|---|---|
|Anil K |27 |94588 |
|Dan Li |18 |94588 |
|John V |null |94588 |
|Zen Hui |50 |94588 |
|Aryan B. |18 |94511 |
|David K |42 |94511 |
|Lalit B. |null |94511 |


<span id="_4-orderby-子句"></span>
## 4 orderby clause

The `ORDER BY` clause is used to return result rows sorted in the order specified by the user. Unlike the `SORT BY` clause, this clause guarantees the overall order in the output.

Suppose we have a table named person, which contains each person's id, name, and age. The table structure is as follows:

```sql
CREATE TABLE person (id INT, name STRING, age INT);
```


The table contains the following data:


|id |name |age |
|---|---|---|
|100 |John |30 |
|200 |Mary |NULL |
|300 |Mike |80 |
|400 |Jerry |NULL |
|500 |Dan |50 |


We want to select information for all employees and sort by age in ascending order. For null values, we place them at the end.


* The statement


```sql
[ ORDER BY { expression [ ASC | DESC ] [ NULLS { FIRST | LAST } ] [ , ... ] } ]
```



* Example of statement execution


```plaintext
SELECT name, age FROM person ORDER BY age NULLS LAST;
```



* Execution results



|name |age |
|---|---|
|John |30 |
|Dan |50 |
|Mike |80 |
|Mary |null |
|Jerry |null |


<span id="_5-groupby-子句"></span>
## 5 groupby clause

The GROUP BY clause in SQL is used to group query results by the values of one or more columns, and apply aggregate functions such as SUM, AVG, MAX, MIN, COUNT, and so on to each group for calculation. In Apache Spark SQL, the usage of GROUP BY is consistent with standard SQL.

Suppose we have a table named dealer, which contains the dealer's id, city, model, and sales volume data.

The table structure:

```sql
CREATE TABLE dealer (id INT, city STRING, car_model STRING, quantity INT);
```


The table contains the following data:


|id |city |car_model |quantiry |
|---|---|---|---|
|100 |Fremont |Honda Civic |10 |
|100 |Fremont |Honda Accord |15 |
|100 |Fremont |HondaCRV |7 |
|200 |Dublin |Honda Civic |20 |
|200 |Dublin |Honda Accord |10 |
|200 |Dublin |HondaCRV |3 |
|300 |San Jose |Honda Civic |5 |
|300 |San Jose |Honda Accord |8 |


Now, we want to calculate the total sales for each dealer by model, and sort by dealer id:


* Example of statement execution


```sql
SELECT id, sum(quantity) FROM dealer GROUP BY id ORDER BY id;
```



* Execution results



|id |sum(quantity) |
|---|---|
|100 |32 |
|200 |33 |
|300 |13 |


Then, we want to calculate the sales for each dealer for only the Honda Civic and Honda CRV models:

```sql
SELECT id, sum(quantity) FILTER (WHERE car_model IN ('Honda Civic', 'Honda CRV')) AS `sum(quantity)` FROM dealerGROUP BY id ORDER BY id;
```



* Execution results



|id |sum(quantity) |
|---|---|
|100 |17 |
|200 |23 |
|300 |5 |


<span id="_6-distributedby-子句"></span>
## 6 distributeby clause

The `DISTRIBUTE BY` clause is used to repartition data based on the input expression. Unlike the `CLUSTER BY` clause, it does not sort data within each partition.

Suppose we have a table named person, which records each person's name and age:

```sql
CREATE TABLE person (name STRING, age INT);
```


The table contains the following data:


|Name |Age |
|---|---|
|Zen Hui |25 |
|Anil B |18 |
|Shone S |16 |
|Mike A |25 |
|John A |18 |
|Jack N |16 |


Now we set its number of partitions to 2:

```sql
SET spark.sql.shuffle.partitions = 2;
```


First, we execute SELECT and can see that the data is not sorted:

```sql
SELECT age, name FROM person;
```



|age |name |
|---|---|
|16 |Shone S |
|25 |Zen Hui |
|16 |Jack N |
|25 |Mike A |
|18 |John A |
|18 |Anil B |


Then we apply DISTRIBUTED BY based on age. According to the definition of DISTRIBUTED BY, it repartitions the data according to the number of partitions, but does not sort by age within the partitions.


* Statement


```sql
[ DISTRIBUTE BY { expression [, ... ] } ]
```



* Example of execution statement


```sql
SELECT age, name FROM person DISTRIBUTED BY age;
```



* Execution result



|age |name |
|---|---|
|25 |Zen Hui |
|25 |Mike A |
|18 |John A |
|18 |Anil B |
|16 |Shone S |
|16 |Jack N |


In this result, since we set the number of partitions to 2, people with age 25 and 18 are grouped into one group, and people with age 16 are grouped into another group. However, within the partitions, the data is not sorted by age.

<span id="_7-clusterby-子句"></span>
## 7 Cluster By clause

Using the `CLUSTER BY` clause first repartitions the data based on the input expression, then sorts the data within each partition. Semantically, this is equivalent to first executing `DISTRIBUT BY` and then `SORT BY`. This clause only ensures that the result rows are sorted within each partition and does not guarantee the overall output order.

Suppose we have a table named person that records each person's name and age:

```sql
CREATE TABLE person (name STRING, age INT);
```


The data in the table is as follows:


|Name |Age |
|---|---|
|Zen Hui |25 |
|Anil B |18 |
|Shone S |16 |
|Mike A |25 |
|John A |18 |
|Jack N |16 |


Now we set its number of partitions to 2:

```sql
SET spark.sql.shuffle.partitions = 2;
```


First, we execute SELECT and can see that the data is not sorted:

```sql
SELECT age, name FROM person;
```



|age |name |
|---|---|
|16 |Shone S |
|25 |Zen Hui |
|16 |Jack N |
|25 |Mike A |
|18 |John A |
|18 |Anil B |


Then we apply CLUSTER BY based on age. According to the definition of CLUSTER BY, it repartitions the data according to the number of partitions and then sorts within each partition.


* Statement


```sql
[ CLUSTER BY { expression [ , ... ] } ]
```



* Example of execution statement


```sql
SELECT age, name FROM person CLUSTER BY age;
```



* Execution result



|age |name |
|---|---|
|18 |John A |
|18 |Anil B |
|25 |Zen Hui |
|25 |Mike A |
|16 |Shone S |
|16 |Jack N |


Since we set the number of partitions to 2, people with age 18 and 25 are grouped into one group, and people with age 16 are grouped into another group.

<span id="_8-window-function"></span>
## 8 Window Function

Window functions operate on a set of rows (called a window) and calculate the return value for each row based on this set. Window functions are very useful for processing tasks such as calculating moving averages, computing cumulative statistics, or accessing the value of a row based on its relative position to the current row.

Window functions themselves are relatively complex and consist of three main parts:


* Rank function: Used for sorting, and is further divided into several subclasses

   * RANK: Assigns a unique sequence number to each row within the window. If there are identical values, the sequence numbers will be skipped. For example, if two rows are tied for first place, the next sequence number will be 3.

   * DENSE_RANK: Similar to `RANK()`, but it does not skip sequence numbers. If there are tied rankings, the subsequent sequence numbers will be consecutive.

   * PERCENT_RANK: Calculates the relative rank of each row within a window and returns a value between 0 and 1. This value represents the rank of the row divided by the total number of rows in the window, multiplied by 100.

   * NTILE: Divides the rows in the window into N groups, each with approximately the same number of rows. This function returns an integer between 1 and N, indicating the group to which the row belongs.

   * ROW_NUMBER: Assigns a consecutive sequence number to each row within the window, starting from 1.

* Analytic functions

   * CUME_DIST: Calculates the distribution position of a value among all rows in the window. It returns a value between 0 and 1, representing the cumulative distribution of the current row's rank relative to all rows in the window. Simply put, if there are many rows with the same value, `CUME_DIST()` treats these rows as a group and calculates the relative position of this group within the overall distribution.

   * LAG: Used to access data from rows preceding the current row within the window. You can specify the number of rows to retrieve, as well as the default value to return if the row does not exist.

   * LEAD: The opposite of the `LAG()` function; it is used to access data from rows following the current row within the window. Similarly, you can specify the number of rows to retrieve and the default value.

* Aggregate functions

   * MAX: Returns the maximum value

   * MIN: Returns the minimum value

   * COUNT: Counts the number of rows

   * SUM: Returns the sum

   * AVG: Returns the average

   * ...


Apart from the calculation aspect, the window also has a size definition:


* RANGE: Defines a range

* ROWS: Defines which rows are included


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">All of these window functions require an <code>OVER</code> clause, which is used to define the rules of the window.</div>


* <div data-tips="true" data-tips-type="warning">The <code>OVER</code> clause can include <code>PARTITION BY</code> and <code>ORDER BY</code>. <code>PARTITION BY</code> is similar to <code>GROUP BY</code>, indicating which columns are used to partition the data. <code>ORDER BY</code> defines the sorting rules for rows within the window.</div>



Suppose we have a table named employee, which contains each employee's name, department, salary, and age.

Table structure:

```sql
CREATE TABLE employees (name STRING, dept STRING, salary INT, age INT);
```


Included data:


|name |dept |salary |age |
|---|---|---|---|
|Chloe |Engineering |23000 |25 |
|Fred |Engineering |21000 |28 |
|Paul |Engineering |29000 |23 |
|Helen |Marketing |29000 |40 |
|Tom |Engineering |23000 |33 |
|Jane |Marketing |29000 |28 |
|Jeff |Marketing |35000 |38 |
|Evan |Sales |32000 |38 |
|Lisa |Sales |10000 |35 |
|Alex |Sales |30000 |33 |


Now, let us calculate their salary ranking by department:


* Example execution statement


```sql
SELECT name, dept, RANK() OVER (PARTITION BY dept ORDER BY salary) AS rank FROM employees;
```



* Execution result



|name |dept |salary |rank |
|---|---|---|---|
|Lisa |sales |10000 |1 |
|Alex |sales |30000 |2 |
|Evan |sales |32000 |3 |
|Fred |Engineering |21000 |1 |
|Tom |Engineering |23000 |2 |
|Chloe |Engineering |23000 |2 |
|Paul |Engineering |29000 |4 |
|Helen |Marketing |29000 |1 |
|Jane |Marketing |29000 |1 |
|Jeff |Marketing |35000 |3 |


Now we sort the salaries by department and assign a sequence number to each row in the ranking. This numbering uses the `DENSE_RANK` format, which means that if there are identical values, the same number is assigned, and the next number continues from the previous one.

```sql
SELECT name, dept, DENSE_RANK() OVER (PARTITION BY dept ORDER BY salary) AS dense_rank FROM employees;
```



* Execution result



|name |dept |salary |dense_rank |
|---|---|---|---|
|Lisa |Sales |10000 |1 |
|Alex |Sales |30000 |2 |
|Evan |Sales |32000 |3 |
|Fred |Engineering |21000 |1 |
|Tom |Engineering |23000 |2 |
|Chloe |Engineering |23000 |2 |
|Paul |Engineering |29000 |3 |
|Helen |Marketing |29000 |1 |
|Jane |Marketing |29000 |1 |
|Jeff |Marketing |35000 |2 |
