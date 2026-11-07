---
title: "remote"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/remote-function"
---

<span id="remote, remoteSecure {#remote-remotesecure}"></span>
# remote, remoteSecure
Allows you to access remote servers without creating a `Distributed` table. `remoteSecure` is the same as `remote`, but it uses an encrypted link.
Both functions can be used `in SELECT` `and INSERT` queries.
Grammar:
```sql
remote('addresses_expr', db, table[, 'user'[, 'password'], sharding_key])
remote('addresses_expr', db.table[, 'user'[, 'password'], sharding_key])
remoteSecure('addresses_expr', db, table[, 'user'[, 'password'], sharding_key])
remoteSecure('addresses_expr', db.table[, 'user'[, 'password'], sharding_key])
```

**Param**
`Expression` - An expression representing the address of a remote server. It could just be a single server address. The server address can be either `host:port` or `host`.
`host` can be specified as a server name, or as an IPV4 or IPV6 address. IPv6 address is specified within square brackets.
`port` is the TCP port on the remote server. If the port is omitted, then `remote` uses the tcp_port from the server configuration file (default is 9000), `remoteSecure` uses tcp_port_secure (default is 9440).
IPv6 address requires specifying a port.
Type: String.

      * `db` — Database name. Type: String.
      * `table` — Table name. Type: String.
      * `User` — Username. If no user is specified, use `Default`. Type: String.
      * `Password` — User password. If no password is specified, use an empty password. Type: String.
      * `Sharding_key` — Sharding key for distributing data across nodes. Example: `Insert into remote('127.0.0.1:9000,127.0.0.2', db, table, 'Default', rand())`. Type: UInt32.

**Return value.**
Data from a remote server.
**Usage**
Using the `remote` table function without creating a `Distributed` table is preferable because a server connection will be re-established for each request in this case. Moreover, if hostnames are set, they will be resolved, and errors will not be counted when using various<_copy>s. When dealing with a large number of queries, always prioritize creating `Distributed` tables over using `remote` table functions.
The `remote` table function can be useful in the following scenarios:
Accessing specific servers for data comparison, debugging, and testing.
Queries for the purpose of user research across multiple ClickHouse clusters.
Manually issued infrequent distributed requests.
Distributed requests that redefine the server set each time.
**Address**
```text
example01-01-1
example01-01-1:9000
localhost
127.0.0.1
[::]:9000
[2a02:6b8:0:1111::11]:9000
```

Multiple addresses can be separated by commas. In such cases, ClickHouse will handle the process distributively, and it will send the query to all specified addresses (such as shards with different data).
```text
example01-01-1,example01-02-1
```

Part of the expression can be specified using braces. The previous example can be written as follows:
```text
example01-0{1,2}-1
```

Braces can contain a range of numbers separated by two dots (non-negative integers). In this case, the range will expand to generate a set of values for shard addresses. If the first number starts with zero, the same zero alignment will be used to form values. The previous example can be written as follows:
```text
example01-{01..02}-1
```

If you have multiple pairs of braces, it will generate the direct product of the corresponding set.
Addresses within the curly braces can be separated using the pipe symbol (|). In this case, the corresponding set of addresses is treated as copies, and the query is sent to the first Normal copy. However, the copies will be iterated in the order set by the current load_balancing settings. This example specifies two shards, each with two copies:
```text
example01-{01..02}-{1|2}
```

The number of generated addresses is constrained by a constant. Currently, there are 1000 addresses.
**Example**
Selecting data from a remote server:
```sql
SELECT * FROM remote('127.0.0.1', db.remote_engine_table) LIMIT 3;
```

Inserting data from a remote server into a table:
```sql
CREATE TABLE remote_table (name String, value UInt32) ENGINE=Memory;
INSERT INTO FUNCTION remote('127.0.0.1', currentDatabase(), 'remote_table') VALUES ('test', 42);
SELECT * FROM remote_table;
```
