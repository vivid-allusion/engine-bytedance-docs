---
title: "Functions description"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/functions-description"
---

ByteHouse offers two query modes **ClickHouse** and **ANSI**.

For ClickHouse mode, most functions are consistent with the community version of ClickHouse, but there are also some in\-house developed functions available. We will cite [part of the document content](https://clickhouse.com/docs/en/sql-reference/functions/) from the community to explain the specific differences and how to use them.

For ANSI SQL mode, this mode provides a rich set of SQL syntax. In this mode, SQL statements are sent to Apache Calcite for parsing and validation, and then sent to the engine side for execution. Apache Calcite supports standard ANSI SQL, please refer to the BNF syntax here for more details: [https://calcite.apache.org/docs/reference.html](https://calcite.apache.org/docs/reference.html)
