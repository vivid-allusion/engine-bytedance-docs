---
title: "IN operator"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/in-operator"
---

The `IN`, `NOT IN`, `GLOBAL IN`, and `GLOBAL NOT IN` operators are considered separately for their rich functionality.
The left side of the operator is a single column or tuple.
Example:
```SQL
SELECT UserID IN (123, 456) FROM ...SELECT (CounterID, UserID) IN ((34, 123), (101500, 456)) FROM ...
```

If the left side is a single column in the index and the right side is a set of constants, the system uses the index to process the query.
Please do not list too many specific constants (such as several million). If the dataset is very large, place it in a temporary table and then use a subquery.
The right side of the operator can be a set of constant expressions, a set of tuples with constant expressions as shown in the above example, or a database table or SELECT subquery in brackets.
If the right side of the operator is a table name (e.g., `User ID IN users`), this is equivalent to the subquery `User ID IN (SELECT * FROM users)`. Use this option when sending external data along with the query. For example, queries sent to a temporary table that should filter 'users' can be accompanied by a set of User IDs.
If the right side of the operator is a table name with a Set engine (a dataset always ready in RAM), the dataset will not be recreated for every query.
Subqueries can specify multiple columns for filtering tuples. Example:
```SQL
SELECT (CounterID, UserID) IN (SELECT CounterID, UserID FROM ...) FROM ...
```

The columns on the left and right sides of the IN operator should be of the same type.
The IN operator and subqueries may appear in any part of the query, including aggregate functions and lambda functions. Example:
```SQL
SELECT    EventDate,    avg(UserID IN    (        SELECT UserID        FROM test.hits        WHERE EventDate = toDate('2014-03-17')    )) AS ratioFROM test.hitsGROUP BY EventDateORDER BY EventDate ASC
```

```SQL
┌──EventDate─┬────ratio─┐
│ 2014-03-17 │        1 │
│ 2014-03-18 │ 0.807696 │
│ 2014-03-19 │ 0.755406 │
│ 2014-03-20 │ 0.723218 │
│ 2014-03-21 │ 0.697021 │
│ 2014-03-22 │ 0.647851 │
│ 2014-03-23 │ 0.648416 │
└────────────┴──────────┘
```

Calculate the percentage of page views for users who visited the site on Mar 17th for each day after Mar 17th. The subquery in the IN clause always runs only once on a single server. No dependencies on subqueries.
<span id="5c640eb8"></span>
## Empty handling
In the request processing, the `IN` operator assumes the outcome of the calculation NULL always equals to `0`, regardless of whether `NULL` is on the right or left side of the operator. `NULL` values are not included in any dataset, do not correspond to each other, and cannot be compared when transform_null_in=0.
Here is an example of a `t_null` table:
```Plain
┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │    3 │
└───┴──────┘
```

Running the query `SELECT x FROM t_null WHERE y IN (NULL,3)` provides the following results:
```Plain
┌─x─┐
│ 2 │
└───┘
```

You can see, in the query results, the rows where `y = NULL` are omitted. This is because ClickHouse cannot decide whether `NULL` is included in the `(NULL,3)` set, returns `0` as the outcome of the operation, and the `SELECT` excludes this row from the final output.
```SQL
SELECT y IN (NULL, 3)FROM t_null
```

```Plain
┌─in(y, tuple(NULL, 3))─┐
│                     0 │
│                     1 │
└───────────────────────┘
```

<span id="ccc8fa00"></span>
## Distributed subqueries
IN-s with subqueries have two options (similar to joins): normal `IN` / `JOIN` and `GLOBAL IN` / `GLOBAL JOIN`. They differ in the way they run distributed query processing.
:::warning
Keep in mind, the algorithm described below may work differently depending on the settings `distributed_product_mode` settings.
:::
When using `IN` regularly, the query is sent to remote servers, and each server runs a subquery using IN or J or JOIN clauses.
When using `GLOBAL IN` / `GLOBAL JOINs`, all subqueries are run first with `GLOBAL IN` / `GLOBAL JOINs`, and the results are collected in a temporary table. Then, the temporary table is sent to each remote server where queries run using this temporary data.
For non-distributed queries, use regular `IN` / `JOIN`.
Be careful when using subqueries with `IN` / `JOIN` clauses for distributed query processing.
Let's look at some examples. Assume each server in the cluster has a normal **local_table**. Each server also has a **distributed_table** with a **distribution** type, which views all servers in the cluster.
For queries on **distributed_table**, the query is sent to all remote servers and run using the command on **local_table**.
For example, search
```SQL
SELECT uniq(UserID) FROM distributed_table
```

