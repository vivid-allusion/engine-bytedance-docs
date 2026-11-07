---
title: "Materialized view"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-materialized-view"
---

Materialized view is a technical method that stores query result data. It accelerates queries and simplifies query logic by exchanging space for time to avoid recalculating and aggregating data during queries.

ByteHouse supports transparent query rewrite mechanisms for materialized views, which can automatically select appropriate materialized views for query rewriting without changing the original query statements. Currently, the materialized views in ByteHouse are online, and they do not have a manual refresh feature, allowing real\-time data synchronization from the source table to the target table.

This article will explain the basic syntax for creating materialized views. For detailed usage, please refer to [Best practices for materialized view](https://docs.byteplus.com/docs/bytehouse/best-practices-for-materialized-view).

<span id="2d704a85"></span>
# Usage restrictions

Currently, there are the following restrictions on the use of materialized views:


1. The target table engine **does not support HaUniqueMergeTree yet**. It currently only supports HaMergeTree, HaAggregatingMergeTree, and HaSummingMergeTree engines.

2. The query SQL used to generate materialized views **does not currently support multi\-table queries**.


<span id="3d78b02e"></span>
# Create materialized view

<span id="c9ec73f0"></span>
## Basic syntax

```SQL
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster_name]
    [TO [db.]name]
    [ENGINE = engine]
    [ORDER BY order_by_key]
    [PARTITION BY partition_key]
    [TTL ttl_expr]
    [POPULATE] AS SELECT ...
```


<span id="da63e1fe"></span>
## Parameter Explanation


* `TO [db.]name`: Target table name, it is recommended that the target table is a local table. If not provided, a table will be automatically generated with an automatically generated name (for example, `.inner_id.24c211a5-fec3-45a3-afed-e3d3cf46a1ea`).

* `ENGINE = engine`: Target table engine, needs to be specified if the target table name is not provided. Currently, only supports HaMergeTree, HaAggregatingMergeTree, and HaSummingMergeTree engines, does not support HaUniqueMergeTree yet.

* `[ORDER BY order_by_key]`, `[PARTITION BY partition_key]`, `[TTL ttl_expr]`: Required if the target table name is not provided, with the same specification requirements as when creating a local table for `order_by_key`, `partition_key`, and `ttl`.

* `[POPULATE]`: When creating a materialized view, you can add the keyword POPULATE before AS SELECT, allowing data already existing in the source table to be written into the materialized view. However, it is generally not recommended to set this field: on one hand, the data volume in the source table might be very large, and setting `POPULATE` to write all data into the view might result in timeouts or failures; on the other hand, during the creation process of the view, POPULATE cannot allow data being written into the source table to be inserted into the view.

* `AS SELECT`: The SQL used to generate materialized views, not yet supporting multi\-table queries.
