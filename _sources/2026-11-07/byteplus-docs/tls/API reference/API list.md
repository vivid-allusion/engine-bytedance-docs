---
title: "API list"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Operations"
---

This topic provides a detailed list of all TLS APIs.

<span id=".5pel5b-X6aG555uu566h55CG"></span>
## Log project management


|API |Description |
|---|---|
|[CreateProject](https://docs.byteplus.com/docs/tls/api-createproject) |Call the CreateProject API to create a log project. |
|[DeleteProject](https://docs.byteplus.com/docs/tls/api-deleteproject) |Call the DeleteProject API to delete a log project. |
|[ModifyProject](https://docs.byteplus.com/docs/tls/api-modifyproject) |Call the ModifyProject API to modify a log project. |
|[DescribeProject](https://docs.byteplus.com/docs/tls/api-describeproject) |Call the DescribeProject API to query information about a specified log project. |
|[DescribeProjects](https://docs.byteplus.com/docs/tls/api-describeprojects) |Call the DescribeProjects API to view information about all log projects. |


<span id=".5pel5b-X5Li76aKY566h55CG"></span>
## Log topic management


|API |Description |
|---|---|
|[CreateTopic](https://docs.byteplus.com/docs/tls/api-createtopic) |Call the CreateTopic API to create a log topic. |
|[DeleteTopic](https://docs.byteplus.com/docs/tls/api-deletetopic) |Call the DeleteTopic API to delete a log topic. |
|[ModifyTopic](https://docs.byteplus.com/docs/tls/api-modifytopic) |Call the ModifyTopic API to modify log topic information. |
|[DescribeTopic](https://docs.byteplus.com/docs/tls/api-describetopic) |Call the DescribeTopic API to obtain basic information about a specified log topic. |
|[DescribeTopics](https://docs.byteplus.com/docs/tls/api-describetopics) |Call the DescribeTopics API to obtain information about all log topics in a log project. |


<span id=".5YiG5Yy6566h55CG"></span>
## Shard management


|API |Description |
|---|---|
|[DescribeShards](https://docs.byteplus.com/docs/tls/api-describeshards) |Call the DescribeShards API to obtain the shard list of a log topic. |
|[ManualShardSplit](https://docs.byteplus.com/docs/tls/api-manualshardsplit) |Call the ManualShardSplit API to manually split a specified shard. |


<span id=".57Si5byV566h55CG"></span>
## Index management


|API |Description |
|---|---|
|[CreateIndex](https://docs.byteplus.com/docs/tls/api-createindex) |Call the CreateIndex API to create an index. |
|[DeleteIndex](https://docs.byteplus.com/docs/tls/api-deleteindex) |Call the DeleteIndex API to delete an index configuration. |
|[ModifyIndex](https://docs.byteplus.com/docs/tls/api-modifyindex) |Call the ModifyIndex API to modify an index configuration. |
|[DescribeIndex](https://docs.byteplus.com/docs/tls/api-describeindex) |Call the DescribeIndex API to obtain index configuration information. |


<span id=".5pel5b-X566h55CG"></span>
## Log management


|API |Description |
|---|---|
|[PutLogs](https://docs.byteplus.com/docs/tls/api-putlogs) |Call the PutLogs API to upload logs to a specified log topic. |
|[DescribeCursor](https://docs.byteplus.com/docs/tls/api-describecursor) |Call the DescribeCursor API to obtain the log download cursor. |
|[ConsumeLogs](https://docs.byteplus.com/docs/tls/api-consumelogs) |Call the ConsumeLogs API to consume logs. |
|[SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) |Call the SearchLogs API to search logs. |
|[DescribeLogContext](https://docs.byteplus.com/docs/tls/api-describelogcontext) |Call the DescribeLogContext API to view the context information of a specified log. |
|DescribeHistogram(deprecated) |Call the DescribeHistogram API to search logs and view the time distribution of log data that meets the conditions. |
|[DescribeHistogramV1](https://docs.byteplus.com/en/docs/tls/DescribeHistogramV1) |Call the DescribeHistogramV1 API to search logs and view the time distribution of log data that meets the conditions. |
|[WebTracks](https://docs.byteplus.com/docs/tls/api-webtracks) |Call the WebTracks API to batch upload logs to a specified log topic. |
|[CreateDownloadTask](https://docs.byteplus.com/docs/tls/api-createdownloadtask) |Call the CreateDownloadTask API to create a log download task. |
|[DescribeDownloadTasks](https://docs.byteplus.com/docs/tls/api-describedownloadtasks) |Call the DescribeDownloadTasks API to obtain the list of log download tasks in a specified log topic. |
|[DescribeDownloadUrl](https://docs.byteplus.com/docs/tls/api-describedownloadurl) |Call the DescribeDownloadUrl API to obtain the log download link for a specified task. |
|[CancelDownloadTask](https://docs.byteplus.com/en/docs/tls/api-canceldownloadtask) |Call the CancelDownloadTask API to cancel a log download task. |


&nbsp;

<span id=".5py65Zmo57uE566h55CG"></span>
## Host group management


|API |Description |
|---|---|
|[CreateHostGroup](https://docs.byteplus.com/docs/tls/api-createhostgroup) |Call the CreateHostGroup API to create a host group. |
|[DeleteHostGroup](https://docs.byteplus.com/docs/tls/api-deletehostgroup) |Call the DeleteHostGroup API to delete a host group. |
|[ModifyHostGroup](https://docs.byteplus.com/docs/tls/api-modifyhostgroup) |Call the ModifyHostGroup API to modify a host group. |
|DescribeHostGroups(Deprecated) |Call the DescribeHostGroups API to retrieve all host groups. |
|DescribeHostGroup(Deprecated) |Call the DescribeHostGroup API to view information about a specified host group. |
|[DescribeHostGroupsV2](https://docs.byteplus.com/en/docs/tls/DescribeHostGroupsV2) |Call the DescribeHostGroupsV2 API to retrieve information about all host groups, excluding host group heartbeat information and the list of associated collection rules. |
|[DescribeHostGroupV2](https://docs.byteplus.com/en/docs/tls/DescribeHostGroupV2) |Call the DescribeHostGroupV2 API to retrieve information about a host group, excluding host group heartbeat information and the list of associated collection rules. |
|[DescribeHosts](https://docs.byteplus.com/en/docs/tls/api-describehosts) |Call the DescribeHosts API to retrieve all hosts. |
|[DeleteHost](https://docs.byteplus.com/docs/tls/api-deletehost) |Call the DeleteHost API to delete a host with a specified IP address from a host group. |
|[DescribeHostGroupRules](https://docs.byteplus.com/docs/tls/api-describehostgrouprules) |Call the DescribeHostGroupRules API to retrieve the list of collection configurations already applied to a host group. |
|[ModifyHostGroupsAutoUpdate](https://docs.byteplus.com/docs/tls/api-modifyhostgroupsautoupdate) |Call the ModifyHostGroupsAutoUpdate API to batch modify the LogCollector auto\-upgrade configuration for host groups. |
|[DeleteAbnormalHosts](https://docs.byteplus.com/en/docs/tls/api-deleteabnormalhosts) |Call the DeleteHost API to delete a host with a specified IP address from a host group. |


<span id=".6YeH6ZuG6YWN572u566h55CG"></span>
## Collection configuration management


|API |Description |
|---|---|
|[CreateRule](https://docs.byteplus.com/docs/tls/api-createrule) |Call the CreateRule API to create a collection configuration. |
|[DeleteRule](https://docs.byteplus.com/docs/tls/api-deleterule) |Call the DeleteRule API to delete a collection configuration. |
|[ModifyRule](https://docs.byteplus.com/docs/tls/api-modifyrule) |Call the ModifyRule API to modify a collection configuration. |
|DescribeRule(Deprecated) |Call the DescribeRule API to view information about a specified collection configuration. |
|[DescribeRuleV2](https://docs.byteplus.com/en/docs/tls/DescribeRuleV2) |Call the DescribeRuleV2 API to query details of a collection rule, excluding host group information. |
|[DescribeRules](https://docs.byteplus.com/docs/tls/api-describerules) |Call the DescribeRules API to view the list of collection configurations in a specified project. |
|[ApplyRuleToHostGroups](https://docs.byteplus.com/docs/tls/api-applyruletohostgroups) |Call the ApplyRuleToHostGroups API to bind a collection configuration to a list of host groups. |
|[DeleteRuleFromHostGroups](https://docs.byteplus.com/docs/tls/api-deleterulefromhostgroups) |Call the DeleteRuleFromHostGroups API to unbind a collection configuration from a list of host groups. |
|[DescribeBoundHostGroups](https://docs.byteplus.com/en/docs/tls/DescribeBoundHostGroups) |Call the DescribeBoundHostGroups API to query the list of host groups bound to a collection rule. |


<span id="cc5bb7fc"></span>
## Scheduled SQL analysis


|API |Description |
|---|---|
|[CreateScheduleSqlTask](https://docs.byteplus.com/docs/tls/api-createschedulesqltask) |Call the CreateScheduleSqlTask API to create a scheduled SQL analysis task. |
|[ModifyScheduleSqlTask](https://docs.byteplus.com/docs/tls/api-modifyschedulesqltask) |Call the ModifyScheduleSqlTask API to modify a scheduled SQL analysis task. |
|[DeleteScheduleSqlTask](https://docs.byteplus.com/docs/tls/api-deleteschedulesqltask) |Call the DeleteScheduleSqlTask API to delete a scheduled SQL analysis task. |
|[DescribeScheduleSqlTask](https://docs.byteplus.com/docs/tls/api-describeschedulesqltask) |Call the DescribeScheduleSqlTask API to view details of a specified scheduled SQL analysis task. |
|[DescribeScheduleSqlTasks](https://docs.byteplus.com/docs/tls/api-describeschedulesqltasks) |Call the DescribeScheduleSqlTasks API to view details of all scheduled SQL analysis tasks in a specified region. |


<span id="0bde13c7"></span>
## Data import


|API |Description |
|---|---|
|[CreateImportTask](https://docs.byteplus.com/en/docs/tls/CreateImportTask) |Call the CreateImportTask API to create a data import task. |
|[DeleteImportTask](https://docs.byteplus.com/en/docs/tls/DeleteImportTask) |Call the DeleteImportTask API to delete a specified data import task. |
|[ModifyImportTask](https://docs.byteplus.com/en/docs/tls/ModifyImportTask) |Call the ModifyImportTask API to modify a specified data import task. |
|[DescribeImportTask](https://docs.byteplus.com/en/docs/tls/DescribeImportTask) |Call the DescribeImportTask API to obtain information about a data import task. |
|[DescribeImportTasks](https://docs.byteplus.com/en/docs/tls/DescribeImportTasks) |Call the DescribeImportTasks API to obtain the list of data import tasks. |


<span id="04c2f990"></span>
## Data transformation


|API |Description |
|---|---|
|[CreateETLTask](https://docs.byteplus.com/en/docs/tls/CreateETLTask) |Call the CreateETLTask API to create an ETL task. |
|[DeleteETLTask](https://docs.byteplus.com/en/docs/tls/DeleteETLTask) |Call the DeleteETLTask API to delete an ETL task. |
|[ModifyETLTask](https://docs.byteplus.com/en/docs/tls/ModifyETLTask) |Call the ModifyETLTask API to modify a specified ETL task. |
|[DescribeETLTask](https://docs.byteplus.com/en/docs/tls/DescribeETLTask) |Call the DescribeETLTask API to obtain detailed information about a specified ETL task. |
|[DescribeETLTasks](https://docs.byteplus.com/en/docs/tls/DescribeETLTasks) |Call the DescribeETLTasks API to obtain the list of ETL tasks. |
|[ModifyETLTaskStatus](https://docs.byteplus.com/en/docs/tls/ModifyETLTaskStatus) |Call the ModifyETLTaskStatus API to modify the status of an ETL task. |


<span id="e5f815c2"></span>
## Log shipping


|API |Description |
|---|---|
|[CreateShipper](https://docs.byteplus.com/en/docs/tls/CreateShipper) |Call the CreateShipper API to create a delivery configuration. |
|[DeleteShipper](https://docs.byteplus.com/en/docs/tls/DeleteShipper) |Call the DeleteShipper API to delete a specified delivery configuration. |
|[ModifyShipper](https://docs.byteplus.com/en/docs/tls/ModifyShipper) |Call the ModifyShipper API to modify a specified delivery configuration. |
|[DescribeShipper](https://docs.byteplus.com/en/docs/tls/DescribeShipper) |Call the DescribeShipper API to obtain detailed information about a delivery configuration. |
|[DescribeShippers](https://docs.byteplus.com/en/docs/tls/DescribeShippers) |Call the DescribeShippers API to obtain the list of delivery configurations. |


<span id="7ba84c65"></span>
## Data backflow


|API |Description |
|---|---|
|[CreateLogBackFlowTask](https://docs.byteplus.com/en/docs/tls/CreateLogBackFlowTask) |Call the CreateLogBackFlowTask API to create a log re\-ingestion task. |
|[DeleteLogBackFlowTask](https://docs.byteplus.com/en/docs/tls/DeleteLogBackFlowTask) |Call the DeleteLogBackFlowTask API to delete a log re\-ingestion task. |
|[DescribeLogBackFlowTasks](https://docs.byteplus.com/en/docs/tls/DescribeLogBackFlowTasks) |Call the DescribeLogBackFlowTasks API to query the list of log re\-ingestion tasks. |
|[ModifyLogBackFlowTask](https://docs.byteplus.com/en/docs/tls/ModifyLogBackFlowTask) |Call the ModifyLogBackFlowTask API to modify a log re\-ingestion task. |


<span id=".5ZGK6K2m566h55CG"></span>
## Alert management


|API |Description |
|---|---|
|[CreateAlarmNotifyGroup](https://docs.byteplus.com/docs/6470/112220) |Call the CreateAlarmNotifyGroup API to create an alarm group. |
|[DeleteAlarmNotifyGroup](https://docs.byteplus.com/docs/6470/112221) |Call the DeleteAlarmNotifyGroup API to delete an alarm group. |
|[ModifyAlarmNotifyGroup](https://docs.byteplus.com/docs/6470/112222) |Call the ModifyAlarmNotifyGroup API to modify an alarm group. |
|[DescribeAlarmNotifyGroups](https://docs.byteplus.com/docs/6470/112223) |Call the DescribeAlarmNotifyGroups API to obtain the list of alarm groups. |
|[CreateAlarm](https://docs.byteplus.com/docs/6470/112216) |Call the CreateAlarm API to create an alarm policy. |
|[DeleteAlarm](https://docs.byteplus.com/docs/6470/112217) |Call the DeleteAlarm API to delete an alarm policy. |
|[ModifyAlarm](https://docs.byteplus.com/docs/6470/112218) |Call the ModifyAlarm API to modify an alarm policy. |
|[DescribeAlarms](https://docs.byteplus.com/docs/6470/112219) |Call the DescribeAlarms API to view the list of alarm policies. |


&nbsp;

<span id=".5raI6LS557uE566h55CG"></span>
## Consumer group management


|API |Description |
|---|---|
|[CreateConsumerGroup](https://docs.byteplus.com/docs/tls/api-createconsumergroup) |Call the CreateConsumerGroup API to create a TLS consumer group (ConsumerGroup). |
|[DeleteConsumerGroup](https://docs.byteplus.com/docs/tls/api-deleteconsumergroup) |Call the DeleteConsumerGroup API to delete a TLS consumer group. |
|[DescribeConsumerGroups](https://docs.byteplus.com/docs/tls/api-describeconsumergroups) |Call the DescribeConsumerGroups API to obtain information about all consumer groups in a project. |
|[ModifyConsumerGroup](https://docs.byteplus.com/docs/tls/api-modifyconsumergroup) |Call the ModifyConsumerGroup API to modify the configuration of a TLS consumer group. |
|[ConsumerHeartbeat](https://docs.byteplus.com/docs/tls/api-consumerheartbeat) |Call the ConsumerHeartbeat API to send heartbeat information for a consumer in a consumer group to TLS. |
|[DescribeCheckPoint](https://docs.byteplus.com/docs/tls/api-describecheckpoint) |Call the DescribeCheckPoint API to view the current consumer checkpoint of the specified consumer group on the specified log shard. |
|[ModifyCheckPoint](https://docs.byteplus.com/docs/tls/api-modifycheckpoint) |Call the ModifyCheckPoint API to reset the consumer checkpoint of the specified consumer group for the specified shard. |
|[ResetCheckPoint](https://docs.byteplus.com/docs/tls/api-resetcheckpoint) |Call the ResetCheckPoint API to reset all consumer checkpoints for the specified consumer group. |


<span id=".a2Fma2Et5Y2P6K6u5raI6LS5"></span>
## Kafka protocol consumption


|API |Description |
|---|---|
|[OpenKafkaConsumer](https://docs.byteplus.com/docs/tls/api-openkafkaconsumer) |Call the OpenKafkaConsumer API to enable Kafka protocol consumption for the specified log topic. |
|[CloseKafkaConsumer](https://docs.byteplus.com/docs/tls/api-closekafkaconsumer) |Call the CloseKafkaConsumer API to disable Kafka protocol consumption for the specified log topic. |
|[DescribeKafkaConsumer](https://docs.byteplus.com/docs/tls/api-describekafkaconsumer) |Call the DescribeKafkaConsumer API to view the Kafka consumption status of the specified log topic. |


<span id=".5qCH562-566h55CG"></span>
## Tag management


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/docs/tls/api-dddtagstoresource) |Call the AddTagsToResource API to batch bind tags to the specified project or log topic. |
|[RemoveTagsFromResource](https://docs.byteplus.com/docs/tls/api-removetagsfromresource) |Call the RemoveTagsFromResource API to batch unbind tags from the specified project or log topic. |
|[UntagResources](https://docs.byteplus.com/en/docs/tls/UntagResources) |Call the UntagResources API to batch remove resource tags. |
|[TagResources](https://docs.byteplus.com/en/docs/tls/TagResources) |Call the TagResources API to batch bind tags to resources. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/tls/ListTagsForResources) |Call the ListTagsForResources API to query all tags bound to resources. |


<span id="d7f2f5bb"></span>
## Trace storage


|API |Description |
|---|---|
|[CreateTraceInstance](https://docs.byteplus.com/en/docs/tls/CreateTraceInstance) |Call the CreateTraceInstance API to create a Trace instance. |
|[ModifyTraceInstance](https://docs.byteplus.com/en/docs/tls/ModifyTraceInstance) |Call the ModifyTraceInstance API to modify Trace instance information. |
|[DeleteTraceInstance](https://docs.byteplus.com/en/docs/tls/DeleteTraceInstance) |Call the DeleteTraceInstance API to delete a Trace instance. |
|[DescribeTraceInstances](https://docs.byteplus.com/en/docs/tls/DescribeTraceInstances) |Call the DescribeTraceInstances API to obtain the list of Trace instances. |
|[DescribeTraceInstance](https://docs.byteplus.com/en/docs/tls/DescribeTraceInstance) |Call the DescribeTraceInstance API to obtain Trace instance information. |
|[DescribeTrace](https://docs.byteplus.com/en/docs/tls/DescribeTrace) |Call the DescribeTrace API to query the list of Spans under the Trace by specifying the Trace instance ID and TraceID. |
|[SearchTraces](https://docs.byteplus.com/en/docs/tls/SearchTraces) |Call the SearchTraces API to query the Trace details list based on specific conditions. |


<span id="db013580"></span>
## Account management


|API |Description |
|---|---|
|[ActiveTlsAccount](https://docs.byteplus.com/en/docs/tls/ActiveTIsAccount) |Call the ActiveTlsAccount API to activate TLS. |
|[GetAccountStatus](https://docs.byteplus.com/en/docs/tls/GetAccountStatus) |Call the GetAccountStatus API to check whether TLS is activated. |
