---
title: "Use of Variables"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Use_of_Variables"
---

When you create a variable, you can directly reference it in the WITH parameter when creating default temporary tables or specifying tables in InMemoryCatalog in SQL tasks.

This article demonstrates how to use variables with a simple demo.

<span id="d2bd02a1"></span>
## Variable Priority Explanation

Domain\-specific variable priority is higher than global variables.


* If only referencing global variables, the search will be limited to global variables.

* If only referencing domain\-specific variables, the search will begin in the specified scope, then proceed to global variables. If the variable does not exist, an error will occur.

* When referencing both global and domain\-specific variables, the search starts in the specified variable scope and then moves to global variables. If a variable does not exist, an error will occur.


<span id="bc33c133"></span>
## Example Demo

This article simulates a scenario of reading data from MySQL, aiming to present the MySQL username and password as variables instead of plain text. Please create variables in advance; for specific operations, refer to [Create Variables](https://docs.byteplus.com/docs/flink/Create_Variables).

In the example, the MySQL username and password are presented as variables. In SQL tasks, variables are referenced in the format `${secret_values.variable_name}`, where `secret_values.` is a fixed prefix, and `variable_name` is the name of the variable you created.


* `${secret_values.username}`: Refers to the global variable *username variable.* 

* `${secret_values.password}`: Refers to the global variable password variable.

* `${secret_values.tablename}`: Refers to the specified domain variable tablename \*\* variable. Note: It is also necessary to specify the correct variable scope in the parameter settings. As shown in the diagram below:


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When referencing a specific domain variable, you need to select the Variable Scope \-\> Specified Domain in the dialog box on the right side of the SQL Editor and choose the correct scope. If the specified scope and global variables do not contain the referenced variable, an error will be reported during the task execution.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51c9c0c6ad7048889f55ce7d4ded2bb9~tplv-goo7wpa0wc-image.image" width="1908px" /></div>


```SQL
CREATE TEMPORARY TABLE
  mysql_source (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time timestamp,
    PRIMARY KEY (order_id) NOT ENFORCED
  )
WITH
  (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://192.*.*.*:30294/doc_test',            
    'username' = '${secret_values.username}',   //username variables
    'password' = '${secret_values.password}',   //password variables
    'table-name' = '${secret_values.tablename}'  //tablename variables
  );


create table
  print_sink (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time timestamp
  )
WITH
  ('connector' = 'print');


insert into
  print_sink
select
  *
from
  mysql_source;
```
