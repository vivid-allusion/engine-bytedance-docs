---
title: "Middleware monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring"
---

Middleware monitoring aggregates data from application internal accesses to middleware, providing unified observation from the middleware perspective and facilitating middleware maintenance personnel in troubleshooting middleware issues.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

To access middleware, the application must integrate Trace capability. For details, see [Application integration](https://docs.byteplus.com/en/docs/apmplus/Java_application_integration).

<span id=".U1FM57G755uR5o6n"></span>
## SQL monitoring

SQL databases include Oracle, MySQL, and more.

<span id=".5pWw5o2u5bqT5YiX6KGo"></span>
### Database list


* Databases accessed are categorized by database granularity, displaying error rate, average QPS, mean latency quantile, and slow query proportion.

* All metrics support sorting.

* You can search by database name.

* You can subscribe to databases as needed.


<span id=".5pWw5o2u5bqT5oC76KeI"></span>
### Database overview

The database overview enables you to quickly obtain the most critical monitoring metrics for the current database, helping you identify issues such as excessive calls, high failure rate, or high latency.


* Metrics: QPS, upstream failure rate, response latency, slow query proportion


<span id=".6LCD55So5ouT5omR"></span>
### Call topology

The call topology allows you to quickly discover which services are calling the database, and you can search based on the call latency and status code to obtain the overall topology map.

Call relationships with excessive errors are highlighted in red, and services with a high failure rate are also highlighted in red.

Click a node in the topology map to open the **Service metric details** panel on the right, which displays core metrics such as the node's call QPS, error rate, and latency, and provides the following quick navigation options:


* Service node: [Service details](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pyN5Yqh5oC76KeI), [Trace Analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis?lang=en), [Log analysis](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pel5b-X5YiG5p6Q)

* Middleware node: [Middleware details](https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring?lang=en)


<span id=".U1FM5YiG5p6Q"></span>
### SQL analysis

The application reports specific information about database access, which is normalized to form SQL Patterns. SQL analysis enables clustering of SQL Patterns and provides key metrics such as events, failure rate, and average time for different SQL Patterns.

After clicking a specific SQL Pattern, you can drill down to the analysis page for that SQL Pattern. Here, you can view the events, failure rate, average response time, and quantile for the SQL Pattern, as well as individual execution records. You can filter by status code to quickly locate error execution records, and also filter and sort by execution time to quickly identify slow queries.

Clicking the original SQL allows you to view the complete request trace information, making it easier to troubleshoot issues using logs and other contextual information. You can also obtain the intelligently desensitized original execution SQL.

<span id=".57yT5a2Y57G755uR5o6n"></span>
## Cache monitoring

Cache databases include Redis, Memcached, MongoDB, DynamoDB, and more.

<span id=".57yT5a2Y5YiX6KGo"></span>
### Cache list

The list displays the Redis name, error rate, QPS, latency, most recent view time, and other information. All metrics support sorting, service name search, and you can subscribe to Redis names as needed.

<span id=".57yT5a2Y5oC76KeI"></span>
### Cache overview

Click the Redis name to enter the Redis details page, which displays trend charts for QPS, failure rate, and response time for that Redis.

<span id="v2v9EMYq"></span>
### Call topology

The call topology feature allows you to view the upstream call topology information for Redis, and supports filtering by call interface, status code, and time.

Click a node in the topology map, and a **service metric details** panel will pop up on the right, displaying core metrics such as QPS, error rate, and latency for that node, and providing the following quick navigation options:


* Service node: [service details](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pyN5Yqh5oC76KeI), [Trace Analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis?lang=en), [log analysis](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pel5b-X5YiG5p6Q)

* Middleware node: [middleware details](https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring?lang=en)


<span id=".5oyH5Luk5YiG5p6Q"></span>
### Command analysis

The command analysis feature allows you to view the Cmd commands received by Redis, along with QPS, error, and latency information for each command. Trend charts are shown on the right, and grouping by command is supported.

Click the command name to drill down to the trace search page for that specific command.

<span id=".5raI5oGv6Zif5YiX55uR5o6n"></span>
## Message queue monitoring

Message queues include Kafka, RabbitMQ, RocketMQ, and more.

<span id=".5raI5oGv6Zif5YiX5YiX6KGo"></span>
### Message queue list

The list displays the Kafka name, write QPS, consumption, write error rate, write latency, most recent view time, and other information.

All metrics support sorting, service name search, and you can subscribe to Kafka as needed.

<span id=".5raI5oGv6Zif5YiX5oC76KeI"></span>
### Message queue overview

Click the Kafka name to enter the Kafka details page, where trend charts for this Kafka's write and consumption QPS, failure rate, and latency are displayed.

<span id="OKgBm6ZE"></span>
### Call topology

The call topology displays the upstream producers and downstream consumers of this Kafka.

Click a node in the topology map to open the **service metric details** panel on the right, which displays the core metrics for that node, including call QPS, error rate, and latency, and provides the following quick navigation options:


* Service node: [service details](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pyN5Yqh5oC76KeI), [Trace Analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis?lang=en), [log analysis](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pel5b-X5YiG5p6Q)

* Middleware node: [middleware details](https://docs.byteplus.com/en/docs/apmplus/Middleware_monitoring?lang=en)


<span id=".55Sf5Lqn6ICF"></span>
### Producer

The producer section displays this Kafka's producers along with QPS, error, and latency information. Trend charts are shown on the right, and grouping by producer is supported.

<span id=".5raI6LS56ICF"></span>
### Consumer

The consumer section displays this Kafka's consumers along with QPS, error, and latency information. Trend charts are shown on the right, and grouping by consumer is supported.
