---
title: "Service log fields"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/service_log_fields"
---

Torch Log Service (TLS) offers log data about the run information of multiple features, such as Torch Object Storage (TOS) data import. This topic describes the fields for each service log type.

<span id=".5pyN5Yqh5pel5b-X57G75Z6L"></span>
## Service log types

TLS supports the following service log types:


|Log Type |Feature |Topic |Description |
|---|---|---|---|
|[Data import logs](https://docs.byteplus.com/docs/tls/service_log_fields#.dG9zLeaVsOaNruWvvOWFpei_kOihjOaXpeW_lw==) |TOS data import |tls_import\-task |After a TOS data import task is completed, its log is automatically recorded. TLS records the run data and details of each import task. |
|[Data import error logs](https://docs.byteplus.com/docs/tls/service_log_fields#.dG9zLeaVsOaNruWvvOWFpemUmeivr-aXpeW_lw==) |TOS data import |tls_import\-task |The logs are reported only if an error occurs during the process of importing data from TOS. A log entry is recorded for each file that fails to be imported. |
|[LogCollector status logs](https://docs.byteplus.com/docs/tls/service_log_fields#.bG9nY29sbGVjdG9yLeeKtuaAgeaXpeW_lw==) |LogCollector host group |tls_log\-collector\-status |The logs are recorded only after the LogCollector service log feature is manually enabled. After enabled, each LogCollector client records the run status every minute in the logs. |
|[LogCollector business logs](https://docs.byteplus.com/docs/tls/service_log_fields#.bG9nY29sbGVjdG9yLeS4muWKoeaXpeW_lw==) |LogCollector host group |tls_log\-collector\-business |The logs are recorded only after the LogCollector service log feature is manually enabled. After enabled, LogCollector reports the collection progress of each file every minute. |
|[Data transformation logs](https://docs.byteplus.com/docs/tls/service_log_fields#.5pWw5o2u5Yqg5bel6L-Q6KGM5pel5b-X) |Data transformation |tls_etl\-log |When a transformation task is running, TLS automatically records the task progress and prints the information to service logs at regular intervals.<br><br>If an error occurs during the data transformation process, the error message is recorded in the run logs and `logging.level` is set to ERROR. |
|[Data shipping logs](https://docs.byteplus.com/docs/tls/service_log_fields#.5pWw5o2u5oqV6YCS6L-Q6KGM5pel5b-X) |Shipping data to TOS or Kafka |tls_shipper\-log |After data shipping is enabled, TLS automatically records the execution information about a shipping task that is triggered on schedule and prints the information to service logs.<br><br>If an error occurs during the shipping process, the error message is recorded in the run logs. |
|[Consumer group lag logs](https://docs.byteplus.com/docs/tls/service_log_fields#.5raI6LS557uE5bu26L-f5pel5b-X) |Consumer group |tls_consumergroup\-log |If you use the SDK consumer group feature, TLS records the consumption lag in seconds for each shard in the consumer group every 2 minutes and prints the information to service logs. |
|[Scheduled SQL logs](https://docs.byteplus.com/docs/tls/service_log_fields#.5a6a5pe2LXNxbC3ov5DooYzml6Xlv5c=) |Scheduled SQL |tls_schedule\-sql\-log |After the instances of a scheduled SQL task start running, TLS periodically records the execution information of each instance and prints the information to service logs. |
|[Alarm policy execution logs](https://docs.byteplus.com/docs/tls/service_log_fields#275238d1) |Log alarms |tls_alarm\-log |After an alarm policy takes effect, TLS periodically records the execution information about each monitoring task, such as the execution time and result, and prints the information to service logs. |
|[Alarm event logs](https://docs.byteplus.com/docs/tls/service_log_fields#6487bd15) |Log alarms |tls_alarm\-log |Every time an alarm policy is triggered, TLS prints an alarm event log entry to record the metadata when the alarm is triggered. |


<span id=".dG9zLeaVsOaNruWvvOWFpei_kOihjOaXpeW_lw=="></span>
## Data import logs

The run logs of TOS data import tasks are stored in the tls_import\-task topic. TLS records the run data and details of each import task.


|Field |Example |Description |
|---|---|---|
|TaskID |123\-xxx |The ID of the import task. |
|TaskStatus |Finished |The status of the import task, including:<br><br><br>* Finished: The data is imported successfully.<br><br>* Transferring: The data is being imported.<br><br>* Abnormal: An error occurs when the data is imported. |
|SourceType |tos |The type of the data source from which the data is imported, including:<br><br><br>* tos: TOS data. |
|Transferred |5004 |The number of imported objects. |
|Failed |0 |The number of objects that fail to be imported. |
|Skipped |0 |The number of objects that are skipped during the import. |
|NotExist |0 |The number of objects that fail to be imported as they do not exist. |
|Total |5004 |The total number of objects in the task. |
|BytesTransferred |20372186 |The size of imported files. Unit: bytes. |
|BytesTotal |20372186 |The total size of all files. Unit: bytes. |


<span id=".dG9zLeaVsOaNruWvvOWFpemUmeivr-aXpeW_lw=="></span>
## Data import error logs

The error logs of TOS data import tasks are stored in the tls_import\-task topic. The logs are reported only if an error occurs during the process of importing data from TOS. A log entry is recorded for each file that fails to be imported.


|Field |Example |Description |
|---|---|---|
|TaskID |123\-xxx |The ID of the import task. |
|SourceType |tos |The type of the data source from which the data is imported, including:<br><br><br>* tos: TOS data. |
|Object |abc.log |The path for storing the imported objects in TOS. |
|Status |NotExist |The status of the imported objects, including:<br><br><br>* Success: The object is imported successfully.<br><br>* Failed: The object fails to be imported. For more information on the failure cause, refer to the Error field.<br><br>* Skip: The object is skipped. For example, the object size exceeds the limit or the file fails to be uncompressed.<br><br>* NotExist: The object does not exist. For example, the file cannot be found by TLS as it was deleted during the import process. |
|Error |Obj not exist |The cause of the import failure, including:<br><br><br>* Obj not exist: The imported object does not exist. For example, the file cannot be found by TLS as it was deleted during the import process.<br><br>* Other causes such as TOS access failures. For more information on the error message, refer to the value of the Error field. |


<span id=".bG9nY29sbGVjdG9yLeeKtuaAgeaXpeW_lw=="></span>
## LogCollector status logs

LogCollector status logs are stored in the tls_log\-collector\-status topic. Each LogCollector client records the run status every minute in the logs.


|Field |Description |
|---|---|
|InstanceId |The unique identifier of the LogCollector client. |
|Label |The host label array. |
|IP |The IP address of the host. |
|Version |The LogCollector version number. |
|HeartbeatStatus |The status of the latest LogCollector heartbeat:<br><br><br>* normal: The heartbeat status is normal.<br><br>* abnormal: The heartbeat status is abnormal. |
|MemoryUsed |The memory usage. Unit: bytes. |
|CpuUsage |The CPU utilization. |
|SendTotalLogSize |The total volume of logs that are sent since the last time LogCollector started. Unit: bytes. |
|SendTotalLogCount |The number of log entries that are sent. |
|SendSuccessLogSize |The total volume of logs that are sent. Unit: bytes. |
|SendSuccessLogCount |The number of log entries that are sent successfully. |
|SendDropLogSize |The total volume of logs that are discarded as they fail to be sent. Unit: bytes. |
|SendDropLogCount |The number of log entries that are discarded as they fail to be sent. |
|SendTotalReqs |The total number of requests sent to the server. |
|SendSuccessReqs |The number of successful requests. |
|SendFailReqs |The number of failed requests. |
|SendLimitReqs |The number of requests intercepted due to rate limiting. |
|SendDeleteReqs |The number of requests intercepted as the target topic was deleted. |
|QueueCurrSize |The number of logs currently cached on the LogCollector client. |
|QueueCurrBytes |The volume of logs currently cached on the LogCollector client. Unit: bytes. |


<span id=".bG9nY29sbGVjdG9yLeS4muWKoeaXpeW_lw=="></span>
## LogCollector business logs

LogCollector business logs are stored in the tls_log\-collector\-business topic. LogCollector reports the collection progress of each file every minute.


|Field |Description |
|---|---|
|InstanceId |The unique identifier of the LogCollector client. |
|Label |The host label array. |
|IP |The IP address of the host. |
|Version |The LogCollector version number. |
|TopicId |The topic to which logs are written. |
|FilePath |The path of the log file that is being collected. |
|RealFilePath |The actual path of the log file that is being collected on the physical machine. |
|FileSize |The size of the log file that is being collected. Unit: bytes. |
|ReadOffset |The offset for reading the file. Unit: bytes. |
|SendSuccessOffset |The offset for successfully sending log data. Unit: bytes. |
|StartReadTimestamp |The timestamp of when the file reading starts. |
|LastReadTimestamp |The timestamp of when the file is most recently read. |
|ParseSuccessSize |The volume of logs that are parsed successfully. Unit: bytes. |
|ParseSuccessCount |The number of log entries that are parsed successfully. |
|ParseFailSize |The volume of logs that fail to be parsed. Unit: bytes. |
|ParseFailCount |The number of log entries that fail to be parsed. |
|FormatTimeSuccessSize |The size of log entries that are parsed when the time field is parsed based on a specified time format. Unit: bytes. |
|FormatTimeSuccessCount |The number of log entries that are parsed when the time field is parsed based on a specified time format. |
|FormatTimeFailSize |The size of log entries that fail to be parsed when the time field is parsed based on a specified time format. Unit: bytes. |
|FormatTimeFailCount |The number of log entries that fail to be parsed when the time field is parsed based on a specified time format. |
|FilterSize |The size of log entries that are filtered based on the specified filter configuration. Unit: bytes. |
|FilterCount |The number of log entries that are filtered based on the specified filter configuration. |
|HarvesterStatus |The file collector status, including:<br><br><br>* started: The file collector is started.<br><br>* waiting: The file collector is waiting for collecting a file.<br><br>* running: The file collector is collecting a file.<br><br>* closed: The collection ends. |


<span id=".5pWw5o2u5Yqg5bel6L-Q6KGM5pel5b-X"></span>
## Data transformation logs

Data transformation logs are stored in the tls_etl\-log topic. TLS periodically records the running logs of each data transformation task, including the source topic shard\-level input, filter, failure, and output information.


|Field |Example |Description |
|---|---|---|
|task_id |123\-xxx |The ID of the transformation task. |
|etl_context.project |abc\-xxx |The project to which the source topic of the transformation task belongs. |
|etl_context.topic |edf\-xxx |The source topic ID of the transformation task. |
|etl_context.shard_id |0 |The shard ID of the source topic consumed by the transformation task. |
|logging.level |INFO |The log level, including:<br><br><br>* DEBUG: debug logs<br><br>* INFO: normal logs<br><br>* WARN: warning logs<br><br>* ERROR: error logs |
|logging.message |division zero |The information related to the data transformation task.<br><br><br>* If logging.level is INFO, this field is empty.<br><br>* If logging.level is ERROR, the field value is an error message. Examples:<br><br>   * `invalid literal for int() with base 10: 'ss'`: Fail to convert the string ss to a decimal number. Handle such non\-number fields to be converted in a special way.<br><br>   * `division zero`: The dividend cannot be 0. We recommend that you verify the transformation rule. Verify whether the divisor is 0 before you perform a division operation. |
|process_info.accept |100 |The number of consumed logs during the running process of the transformation task. In other words, the number of log entries read from the source topic. |
|process_info.dropped |0 |The number of filtered logs during the running process of the transformation task. In other words, the number of logs deleted by calling the e_drop function, or the number of logs that fail to be converted by the transformation function. |
|process_info.delivered |100 |The number of output logs during the running process of the transformation task. In other words, the number of logs that are transformed and are ready to be written to the target topic. |
|process_info.failed |0 |The number of logs that fail to be output during the running process of the transformation task. For example, the logs fail to be output as the target topic is deleted. |


<span id=".5pWw5o2u5oqV6YCS6L-Q6KGM5pel5b-X"></span>
## Data shipping logs

Data shipping logs are stored in the ls_shipper\-log topic. TLS periodically records the running information about each data shipping task during the execution process, including the task ID, task status, shipping quantity, and traffic.


|Field |Example |Description |
|---|---|---|
|LogCount |10 |The number of log entries processed by the shipping task. |
|LogStartTime |1678781706 |The timestamp of when the first log entry is processed by the shipping task. |
|LogEndTime |1678781706 |The timestamp of when the last log entry is processed by the shipping task. |
|ProcessSpeed |1000 |The shipping rate of the shipping task. Unit: bytes/s. |
|SendStartTime |1678781706 |The start timestamp of the shipping task. |
|SendEndTime |1678781706 |The end timestamp of the shipping task. |
|ShardId |0 |The topic shard processed by the shipping task. |
|ShipperId |411\-xxx |The shipping configuration ID of the shipping task. |
|TaskId |task\-xxx |The ID of the shipping task. |
|TopicId |b67\-xxx |The topic ID of the shipping task. |
|TopicName |testtopic |The topic name of the shipping task. |
|WriteTraffic |1000 |The write traffic generated by the shipping task. Unit: bytes. |
|ReadTraffic |1000 |The read traffic generated by the shipping task. Unit: bytes. |
|Message |Task shipper success. |The response message of the shipping task. If the task fails to be executed, the error cause is recorded. The response includes:<br><br><br>* StatusCode: the status code. If the code is 1, the task is executed. Otherwise, the task fails.<br><br>* ErrorCode: the error code that indicates the failure cause type.<br><br>* ErrorMessage: the error message that indicates the failure details. Common response messages are as follows:<br><br>   * `Task shipper success`: The task is executed.<br><br>   * `No log data`: The task is executed, but no logs are to be shipped.<br><br>   * `Shipper tos bucket not exist`: The task fails as the specified TOS bucket in the shipping configuration does not exist.<br><br>   * `Shipper Task is cancelled`: The task fails as the shipping task was canceled. |
|Status |Success |The execution result of the shipping task, including:<br><br><br>* Success: The task is executed, and the logs entries are shipped.<br><br>* Failed: The task fails. View the Message field for the failure details. |


<span id=".5raI6LS557uE5bu26L-f5pel5b-X"></span>
## Consumer group lag logs

Consumer group lag logs are stored in the tls_consumergroup\-log topic. TLS records a consumption lag of each consumer group to service logs every two minutes. The information includes the consumer group ID, topic ID, shard ID, and lag duration.


|Field |Example |Description |
|---|---|---|
|ConsumerGroupName |test |The name of the consumer group. |
|ProjectId |xxx |The ID of the project to which the consumer group belongs. |
|TopicId |xxx |The topic ID corresponding to the lag information. |
|ShardId |0 |The shard ID corresponding to the lag information. |
|FallBehindSecond |10 |The number of consumption lag seconds of the current consumer group in the current shard. In other words, the timestamp difference between the latest consumed data and the actual latest data in the current shard. |


<span id=".5a6a5pe2LXNxbC3ov5DooYzml6Xlv5c="></span>
## Scheduled SQL logs

Scheduled SQL logs are stored in the tls_schedule\-sql\-log topic. Scheduled SQL logs record the execution details of each instance of a scheduled SQL task. The information includes the scheduled SQL task ID, instance ID, and scheduling time.


|Field |Example |Description |
|---|---|---|
|task_id |0c554a3a\-a307\-43ec\-857a\-3743f8a0\*\*\*\* |The ID of the scheduled SQL task. |
|process_id |0c554a3a\-a307\-43ec\-857a\-3743f8a0\*\*\*\* |The instance ID of the scheduled SQL task. |
|task_start_time |1692180957000 |The start time of the task in millisecond\-level timestamp format. |
|task_end_time |1692181022000 |The end time of the task in millisecond\-level timestamp format. |
|task_running_time |65 |The task execution duration. Unit: milliseconds. |
|process_time |1692180883 |The scheduled time for the instance in second\-level timestamp format. |
|process_start_time |1692180780 |The scheduling start time in second\-level timestamp format. |
|process_end_time |1692180840 |The scheduling end time in second\-level timestamp format. |
|process_log_nums |1 |The number of processed logs. |
|process_result | |The instance scheduling result, where:<br><br><br>* status: the scheduling result, including:<br><br>   * success: The scheduling is successful.<br><br>   * error: The scheduling fails.<br><br>* message: the message that describes the status details.<br><br>   * If the instance status is `error`, an error message is returned. For example, `Dest topic xxx doesn't exist` indicates that the target topic does not exist.<br><br>   * If the instance status is `success` , `success` is returned. |


<span id="275238d1"></span>
## Alarm policy execution logs

Alarm policy execution logs are stored in the tls_alarm\-log topic. After an alarm policy takes effect, TLS records the execution information about alarm monitoring, such as the execution time and result, and prints the information to service logs.


|Field |Example |Description |
|---|---|---|
|AccountId |200000\*\*\*\* |The BytePlus account ID. |
|ProjectId |a2026e02\-91d8\-460e\-887f\-19db4da9\*\*\*\* |The project ID. |
|ProjectName |tls_service\-project |Name of the project. |
|AlarmName |rewrwer\-copy |The alarm name. |
|AlarmId |1482fce9\-6655\-4aa2\-bf6b\-9a1d4e20\*\*\*\* |The alarm policy ID. |
|TopicIds |ebee41c6\-ba2f\-4dba\-84be\-b310ce4c\*\*\*\* |The list of topic IDs. |
|TopicNames |tls_etl\-log |The list of topic names. |
|HappenThreshold |$1.count\>=100 |The trigger threshold configured in the alarm policy. |
|AlarmFrequency |30 |The alarm frequency. |
|ReachTrigger |FALSE |Whether to trigger an alarm. |
|Notify |NotSend |The execution result.<br><br><br>* NotSend: not sent<br><br>* SendFailed: send failure<br><br>* PartialSuccess: partly sent<br><br>* AllSuccess: all sent |
|NotifyGroup |[{"NotifyGroupId":"87527591\-06b2\-4e40\-bcee\-c92416ba\*\*\*\*","Name":"yyj\-tsy\-001"}] |The alarm notification group list.<br><br><br>* NotifyGroupId: the alarm notification group ID.<br><br>* Name: the alarm notification group name. |
|ProcessResult |AlarmConditionEvaluateError |The execution result. Common execution results:<br><br><br>* SendFail: Fail to send alarms.<br><br>* QueryError: An error occurs while executing the analysis statement. Verify the index configuration of the analysis statement and topic.<br><br>* PartialSent: Some alarms are sent successfully. |
|ProcessMsg |Alarm evaluate error: result of '$1.count' does not exist |The execution result details. |
|NotifyType |AlarmRecover |The alarm type. |
|Severity |notice |The alarm severity level. |
|AlarmDuration |0 |The alarm cycle. |
|SmsBillingCount |0 |The number of sent messages that incur fees. |
|AlarmVersion |2 |The alarm version. |
|SmsSuccessCount |0 |The number of successful alarm messages. |
|SmsFailedCount |0 |The number of failed alarm messages. |
|VmsSuccessCount |0 |The number of successful alarm calls. |
|VmsFailedCount |0 |The number of failed alarms calls. |
|EmailSuccessCount |0 |The number of successful alarm emails. |
|EmailFailedCount |0 |The number of failed alarm emails. |
|WebHookSuccessCount |0 |The number of successful WebHook requests. |
|WebHookFailedCount |0 |The number of failed WebHook requests. |
|Env |`{"AlarmStartTime":"","FireResults":"","FireResultsCount":0,"Results":"[{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c****\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf08****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}},{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c5b9f\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf0****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}},{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c****\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf0****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}}]"}` |The common variable values used during the alarm task execution. |
|LogType |Alarm |The log type.<br><br><br>* Alarm: alarm policy execution log<br><br>* Incident: alarm event log |
|QueryUrl |`https://console.byteplus.com/tls/region:tls+cn-chongqing-sdv/project/a2026e02-91d8-460e-887f-19db4da9****/search?codebase64=KiBBTkQgIHRhc2tfaWQ6Ijc5NzVlZmQ3LWU2M2ItNGNkZC1iNTFjLTA2ZDljZjA4N2VmMiIgfCBzZWxlY3Qgc3VtKHByb2Nlc3NfaW5mby5mYWlsZWQpIEFTIGZhaWxlZF9j****==&hideIndexBtn=false&hideShareBtn=false&hideTitle=false&hideTopic=false&time=2023-12-04%2016:22:44%2C2023-12-04%2016:37:44&topicId=ebee41c6-ba2f-4dba-84be-b310ce4****` |The query and analysis page URL of the first alarm query statement. |


<span id="6487bd15"></span>
## Alarm event logs

Alarm event logs are stored in the tls_alarm\-log topic. Every time an alarm policy is triggered, TLS prints an alarm event log entry to record the metadata when the alarm is triggered.


|Field |Example |Description |
|---|---|---|
|AccountId |200000\*\*\*\* |The BytePlus account ID. |
|InstanceId |94285baf\-7568\-48dc\-983f\-26402bb\*\*\*\* |The alarm instance ID. |
|IncidentId |06a80b71\-f578\-4732\-aeab\-f215a7e8\*\*\*\* |The alarm event ID. |
|AlarmAnnotations | |The alarm metadata description. |
|ProjectId |a2026e02\-91d8\-460e\-887f\-19db4da\*\*\*\* |The project ID. |
|ProjectName |tls_service\-project |Name of the project. |
|AlarmName |rewrwer\-copy |The alarm name. |
|AlarmId |1482fce9\-6655\-4aa2\-bf6b\-9a1d4e20\*\*\*\* |The alarm policy ID. |
|Env |`{"AlarmStartTime":"","FireResults":"","FireResultsCount":0,"Results":"[{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c****\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf08****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}},{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c5b9f\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf0****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}},{\"TopicId\":\"ebee41c6-ba2f-4dba-84be-b310ce4c****\",\"TopicName\":\"tls_etl-log\",\"Query\":\"* AND task_id:\\\"7975efd7-e63b-4cdd-b51c-06d9cf0****\\\" \| select sum(process_info.failed) AS failed_count\",\"StartTime\":1701678164,\"EndTime\":1701679064,\"RawResults\":[{\"failed_count\":\"0\"}],\"RawResultsCount\":1,\"FireResult\":{}}]"}` |The common variable values used during the alarm task execution. |
|LogType |Alarm |The log type.<br><br><br>* Alarm: alarm policy execution log<br><br>* Incident: alarm event log |
