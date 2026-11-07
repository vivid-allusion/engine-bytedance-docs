---
title: "input"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/input-function"
---

`Input(structure)` function - efficiently transforms the data sent to the server into data with a given structure and inserts it into a table with a different structure.
`Structure` - Format of data structure sent to the server `'column1_name column1_type, column2_name column2_type, ...'`. For example, `'id UInt32, name String'`.
The function can only be used in `INSERT SELECT` queries and can only be used once, but otherwise, it behaves like a normal table function (for example, it can be used in subqueries). ).
Data can be sent like a normal `INSERT` query and delivered in any available format that must be specified at the end of the query (unlike a normal `INSERT SELECT`).
The function's main feature is that, when the server receives data from the client, it simultaneously transforms it based on the expression list in the `SELECT` clause and inserts it into the target table. No temporary table containing all transmitted data will be created.
**Example**

* Make the `test` table have the following structure `(a String, b String)` and the data in `data.csv` have a different structure `(col1 String, col2 Date, col3 Int32)`. Insert data from `data.csv` into the `test` table, while the query to perform the conversion is as follows:
   ```Bash
   $ cat data.csv | clickhouse-client --query="INSERT INTO test SELECT lower(col1), col3 * col3 FROM input('col1 String, col2 Date, col3 Int32') FORMAT CSV";
   ```

* If `data.csv` contains data with the same structure as the `test` table `test_structure`, then these two queries are equivalent:
   ```Bash
   $ cat data.csv | clickhouse-client --query="INSERT INTO test FORMAT CSV"$ cat data.csv | clickhouse-client --query="INSERT INTO test SELECT * FROM input('test_structure') FORMAT CSV"
   ```
