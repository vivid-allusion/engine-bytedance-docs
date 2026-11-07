---
title: "dictionary"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dictionary-function"
---

Display dictionary data as a ClickHouse table.
**Syntax**
```SQL
dictionary('dict')
```

**Parameters**

* `dict` — Dictionary name. String.

**Return value**
ClickHouse table.
**Example**
Input table `dictionary_source_table`
```Plain
┌─id─┬─value─┐
│  0 │     0 │
│  1 │     1 │
└────┴───────┘
```

Create Dictionary
```SQL
CREATE DICTIONARY new_dictionary(id UInt64, value UInt64 DEFAULT 0) PRIMARY KEY id
SOURCE(CLICKHOUSE(HOST 'localhost' PORT tcpPort() USER 'default' TABLE 'dictionary_source_table')) LAYOUT(DIRECT());
```

Search
```SQL
SELECT * FROM dictionary('new_dictionary');
```

As a result
```Plain
┌─id─┬─value─┐
│  0 │     0 │
│  1 │     1 │
└────┴───────┘
```
