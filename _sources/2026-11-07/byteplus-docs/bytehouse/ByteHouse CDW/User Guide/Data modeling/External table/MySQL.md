---
title: "MySQL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-mysql-external-table"
---

<span id="42476c04"></span>
## Function introduction

ByteHouse supports MySQL foreign tables through the MySQL engine, enabling **`SELECT`** queries on data stored on remote MySQL servers.

<span id="21f0af4a"></span>
## Restrictions


* The current network requirements for accessing MySQL external tables are as follows:

   * Private network access requires connectivity via Private Link. To use this method, please contact the ByteHouse team to enable it.

   * Public network access requires configuring a public IP. For detailed settings, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings).

* If your network environment has access restrictions, please add ByteHouse's service IP address to the white list. For more details, refer to [Set up IP allowlist](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#30753141).


<span id="462b7c37"></span>
## Invocation format

```sql
MySQL('host:port', 'database', 'table', 'user', 'password');
```


<span id="d462cf61"></span>
## **Parameter description**


* `host:port` — MySQL server address.

* `database` — Name of the database.

* `Table` — Name.

* `User` — Database User.

* `Password` — User Password.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL <code>host:port</code> must support public network access.</div>


<span id="6f694b46"></span>
## Example

```sql
DROP TABLE IF EXISTS db.mysql_test;

-- Create a MySQL external table, ensure that the DDL of the synchronized table is consistent with that of ByteHouse
CREATE TABLE db.mysql_test(x Int32) Engine = MySQL('127.0.0.1:3306', 'test_db', 'test_tb', 'user', 'password');

-- Query data in the external table
SELECT x FROM db.mysql_test limit 10;

-- Update information such as username and password
ALTER TABLE db.mysql_test Engine = MySQL('127.0.0.2:3306', 'test_db', 'test_tb', 'user', 'password');

-- View the table creation statement
SHOW CREATE TABLE db.mysql_test;

-- Clear the external table
DROP TABLE db.mysql_test;
```
