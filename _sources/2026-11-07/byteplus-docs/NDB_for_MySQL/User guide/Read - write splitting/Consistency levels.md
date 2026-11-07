---
title: "Consistency levels"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels"
---

The read\-write separation capability of the database proxy will parse every SQL sent in. If it is a write operation such as `UPDATE`, `DELETE`, `INSERT`, `CREATE`, it will be sent directly to the primary node. If it is a `SELECT` read operation, it will be sent to the read\-only node, thus achieving read\-write separation. However, when the database load is high, for example, when performing DDL operations (such as adding fields) on a large table or inserting data in large quantities, the data synchronization delay will be very high, resulting in the inability to read the latest data from the read\-only node. The read\-write splitting proxy feature cannot solve the query inconsistency problem caused by latency.

After data is written to the read\-write node, the related updates will be synchronized to the read\-only node. The delay time of data synchronization is related to the write pressure. NDB for MySQL provides different consistency levels to ensure data consistency requirements for business access to the database.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The consistency level can be adjusted from eventual consistency to session consistency or global consistency, which takes effect only for new connections. When the session consistency or global consistency is adjusted to the eventual consistency, the existing connections take effect immediately. For operation steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Editing connection endpoints</a>.</div>


<span id=".5pyA57uI5LiA6Ie05oCn"></span>
## Eventual consistency

<span id=".5Yqf6IO95LuL57uN"></span>
### Function introduction

NDB for MySQL provides automatic read\-write separation capabilities and provides an eventual consistency level for data by default, thus ensuring that read\-only nodes can eventually read updated data. However, eventual consistency does not guarantee that the latest data can be read immediately, because the master\-slave replication delay will cause different query results from different nodes. For example, if query operations are executed continuously within a session, the final `SELECT` results may be different.

<span id=".6YCC55So5Zy65pmv"></span>
### Applicable scenarios

In scenarios where consistency requirements are not very high, you can choose eventual consistency. Through the read\-write separation capability, you can reduce the pressure on the primary node and route read requests to read\-only nodes as much as possible.

<span id=".5Lya6K-d5LiA6Ie05oCn"></span>
## Session consistency

<span id=".5Yqf6IO95LuL57uN"></span>
### Function introduction

Since eventual consistency cannot guarantee the same results for consecutive queries within a session, it cannot meet scenarios with high consistency requirements. In this case, the business needs to be split, and only read/write nodes are accessed for services with high consistency requirements, while read and write separation mode can be adopted for services with low consistency requirements. To further reduce the burden of business transformation, NDB for MySQLprovides session consistency capabilities. Session consistency ensures that data that has been updated before the read request is executed can be queried within the same session. After this session is updated, the read result is stable until this session or other sessions are updated again.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61a0c1cff99bbd7769d49e2254468aec.jpg) </span>

In the NDB for MySQL link, the database proxy provides the ability to separate reads and writes, and the implementation of session consistency mainly depends on the database proxy.


1. The database agent records the log position that has been applied to each node, that is, the log sequence number (LSN).

2. Each time a read\-write transaction is committed, NDB for MySQL records the updated location as the Session LSN.

3. When a read request arrives, the database agent compares the Session LSN with the LSN of each node.

4. Requests are only sent to read nodes whose LSN is greater than or equal to the Session LSN, thus ensuring session consistency.


Because the database proxy node compares the advancement position of the read\-only node LSN, if the delay between the master and slave nodes is large, the business cannot wait all the time, which will affect the overall performance. Therefore, NDB for MySQL supports configuring the timeout threshold and the strategy after the timeout.


* Configure the timeout threshold: the default value is 10000us, and the value range is 1us~100000000us.

* Configure timeout policy:

   * Send request to primary node: If the master\-slave delay is too large and the configured timeout threshold is small, the read request will be sent to the primary node, increasing the pressure on the primary node.

   * SQL error: If the leader/follower delay is too large and exceeds the threshold, it will directly return an error (`wait replication complete timeout, please retry`).


In the above scenario, when the update is completed and the result is returned, data replication has already begun. Therefore, when the next read request arrives, the data replication between the primary node and the read\-only node is very likely to have been completed, that is, the read\-only node can provide the latest data query. Therefore, under this architecture, both session consistency and read\-write separation load balancing are guaranteed.

<span id=".6YCC55So5Zy65pmv"></span>
### Applicable scenarios

Applicable to scenarios with high consistency requirements. This level has little impact on performance and can meet the needs of most application scenarios.

<span id=".5YWo5bGA5LiA6Ie05oCn"></span>
## Global consistency

<span id=".5Yqf6IO95LuL57uN"></span>
### Function introduction

For scenarios where there may be causal relationships or dependencies between all sessions, session consistency will not be able to guarantee the consistency of query results. So NDB for MySQL also provides global consistency. When each read request reaches the database agent, the agent will first go to the primary node to confirm the current latest COMMIT LSN location, then find a suitable read\-only node, and then send the read request to the read\-only node. This ensures that the read request can read any data that has been updated up to the time the request is initiated.

To ensure the normal use of services, global consistency also supports the configuration of timeout thresholds and policies after timeout.


* Configure the timeout threshold: the default value is 10000us, and the value range is 1us~100000000us.

* Configure timeout policy:

   * Send request to primary node: If the master\-slave delay is too large and the configured timeout threshold is small, the read request will be sent to the primary node, increasing the pressure on the primary node.

   * SQL error: If the leader/follower delay is too large and exceeds the threshold, it will directly return an error (`wait replication complete timeout, please retry`).


<span id=".6YCC55So5Zy65pmv"></span>
### Applicable scenarios

When the master\-slave delay is high, the read\-only node cannot synchronize the latest data in time, which may cause more requests to be routed to the primary node, causing increased pressure on the primary node. Therefore, it is recommended to choose global consistency in scenarios with more reads than writes.

<span id="Qt97CXk8"></span>
## How to choose a consistency level


* The higher the consistency level, the lower the instance performance. Therefore, it is recommended to use **Session consistency**, which has little impact on performance and can meet the needs of most application scenarios.

* Try to avoid choosing global consistency. If a small amount of business logic requires global consistency, Hint can be used to force the corresponding request to be routed to the primary node. For details on using Hint, see [Hint syntax usage instructions](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Hint_syntax_usage_instructions).
