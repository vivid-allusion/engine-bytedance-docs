---
title: "Limits"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Limits"
---

<span id="Resource limits"></span>
## Resource limits

The following table describes the limits on the quotas of basic Torch Log Service (TLS) resources.


|Item |Description |
|---|---|
|Number of projects |Each BytePlus account can have up to 100 projects in a region by default. |
|Number of topics |Up to 200 topics can be created in a project by default. |
|Number of shards |* When you create a topic, up to 10 shards can be created for the topic by default.<br><br>* After you create a topic, use the feature of splitting shards to add shards. A topic supports up to 256 shards in the read/write state. |
|Host group |* A BytePlus account can have up to 200 host groups in a Region by default.<br><br>* Up to 200 IP addresses can be added to a host group by default. |
|Dashboard |* Up to 50 dashboards can be created in a project by default.<br><br>* The sum of filters, variables, and charts on a dashboard cannot exceed 50. |
|Data transformation |* Up to 100 transformation tasks can be created in a project by default.<br><br>* Up to 30 transformation tasks can be created in a topic by default. |
|Data consumption |Up to 150 consumer groups can be created in a project by default. |
|Alarm |* Up to 100 alarm policies can be created in a project by default.<br><br>* Up to 10 alarm policies can be created in a topic by default. |
|Log storage period |The log storage period can range from 1 to 3,650 days. 3650 means that log data is permanently stored. |


<span id="Reserved fields"></span>
## flow control limits

<span id="8eccd420"></span>
### Literacy limits

<span id="06fd6425"></span>
#### account level

Each BytePlus account provides certain reading and writing capabilities. Please refer to the following table for details.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Non\-mandatory requirements, when data reads and writes exceed the reading and writing capabilities of the shard, the system will provide services as much as possible, but does not promise quality of service.</div>



|Item |Description |
|---|---|
|Read QPS |20000 queries/s |
|Write QPS |20000 queries/s |
|read traffic |1 GiB/s |
|write traffic |1 GiB/s |


<span id="ba7603ed"></span>
#### Shard level

Each shard provides some reading and writing capabilities. Please refer to the following table for details.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Non\-mandatory requirements, when data reads and writes exceed the reading and writing capabilities of the shard, the system will provide services as much as possible, but does not promise quality of service.</div>



|Item |Description |
|---|---|
|Read QPS |100 queries/s |
|Write QPS |500 queries/s |
|read traffic |20 MiB/s |
|write traffic |5 MiB/s |


<span id="c4b76081"></span>
### Other flow control limits

Each BytePlus account also defines a number of other TLS flow control limits. Please refer to the following table for details.


|Item |Description |
|---|---|
|QPS for obtaining LogCollector configuration |4000 queries/s |
|QPS for reporting LogCollector heartbeat |2000 queries/s |
|QPS for reporting consumer group heartbeat |2000 queries/s |
|QPS for obtaining consumer group Checkpoint |500 queries/s |
|Dashboard subscription QPM |1 queries/min |
|QPS for calling control interface |20 queries/s |


<span id="0c55d1f9"></span>
## LogCollector limits

