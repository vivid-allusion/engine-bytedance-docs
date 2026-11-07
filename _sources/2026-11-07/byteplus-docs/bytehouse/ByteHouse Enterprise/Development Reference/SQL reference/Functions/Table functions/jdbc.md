---
title: "jdbc"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/jdbc-function"
---

`jdbc(datasource, schema, table)` - Returns the table connected via the JDBC driver.
This table function requires a separate [clickhouse-jdbc-bridge](https://github.com/ClickHouse/clickhouse-jdbc-bridge) program to operate.
It supports nullable types (based on DDL of remote tables from the query).
**Example**
```sql
SELECT * FROM jdbc('jdbc:mysql://localhost:3306/?user=root&password=root', 'schema', 'table')
```

```sql
SELECT * FROM jdbc('mysql://localhost:3306/?user=root&password=root', 'select * from schema.table')
```

```sql
SELECT * FROM jdbc('mysql-dev?p1=233', 'num Int32', 'select toInt32OrZero(''{{p1}}'') as num')
```

```sql
SELECT * 
FROM jdbc('mysql-dev?p1=233', 'num Int32', 'select toInt32OrZero(''{{p1}}'') as num')
```

```sql
SELECT a.datasource AS server1, b.datasource AS server2, b.name AS db
FROM jdbc('mysql-dev?datasource_column', 'show databases') a
INNER JOIN jdbc('self?datasource_column', 'show databases') b ON a.Database = b.name
```
