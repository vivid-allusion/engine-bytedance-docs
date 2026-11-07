---
title: "SHOW statement (SHOW)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/show-statement"
---

<span id="f5a86999"></span>
### SHOW DATABASES

This statement prints a list of all databases; this query is equivalent to `SELECT name FROM system.databases`.

**Syntax**

```SQL
SHOW DATABASES 
```


**Example**

```SQL
SHOW DATABASES LIMIT 10;
```


Result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39779123b4e64be2aefcf089de0f9229~tplv-goo7wpa0wc-image.image) </span>

<span id="44754378"></span>
### SHOW TABLES

The `SHOW TABLES` statement displays a list of tables.

**Syntax**

```SQL
SHOW TABLES [FROM [databaseIdentifier] [LIKE STRING_LITERAL]
```


If a `FROM` clause is not specified, the query will return a list of tables in the current database.

**Example**

```SQL
SHOW TABLES FROM doc_demo LIKE '%employment%';
```


Result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb726c4cc9ea4834bdf480f9a967b8bb~tplv-goo7wpa0wc-image.image) </span>

<span id="44197ac2"></span>
### SHOW CREATE TABLE

This statement displays the SQL used to create the table.

**Syntax**

```SQL
SHOW CREATE [TABLE] [tableIdentifier]
```


**Example**

```SQL
-- step 1: create a table 
CREATE TABLE doc_demo.sale_table (
    id UInt32,
    name String,
    price UInt32
)
ENGINE = CnchMergeTree
ORDER BY id;

-- step 2: show create table
SHOW CREATE TABLE doc_demo.sale_table;
```


Result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d844704fb7064f78842f145f064614de~tplv-goo7wpa0wc-image.image) </span>

<span id="7d4c2945"></span>
### SHOW DICTIONARIES

This statement displays a list of dictionaries.

```SQL
SHOW DICTIONARIES [FROM ] [LIKE ''] [LIMIT ] [INTO OUTFILE ] [FORMAT ]
```


If the `FROM` clause is not specified, the query returns a list of dictionaries from the current database.

The following query is equivalent to `SHOW DICTIONARIES`:

```SQL
SELECT name FROM system.dictionaries WHERE database =  [AND name LIKE ] [LIMIT ] [INTO OUTFILE ] [FORMAT ]
```


**Example**

The following query retrieves the top two dictionaries from the `db` database whose names contain 'reg'.

```SQL
SHOW DICTIONARIES FROM db LIKE '%reg%' LIMIT 2
```


```SQL
┌─name─────────┐
│ regions      │
│ region_names │
└──────────────┘
```


<span id="60fb18df"></span>
### SHOW PROCESSLIST

This statement lists current requests from the `system.processes` table, but excludes the `SHOW PROCESSLIST` query itself from the results. The `SELECT * FROM system.processes` query returns all data for current requests.

**Syntax**

```SQL
SHOW PROCESSLIST [WHERE expr]
```


**Parameters**

The optional `WHERE` clause can be used to filter results based on fields such as the virtual warehouse, query text, or query ID. For example,

```SQL
SHOW PROCESSLIST WHERE virtual_warehouse = '<vw_id>'
SHOW PROCESSLIST WHERE virtual_warehouse = '<vw_id>' AND query LIKE '%<pattern>%'
SHOW PROCESSLIST WHERE query_id = '<id>'
SHOW PROCESSLIST WHERE query_id IN ('<id1>', '<id2>', ...)
```


<span id="b2e5b7c4"></span>
### SHOW GRANTS

This statement shows the privileges granted to a user.

**Syntax**

```SQL
SHOW GRANTS [FOR user]
```


If no user is specified, it displays the current user's privileges.

<span id="9a67bbe1"></span>
### SHOW CREATE USER

This statement shows the `CREATE USER` statement for a specified user.

`SHOW CREATE USER` does not output the user's password information.

**Syntax**

```SQL
SHOW CREATE USER [name | CURRENT_USER]
```


<span id="dc85f7c4"></span>
### SHOW CREATE ROLE

This statement shows the `CREATE ROLE` statement for a specified role.

**Syntax**

```SQL
SHOW CREATE ROLE name
```


<span id="1026f094"></span>
### SHOW CREATE ROW POLICY

This statement shows the `CREATE ROW POLICY` statement for a specified policy.

**Syntax**

```SQL
SHOW CREATE [ROW] POLICY name ON [database.]table
```
