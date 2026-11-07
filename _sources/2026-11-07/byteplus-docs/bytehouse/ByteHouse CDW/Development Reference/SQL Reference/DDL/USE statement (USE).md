---
title: "USE statement (USE)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/use-statement"
---

Set the current database for the session. If the database is not explicitly defined before the table name with a dot in the query, then use the current database to search for the table.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This query cannot be carried out using the HTTP protocol, as there is no concept of a session.</div>


**Syntax**

```SQL
USE [databaseIdentifier];
```


**Example**

```SQL
USE example_db
```
