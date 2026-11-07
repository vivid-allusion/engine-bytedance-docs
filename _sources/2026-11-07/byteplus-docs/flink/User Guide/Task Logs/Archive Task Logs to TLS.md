---
title: "Archive Task Logs to TLS"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Archive_Task_Logs_to_TLS"
---

You can configure job log output to TLS. Enhance log usage experience using TLS's powerful retrieval alarm capabilities. This article explains how to configure Flink job log output to TLS.

<span id="3a404d36"></span>
# Prerequisites


* It is required that you activate the TLS service in advance, and create the projects and topics that will receive the Flink logs. Please refer to the [TLS Log Topic Documentation](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* You need to prepare AK/SK with TLS write permissions for configuring Flink to authenticate writing to TLS. Please refer to [Access Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* It is recommended to configure the indexing for the Flink log topics in advance to facilitate subsequent log retrieval; see the next section for specific log fields.


<span id="5b6f50d4"></span>
# Log Field Description

Flink logs are archived into TLS with the following default fields.


|Field name |Description |
|---|---|
|`level` |Log Level. |
|`location` |Code location for log print statements. |
|`message` |Log Content. |
|`throwable` |Log Exception Information.<br><br>This field is only displayed in the log if the exception information is recorded. |
|`thread` |Thread Name. |
|`time` |Log printing time.<br><br>Supports configuration of the format and time zone of the time field through `timeFormat` parameter or `timeZone` parameter. |
|`log` |Customize the log format. |
|`__tag____client_ip__` |Log collection side IP address. |
|`__tag____receive_time__` |TLS log reception time. |
|`job_name` |Flink Job Name. |
|`deployment_id` |Unique ID after the Flink Job is deployed.<br><br>The current console does not display this ID; in most cases, different jobs can be distinguished using `job_name`. If duplicate job names exist, the deployment_id can be found in the job operation list page by inspecting the response of a browser’s debugging tool `deployment_id`. |
|`application_id` |Flink job's runtime instance ID, a new ID is auto\-generated every time the job is started.<br><br>This ID can be viewed on the job operations page. |
|`role` |Enumeration type: jobManager/taskManager<br><br>Used to differentiate between Flink JobManager and TaskManager. |
|`pod_name` |Pod name where logs are located, used to distinguish between multiple JobManager and TaskManager instances. |


<span id="dedb3294"></span>
# Configure log archiving into TLS


1. Log configuration entry.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2db7029e55b1477e804c2f126d827694~tplv-goo7wpa0wc-image.image) </span>

   1. Login to the Flink console and enter the corresponding project.

   2. Click **JupyterLab/Job Development** to enter the job development page and select the job that needs configuration.

   3. In the bottom right corner of the job development page, click **Log Configuration** to enter the configuration page.

2. Enable TLS archiving.

   1. Enable log archiving to TLS configuration. Enabling log archiving will display subsequent parameter configuration entry points.

3. Configure the root log level.

   1. Configure the root log level.

   2. Note that this configuration applies to both TLS archiving and Flink platform logs.

   3. Changing to a higher log level may result in inability to troubleshoot issues.

4. Configure class\-specific log levels.

   1. Set log levels for different classes; effective for both TLS archiving and Flink platform logs.

5. Configure custom TLS parameters.

   1. Common parameters for TLS log collectors are as follows.

   
   | |Parameter name |Default value |Description |
   |---|---|---|---|
   |Access information |topicId |Mandatory, no default value |TLS log topic ID, viewable on the TLS log project page.<br><br>For example:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15235a9db9764dd393b7f2adbd8f3e0d~tplv-goo7wpa0wc-image.image) </span> |
   ||region |Required, no default value |Region where the service is located. For example: cn\-beijing/cn\-shanghai/cn\-guangzhou, etc. |
   ||endpoint |Required, no default value |Required, TLS log project address. Use a private network address within the same region; a public network address is needed for cross\-region writing. View on the TLS log project page.v |
   ||accessKeyId |Required, no default value |TLS service associated account's AccessKey ID. |
   ||accessKeySecret |Required, no default value. |TLS service associated account's AccessKey Secret. |
   |Field configuration |timeZone |Asia/Shanghai |Time field time zone. |
   ||timeFormat |yyyy\-MM\-dd HH:mm:ss,SSS |Time Field Format. |
   ||layout.type |PatternLayout |Log output format, must be used in conjunction with `layout.pattern`. |
   ||layout.pattern |%d{yyyy\-MM\-dd HH:mm:ss,SSS} %\-5p %\-60c %x \- %m%n |Log output format, must be used in conjunction with `layout.type`. |
   ||fields.{custom field}.type |None |Custom fields, which can be used to add some fixed key\-value pairs to distinguish different Flink jobs.<br><br>The {custom field} must be replaced with a unique name that does not conflict with Flink's built\-in keywords (name, app, deployment, role, pod).<br><br>type, name, and value must be used together.<br><br>The type is fixed as `TLSField`.<br><br>The name should be a field name that does not duplicate Flink’s default fields; see **the log field description** for the detailed list.<br><br>The value is the actual content of the field. |
   ||fields.{custom field}.name |None ||
   ||fields.{custom field}.value |None ||
   |TLS write parameter configuration |totalSizeInBytes |104857600 |The upper limit of log size that a single producer instance can cache, default is 100MB. |
   ||maxBlockMs |0 |If there is insufficient space available for the producer, the maximum block time on the send method call, by default, is 0 seconds. To prevent blocking the log printing thread, it's strongly recommended to set this value to 0. |
   ||maxThreadCount |Number of processors |The size of the thread pool for executing log sending tasks, by default, equals the number of available processors. |
   ||maxBatchSizeBytes |524288 |When the log size in a ProducerBatch is greater than or equal to maxBatchSizeBytes, the batch will be sent. The default is 512 KB, and it can be set up to 5MB. |
   ||maxBatchCount |4096 |When the number of logs in a ProducerBatch is greater than or equal to maxBatchCount, the batch will be sent. The default is 4096, and it can be set up to 40960. |
   ||lingerMs |2000 |The linger time of a ProducerBatch from creation to being ready to send is 2 seconds by default, with a minimum possible setting of 100 milliseconds. |
   ||retryCount |10 |If a ProducerBatch fails on its first send, the default number of retries allowed is 10.<br><br>If the retryCount is less than or equal to 0, the ProducerBatch will be placed directly in the failure queue after its first send failure. |
   ||maxReservedAttempts |3 |The larger this parameter, the more information you can trace, but it will also consume more memory. |
   

6. Save configurations, launch tasks, and restart tasks to take effect.


<span id="e67a988c"></span>
# Use case scenarios.


1. Collect logs above the WARN level to TLS to reduce TLS storage costs. Add the following settings


```YAML
filter.threshold.type: ThresholdFilter
filter.threshold.level: WARN
```



2. Add custom fields to distinguish between production tasks and test tasks


```YAML
fields.env.type: TLSField # Fixed usage
fields.env.name: env # TLS filed name
fields.env.value: test/pre/online # Configure different values for different tasks to differentiate the environment
```


<span id="3db77a46"></span>
# Related links


1. [TLS configuration index.](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2)

2. [TLS retrieves logs.](https://docs.byteplus.com/en/docs/tls/Query-logs-2)

3. [TLS configures log alerts.](https://docs.byteplus.com/en/docs/tls/alert_overview)


&nbsp;
