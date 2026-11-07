---
title: "Distributed table practice guide"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/distributed-table-practice-guide"
---

<span id="7f3f276a"></span>
# Compatible table creation mode

<span id="c31ed4cf"></span>
## Definition

For ByteHouse, by default, DDLs such as CREATE, DROP, ALTER, and RENAME are executed only on the current node. If you want the changes to affect the entire cluster, you can use the `ON CLUSTER` clause to run such queries in a distributed manner; the initial node will automatically send the DDL to each node for execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6bd239176044e358e0ce16eb63cb882~tplv-goo7wpa0wc-image.image) </span>

For example, the following query will create a distributed table named `all_hits` on every host in the cluster:

```SQL
CREATE TABLE IF NOT EXISTS all_hits ON CLUSTER cluster (p Date, i Int32) 
    ENGINE = Distributed(cluster, default, hits)
```


<span id="dfe42da9"></span>
## Operational details


1. Transactional Aspects: `On cluster` is not transactional, it cannot ensure complete success, nor can it be rolled back on a single node when it is being executed.

2. Idempotency: `On cluster` guarantees the order of query execution within a single node, thus if a distributed DDL is sent, each node will execute these DDLs in the sent order.

3. Queue: Distributed DDLs are scheduled through ZK and executed sequentially in the queue. Thus, even if some nodes are currently unavailable, once they restore response, the DDL will eventually be executed. You can view the queue through the system table `system.distributed_ddl_queue`.

4. Timeout: The timeout period is configured through `distributed_ddl_task_timeout` (session level parameter, default 180 seconds), and if the DDL times out, a timeout will be reported, but it will still be executed in the background according to the queue.


<span id="69d23c43"></span>
## Best practices


1. Each DDL (including Create, Alter, Truncate, Rename, Drop, and others) should be sent as a distributed DDL. Do not perform operations on a single node only, as it may cause inconsistency in metadata across multiple nodes.

2. If not initially executed as a distributed DDL, some nodes might have tables while others might not, leading to tables missing displays and causing intermittent errors in subsequent queries routed through the gateway. Suggestion: Resend a distributed DDL (no need to delete tables), which will complete these missing node tables.


<span id="733e4544"></span>
# General table creation mode

<span id="65d9ab88"></span>
## Definition

For ByteHouse, as long as the general table creation mode is activated, DDLs such as CREATE, DROP, ALTER, and RENAME sent to the ByteHouse gateway will be executed as distributed DDL queries. The initial node automatically sends the DDL to each node for execution. This ensures that the table information metadata across nodes is consistent, applicable in scenarios for general database creation, table creation, and table modification.

However, if DDLs are sent directly to nodes or queries are sent through the gateway's specified node mode, the DDL will only take effect on the target node. Commonly used for fixing data issues on a single node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bd543f7d17a4f51b798c9b2cdc09428~tplv-goo7wpa0wc-image.image) </span>

For example, the following query creates the `all_hits` distributed table on each host in the cluster:

```SQL
CREATE TABLE IF NOT EXISTS all_hits (p Date, i Int32) ENGINE = Distributed(cluster, default, hits)
```


<span id="bb8268a4"></span>
## Operational details


1. Transactional: The distributed DDL method is non\-transactional, cannot ensure complete success, nor can it be rolled back on a single node.

2. Idempotence: The order in which queries are executed within a single node is guaranteed with the distributed DDL method, so if a distributed DDL is sent, each node will execute these DDLs in the order they were sent.

3. Queue: Distributed DDLs are scheduled through ZK and executed sequentially in a queue. Thus, even if some nodes are currently unavailable, once the nodes regain responsiveness, the DDL will ultimately be executed. You can view the queue through the system table `system.distributed_ddl_queue`.

4. Timeout: The timeout period is configured by `distributed_ddl_task_timeout` (session\-level parameter, default 180 seconds). If a DDL times out, a timeout will be returned, but the operation will still proceed in the background according to the queue.


<span id="084bb4dc"></span>
## Best practice


1. Every DDL (including Create, Alter, Truncate, Rename, Drop, and others) should be sent through the gateway in the method of distributed DDL rather than being operated only on a single node, which would cause inconsistencies in metadata across multiple nodes.

2. If initially not executed through distributed DDL, partial nodes might have the table while others do not, the interface will display the table as missing, and it may cause intermittent errors in subsequent queries routed through the gateway. Suggestion: Reissue the distributed DDL (no need to drop the table) to complete the tables on the missing nodes.