When you use LogCollector to collect log data, pay attention to the limits on the installation environment and collection behaviors of LogCollector. For more information, refer to [LogCollector limits](https://docs.byteplus.com/docs/tls/logcollector_limits).

<span id="Query and analysis limits"></span>
## Query and analysis limits

The following table describes the limits on log query and analysis operations in TLS.

<span id="Query limits"></span>
### Query limits


|Item |Description |Remarks |
|---|---|---|
|Number of characters for a single field |After a log is separated by delimiters, the length of a single field cannot exceed 255 characters. |If the length exceeds the limit, the log cannot be queried by keyword, but the log data remains complete on the server. |
|Query statement length |The maximum length of a single query statement is 4,096 characters. |/ |
|Phrase search |Phrase search selects a maximum of 10,000 logs for phrase matching. |/ |
|Number of concurrent operations |* Standard Storage:<br><br>   * Each project supports up to 100 concurrent query operations.<br><br>   * Each topic supports up to 15 concurrent query operations.<br><br>* Infrequent Access Storage:<br><br>   * Each topic supports up to 10 concurrent query operations.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Infrequent Access Storage is a beta feature, and if there are business needs, you can contact your account manager to apply for the whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the search range of logs includes both Standard Storage and Infrequent Access Storage, the number of concurrent operations is based on the limit for Infrequent Access Storage.</div><br> |/ |
|Timeout period |The query timeout period is 55 seconds. |/ |
|Fuzzy search |In a fuzzy search, TLS can retrieve up to 100 words that meet the search condition and return all logs that contain these 100 words and meet the search condition. |/ |
|Keyword search |In a keyword search, you can specify up to 30 search conditions excluding Boolean logical operators. |/ |
|Number of return results |After a query, up to 100 query results are returned by default. |Turn pages to get up to 100,000 log entries. |
|Query result sorting |By default, the latest logs are displayed. The log time is accurate to seconds or milliseconds. |/ |
|Display of a single log entry |TLS performs the Document Object Model (DOM) operation only on the first 10,000 characters of a log due to browser performance limits. |/ |


<span id="dc5d94b9"></span>
### Analysis limits


|Item |Description |
|---|---|
|Data volume |A single shard supports analyzing up to 1 GiB of data at a time. |
|Length of a single query and analysis statement |The maximum length of a single query and analysis statement is 50,000 characters, with the query statement portion having a maximum length of 4,096 characters. |
|Size of field values |The maximum value of a single field is 16 KB, that is, 16384 bytes, and the part exceeding this limit will not be involved in the analysis.<br><br>The maximum length of the field values supported by TLS by default is 2048 bytes, that is, 2 KB. When you need to adjust the maximum length of the field values, you can set the maximum length of the statistical fields. For specific operations, please refer to [Set the maximum length of the field](https://docs.byteplus.com/docs/tls/Configure-indexes-2#3233079a).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the maximum length of the field is updated, it is only valid for incremental data.</div><br> |
|Number of concurrent operations |* Standard Storage:<br><br>   * Each project supports up to 100 concurrent analysis operations.<br><br>   * Each topic supports up to 15 concurrent analysis operations.<br><br>* Infrequent Access Storage:<br><br>   * Each topic supports up to 2 concurrent analysis operations.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Infrequent Access Storage is a beta feature, and if there are business needs, you can contact your account manager to apply for the whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the search range of logs includes both Standard Storage and Infrequent Access Storage, the number of concurrent operations is based on the limit for Infrequent Access Storage.</div><br> |
|Applicable data scope |The analysis feature only takes effect for data written to TLS after the statistics feature is enabled. For fields where the statistics feature is not enabled, SQL analysis results are empty. |
||SQL analysis only takes effect for data corresponding to the latest version of the index. Data before index modification can only be queried. |
|Timeout period |The query timeout period is 55 seconds. |
|Number of results |After analysis, up to 100 results are returned by default.<br><br>To view more data, use the [LIMIT syntax](https://docs.byteplus.com/docs/tls/LIMIT-syntax-2) to get up to 100,000 results. |


<span id="Data transformation"></span>
## Data transformation limits


|Item |Description |
|---|---|
|Number of tasks |A maximum of 100 data transformation tasks can be created in each project, and a maximum of 30 data transformation tasks can be created in each topic. Tasks of all statuses displayed on the page are included.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Paused and completed tasks consume the quota. If you confirm that these tasks are no longer used, we recommend that you clear the task list in a timely manner to reduce quota usage. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/manage_data_transformation_tasks">Manage data transformation tasks</a>.</div><br> |
|Number of target topics |In 1 data transformation task, a maximum of 20 different topics can be configured to store transformed data. |
|Execution preview |The execution preview feature of data transformation is used to debug data transformation code online. Note the following limits:<br><br><br>* Include up to 20 logs or test data entries in a single request. Otherwise, your preview request returns an error.<br><br>* In a single request, at most the first 100 transformation results can be returned. |
|Transformation performance |The calculation formula for the overall rate of a transformation task is `Number of read/write shards in the source topic × 1 MiB/s (traffic before compression)`. Meanwhile, the rate is limited by factors such as the complexity of transformation rules, the transformation concurrency of the source topic, the rate of consuming the source topic, and the rate of writing data to the target topic. |


<span id="1a53ed29"></span>
## Scheduled SQL limits


|Category |Item |Description |
|---|---|---|
|Resource management |Number of scheduled SQL tasks |* Up to 100 scheduled SQL tasks can be created in a project.<br><br>* Up to 15 scheduled SQL tasks can be created in a source topic. |
||Deletion of scheduled SQL tasks |The Trace feature of TLS is available when the scheduled SQL tasks run as expected. To ensure the availability of the Trace service, do not manually perform change operations on the scheduled SQL tasks corresponding to the Trace service. For example, do not modify the corresponding configuration or delete the scheduled tasks. To modify the configuration of the Trace service or deactivate the service, perform the operation on the pages of the Trace service. |
||Historical records for task execution |Historical records for task execution can be saved for up to seven days. We recommend that you create an alarm monitoring task for the service logs generated due to scheduled SQL tasks. This way, you can find issues and retry instances that report errors in a timely manner. |
||Task scheduling concurrency |A single account supports 10 concurrent operations. |
|Data write |Data latency |If data latency exists, the corresponding data may not be written to TLS during data query. If data at a point in time arrives after the corresponding scheduling instance completes execution, the next scheduling instance does not query the data. |
||Instance concurrency |In a Region, up to 10 scheduling instances can run at the same time, and only one scheduling instance can be in the scheduling state in a task. |
||Retry after write failures |After a data write operation fails, the system retries the operation 3 times with an interval of 60 seconds each time. If the operation still fails after the system retries it 3 consecutive times, the instance changes to the status that indicates failed execution. We recommend that you create an alarm monitoring task for the service logs generated due to scheduled SQL tasks. This way, you can find issues and retry instances that report errors in a timely manner. |


<span id="67bf058c"></span>
## Data shipping limits

<span id="f02ae06f"></span>
### Shipping limits for Torch Object Storage (TOS)


|Item ||Description |
|---|---|---|
|Account ||Log data cannot be shipped across BytePlus accounts. The project and TOS bucket must be in the same BytePlus account. |
|Region ||Log data cannot be shipped across Regions. The topic and TOS bucket must be in the same Region. |
|Field ||For shipping log data in JSON format, all fields including metadata fields such as `__source__` are shipped by default. For shipping log data in CSV format, you can configure the list of fields to be shipped as needed. |
|Resource quota |Number of shipping configurations |Up to 10 TOS shipping configurations can be created in a topic. |
||Shipping task query |Shipping tasks triggered within the last 3 days can be queried. |
||Shipping interval |A shipping interval can be set to 60–900 seconds. |
||Shipping data size |The size of a package is 5–256 MiB. |


<span id="78a74668"></span>
### Shipping limits for Kafka


|Item |Description |
|---|---|
|Account |Log data cannot be shipped across BytePlus accounts. The project and Kafka instance must be in the same BytePlus account. |
|Region |Log data cannot be shipped across Regions. The topic and Kafka instance must be in the same Region. |
|Resource quota |Up to 10 Kafka shipping configurations can be created in a topic. |


<span id="be0efdba"></span>
## Alarm limits


|Category |Item |Description |
|---|---|---|
|Alarm monitoring |Number of alarm policies |Up to 100 alarm policies can be created in a project. Up to 10 alarm policies can be created in a topic. |
||Length of a field value |If the value of a field exceeds 1,024 characters in length, only the first 1,024 characters are truncated for analysis. |
||Time range for query and analysis |Each query and analysis statement cannot span more than 24 hours. |
||Query and analysis results |* When there is no set operation, the monitoring task selects at most the first 1000 rows of data in the query analysis result for alarm triggering. when there is a set operation, the monitoring task selects at most the first 1000 rows of data in the set operation result for alarm triggering.<br><br>* When monitoring three sets in association, the monitoring task selects at most the first 100 rows of data in each query analysis result for the set operations. |
||Length of an alarm expression |An alarm expression can contain from 4 through 1,024 characters. |
|Notification management |Number of alarm notification groups |You can create up to 100 alarm notification groups in each Region. |
||Number of notification channels |You can add a maximum of 10 notification channels to each alarm notification group. |
||Notification content |The notification content cannot exceed 4,096 Chinese characters in length. |


<span id="2c1ff6c3"></span>
## Resource Naming Limit

TLS includes project, topic, external data sources, dashboards, collection configuration, scheduled SQL tasks, transformation tasks, trace instances, shipping tasks and other resources. The naming rules are as follows:


|Resources |Description |
|---|---|
|project, topic, external data source |* The length is 3 to 64 characters.<br><br>* Only chinese characters, lowercase letters, numbers, underscores (_) and hyphens (\-) are supported.<br><br>* It is not supported to start or end with Underscores (_) and hyphens (\-) .<br><br>* It does not support the fields starting with reserved keywords such as `tls_`, `tos_`, `tls-`, `volc_`. |
|Resources other than project, topic, external data sources |* The length is 3 to 64 characters.<br><br>* Only chinese characters, letters, numbers, underscores (_) and hyphens (\-) are supported.<br><br>* It is not supported to start or end with a hyphen (\-).<br><br>* It does not support the fields starting with reserved keywords such as `tls_`, `tos_`, `tls-`, `volc_`. |
