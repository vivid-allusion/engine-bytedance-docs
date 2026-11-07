---
title: "Terms"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Related_concepts"
---

This topic describes the terms of Torch Log Service (TLS).

<span id="9201d000"></span>
## Basic resources


|Terms |Description |
|---|---|
|Log |Logs are records of events that occur during the runtime of a system or a program. The events include user operation events, API access events, and runtime error events. All types of logs have a unified structure and format. |
|Trace data |Trace data records information about the entire trace of calling services, including the call relationship, latency, and result. |
|Project |A project is a unit of resource management. It isolates the resources of different tenants and controls access to resources. In general, 1 project corresponds to 1 application, business, or product. |
|Topic |A topic is a unit of data collection and storage. A project consists of one or more topics. Each topic belongs to one project. For one topic, you can configure different data sources and collection rules. |
|Shard |A shard is a basic unit of data reads and writes. All data is stored in shards. Each shard has a certain read and write capability. We recommend that you plan the number of shards based on your business needs. |


<span id="a29da203"></span>
## Data collection


|Terms |Description |
|---|---|
|LogCollector |LogCollector is a log collection tool developed by the BytePlus TLS team based on the open\-source tool Filebeat. LogCollector can receive collection rules and report logs to the server in real time. |
|Collection rule |A collection configuration is a set of rules used by LogCollector to collect logs. A collection configuration specifies various information, such as log file paths and collection methods. |
|Host group |In TLS, a host group is a virtual configuration unit that contains multiple servers. TLS distributes LogCollector collection rules by host group, and LogCollector batch collects logs from multiple servers in host groups. |


<span id="a77d76ec"></span>
## Data query and analysis


|Terms |Description |
|---|---|
|Query |TLS offers the real\-time query capability to search for tens of billion rows of data in seconds. To quickly find target logs, you can specify conditions in query statements. |
|Analysis |TLS supports the real\-time SQL calculation capability based on the query feature. This capability allows TLS to analyze and calculate massive logs in real time and display the analysis results in charts. |
|Query and analysis statement |A query and analysis statement consists of a query condition and an SQL analysis statement in the format of `&{query condition} \| &{SQL analysis statement}`. |
|Index |An index is a storage structure that sorts the values of one or more columns of a table. An index is similar to a data catalog. You can quickly find the target data row by keyword. TLS allows you to create full\-text indexes and key\-value indexes. |


<span id="5b34bc29"></span>
## Visualization


|Terms |Description |
|---|---|
|Dashboard |A dashboard is a real\-time data analysis tool offered by TLS to display query and analysis results in a centralized manner. |
|Chart |Charts visualize query and analysis results, including tables, line charts, pie charts, single value charts, and flow charts. |
|Dashboard filter |Dashboard filters can work with charts to filter chart data based on field names and field values. |


<span id="4eb346ad"></span>
## Data transformation


|Terms |Description |
|---|---|
|ETL |Extract, transform, and load (ETL) is the process of extracting, transforming, and loading data from a source to a destination. ETL integrates, standardizes, and unifies data. TLS can transform log data in a source topic and output the transformed data to a specified topic. |
|TLS DSL |TLS Domain Specific Language (DSL) is a Python\-like scripting language. TLS DSL is used to specify data processing logic in data transformation. TLS DSL offers dozens of functions to transform data. It can meet the data transformation requirements in various big data analysis and data warehouse scenarios. |
|Transformation rule |A transformation rule is an execution script for data transformation and a set of logical codes orchestrated using TLS DSL. |
|Transformation task |A transformation task is a unit for scheduling in data transformation. A transformation task defines configuration items such as the source topic, target topic, and transformation rule. |


<span id="d7df7e30"></span>
## Scheduled SQL


|Terms |Description |
|---|---|
|Scheduled SQL task |A scheduled SQL task is a collection of scheduled SQL rules. A scheduled SQL task defines configuration items such as the source topic, target topic, scheduling cycle, and SQL time window. |
|Scheduled SQL task instance |After scheduled SQL tasks start, TLS creates instances based on the specified scheduling cycle. Each instance runs the scheduled SQL task once on the source topic and writes the calculation results to the specified topic. |


<span id="1dbc1353"></span>
## Data consumption and shipping


|Terms |Description |
|---|---|
|Consumer group |A consumer group is a virtual collection of multiple consumers. When you consume log data using a consumer group, all consumers in the consumer group subscribe to the same topic and consume data in that topic. Each consumer consumes data in one or more shards of a topic. Consumers do not repeatedly consume data. |
|Consumer |A consumer is a client that consumes data from TLS. It is part of a consumer group.<br><br><br>* Consumer names in a consumer group are unique.<br><br>* At the same time, a shard of a topic can be assigned to a specific consumer in a consumer group, and 1 consumer can consume data from multiple shards. When a consumer group runs, how shards are assigned to its consumers may change. |
|Checkpoint |During consumption, a consumer program records checkpoints (cursors) of the current shard and reports the checkpoints to the server. The last checkpoint recorded before the program restarts becomes the start cursor when the program restarts. This checkpoint is used to ensure the program does not repeatedly consume data. |


<span id="3a84413a"></span>
## Alarm


|Terms |Description |
|---|---|
|Alarm policy |An alarm policy defines the data monitoring methods and alarm rules of TLS. In an alarm policy, you are required to specify configuration items such as the monitoring task, alarm rule, and alarm notification method. |
|Alarm notification group |An alarm notification group is a collection of alarm notification policies. An alarm notification group includes information such as the alarm notification type, receiving channel, and recipient. |
|Alarm trigger |An alarm trigger is an alarm notification type. When a monitoring result meets an alarm trigger expression, an alarm notification is sent. |
|Alarm clearance |Alarm clearance is an alarm notification type. When a monitored object becomes normal, a clearance notification is sent. |
|Content template |If alarm notifications are sent through the custom API callback channel, TLS sends an alarm notification based on content defined in a content template. In a content template, you can add variables. When a notification is sent, these variables are replaced with the actual values. |
