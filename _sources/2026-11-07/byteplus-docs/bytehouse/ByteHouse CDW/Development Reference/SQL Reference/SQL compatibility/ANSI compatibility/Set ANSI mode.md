---
title: "Set ANSI mode"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/set-ansi-mode"
---

ANSI mode is designed to make SQL syntax and execution behavior more consistent with the ANSI standard or other mainstream databases.

<span id="e381053d"></span>
### Set ANSI Mode

Through the `dialect_type` option, ByteHouse can switch between ANSI Mode and ClickHouse Mode, for example:

```SQL
SET dialect_type = 'CLICKHOUSE';
SET dialect_type = 'ANSI';
```


ByteHouse defaults to using ClickHouse Mode.

Description

It's recommended to set `dialect_type` using the aforementioned SET command, and not recommended to set it through query\-level SETTINGS, like:

```SQL
SELECT ... SETTINGS dialect_type = 'ANSI';
```


In implementation, many ANSI features are controlled by separate sub\-options, and dialect_type can be considered the sum of these sub\-options. If needed, sub\-options can be used to control specific behaviors in ANSI mode, for example:

```SQL
SET dialect_type = 'ANSI'；

SELECT ... SETTINGS join_use_nulls = 0;
```


[ANSI compatibility](https://docs.byteplus.com/docs/bytehouse/docs-ansi-compatibility) lists functions related to ANSI. If there are separate sub\-options for a particular feature, they will provide the relevant explanations.
