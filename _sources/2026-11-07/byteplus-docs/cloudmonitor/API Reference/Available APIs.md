---
title: "Available APIs"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/API-overview"
---

Cloud Monitor provides the following OpenAPI interfaces.

<span id=".5ZGK6K2m6IGU57O757uE"></span>
## Alert contact group


|API name |Feature |
|---|---|
|[UpdateContactGroup](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactGroup) |Update the basic information of the specified contact group. |
|[CreateContactGroup](https://docs.byteplus.com/en/docs/cloudmonitor/CreateContactGroup) |Create an alert contact group. |
|[UpdateContactGroupWithContacts](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactGroupWithContacts) |Modify the members of the specified contact group, including adding and deleting specified members. |
|[ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) |Query the list of contact groups. Fuzzy search by contact group name keyword is supported. |
|[ListContactGroupByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroupByIds) |Query the details of the specified contact group. |
|[DeleteContactGroupByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteContactGroupByIds) |Delete an alert contact group. |


<span id=".5ZGK6K2m6IGU57O75Lq6"></span>
## Alert contact


|API name |Feature |
|---|---|
|[CreateContacts](https://docs.byteplus.com/en/docs/cloudmonitor/CreateContacts) |Create contacts. |
|[UpdateContacts](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContacts) |Update all the attributes of the specified contact, including the name, mobile phone, and email address. |
|[UpdateContactsWithContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactsWithContactGroups) |Add contacts to one or more specified contact groups. |
|[ListContacts](https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts) |Query the list of contacts. Fuzzy search by contact name keywords is supported. |
|[ListContactsByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactsByIds) |Query the details of the specified contact. |
|[DeleteContactsByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteContactsByIds) |Delete contacts. |


<span id=".5ZGK6K2m562W55Wl"></span>
## Alert policy


|API name |Feature |
|---|---|
|[CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) |Create an alert policy. |
|[DeleteRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteRulesByIds) |Delete an alert policy. |
|[UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) |Update an alert policy. |
|[ListRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds) |Query an alert policy by alert policy ID. |
|[ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) |Query alert policies based on specified conditions. |
|[SetStateOfRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds) |Enable or disable an alert policy. |


<span id=".5p-l6K-i5LqR5Lqn5ZOB55uR5o6n5oyH5qCH5oiW5LqL5Lu2"></span>
## Querying cloud product monitor metrics or events


|API name |Feature |
|---|---|
|[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData) |Query the time series data aggregated for the specified metric within the selected time period. |
|[ListEvents](https://docs.byteplus.com/en/docs/cloudmonitor/ListEvents) |Query events that occurred within the specified time period. |
|[GetTopData](https://docs.byteplus.com/en/docs/cloudmonitor/GetTopData) |Query top\-ranked entries for the specified metrics and corresponding data of other metrics under the same dimension |


<span id=".5LqL5Lu26KeE5YiZ"></span>
## Event rule


|API name |Feature |
|---|---|
|[CreateEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateEventRule) |Create an event rule. |
|[DeleteEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteEventRule) |Delete an event rule. |
|[UpdateEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateEventRule) |Update an event rule. |
|[ListEventRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListEventRules) |Query event rules. |
|[EnableEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/EnableEventRule) |Enable an event rule. |
|[DisableEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/DisableEventRule) |Disable an event rule. |


<span id=".5ZGK6K2m5Y6G5Y-y"></span>
## Alert record


|API name |Feature |
|---|---|
|[ListAlertGroup](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertGroup) |Query the alert history of the specified resource. |
|[ListSendAlert](https://docs.byteplus.com/en/docs/cloudmonitor/ListSendAlert) |Query the list of alert notifications sent. |


<span id=".5a-56LGh5YiG57uE"></span>
## Resource Group


|API name |Feature |
|---|---|
|[CreateObjectGroup](https://docs.byteplus.com/en/docs/cloudmonitor/CreateObjectGroup) |Create an object group. |
|[UpdateObjectGroup](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateObjectGroup) |Update an object group. |
|[ListObjectGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListObjectGroups) |Query the list of object groups. |
|[DeleteObjectGroup](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteObjectGroup) |Delete the specified object group. |


<span id=".5ZGK6K2m5Zue6LCD"></span>
## Alert callback


|API name |Feature |
|---|---|
|[CreateWebhook](https://docs.byteplus.com/en/docs/cloudmonitor/CreateWebhook) |Create an alert callback. |
|[ListWebhooksByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooksByIds) |Query alert callbacks by ID. |
|[ListWebhooks](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks) |Query the list of alert callbacks. |
|[UpdateWebhook](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateWebhook) |Update an alert callback. |
|[DeleteWebhooksByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteWebhooksByIds) |Delete an alert callback. |


<span id=".6YCa55-l562W55Wl"></span>
## Notification policy


|API name |Feature |
|---|---|
|[CreateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotification) |Create a notification policy. |
|[DeleteNotificationsByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteNotificationsByIds) |Delete notification policies. |
|[ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) |Query the list of notification policies. |
|[UpdateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateNotification) |Update a notification policy. |


<span id=".5qCH562-566h55CG"></span>
## Tags


|API name |Feature |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/cloudmonitor/TagResources) |Bind tags to resources in batches. |
|[UntagResources](https://docs.byteplus.com/en/docs/cloudmonitor/UntagResources) |Unbind tags from resources in batches. |


<span id=".5bGP6JS9562W55Wl"></span>
## Suppression policy


|API name |Feature |
|---|---|
|[CreateSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/CreateSilencePolicy) |Create a suppression policy. |
|[DeleteSilencePolicyByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteSilencePolicyByIds) |Delete suppression policies. |
|[ListSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/ListSilencePolicy) |Query suppression policies. |
|[UpdateSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateSilencePolicy) |Update a suppression policy. |
|[ModifyStateOfSilencePolicyByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ModifyStateOfSilencePolicyByIds) |Modify the status of suppression policies. |


<span id=".5ZGK6K2m5qih54mI"></span>
## Alert template


|API name |Feature |
|---|---|
|[EnablePresetAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/EnablePresetAlertTemplate) |Enable a preset alert template to create alert policies in batches. |
|[ListPresetAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListPresetAlertTemplates) |Query the list of preset alert templates. |
|[DisablePresetAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/DisablePresetAlertTemplate) |Disable a preset alert template and delete alert policies associated with the preset alert template. |
|[CreateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/CreateAlertTemplate) |Create an alert template. |
|[ListAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertTemplates) |Query alert templates. |
|[UpdateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateAlertTemplate) |Update an alert template. |
|[ApplyObjectGroupsByAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/ApplyObjectGroupsByAlertTemplate) |Associate object groups and notification policies with an alert template. |
|[DeleteAlertTemplatesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteAlertTemplatesByIds) |Delete the specified alert template. |


<span id=".6YCa55-l5qih54mI"></span>
## Notification template


|API name |Feature |
|---|---|
|[CreateNotifyTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotifyTemplate) |Create a notification template. |
|[DeleteNotifyTemplatesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteNotifyTemplatesByIds) |Delete notification templates. |
|[ListDefaultNotifyTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListDefaultNotifyTemplates) |Query the list of default notification templates. |
|[ListNotifyTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifyTemplates) |Query the list of notification templates. |
|[UpdateNotifyTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateNotifyTemplate) |Update a notification template. |


<span id=".6YeH6ZuG5o-S5Lu2"></span>
## Collection add\-ons


|API name |Feature |
|---|---|
|[UpdateO11yAgentECSAutoInstall](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateO11yAgentECSAutoInstall) |Enable or disable automatic installation of the collection add\-on for newly purchased ECS instances. |
|[GetO11yAgentECSAutoInstall](https://docs.byteplus.com/en/docs/cloudmonitor/GetO11yAgentECSAutoInstall) |Query whether automatic installation of the collection add\-on is enabled for newly purchased ECS instances. |
|[CreateO11yAgentECSDeployTask](https://docs.byteplus.com/en/docs/cloudmonitor/CreateO11yAgentECSDeployTask) |Create an installation or upgrade task for the ECS instance collection add\-on. |
|[PerformO11yAgentECSDeployTask](https://docs.byteplus.com/en/docs/cloudmonitor/PerformO11yAgentECSDeployTask) |End the installation or upgrade task of the collection add\-on on an ECS instance. |
|[ListO11yAgentECSInstances](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstances) |Query the collection add\-on list on ECS instances. |
|[ListO11yAgentVpcEndpoints](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentVpcEndpoints) |Obtain the list of endpoints associated with the O11yAgent Service. |
|[UpdateO11yAgentECSProcessConfig](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateO11yAgentECSProcessConfig) |Modify the configuration of monitored processes on ECS instances. |
|[ListO11yAgentECSProcessConfigs](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSProcessConfigs) |Query the list of monitored ECS instance processes. |
|[ListO11yAgentECSInstanceMetadata](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstanceMetadata) |Query metadata of the ECS instance collection add\-on. |


&nbsp;
