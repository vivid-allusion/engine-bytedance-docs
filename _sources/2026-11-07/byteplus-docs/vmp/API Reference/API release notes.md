---
title: "API release notes"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Change-history"
---

This topic provides the release notes for all the OpenAPI operations of Vital Managed Service for Prometheus.

<span id=".XzIwMjUt5bm0LTEyLeaciA=="></span>
## December 2025


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|0rliTg">新增</span> [GetWorkspaceAuthInfo](https://docs.byteplus.com/en/docs/vmp/GetWorkspaceAuthInfo) |2025\-12\-01 |A new API is added to obtain workspace authentication information. |workspace |
|<span data-api-tag="update\|89DFLl">更新</span> [CreateWorkspace](https://docs.byteplus.com/en/docs/vmp/CreateWorkspace) ||* The `AuthType` field is added to select the authentication type for workspaces.<br><br>* The `BearerToken` field is added to generate a `BearerToken` authentication `Token`. ||
|<span data-api-tag="update\|CbWiDv">更新</span> [UpdateWorkspace](https://docs.byteplus.com/en/docs/vmp/UpdateWorkspace) ||The `AuthType` field is added to select the authentication type for workspaces. ||
|<span data-api-tag="update\|nGtDuj">更新</span> [GetWorkspace](https://docs.byteplus.com/en/docs/vmp/GetWorkspace) ||The `AuthType` field is added to view the authentication type of workspaces. ||


<span id=".XzIwMjUt5bm0LTExLeaciA=="></span>
## November 2025


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|kq1ZT4">更新</span> [Public error code](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) |2025\-11\-01 |Changed the API error code by replacing `Vital Managed Service for Prometheus (VMP)` with `VMP`. |Error code |


<span id=".XzIwMjUt5bm0LTA4LeaciA=="></span>
## August 2025


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|NjvysR">新增</span> [CreateIntegrationTask](https://docs.byteplus.com/en/docs/vmp/CreateIntegrationTask) |2025\-08\-21 |A new operation to create an integration task. |Integration tasks |
|<span data-api-tag="add\|w4zmfs">新增</span> [UpdateIntegrationTask](https://docs.byteplus.com/en/docs/vmp/UpdateIntegrationTask) ||A new API to update an integration task. ||
|<span data-api-tag="add\|RV7tIa">新增</span> [GetIntegrationTask](https://docs.byteplus.com/en/docs/vmp/GetIntegrationTask) ||A new operation to get an integration task. ||
|<span data-api-tag="add\|RsNOt3">新增</span> [DeleteIntegrationTask](https://docs.byteplus.com/en/docs/vmp/DeleteIntegrationTask) ||A new API to delete integration tasks. ||
|<span data-api-tag="add\|TJ1ynO">新增</span> [ListIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/ListIntegrationTasks) ||A new API to get a list of integration tasks. ||
|<span data-api-tag="add\|ziCZLJ">新增</span> [EnableIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/EnableIntegrationTasks) ||A new operation to enable integration tasks. ||
|<span data-api-tag="add\|qQa8RV">新增</span> [DisableIntegrationTasks](https://docs.byteplus.com/en/docs/vmp/DisableIntegrationTasks) ||A new operation to disable integration tasks. ||


<span id=".XzIwMjUt5bm0LTA1LeaciA=="></span>
## May 2025


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|9aXgt1">更新</span> [CreateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/CreateSilencePolicy) |2025\-05\-23 |* A new field `LabelMatchers` to find alerts that need to be silenced by using labels.<br><br>* New fields `Weekday` and `DayOfMonth` to specify the days in each week and month respectively in alerting silence policies. |Alerting silence policies |
|<span data-api-tag="update\|wSDXle">更新</span> [UpdateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/UpdateSilencePolicy) ||||
|<span data-api-tag="update\|FQEjNz">更新</span> [ListSilencePolicies](https://docs.byteplus.com/en/docs/vmp/ListSilencePolicies) ||||
|<span data-api-tag="update\|tc2PX7">更新</span> [CreateAlertingRule](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule) ||New fields `Annotations` and `Labels` to add annotations and labels to alerting rules. |Alert rules |
|<span data-api-tag="update\|D3HvEF">更新</span> [UpdateAlertingRule](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule) ||||
|<span data-api-tag="update\|R6jA14">更新</span> [ListAlertingRules](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules) ||||
|<span data-api-tag="update\|iA1BOe">更新</span> [CreateWorkspace](https://docs.byteplus.com/en/docs/vmp/CreateWorkspace) ||Added the `Tags` field for tagging workspaces. |workspace |
|<span data-api-tag="update\|P31qTA">更新</span> [ListWorkspaces](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) ||A new field `TagFilters` to filter workspaces by labels. ||
|<span data-api-tag="add\|7oOiZo">新增</span> [GetWorkspace](https://docs.byteplus.com/en/docs/vmp/GetWorkspace) ||A new API operation to get workspace details. ||
|<span data-api-tag="add\|kMobC0">新增</span> [TagResources](https://docs.byteplus.com/en/docs/vmp/TagResources) ||A new API to add labels to resources. |Resource labels |
|<span data-api-tag="add\|eeeUZO">新增</span> [UntagResources](https://docs.byteplus.com/en/docs/vmp/UntagResources) ||A new API operation to delete labels of resources. ||
|<span data-api-tag="add\|d8tWZW">新增</span> [ListTagsForResources](https://docs.byteplus.com/en/docs/vmp/ListTagsForResources) ||A new API to obtain a list of resource labels. ||
|<span data-api-tag="update\|M3H3TE">更新</span> [CreateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/CreateNotifyPolicy) |2025\-05\-26 |A new field `ChannelNotifyTemplateIds` to specify custom notification templates when creating alert notification policies. |Alert notification policy |
|<span data-api-tag="update\|1MVMr9">更新</span> [ListNotifyPolicies](https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies) ||A new field `ChannelNotifyTemplateIds` to get custom notification templates used in different alert channels of alert notification policies. ||
|<span data-api-tag="update\|yhYHwg">更新</span> [UpdateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyPolicy) ||A new field `ChannelNotifyTemplateIds` to specify custom notification templates when configuring alerting notification policies. ||


<span id=".XzIwMjUt5bm0LTA0LeaciA=="></span>
## April 2025


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="update\|S0KhHh">更新</span> [UpdateWorkspace](https://docs.byteplus.com/en/docs/vmp/UpdateWorkspace) |2025\-04\-01 |The API is improved to allow updating workspace specifications. |workspace |


<span id=".XzIwMjQt5bm0LTA4LeaciA=="></span>
## August 2024


|API |Release Month |Change |Related feature |
|---|---|---|---|
|<span data-api-tag="add\|0wrKFn">新增</span> [TestWebhook](https://docs.byteplus.com/en/docs/vmp/TestWebhook) |2024\-08\-16 |A new API operation to test the connectivity of Webhook. |Contacts |
|<span data-api-tag="add\|NuGios">新增</span> [TestLarkBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestLarkBotWebhook) ||A new API operation to test the connectivity of Feishu bots. ||
|<span data-api-tag="add\|MTPPKO">新增</span> [TestDingTalkBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestDingTalkBotWebhook) ||A new API to test the connectivity of DingTalk robot. ||
|<span data-api-tag="add\|NO3Amk">新增</span> [TestWeComBotWebhook](https://docs.byteplus.com/en/docs/vmp/TestWeComBotWebhook) ||A new API operation to test the connectivity of WeCom robots. ||
|<span data-api-tag="add\|cyCsYk">新增</span> [CreateNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/CreateNotifyTemplate) ||A new API operation to create alerting notification templates. |Notification template |
|<span data-api-tag="add\|7FmoZK">新增</span> [UpdateNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyTemplate) ||A new API operation to update alerting notification templates. ||
|<span data-api-tag="add\|7PEURh">新增</span> [ListNotifyTemplates](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates) ||A new API to query alerting notification templates. ||
|<span data-api-tag="add\|Hma7EN">新增</span> [DeleteNotifyTemplate](https://docs.byteplus.com/en/docs/vmp/DeleteNotifyTemplate) ||A new API operation to delete alerting notification templates. ||
|<span data-api-tag="add\|zMfGgO">新增</span> [CreateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/CreateSilencePolicy) ||A new API to create alerting silence policies. |Alerting silence policies |
|<span data-api-tag="add\|QcpLrO">新增</span> [UpdateSilencePolicy](https://docs.byteplus.com/en/docs/vmp/UpdateSilencePolicy) ||A new API to update alerting silence policies. ||
|<span data-api-tag="add\|Ec89Mj">新增</span> [EnableSilencePolicies](https://docs.byteplus.com/en/docs/vmp/EnableSilencePolicies) ||A new API operation to enable alerting silence policies. ||
|<span data-api-tag="add\|85f2Kn">新增</span> [DisableSilencePolicies](https://docs.byteplus.com/en/docs/vmp/DisableSilencePolicies) ||A new API operation to disable alerting silence policies. ||
|<span data-api-tag="add\|arCtha">新增</span> [DeleteSilencePolicies](https://docs.byteplus.com/en/docs/vmp/DeleteSilencePolicies) ||A new API operation to delete alerting silence policies. ||
|<span data-api-tag="add\|BGe6dU">新增</span> [ListSilencePolicies](https://docs.byteplus.com/en/docs/vmp/ListSilencePolicies) ||A new API to query alerting silence policies. ||
|<span data-api-tag="update\|aAZVb0">更新</span> [CreateContact](https://docs.byteplus.com/en/docs/vmp/CreateContact) ||New request parameters:<br><br><br>* `WeComBotWebhook`: represents the alerting notification method used by WeCom. |Alerting contact person |
|<span data-api-tag="update\|eDx1HX">更新</span> [UpdateContact](https://docs.byteplus.com/en/docs/vmp/UpdateContact) ||||
|<span data-api-tag="update\|mX3d7z">更新</span> [CreateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/CreateNotifyPolicy) ||New request parameters:<br><br><br>* Added a new parameter `WeComBotWebhook` to `Channels`: represents the alerting notification method used by WeCom. |Alert notification policy |
|<span data-api-tag="update\|gSqjbC">更新</span> [UpdateNotifyPolicy](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyPolicy) ||||


<span id=".XzIwMjMt5bm0LTA2LeaciA=="></span>
## June 2023


|API |Release Month |Change |Related feature |
|---|---|---|---|
|[Available APIs](https://docs.byteplus.com/en/docs/vmp/API-overview) |2023\-06\-30 |Official release of documentation for the OpenAPIs of Vital Managed Service for Prometheus. |None |


&nbsp;
