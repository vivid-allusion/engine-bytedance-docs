---
title: "Authorizable actions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Authorizable_actions"
---

You can grant the following permissions for a TLS resource in IAM.


|Resource type (Source) |Actions |Description |
|---|---|---|
|Log project (Project)<br><br> |tls:CreateProject |Create a project. |
||tls:ModifyProject |Modify project. |
||tls:DeleteProject |Delete project. |
||tls:DescribeProject |Get project details. |
||tls:DescribeProjects |Get list of projects. |
|Log topic (Topic) |tls:CreateTopic |Create a log topic. |
||tls:DeleteTopic |Delete log topic. |
||tls:ModifyTopic |Edit log topic. |
||tls:DescribeTopic |Get topic details. |
||tls:DescribeTopics |Get topic list. |
||tls:DescribeShards |Get the shard list for the topic. |
||tls:ManualShardSplit |Manually split the specified shard. |
||tls:PutLogs |Upload logs to TLS. |
||tls:DescribeCursor |Obtain the log download cursor. |
||tls:ConsumeLogs |Consume logs in the topic. |
||tls:SearchLogs |Query and analyze logs in the topic. |
||tls:DescribeLogContext |View the context information of the specified log. |
||tls:DescribeHistogram |Query logs and view the distribution of logs that meet the conditions over time. |
||tls:DescribeHistogramV1 |Query logs and view the distribution of logs that meet the conditions over time. |
||tls:WebTracks |Upload logs in batches to the log topic. |
||tls:CreateDownloadTask |Create log download task. |
||tls:DescribeDownloadTasks |Get the list of log download tasks. |
||tls:DescribeDownloadUrl |Obtain the download link for the corresponding download task. |
||tls:CancelDownloadTask |Cancel the log download task. |
||tls:OpenKafkaConsumer |Enable Kafka protocol consumption for the log topic. |
||tls:CloseKafkaConsumer |Disable Kafka protocol consumption for the log topic. |
||tls:DescribeKafkaConsumer |View the Kafka consumer status for the log topic. |
||tls:CreateIndex |Create index. |
||tls:DeleteIndex |Delete index. |
||tls:ModifyIndex |Edit index. |
||tls:DescribeIndex |Obtain index configuration information. |
||tls:CreateSavedSearch |Create quick analysis. |
||tls:DeleteSavedSearch |Delete quick analysis. |
||tls:DescribeSavedSearch |Query quick analysis. |
||tls:DescribeSavedSearches |Query quick analysis list. |
|Collection configuration (Rule) |tls:CreateRule |Create collection configuration. |
||tls:DeleteRule |Delete collection configuration. |
||tls:ModifyRule |Update collection configuration. |
||tls:DescribeRule |Obtain collection configuration. |
||tls:DescribeRules |Obtain collection configuration list. |
||tls:ApplyRuleToHostGroups |Apply the collection configuration to host groups. |
||tls:DeleteRuleFromHostGroups |Unbind the collection configuration from the host group. |
|Host group (HostGroup)<br><br> |tls:CreateHostGroup |Create a host group |
||tls:DeleteHostGroup |Delete host group. |
||tls:ModifyHostGroup |Update host group. |
||tls:DescribeHostGroup |Get detailed information about the host group. |
||tls:DescribeHostGroups |Get list of all host groups. |
||tls:DescribeHosts |Get list of machines in the host group. |
||tls:DeleteHost |Delete a machine with the specified IP address in the host group. |
||tls:DescribeHostGroupRules |Get list of collection configurations applied to the host group. |
||tls:ModifyHostGroupsAutoUpdate |Batch modify the LogCollector auto\-upgrade configuration for host groups. |
||tls:DeleteAbnormalHosts |Clear all hosts with heartbeat exceptions in the host group with one click. |
|Notification group (AlarmNotifyGroup)<br><br> |tls:CreateAlarmNotifyGroup |Create alarm contact group. |
||tls:DeleteAlarmNotifyGroup |Delete an alert contact group. |
||tls:DescribeAlarmNotifyGroups |Get the list of alert contact groups. |
||tls:ModifyAlarmNotifyGroup |Edit notification group. |
|Alarm policy (Alarm)<br><br> |tls:CreateAlarm |Create alarm policy. |
||tls:DeleteAlarm |Delete alarm policy. |
||tls:DescribeAlarms |Retrieve list of alarm policies. |
||tls:ModifyAlarm |Edit alarm policy. |
||tls:DescribeAlarmLogs |View alarm history. |
||tls:ManualTriggerAlarm |Test alarm policy. |
||tls:DescribeManualTriggerAlarmTask |View alarm test tasks. |
||tls:ModifyAlarmIncident |Edit login\-free page configuration. |
||tls:DescribeAlarmIncident |View login\-free page configuration. |
||tls:DisableAlarm |Close alarm policy. |
||tls:EnableAlarm |Enable alarm policy. |
|Alarm Webhook integration configuration (WebhookIntegration)<br><br> |tls:CreateAlarmWebhookIntegration |Create alarm Webhook integration configuration. |
||tls:DeleteAlarmWebhookIntegration |Delete alarm Webhook integration configuration. |
||tls:DescribeAlarmWebhookIntegrations |Get list of alarm Webhook integration configurations. |
||tls:ModifyAlarmWebhookIntegration |Modify the alarm Webhook integration configuration. |
|Alarm content templates (ContentTemplates) |tls:CreateAlarmContentTemplates |Create alarm content template. |
||tls:ModifyAlarmContentTemplates |Modify alarm content template. |
||tls:DeleteAlarmContentTemplate |Delete alarm content template. |
||tls:DescribeAlarmContentTemplates |Retrieve the list of alarm content template configurations. |
|Scheduled SQL analysis task (ScheduleSqlTask)<br><br> |tls:CreateScheduleSqlTask |Create scheduled SQL analysis task. |
||tls:ModifyScheduleSqlTask |Edit scheduled SQL analysis task. |
||tls:DeleteScheduleSqlTask |Delete scheduled SQL analysis task. |
||tls:DescribeScheduleSqlTask |Get details of the scheduled SQL analysis task. |
||tls:DescribeScheduleSqlTasks |View the list of scheduled SQL analysis tasks. |
|Consumer Group (ConsumerGroup)<br><br> |tls:CreateConsumerGroup |Create TLS consumer group. |
||tls:DeleteConsumerGroup |Delete TLS consumer group. |
||tls:DescribeConsumerGroups |Retrieve the list of consumer groups in TLS. |
||tls:ModifyConsumerGroup |Update the configuration of a TLS consumer group. |
||tls:ConsumerHeartbeat |Send the heartbeat information of a consumer in a consumer group to TLS. |
||tls:DescribeCheckPoint |View the current consumer offset for a consumer group on a shard. |
||tls:ModifyCheckPoint |Reset the consumer offset for a specified shard in a consumer group. |
||tls:ResetCheckPoint |Reset all consumption checkpoints for the consumer group. |
|Tag |tls:AddTagsToResource |Batch bind tags to projects or topics. |
||tls:RemoveTagsFromResource |Batch unbind tags from projects or topics. |
|Dashboard |tls:CreateDashboard |Create dashboard. |
||tls:DeleteDashboard |Delete dashboard. |
||tls:ModifyDashboard |Edit dashboard information. |
||tls:DescribeDashboard |View dashboard information. |
||tls:DescribeDashboards |View dashboard list. |
|Password\-free link (DashboardShares) |tls:CreateDashboardShare |Create password\-free link. |
||tls:DeleteDashboardShare |Delete password\-free link. |
||tls:ModifyDashboardShare |Modify password\-free link. |
||tls:DescribeDashboardShares |View the list of password\-free links. |
||tls:ModifyDashboardShareAvailable |Modify the availability status of password\-free links. |
|Import Task (ImportTask) |tls:CreateImportTask |Create data import task. |
||tls:DeleteImportTask |Delete data import task. |
||tls:ModifyImportTask |Edit data import task. |
||tls:DescribeImportTask |View data import task details. |
||tls:DescribeImportTasks |View data import task list. |
|Processing task (ETL) |tls:CreateETLTask |Create data transformation task. |
||tls:DeleteETLTask |Delete data transformation task. |
||tls:DescribeETLFunctions |Get data transformation functions. |
||tls:DescribeETLLogDataInfo |Get data transformation progress. |
||tls:DescribeETLPreviewDataInfo |Get data transformation preview information. |
||tls:DescribeETLTask |Get details of the data transformation task. |
||tls:DescribeETLTasks |Get the list of data transformation tasks. |
||tls:ModifyETLTask |Edit the data transformation task. |
||tls:ModifyETLTaskStatus |Edit the status of the data transformation task. |
|Processors (Processor) |tls:CreateProcessor |Create a processor, including write processors and consumer processors. |
||tls:ModifyProcessor |Modify a processor, including write processors and consumer processors. |
||tls:DeleteProcessor |Delete a processor, including write processors and consumer processors. |
|Delivery configuration (Shipper)<br><br> |tls:CreateShipper |Create log shipping configuration. |
||tls:DeleteShipper |Delete log shipping configuration. |
||tls:DescribeShipper |Retrieve log shipping configuration. |
||tls:DescribeShipperTasks |View log shipping task list. |
||tls:DescribeShippers |View log shipping configuration list. |
||tls:ModifyShipper |Modify log shipping configuration. |
||tls:RetryShipperTask |Retry log shipping task. |
|Trace instance (TraceInstance) |tls:CreateTraceInstance |Create Trace instance. |
||tls:ModifyTraceInstance |Modify Trace instance. |
||tls:DeleteTraceInstance |Delete Trace instance. |
||tls:DescribeTraceInstances |View trace instance list. |
||tls:DescribeTraceInstance |View trace instance details. |
|CloudMonitor |tls:TlsPlatformReconciliation |TLS platform reconciliation. |
||tls:DescribeCloudMonitorDimensions |List dimensions monitored by CloudMonitor services. |
||tls:DescribeCloudMonitorInstances |List monitoring instances for cloud monitoring services. |
|Accounts (Account) |tls:VolcActiveTlsSvc |Activate TLS for a BytePlus IAM account. |
||tls:GetAccountStatus |Check whether the account has activated TLS service. |
||tls:ActiveTlsSvc |Activate TLS. |
||tls:ListRegionsReq |List regions that provide TLS. |
|Log applications (App) |tls:CreateApp |Create a log application. |
||tls:CreateTosLensTask |Create a data pivot task for the CloudLens for TOS log application. |
||tls:ModifyApp |Modify a log application. |
||tls:ModifyCloudLensInstanceStatus |Enable or disable log observation. |
||tls:ModifyTosLensTask |Modify a data pivot task for the CloudLens for TOS log application. |
||tls:DescribeApp |Query details of a log application. |
||tls:DescribeApps |Query a list of log applications. |
||tls:DescribeCloudLensInstances |Query a list of access management instances. |
||tls:DescribeCloudLensInstanceStatus |Query the log status of an instance. |
||tls:DescribeCloudLensTargetTopics |Query target storage topics. |
||tls:DescribeCloudLensOverview |Query the access management overview. |
||tls:DescribeTosLensTasks |Query a list of data pivot tasks for the CloudLens for TOS log application. |
||tls:DescribeTosLensTask |Query details of a data pivot task for the CloudLens for TOS log application. |
||tls:DeleteApp |Delete log applications. |
||tls:DeleteTosLensTask |Delete data pivot tasks of the CloudLens for TOS log application. |
