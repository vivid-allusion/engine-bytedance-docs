---
title: "Available APIs"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/API-overview"
---

The following tables contain all the APIs available for Vital Managed Service for Prometheus

<span id=".5bel5L2c5Yy6"></span>
## Workspace


|API |Descriptions |
|---|---|
|[CreateWorkspace](https://docs.byteplus.com/en/docs/vmp/CreateWorkspace) |Create a workspace. |
|[UpdateWorkspace](https://docs.byteplus.com/en/docs/vmp/UpdateWorkspace) |Update a workspace. |
|[DeleteWorkspace](https://docs.byteplus.com/en/docs/vmp/DeleteWorkspace) |Delete a workspace. |
|[ListWorkspaces](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) |Obtain the workspace list. |
|[ListWorkspaceInstanceTypes](https://docs.byteplus.com/en/docs/vmp/ListWorkspaceInstanceTypes) |Obtain a list of workspace types. |
|[ListWorkspaceStatus](https://docs.byteplus.com/en/docs/vmp/ListWorkspaceStatus) |Query workspace statuses. |
|[GetWorkspace](https://docs.byteplus.com/en/docs/vmp/GetWorkspace) |View workspace details. |
|[GetWorkspaceAuthInfo](https://docs.byteplus.com/en/docs/vmp/GetWorkspaceAuthInfo) |Obtain workspace authentication information. |


<span id="recording-rule"></span>
## Recording rule


|API |Descriptions |
|---|---|
|[CreateRuleFile](https://docs.byteplus.com/en/docs/vmp/CreateRuleFile) |Create a RecordingRule rule file. |
|[DeleteRuleFile](https://docs.byteplus.com/en/docs/vmp/DeleteRuleFile) |Delete a RecordingRule rule file. |
|[GetRuleFile](https://docs.byteplus.com/en/docs/vmp/GetRuleFile) |Obtain the details of a RecordingRule rule file. |
|[ListRuleFiles](https://docs.byteplus.com/en/docs/vmp/ListRuleFiles) |Obtain a list of RecordingRule rule files. |
|[ListRules](https://docs.byteplus.com/en/docs/vmp/ListRules) |Obtain a list of RecordingRule rules. |
|[UpdateRuleFile](https://docs.byteplus.com/en/docs/vmp/UpdateRuleFile) |Update a RecordingRule rule file. |


<span id=".5ZGK6K2m5Lit5b-D"></span>
## Alert center

<span id=".6IGU57O75Lq6"></span>
### Contacts


|API |Descriptions |
|---|---|
|[CreateContact](https://docs.byteplus.com/en/docs/vmp/CreateContact) |Create an alerting contact. |
|[DeleteContacts](https://docs.byteplus.com/en/docs/vmp/DeleteContacts) |Delete alerting contacts. |
|[ListContacts](https://docs.byteplus.com/en/docs/vmp/ListContacts) |Obtain alerting contacts. |
|[UpdateContact](https://docs.byteplus.com/en/docs/vmp/UpdateContact) |Update an alerting contact. |
|[CreateContactGroup](https://docs.byteplus.com/en/docs/vmp/CreateContactGroup) |Create an alerting contact group. |
|[DeleteContactGroups](https://docs.byteplus.com/en/docs/vmp/DeleteContactGroups) |Delete alerting contact groups. |
|[ListContactGroups](https://docs.byteplus.com/en/docs/vmp/ListContactGroups) |Obtain the list of alerting contact groups. |
|[UpdateContactGroup](https://docs.byteplus.com/en/docs/vmp/UpdateContactGroup) |Update a contact group. |
|[SendValidationMessage](https://docs.byteplus.com/en/docs/vmp/SendValidationMessage) |Send verification emails. |
|[TestWebhook](https://docs.byteplus.com/en/docs/vmp/TestWebhook) |Test the connectivity of the Webhook. |
|[TestLarkBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestLarkBotWebhook) |Test the connectivity of the Feishu group bot. |
|[TestDingTalkBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestDingTalkBotWebhook) |Test the connectivity of DingTalk robot. |
|[TestWeComBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestWeComBotWebhook) |Test the connectivity of the WeCom robot. |


<span id=".5ZGK6K2m6YCa55-l562W55Wl"></span>
### Alert notification policy


|API |Descriptions |
|---|---|
|[CreateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/CreateNotifyPolicy) |Create an alerting notification policy. |
|[DeleteNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/DeleteNotifyPolicy) |Delete alerting notification policies. |
|[ListNotifyPolicies](https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies) |Query alerting notification policies. |
|[UpdateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyPolicy) |Update an alert notification policy. |


<span id=".5ZGK6K2m6KeE5YiZ"></span>
### Alert rules


|API |Descriptions |
|---|---|
|[CreateAlertingRule](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule) |Creating an alerting rule. |
|[DeleteAlertingRules](https://docs.byteplus.com/en/docs/vmp/DeleteAlertingRules) |Delete alerting rules. |
|[DisableAlertingRules](https://docs.byteplus.com/en/docs/vmp/DisableAlertingRules) |Disable alerting rules. |
|[EnableAlertingRules](https://docs.byteplus.com/en/docs/vmp/EnableAlertingRules) |Enable alerting rules. |
|[ListAlertingRules](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules) |Obtain a list of alerting rules. |
|[UpdateAlertingRule](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule) |Update an alerting rule. |


<span id=".5ZGK6K2m6IGa5ZCI562W55Wl"></span>
### Alert aggregation policies


|API |Descriptions |
|---|---|
|[CreateNotifyGroupPolicy](https://docs.byteplus.com/en/docs/vmp/CreateNotifyGroupPolicy) |Create an alerting aggregation policy. |
|[DeleteNotifyGroupPolicy](https://docs.byteplus.com/en/docs/vmp/DeleteNotifyGroupPolicy) |Delete an alerting aggregation policy. |
|[ListNotifyGroupPolicies](https://docs.byteplus.com/en/docs/vmp/ListNotifyGroupPolicies) |Obtain a list of alerting aggregation policies. |
|[UpdateNotifyGroupPolicy](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyGroupPolicy) |Update an alerting aggregation policy. |


<span id=".6YCa55-l5raI5oGv5qih54mI"></span>
### Notification template


|API |Descriptions |
|---|---|
|[CreateNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/CreateNotifyTemplate) |Create an alerting notification template. |
|[UpdateNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyTemplate) |Update an alerting notification template. |
|[ListNotifyTemplates](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates) |Query alerting notification templates. |
|[DeleteNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/DeleteNotifyTemplate) |Delete alerting notification templates. |


<span id=".5ZGK6K2m6Z2Z6buY562W55Wl"></span>
### Alerting silence policies


|API |Descriptions |
|---|---|
|[CreateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/CreateSilencePolicy) |Creating an alerting silence policy. |
|[UpdateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/UpdateSilencePolicy) |Update an alerting silence policy. |
|[EnableSilencePolicies](https://docs.byteplus.com/en/docs/vmp/EnableSilencePolicies) |Enable an alerting silence policy. |
|[DisableSilencePolicies](https://docs.byteplus.com/en/docs/vmp/DisableSilencePolicies) |Disable alerting silence policies. |
|[DeleteSilencePolicies](https://docs.byteplus.com/en/docs/vmp/DeleteSilencePolicies) |Delete alerting silence policies. |
|[ListSilencePolicies](https://docs.byteplus.com/en/docs/vmp/ListSilencePolicies) |Query alerting silence policies. |


<span id=".5p-l55yL5ZGK6K2m"></span>
### Viewing alarms


|API |Descriptions |
|---|---|
|[ListAlertSamples](https://docs.byteplus.com/en/docs/vmp/ListAlertSamples) |Obtain a list of alert samples. |
|[ListAlerts](https://docs.byteplus.com/en/docs/vmp/ListAlerts) |Obtain a list of alerts. |


<span id=".6LWE5rqQ5qCH562-"></span>
## Resource labels


|API |Descriptions |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/vmp/TagResources) |Add labels to resources. |
|[UntagResources](https://docs.byteplus.com/en/docs/vmp/UntagResources) |Delete labels for resources. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/vmp/ListTagsForResources) |Obtain a list of resource labels. |


<span id=".5o6l5YWl5Lu75Yqh"></span>
## Integration tasks


|API |Descriptions |
|---|---|
|[CreateIntegrationTask](https://docs.byteplus.com/en/docs/vmp/CreateIntegrationTask) |Create an integration task. |
|[UpdateIntegrationTask](https://docs.byteplus.com/en/docs/vmp/UpdateIntegrationTask) |Update an integration task. |
|[GetIntegrationTask](https://docs.byteplus.com/en/docs/vmp/GetIntegrationTask) |Get an integration task. |
|[DeleteIntegrationTask](https://docs.byteplus.com/en/docs/vmp/DeleteIntegrationTask) |Delete an integration task. |
|[ListIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/ListIntegrationTasks) |Get a list of integration tasks. |
|[EnableIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/EnableIntegrationTasks) |Enable integration tasks. |
|[DisableIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/DisableIntegrationTasks) |Disable integration tasks. |
