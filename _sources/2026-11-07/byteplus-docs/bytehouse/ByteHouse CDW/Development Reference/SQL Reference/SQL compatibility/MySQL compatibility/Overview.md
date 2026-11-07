---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-mysql-compatibility"
---

<span id="d12883f5"></span>
## MySQL syntax compatibility

This article introduces the compatibility comparison between ByteHouse MySQL and native MySQL databases.

Starting from version 2.0.0.0, ByteHouse is compatible with common functions and syntax of MySQL 5.7 and MySQL 8.0. This allows seamless integration with MySQL client applications and tools. Users can interact with ByteHouse using the familiar MySQL protocol and utilize the features of the MySQL ecosystem.

Due to differences in product architecture or customer requirements, some features are not yet supported. This section mainly discusses the differences between ByteHouse MySQL and native MySQL databases in the following aspects:


* Data Type

* Function

   * The use of some functions is not supported

   * The results of some functions are inconsistent with MySQL

* Support for MySQL DQL

* Support for MySQL DML (currently only supports updates and deletes on unique tables)


<span id="57f1de9b"></span>
### Setting MySQL mode

By using the `dialect_type` option, ByteHouse can switch between MySQL mode and ClickHouse mode, for example:

```SQL
SET dialect_type = 'CLICKHOUSE';
SET dialect_type = 'MySQL';
```


ByteHouse defaults to ClickHouse mode.

Description

It is `Recommended` to set the `dialect_type` using the SET command mentioned above, it is not recommended to set it through query\-level SETTINGS, such as:

```SQL
SELECT ... SETTINGS dialect_type = 'MySQL';
```


In implementation, many ANSI functions are controlled by separate sub\-options; dialect_type can be considered as the sum of these sub\-options. If needed, sub\-options can be used to control specific behaviours under MySQL mode, such as:

```SQL
SET dialect_type = 'MySQL'；
```


<span id="b9074475"></span>
### Function

Most MySQL behaviours are the same as ANSI, and will not be listed again. Implicit conversion is introduced for the function part, aligning it with MySQL behaviour.
