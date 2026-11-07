---
title: "url"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/url-table-function"
---

`URL` function creates a table with the specified format and structure from a URL.`format and structure from astructure from a URL`.
The URL function can be used in queries to SELECT and INSERT data in the URL table.
**Syntax**
```sql
url(URL, format, structure)
```

**Parameter**
`URL` — HTTP or HTTPS server address that can accept `GET` or `POST` requests (corresponding to `SELECT` or `INSERT` queries). Type: String.
`Format` — Data Format. Type: String.
`Structure` — Table structure in the format `'UserID UInt64, Name String'`. Confirm column names and types. Type: String.
**Return value**
A table with the specified format and structure and with data from the defined `URL`.
**Example**
Retrieve the first three rows of a table obtained from an HTTP server, containing columns of `String` and UInt32 types, returned in CSV format.
```sql
SELECT * FROM url('http://127.0.0.1:12345/', CSV, 'column1 String, column2 UInt32') LIMIT 3;
```

Insert data from `URL` into the table:
```sql
CREATE TABLE test_table (column1 String, column2 UInt32) ENGINE=Memory;
INSERT INTO FUNCTION url('http://127.0.0.1:8123/?query=INSERT+INTO+test_table+FORMAT+CSV', 'CSV', 'column1 String, column2 UInt32') VALUES ('http interface', 42);
SELECT * FROM test_table;
```

[Original article](https://clickhouse.tech/docs/en/query_language/table_functions/url/)
