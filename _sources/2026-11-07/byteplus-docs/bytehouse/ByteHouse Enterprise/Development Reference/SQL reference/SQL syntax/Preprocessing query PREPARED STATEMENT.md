---
title: "Preprocessing query PREPARED STATEMENT"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/preprocessing-query-prepared-statement"
---

The purpose of the preprocessing query (PREPARED STATEMENT) is to efficiently execute the same (or similar) SQL statements repeatedly, avoiding repeated analysis and plan construction.

<span id="9d337bff"></span>
# Usage restrictions


* ByteHouse Enterprise Version 2.5 and above supports this feature.

* The function is activated `only when the optimizer is enabled (set enable_optimizer=1;)`.

* The preprocessing query function is currently only applicable to `Select` search statements.


<span id="a5f7307c"></span>
# Basic syntax

The basic syntax of the PREPARED STATEMENT includes the following four SQL statements:


1. Create a prepared query: `CREATE [*PERMANENT]* PREPARED STATEMENT`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By using the persistent keyword <strong><em>PERMANENT</em></strong> during creation, the PREPARED STATEMENT can be saved on disk as a file and, after the server is restarted, the plan built by the PREPARED STATEMENT will automatically be saved into memory.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If temporary tables are included when creating a preprocessed search (some tables in the System are temporary with changing StorageIDs), it will not be possible to re\-parse the persistent files into a plan upon server restart.   </div>
   

2. Execute a prepared query: `EXECUTE PREPARED STATEMENT`

3. View created prepared queries: `SHOW PREPARED STATEMENT`

4. Delete a specified prepared query: `DROP PREPARED STATEMENT`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When executing a deletion, if the target is a preprocessed search using the persistent keyword <strong><em>PERMANENT</em></strong>, the persistent files will be deleted.   </div>
   

<span id="9e4e3c7a"></span>
# Usage example

<span id="52ef89e7"></span>
## Create a prepared query

<span id="60e1284a"></span>
### Syntax

```SQL
-- Use the PREPARE statement to define the query template.
-- It is highly recommended to use PERMANENT.
CREATE [PERMANENT] PREPARED STATEMENT [IF NOT EXISTS | OR REPLACE] name [ON CLUSTER cluster_name]
AS
select query with prepared_parameters;
```


<span id="ffc5b4c4"></span>
### Example

```SQL
CREATE PERMANENT PREPARED STATEMENT prep1 AS
SELECT count() 
FROM (SELECT number FROM system.numbers LIMIT 10)
WHERE number < [literal_name: DataType]; 
-- literal_name, constant name
-- DataType，constant parameter type

-- Example:
CREATE PERMANENT PREPARED STATEMENT prep1 AS
SELECT count()
FROM (SELECT number FROM system.numbers LIMIT 10)
WHERE number < [i: UInt32];
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d6cfb80ee7e4f33bb7412d4dd71c44c~tplv-goo7wpa0wc-image.image) </span>

<span id="43b91157"></span>
## Search prepared queries

<span id="a0593207"></span>
### View all preprocessed queries

```SQL
-- View all PREPARED STATEMENT
SHOW PREPARED STATEMENTS;
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b814e71d6aed45c68cce4e5fd22ebb42~tplv-goo7wpa0wc-image.image) </span>

<span id="bef4c1c9"></span>
### View the execution plan of a specific preprocessed query

```SQL
--View all PREPARED STATEMENT
EXPLAIN PREPARED STATEMENT prepared_name;
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70013d58ed334dc2b1f80f77bb1d73c0~tplv-goo7wpa0wc-image.image) </span>

<span id="913a0909"></span>
### View the creation statement of a specific preprocessed query

```SQL
--View all PREPARED STATEMENT
SHOW CREATE PREPARED STATEMENT prepared_name;
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4734e8e826474f7c8fa583985006ea0c~tplv-goo7wpa0wc-image.image) </span>

<span id="2bac7567"></span>
## Run a preprocessed query

<span id="15179887"></span>
### Syntax

```SQL
-- Use the EXECUTE statement to execute the query template and bind the prepared parameters through USING.
EXECUTE PREPARED STATEMENT fooplan USING literal1 = value1, literal2 = value2, ...
```


<span id="bffb6bff"></span>
### Example

```SQL
CREATE PERMANENT PREPARED STATEMENT prep1 AS
SELECT count()
FROM (SELECT number FROM system.numbers LIMIT 10)
WHERE number < [i: UInt32];

EXECUTE PREPARED STATEMENT prep1 USING i = 1;
EXECUTE PREPARED STATEMENT prep1 USING i = 5;
EXECUTE PREPARED STATEMENT prep1 USING foo = 'bar'; -- { serverError 4080 }
-- The system will report an error when the type is inaccurate.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/630c85ba3f824d3c990df1972f51ab5c~tplv-goo7wpa0wc-image.image) </span>

<span id="73c972e5"></span>
### Set item priority

The settings that take effect when the EXECUTE PREPARED STATEMENT statement is executed include the following sources (ranked from highest to lowest priority):


1. Settings of the EXECUTE statement;

2. Settings of the corresponding PREPARE statement;

3. The settings in the current session (set either via command line parameters or SET statements, along with the global default configurations);


The following example demonstrates the priority relationships described above.

```SQL
SET iterative_optimizer_timeout=111111;

CREATE PERMANENT PREPARED STATEMENT prep2 AS
SELECT value FROM system.settings WHERE name = 'iterative_optimizer_timeout';

CREATE PERMANENT PREPARED STATEMENT prep3 AS
SELECT value FROM system.settings WHERE name = 'iterative_optimizer_timeout'
SETTINGS iterative_optimizer_timeout=333333;

SET iterative_optimizer_timeout=222222;

EXECUTE PREPARED STATEMENT prep2; -- Result is 222222
EXECUTE PREPARED STATEMENT prep3; -- Result is 333333
EXECUTE PREPARED STATEMENT prep3 SETTINGS iterative_optimizer_timeout=444444; -- Result is 444444
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The PREPARE STATEMENT statement will use a pre\-built plan, thus parameters related to the Parser/Optimizer will only take effect in the CREATE PREPARED STATEMENT statement.</div>


<span id="5c62a8b1"></span>
## Delete preprocessed searches

<span id="a68968de"></span>
### Syntax

```SQL
-- Delete the specified PREPARED STATEMENT
DROP PREPARED STATEMENT [IF EXISTS] name [ON CLUSTER cluster_name];
```


<span id="5e326e28"></span>
### Example

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38f3d053264c40f7a4657e6e1c4429a8~tplv-goo7wpa0wc-image.image) </span>