will be sent to all remote servers
```SQL
SELECT uniq(UserID) FROM local_table
```

and runs each of them in parallel until a stage is reached where the intermediate results can be combined. Then, the intermediate results are returned to the requesting server for merging, and the final results are sent to the client.
Now let's check a query IN:
```SQL
SELECT uniq(UserID) FROM distributed_table WHERE CounterID = 101500 AND UserID IN (SELECT UserID FROM local_table WHERE CounterID = 34)
```


* Calculate the intersection of audiences between two websites.

This query will be sent to all remote servers in the following way
```SQL
SELECT uniq(UserID) FROM local_table WHERE CounterID = 101500 AND UserID IN (SELECT UserID FROM local_table WHERE CounterID = 34)
```

In other words, the dataset in the IN clause will be independently collected on each server, only gathering data locally stored on each server.
If you are prepared for this situation and have already distributed the data across cluster servers, so that the data of each user ID resides entirely on a single server, then this will work normally and optimally. In this case, all necessary data will be locally available on each server. Otherwise, the result will be inaccurate. We refer to this variant of Query as “local IN”.
To correct how queries work when data is randomly propagated across cluster servers, specify **distributed_table** in the subquery. The query is as follows:
```SQL
SELECT uniq(UserID) FROM distributed_table WHERE CounterID = 101500 AND UserID IN (SELECT UserID FROM distributed_table WHERE CounterID = 34)
```

This query is sent to all remote servers in the following manner:
```SQL
SELECT uniq(UserID) FROM local_table WHERE CounterID = 101500 AND UserID IN (SELECT UserID FROM distributed_table WHERE CounterID = 34)
```

The subquery will start running on each remote server. Since the subquery uses a distributed table, the subquery on each remote server will be re-sent to each remote server.
```SQL
SELECT UserID FROM local_table WHERE CounterID = 34
```

For example, if you have a cluster of 100 servers, running the entire query would require 10,000 basic requests, which is generally considered unacceptable.
In such cases, always use GLOBAL IN instead of IN. Let's take a look at how this query works.
```SQL
SELECT uniq(UserID) FROM distributed_table WHERE CounterID = 101500 AND UserID GLOBAL IN (SELECT UserID FROM distributed_table WHERE CounterID = 34)
```

The requester's server will run a subquery
```SQL
SELECT UserID FROM distributed_table WHERE CounterID = 34
```

The results will be placed in a temporary table in RAM. Then, the request will be sent to each remote server
```SQL
SELECT uniq(UserID) FROM local_table WHERE CounterID = 101500 AND UserID GLOBAL IN _data1
```

and the temporary table `_data1` will be sent via a query to each remote server (the name of the temporary table is implementation-defined).
This is more optimized than using a normal IN. However, remember the following points:

1. When creating a temporary table, the data is not unique. To reduce the amount of data transmitted over the network, specify DISTINCT in the subquery. (You do not need to do this for normal people.) )
2. The temporary table will be sent to all remote servers. Transmission does not consider network topology. For example, if 10 remote servers reside in a data center very far from the requester server, the data will be sent 10 times through the channel to the remote data center. When using GLOBAL IN, try to avoid large datasets.
3. When transferring data to remote servers, network bandwidth limits cannot be configured. You may cause network overload.
4. Try distributing data across servers so you don't need to regularly use GLOBAL IN.
5. If you need to frequently use GLOBAL IN, plan the location of the ClickHouse cluster so that a single replica group resides in no more than one data center and they have fast network between them, so queries can be completely processed within a single data center.

It also makes sense to specify a local table `GLOBAL IN` clause in case this local table is only available on the requester server and you want to use data from it on remote servers.
