---
title: "DML statement security protection (safeupdate)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/safeupdate"
---

Introduction

safeupdate is a lightweight PostgreSQL extension designed to enhance database operation security by enforcing that `update` and `delete` statements must include a `where` clause. When it detects a DML statement that might accidentally modify or delete the entire table, it immediately throws an error and blocks execution.

This extension is particularly useful in scenarios where the database is exposed to external write operations through API gateways such as PostgREST. It effectively prevents catastrophic data loss caused by client errors or malicious attacks.

<span id="tMXW1jOO"></span>
## Applicable scenarios


* **Open API environments**: prevent requests sent through RESTful APIs from accidentally modifying or deleting entire tables.

* **Development and testing environments**: help developers develop good SQL writing habits and avoid data mishandling during development.

* **Multi\-user collaborative databases**: provide a basic security layer for teams to reduce the risk of human errors.


<span id="S4Obb0Oq"></span>
## Create and delete extension

Enabling and disabling safeupdate is controlled by modifying the `shared_preload_libraries` parameter in PostgreSQL's configuration file `postgresql.conf`. The modification takes effect only after a database service restart.

<span id="X9YQA4Nd"></span>
### Create extension (enable)


1. Modify the shared_preload_libraries parameter to add the `safeupdate` value. If other libraries already exist, separate them with commas. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

2. Restart the PostgreSQL service to load the extension.


<span id="h1zJ0sh4"></span>
### Delete extension (disable)


1. Modify the shared_preload_libraries parameter to remove the `safeupdate` value.

2. Restart the PostgreSQL service.


<span id="7wDbCj9G"></span>
## Basic usage

After enabling extensions, any `UPDATE` or `DELETE` statement without a `WHERE` clause will be intercepted.


* `UPDATE` statement without a `WHERE` clause


```SQL
-- create a test table
CREATE TABLE products (id INT, name TEXT);
INSERT INTO products VALUES (1, 'Apple'), (2, 'Orange');

-- attempt to execute UPDATE without a WHERE clause (will be intercepted)
UPDATE products SET name = 'Banana';
```


**Return error:** 

```Plain Text
ERROR:  UPDATE requires a WHERE clause
```



* `DELETE` statement without a `WHERE` clause


```SQL
-- attempt to execute DELETE without a WHERE clause (will be intercepted)
DELETE FROM products;
```


**Return error:** 

```Plain Text
ERROR:  DELETE requires a WHERE clause
```


<span id="fgy2SLnb"></span>
#### Correct usage

An `UPDATE` or `DELETE` statement only succeeds if it includes a `WHERE` clause.

```SQL
-- UPDATE with a WHERE clause (succeeded)
UPDATE products SET name = 'Golden Apple' WHERE id = 1;
-- UPDATE 1

-- DELETE with a WHERE clause (succeeded)
DELETE FROM products WHERE id = 2;
-- DELETE 1
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Safeupdate performs strict checks. Even conditions like <code>WHERE 1=1</code>, which logically apply to the entire table, are considered valid and pass the check. Therefore, it mainly prevents errors caused by forgetting to add a <code>WHERE</code> clause, not logical errors in the condition.</div>


<span id="jlDi2fVP"></span>
## Extension parameter


* safeupdate's behavior can be controlled at runtime through a GUC parameter.

   * `safeupdate.enabled`

      * Function: controls whether to enable extension enforcement of filtering conditions on DML statements.

      * Type: `boolean`

      * Default value: `true` (ON)
