---
title: "API release notes"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/API-Release-History"
---

This topic records the change logs of Cloud Monitor OpenAPI interfaces.

<span id=".XzIwMjUt5bm0LTExLeaciA=="></span>
## November 2025


|API |Release date |Change |Associate feature |
|---|---|---|---|
|<span data-api-tag="add\|4GKl44">新增</span> [UpdateO11yAgentECSAutoInstall](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateO11yAgentECSAutoInstall) |2025\-11\-24 |Added an API that enables or disables automatic installation of the collection add\-on for newly purchased ECS instances. |Collection add\-ons |
|<span data-api-tag="add\|5Xi6Jl">新增</span> [GetO11yAgentECSAutoInstall](https://docs.byteplus.com/en/docs/cloudmonitor/GetO11yAgentECSAutoInstall) ||Added an API that queries whether automatic installation of the collection add\-on is enabled for newly purchased ECS instances. ||
|<span data-api-tag="add\|O9SMUW">新增</span> [CreateO11yAgentECSDeployTask](https://docs.byteplus.com/en/docs/cloudmonitor/CreateO11yAgentECSDeployTask) ||Added an API that creates an installation or upgrade task for the ECS instance collection add\-on. ||
|<span data-api-tag="add\|nQE9as">新增</span> [PerformO11yAgentECSDeployTask](https://docs.byteplus.com/en/docs/cloudmonitor/PerformO11yAgentECSDeployTask) ||Added an API that ends the installation or upgrade task of the collection add\-on on an ECS instance. ||
|<span data-api-tag="add\|nob4du">新增</span> [ListO11yAgentECSInstances](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstances) ||Added an API that queries the list of collection add\-ons for ECS instances. ||
|<span data-api-tag="add\|COpZ8Q">新增</span> [ListO11yAgentVpcEndpoints](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentVpcEndpoints) ||Added an API that queries the list of endpoints associated with the O11yAgent Service. ||
|<span data-api-tag="add\|11lb72">新增</span> [UpdateO11yAgentECSProcessConfig](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateO11yAgentECSProcessConfig) ||Added an API that modifies the configuration of monitored processes for ECS instances. ||
|<span data-api-tag="add\|dSLSdE">新增</span> [ListO11yAgentECSProcessConfigs](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSProcessConfigs) ||Added an API that queries the list of monitored ECS instance processes. ||
|<span data-api-tag="add\|vHinSV">新增</span> [ListO11yAgentECSInstanceMetadata](https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstanceMetadata) ||Added an API that queries collection add\-on metadata for ECS instances. ||


<span id=".XzIwMjUt5bm0LTA5LeaciA=="></span>
## September 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|FHnQyk">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) |2025\-09\-05 |Added request parameters `AlertTemplateIds` and `ObjectGroupIds` to allow queries based on alert template IDs or object group IDs. |Alert policy |
|<span data-api-tag="update\|Nu1dYz">更新</span> [ListObjectGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListObjectGroups) ||Added the request parameter `AlertTemplateIds` to allow queries based on alert template IDs. |Resource Group |
|<span data-api-tag="update\|qcyvpu">更新</span> [CreateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/CreateAlertTemplate) ||Added usage limits, including the number of alert templates allowed to be created per root user and the number of alert policies allowed to be created in each alert template. |Alert template |
|<span data-api-tag="update\|bfXEV6">更新</span> [UpdateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateAlertTemplate) ||||
|<span data-api-tag="update\|Dlj0YJ">更新</span> [ListAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertTemplates) ||Added the request parameter `ObjectGroupIds`, which allows queries based on object group IDs. ||
|<span data-api-tag="update\|7ULAOQ">更新</span> [ApplyObjectGroupsByAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/ApplyObjectGroupsByAlertTemplate) ||Added usage limits, including the number of alert templates allowed to be created per root user and the number of alert policies allowed to be created in each alert template. ||


<span id=".XzIwMjUt5bm0LTA4LeaciA=="></span>
## August 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|TIR0a3">新增</span> [CreateNotifyTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotifyTemplate) |2025\-08\-13 |Added an API that creates a notification template. |Notification template |
|<span data-api-tag="add\|NMxfFg">新增</span> [DeleteNotifyTemplatesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteNotifyTemplatesByIds) ||Added an API that deletes a notification template. ||
|<span data-api-tag="add\|7qaUBg">新增</span> [ListDefaultNotifyTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListDefaultNotifyTemplates) ||Added an API that queries default notification templates. ||
|<span data-api-tag="add\|ZdFlc6">新增</span> [ListNotifyTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifyTemplates) ||Added an API that queries notification templates. ||
|<span data-api-tag="add\|YfvHNR">新增</span> [UpdateNotifyTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateNotifyTemplate) ||Added an API that updates a notification template. ||
|<span data-api-tag="update\|vOSLQq">更新</span> [EnablePresetAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/EnablePresetAlertTemplate) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when applying a preset alert template. |Alert template |
|<span data-api-tag="update\|7kxa9d">更新</span> [ListPresetAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListPresetAlertTemplates) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in preset alert templates. ||
|<span data-api-tag="update\|VLASz2">更新</span> [ListAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertTemplates) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in alert templates. ||
|<span data-api-tag="update\|eeahBm">更新</span> [ApplyObjectGroupsByAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/ApplyObjectGroupsByAlertTemplate) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when associating object groups and notification policies with notification templates. ||
|<span data-api-tag="update\|EO0dzZ">更新</span> [CreateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotification) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when creating notification policies. |Notification policy |
|<span data-api-tag="update\|0UMQpL">更新</span> [ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in notification policies. ||
|<span data-api-tag="update\|jQyoAX">更新</span> [UpdateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateNotification) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when updating notification policies. ||
|<span data-api-tag="update\|9oYZJL">更新</span> [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when creating alert policies. |Alert policy |
|<span data-api-tag="update\|xIul8U">更新</span> [UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when updating alert policies. ||
|<span data-api-tag="update\|qjEi9Y">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in alert policies. ||
|<span data-api-tag="update\|Hpybpg">更新</span> [ListRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in alert policies. ||
|<span data-api-tag="update\|YvGmeT">更新</span> [CreateEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateEventRule) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when creating event rules. |Event rule |
|<span data-api-tag="update\|P79Ork">更新</span> [UpdateEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateEventRule) ||Added the request parameter `NotifyTemplates`, which allows you to specify notification templates when updating event rules. ||
|<span data-api-tag="update\|hZCfgW">更新</span> [ListEventRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListEventRules) ||Added the response parameter `NotifyTemplates`, which allows you to query notification templates configured in event rules. ||


<span id=".XzIwMjUt5bm0LTA2LeaciA=="></span>
## June 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|O39a9F">新增</span> [EnablePresetAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/EnablePresetAlertTemplate) |2025\-06\-19 |Added an API that enables a preset alert template to create alert policies in batches. |Alert template |
|<span data-api-tag="add\|DKTGLd">新增</span> [ListPresetAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListPresetAlertTemplates) ||Added an API that queries preset alert templates. ||
|<span data-api-tag="add\|7NY7Zt">新增</span> [DisablePresetAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/DisablePresetAlertTemplate) ||Added an API that disables a preset alert template and deletes alert policies associated with the preset alert template. ||
|<span data-api-tag="add\|tSpN1u">新增</span> [CreateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/CreateAlertTemplate) ||Added an API that creates an alert template. ||
|<span data-api-tag="add\|N5PD3m">新增</span> [ListAlertTemplates](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertTemplates) ||Added an API that queries alert templates. ||
|<span data-api-tag="add\|Oqw5YQ">新增</span> [UpdateAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateAlertTemplate) ||Added an API that updates an alert template. ||
|<span data-api-tag="add\|N3XFhl">新增</span> [ApplyObjectGroupsByAlertTemplate](https://docs.byteplus.com/en/docs/cloudmonitor/ApplyObjectGroupsByAlertTemplate) ||Added an API that associates object groups and notification policies with an alert template. ||
|<span data-api-tag="add\|jNI135">新增</span> [DeleteAlertTemplatesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteAlertTemplatesByIds) ||Added an API that deletes specified alert templates. ||


<span id=".XzIwMjUt5bm0LTA1LeaciA=="></span>
## May 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|88DsJm">新增</span> [CreateSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/CreateSilencePolicy) |2025\-05\-16 |Added an API that creates a suppression policy. |Suppression policy |
|<span data-api-tag="add\|sPNZus">新增</span> [DeleteSilencePolicyByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteSilencePolicyByIds) ||Added an API that deletes a suppression policy. ||
|<span data-api-tag="add\|IEPH81">新增</span> [ListSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/ListSilencePolicy) ||Added an API that queries suppression policies. ||
|<span data-api-tag="add\|V2asRP">新增</span> [UpdateSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateSilencePolicy) ||Added an API that updates a suppression policy. ||
|<span data-api-tag="add\|LKGRlh">新增</span> [ModifyStateOfSilencePolicyByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ModifyStateOfSilencePolicyByIds) ||Added an API that modifies the status of a suppression policy. ||


<span id=".XzIwMjUt5bm0LTA0LeaciA=="></span>
## April 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|qYzLZ0">新增</span> [CreateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotification) |2025\-04\-11 |\-04Added an API that creates an alert notification template. |Notification template |
|<span data-api-tag="add\|brx4NZ">新增</span> [DeleteNotificationsByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteNotificationsByIds) ||Added an API that deletes an alert template. ||
|<span data-api-tag="add\|W53QfI">新增</span> [ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) ||Added an API that queries alert notification templates. ||
|<span data-api-tag="add\|qZeQww">新增</span> [UpdateNotification](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateNotification) ||Added an API that updates an alert notification template. ||
|<span data-api-tag="add\|d7IazG">新增</span> [TagResources](https://docs.byteplus.com/en/docs/cloudmonitor/TagResources) ||Added an API that adds tags to resources. |Tag management |
|<span data-api-tag="add\|H14WrD">新增</span> [UntagResources](https://docs.byteplus.com/en/docs/cloudmonitor/UntagResources) ||Added an API that removes tags from resources. ||
|<span data-api-tag="update\|aUWCLy">更新</span> [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) ||Optimized the API by adding fields for resource binding, alert level setting, and alert notification template setting. |Alert policy |
|<span data-api-tag="update\|N80bJt">更新</span> [UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) ||||


<span id=".XzIwMjUt5bm0LTAyLeaciA=="></span>
## February 2025


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|nULOyA">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) |2025\-02\-27 |Added the Dimensions field to the API request parameters. This field allows you to filter alert policies based on the Dimensions field of a cloud product. |Alert policy |


<span id=".XzIwMjQt5bm0LTA5LeaciA=="></span>
## September 2024


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|qOaqy0">更新</span> [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) |2024\-09\-27 |Added the DimensionConditions parameter that enables dynamic configuration of resources for alerting. |Alert policy |
|<span data-api-tag="update\|NCxvtx">更新</span> [UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) ||||
|<span data-api-tag="update\|07V7n1">更新</span> [ListRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds) ||||
|<span data-api-tag="update\|YgSWjB">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) ||||
|<span data-api-tag="update\|2j1haa">更新</span> [CreateObjectGroup](https://docs.byteplus.com/en/docs/cloudmonitor/CreateObjectGroup) |||Resource Group |
|<span data-api-tag="update\|i6i3De">更新</span> [UpdateObjectGroup](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateObjectGroup) ||||
|<span data-api-tag="update\|MWJRGE">更新</span> [ListObjectGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListObjectGroups) ||||


<span id=".XzIwMjQt5bm0LTA3LeaciA=="></span>
## July 2024


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|Jg08Ic">更新</span> [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) |2024\-07\-30 |Added alert aggregation support that implements alert notification sending based on rule or resource granularity. |Alert policy |
|<span data-api-tag="update\|TNUHuJ">更新</span> [UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) ||||
|<span data-api-tag="update\|0bq5bg">更新</span> [ListRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds) ||||
|<span data-api-tag="update\|EuSmJi">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) ||||


<span id=".XzIwMjQt5bm0LTA2LeaciA=="></span>
## June 2024


|API |Release date |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|izTd2J">更新</span> [CreateRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateRule) |2024\-06\-26 |Added the NoData parameter to support NoData alerts. |Alert policy |
|<span data-api-tag="update\|VfR2om">更新</span> [UpdateRule](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateRule) ||||
|<span data-api-tag="update\|Aj1Rvk">更新</span> [ListRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListRules) ||||
|<span data-api-tag="update\|0Y4d2V">更新</span> [ListRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListRulesByIds) ||||
|<span data-api-tag="add\|4rMF7g">新增</span> [CreateWebhook](https://docs.byteplus.com/en/docs/cloudmonitor/CreateWebhook) |2024\-06\-25 |Added an API that creates alert callbacks. |Alert callback |
|<span data-api-tag="add\|AS0u3e">新增</span> [ListWebhooksByIds](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooksByIds) ||Added an API that queries alert callbacks by ID. ||
|<span data-api-tag="add\|6XiIYp">新增</span> [ListWebhooks](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks) ||Added an API that queries alert callbacks. ||
|<span data-api-tag="add\|nLaGxz">新增</span> [UpdateWebhook](https://docs.byteplus.com/en/docs/cloudmonitor/UpdateWebhook) ||Added an API that updates an alert callback. ||
|<span data-api-tag="add\|nUNxw1">新增</span> [DeleteWebhooksByIds](https://docs.byteplus.com/en/docs/cloudmonitor/DeleteWebhooksByIds) ||Added an API that deletes alert callbacks. ||


<span id="1a2f2304"></span>
## March 2024


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateObjectGroup](https://docs.byteplus.com/docs/cloudmonitor/CreateObjectGroup) |2024\-03\-11 |Added an API that creates an object group. |Resource Group |
|[UpdateObjectGroup](https://docs.byteplus.com/docs/cloudmonitor/UpdateObjectGroup) ||Added an API that supports full update of a specified object group (namely, updating all attributes of the object group). ||
|[ListObjectGroups](https://docs.byteplus.com/docs/cloudmonitor/ListObjectGroups) ||Added an API that queries a list of object groups. It supports fuzzy search by object group name keyword. ||
|[DeleteObjectGroup](https://docs.byteplus.com/docs/cloudmonitor/DeleteObjectGroup) ||Added an API that deletes a specified object group. ||


<span id="2eb86225"></span>
## October 2023


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateRule](https://docs.byteplus.com/docs/cloudmonitor/CreateRule) |2023\-10\-20 |Added an API that creates an alert policy. |Alert policy |
|[UpdateRule](https://docs.byteplus.com/docs/cloudmonitor/UpdateRule) ||Added an API that updates an alert policy. ||
|[ListRulesByIds](https://docs.byteplus.com/docs/cloudmonitor/ListRulesByIds) ||Added an API that queries alert policies by alert policy ID. ||


<span id="a6c56602"></span>
## September 2023


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateEventRule](https://docs.byteplus.com/docs/cloudmonitor/CreateEventRule) |2023\-09\-05 |Added an API that creates an event rule. |Event rule |
|[UpdateEventRule](https://docs.byteplus.com/docs/cloudmonitor/UpdateEventRule) ||Added an API that updates an event rule. ||
|[ListEventRules](https://docs.byteplus.com/docs/cloudmonitor/ListEventRules) ||Added an API that queries event rules. ||


<span id="4c252c51"></span>
## April 2023


|API |Release date |Change |Related feature |
|---|---|---|---|
|[GetTopData](https://docs.byteplus.com/docs/cloudmonitor/GetTopData) |2023\-04\-15 |Added an API that queries top\-ranked entries for the specified metrics and corresponding data of other metrics under the same dimension. |Querying cloud product monitor metrics or events |


<span id="e97a8feb"></span>
## February 2023


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateEventRule](https://docs.byteplus.com/docs/cloudmonitor/CreateEventRule) |2023\-02\-15 |Optimized the API by supporting event delivery to TLS. |Event rule |
|[UpdateEventRule](https://docs.byteplus.com/docs/cloudmonitor/UpdateEventRule) ||Optimized the API by supporting event delivery to TLS. ||
|[ListEventRules](https://docs.byteplus.com/docs/cloudmonitor/ListEventRules) ||Optimized the API by supporting event delivery to TLS. ||


<span id="7309b28c"></span>
## October 2022


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateRule](https://docs.byteplus.com/docs/cloudmonitor/CreateRule) |2022\-10\-15 |Added an API that creates an alert policy. |Alert policy |
|[DeleteRulesByIds](https://docs.byteplus.com/docs/cloudmonitor/DeleteRulesByIds) ||Added an API that deletes an alert policy. ||
|[UpdateRule](https://docs.byteplus.com/docs/cloudmonitor/UpdateRule) ||Added an API that updates an alert policy. ||
|[ListRulesByIds](https://docs.byteplus.com/docs/cloudmonitor/ListRulesByIds) ||Added an API that queries alert policies by alert policy ID. ||
|[ListRules](https://docs.byteplus.com/docs/cloudmonitor/ListRules) ||Added an API that queries alert policies based on specified conditions. The conditions in the request have a logical AND relationship. ||
|[SetStateOfRulesByIds](https://docs.byteplus.com/docs/cloudmonitor/SetStateOfRulesByIds) ||Added an API that enables or disables alert policies. ||
|[CreateEventRule](https://docs.byteplus.com/docs/cloudmonitor/CreateEventRule) ||Added an API that creates an event rule. |Event rule |
|[DeleteEventRule](https://docs.byteplus.com/docs/cloudmonitor/DeleteEventRule) ||Added a new API that deletes an event rule. ||
|[UpdateEventRule](https://docs.byteplus.com/docs/cloudmonitor/UpdateEventRule) ||Added an API that updates an event rule. ||
|[ListEventRules](https://docs.byteplus.com/docs/cloudmonitor/ListEventRules) ||Added an API that queries event rules. ||
|[EnableEventRule](https://docs.byteplus.com/docs/cloudmonitor/EnableEventRule) ||Added an API that enables one or more event rules. ||
|[DisableEventRule](https://docs.byteplus.com/docs/cloudmonitor/DisableEventRule) ||Added an API that disables one or more event rules. ||
|[ListAlertGroup](https://docs.byteplus.com/docs/cloudmonitor/ListAlertGroup) ||Added an API that queries the alert history of resources. |Alert record |
|[ListSendAlert](https://docs.byteplus.com/docs/cloudmonitor/ListSendAlert) ||Added an API that queries the list of alert notifications sent. ||


<span id="0e00883b"></span>
## August 2022


|API |Release date |Change |Related feature |
|---|---|---|---|
|[ListEvents](https://docs.byteplus.com/docs/cloudmonitor/ListEvents) |2022\-08\-15 |Added an API that queries events that occurred within the specified time period. |Querying cloud product monitor metrics or events |


<span id="27c48290"></span>
## March 2022


|API |Release date |Change |Related feature |
|---|---|---|---|
|[GetMetricData](https://docs.byteplus.com/docs/cloudmonitor/GetMetricData) |2022\-03\-15 |Added an API that supports querying cloud product metric information within a specified time period. |Querying cloud product monitor metrics or events |


<span id="6a4f6d7f"></span>
## November 2021


|API |Release date |Change |Related feature |
|---|---|---|---|
|[CreateContactGroup](https://docs.byteplus.com/docs/cloudmonitor/CreateContactGroup) |2021\-11\-15 |Added an API that creates an alert contact group. |Alert contact group |
|[UpdateContactGroup](https://docs.byteplus.com/docs/cloudmonitor/UpdateContactGroup) ||Added an API that updates the basic information of the specified contact group. ||
|[UpdateContactGroupWithContacts](https://docs.byteplus.com/docs/cloudmonitor/UpdateContactGroupWithContacts) ||Added an API that modifies the members of the specified contact group, including adding and deleting specified contacts. ||
|[ListContactGroups](https://docs.byteplus.com/docs/cloudmonitor/ListContactGroups) ||Added an API that queries contact groups based on fuzzy search by contact group name keyword. ||
|[ListContactGroupByIds](https://docs.byteplus.com/docs/cloudmonitor/ListContactGroupByIds) ||Added an API that queries the details of a specified contact group. ||
|[DeleteContactGroupByIds](https://docs.byteplus.com/docs/cloudmonitor/DeleteContactGroupByIds) ||Added an API that deletes a contact group. ||
|[CreateContacts](https://docs.byteplus.com/docs/cloudmonitor/CreateContacts) ||Added an API that creates a contact. |Alert contact |
|[UpdateContacts](https://docs.byteplus.com/docs/cloudmonitor/UpdateContacts) ||Added an API that performs a full update on all attributes of the specified contact, including the name, mobile phone, and email address. ||
|[UpdateContactsWithContactGroups](https://docs.byteplus.com/docs/cloudmonitor/UpdateContactsWithContactGroups) ||Added an API that adds contacts to one or more specified contact groups. ||
|[ListContacts](https://docs.byteplus.com/docs/cloudmonitor/ListContacts) ||Added an API that queries contacts based on fuzzy search by contact name keyword. ||
|[ListContactsByIds](https://docs.byteplus.com/docs/cloudmonitor/ListContactsByIds) ||Added an API that queries the details of a specified contact. ||
|[DeleteContactsByIds](https://docs.byteplus.com/docs/cloudmonitor/DeleteContactsByIds) ||Added an API that deletes a contact. ||


&nbsp;
