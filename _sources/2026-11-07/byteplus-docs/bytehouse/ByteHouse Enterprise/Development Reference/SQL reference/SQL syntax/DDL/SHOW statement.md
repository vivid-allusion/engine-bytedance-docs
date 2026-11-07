---
title: "SHOW statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-show-statement"
---

You can use the `SHOW` statement to view information about databases, such as the databases in the current cluster, tables in a database, dictionaries, permissions, and more.

<span id="f7fcad83"></span>
# SHOW DATABASES

View the databases in the current cluster. This query is equivalent to `SELECT name FROM system.databases` **.** 

<span id="7a683a0d"></span>
## **Grammar**

```SQL
SHOW DATABASES 
```


<span id="79bec7c2"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. View databases in the current cluster
SHOW DATABASES;
```


<span id="8fe691d0"></span>
# SHOW TABLES

View tables in the database.

<span id="426b7844"></span>
## **Grammar**

When using, if the `FROM` clause is not specified, the query will return the tables in the current database.

```SQL
SHOW TABLES [FROM [databaseIdentifier]] [LIKE STRING_LITERAL]
```


<span id="884eb7a0"></span>
## Parameter description


|Parameters |Required field |Format requirements |Note |
|---|---|---|---|
|LIKE 'STRING_LITERAL' |Optional |String literal<br><br>Wrap in single quotation marks |Table name and schema filtering:<br><br><br>* Supports wildcard `%` (matches any sequence of characters).<br><br>* Supports wildcard `_` (matches a single character).<br><br><br>Example:<br><br><br>* `LIKE 'user%'` matches items such as user_logs, users, and so on.<br><br>* `LIKE 'temp_'` matches temp1, tempA, and so on. |


<span id="65bf9789"></span>
## **Example**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Query tables with names containing 'table'
SHOW TABLES FROM sample_db LIKE '%table'
```


<span id="103ba08a"></span>
# SHOW CREATE TABLE

View the CREATE TABLE statement of the table.

<span id="fd90b22d"></span>
## **Grammar**

```SQL
SHOW CREATE [TABLE] [tableIdentifier]
```


<span id="cb706eff"></span>
## **Example**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
    `order_by_column` String
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`)

-- 3. View the table creation statement, and the system will return the above table creation statement
SHOW CREATE TABLE sample_db.sample_table
```


<span id="79094adb"></span>
# SHOW DICTIONARIES

View the list of dictionaries in the current database or a specified database.

<span id="48730474"></span>
## Grammar

When used, if you do not specify the `FROM` clause, the system will return the list of dictionaries for the current database.

```SQL
SHOW DICTIONARIES [FROM ] 
[LIKE ''] 
[LIMIT ] 
[INTO OUTFILE ] 
[FORMAT ]
```


<span id="6f4ba9b7"></span>
## **Parameter description**


|Parameters |Required field |Note |
|---|---|---|
|LIKE '' |Optional |Dictionary name filter mode:<br><br><br>* Supports using `%` to match any character (for example, `prod_%`).<br><br>* Supports `_` matching a single character (for example, `dict_v_`). |
|LIMIT |Optional |Limit the number of returned results (positive integers, such as `LIMIT 10`). |
|INTO OUTFILE '<file_path\>' |Optional |Export the results to a file (an absolute path is required, such as `/data/dict_list.csv`). |
|FORMAT <format_name\> |Optional |Specify the format of the returned results (such as `JSON`, `CSV`, and others). |


You can also view the list of dictionaries using the following queries:

```SQL
SELECT name 
FROM system.dictionaries 
WHERE database =  [AND name LIKE ] [LIMIT ] [INTO OUTFILE ] [FORMAT ]
```


<span id="53d9c73f"></span>
## **Example**

Execute the following command to query dictionary tables in the system database whose names contain 'dict', and return the first two matching results.

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a dictionary
CREATE DICTIONARY IF NOT EXISTS sample_db.sample_dict ON CLUSTER sample_cluster (
    `user_id` UInt64,
    `username` String,
    `age` UInt8 DEFAULT 0,
    `gender` UInt8 DEFAULT 0,
    `last_login` DateTime
)
PRIMARY KEY user_id
SOURCE(MySQL(
    host 'mysql_host.example.com'
    port 3306
    user 'dict_reader'
    password 'secure_password'
    db 'user_db'
    table 'users'
))
LAYOUT(FLAT())
LIFETIME(MIN 300 MAX 900);

-- 3. View dictionary
SHOW DICTIONARIES FROM sample_db.sample_dict LIKE '%dict%' LIMIT 2
```


```Plain
┌─name─────┐
│ sample_dict  │
└────────┘
```


<span id="8612485a"></span>
# SHOW PROCESSLIST

View current active database processes.

<span id="a74fb844"></span>
## **Grammar**

```SQL
SHOW PROCESSLIST [INTO OUTFILE filename] [FORMAT format]
```


This query displays a list of all currently executing query requests except for the `SHOW PROCESSLIST` query, and its output is equivalent to the contents of the `system.processes` system table.

You can use `SELECT * FROM system.processes` to retrieve all data related to the current request, including the process for the SHOW PROCESSLIST command itself.

Note (to be executed in the console):

```Bash
$ watch -n1 "clickhouse-client --query='SHOW PROCESSLIST'"
```


<span id="d17249bb"></span>
## Example

```SQL
SHOW PROCESSLIST 
INTO OUTFILE '/var/log/long_queries.json';
```


<span id="b6a2c3db"></span>
# SHOW GRANTS

View user permissions. When using this, if no user is specified, the system will output the current user's permissions.

<span id="9aadba39"></span>
## **Grammar**

```SQL
SHOW GRANTS [FOR user]
```


<span id="638c2c5e"></span>
## Example

```SQL
-- View current user permissions
SHOW GRANTS; 

-- View the specified user permissions
SHOW GRANTS FOR 'demo_user';
```


<span id="101208e6"></span>
# SHOW CREATE USER

View the parameters used when creating a user, but `SHOW CREATE USER` does not output the user's password information.

<span id="baf87102"></span>
## **Grammar**

```SQL
SHOW CREATE USER [name | CURRENT_USER]
```


<span id="f9d01298"></span>
## Example

```SQL
SHOW CREATE USER demo_user;
```


<span id="77c75245"></span>
# SHOW CREATE ROLE

View the parameters used when creating a role.

<span id="3280df12"></span>
## **Grammar**

```SQL
SHOW CREATE ROLE name 
```


<span id="e8fc4679"></span>
# SHOW CREATE ROW POLICY

View the creation parameters of the specified row\-level security policy (Row Policy) for auditing or reconstructing the policy.

<span id="f4ab5cf5"></span>
## **Grammar**

```SQL
SHOW CREATE [ROW] POLICY name ON [database.]table 
```


<span id="7b27af8b"></span>
## Example

```SQL
SHOW CREATE POLICY region_policy ON users;
```
