---
title: "[Product update] Migration of the VMP alert notification feature to the Alert Center of the Observability Platform"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/qianyi"
---

Dear user,

VMP now gradually migrate its existing alert notification feature to the Alert Center of the Observability Platform (Unified Alert Center), and new feature iterations stop on September 2, 2026. After October 12, 2026, the system will automatically migrate any alert configurations that have not been migrated, and the original VMP alert notification APIs will be gradually decommissioned. If you are using VMP alert notification APIs, switch the APIs by referring to [API adaptation](https://docs.byteplus.com/en/docs/vmp/qianyi?TagIDs=2,143&lang=en#MsGLhZdD) before October 12, 2026. This prevents subsequent calls from being affected.

This migration will not affect the trigger logic of existing alert rules, nor will it cause alert interruptions. You can manually migrate existing configurations by referring to [Alert configuration migration](https://docs.byteplus.com/en/docs/vmp/qianyi?TagIDs=2,143&lang=en#DsTjtJvz) before October 12, 2026. During the migration, the system will synchronize the relevant resources from the VMP Alert Center to the Unified Alert Center, and rebind the notification policies and aggregation policies attached to existing alert rules to the corresponding resources in the Unified Alert Center. The correspondence relationships between the resource names in the VMP Alarm Center and the Unified Alert Center are as follows:


|VMP Alarm Center |Unified Alert Center |
|---|---|
|Alert notification policy |Notification policy |
|Contacts |Contacts |
|Contact group |Contact group |
|Notification template |Notification templates |
|Alerting silence policies |Silence policy |
|Alert aggregation strategy |Aggregation policies |


<span id="4lGVPASc"></span>
## Considerations


* The original alert notification resources of VMP are at the region level, with configurations in different regions being independent of each other. The alert notification resources in the Unified Alert Center are at the global level and shared globally. If you previously configured alert notification resources with the same name in multiple regions, duplicate configurations may occur after migration. We recommend promptly checking and cleaning up duplicate resources after migration.

* All update‑type APIs perform full updates, requiring the complete resource information to be passed in the request. A full update is an overwriting update that replaces the existing server‑side resource entirely with the full data submitted in the request. If certain fields are missing in the request, those fields will be overwritten with null or default values.

* To obtain technical support if you encounter issues during migration, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/).


<span id="XWbRibVP"></span>
## Migration schedule


|**Timeline** |**Description** |
|---|---|
|Now to September 2, 2026 |During the parallel run period, the original VMP alert notification feature and the Unified Alert Center are both available. |
|2026.09.02 \- 2026.10.12 |The original VMP alert notification feature stops iterating on new features. Before manual migration, the feature still functions as expected. After the migration is complete, all related capabilities are provided by the Unified Alert Center. |
|After October 12, 2026 |The system will automatically migrate alert configurations that have not been manually migrated. The original VMP alert notification APIs will be gradually decommissioned. |


<span id="8F8cGQ2F"></span>
## Migration procedure

<span id="DsTjtJvz"></span>
### **Alert configuration migration**


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Alert center \> Alert rule** to go to the **Alert rule** page.

4. Click **Migrate to unified alert center** and confirm migration based on the on\-screen prompts.


<span id="MsGLhZdD"></span>
### **API adaptation**

Before October 12, 2026, the original VMP alert notification APIs will continue to provide compatibility support. Your existing calls will not be affected. To ensure a smooth experience in the future, switch the VMP alert notification APIs in your code to the [Unified Alert Center APIs](https://api.volcengine.com/api-docs/view/overview?serviceCode=cloudmonitor&version=2025-12-01) before October 12, 2026.

The API mapping for migration is as follows:


|**Resource type** |**VMP Action** |**Unified Alert Center Action** |
|---|---|---|
|**Contacts** |CreateContact |CreateContact + CreateWebhook |
||GetContact |ListContacts+ListWebhooks |
||ListContacts |ListContacts+ListWebhooks |
||UpdateContact |UpdateContact+UpdateWebhook |
||DeleteContacts |DeleteContacts+DeleteWebhooks |
|**Contact group** |CreateContactGroup |CreateContactGroup |
||GetContactGroup |ListContactGroups |
||ListContactGroups |ListContactGroups |
||UpdateContactGroup |ListContactGroups + UpdateContactGroup |
||DeleteContactGroups |DeleteContactGroups |
|**Notification templates** |CreateNotifyTemplate |CreateNotificationTemplate |
||UpdateNotifyTemplate |ListNotificationTemplates + UpdateNotificationTemplate |
||ListNotifyTemplates |ListNotificationTemplates |
||DeleteNotifyTemplate |DeleteNotificationTemplates |
|**Notification policy** |CreateNotifyPolicy |CreateNotificationPolicy |
||GetNotifyPolicy |ListNotificationPolicies |
||ListNotifyPolicies |ListNotificationPolicies |
||UpdateNotifyPolicy |ListNotificationPolicies + UpdateNotificationPolicy |
||DeleteNotifyPolicy |DeleteNotificationPolicies |
|**Aggregation policies** |CreateNotifyGroupPolicy |CreateAggregationPolicy |
||GetNotifyGroupPolicy |ListAggregationPolicies |
||ListNotifyGroupPolicies |ListAggregationPolicies |
||UpdateNotifyGroupPolicy |ListAggregationPolicies + UpdateAggregationPolicy |
||DeleteNotifyGroupPolicy |DeleteAggregationPolicies |
|**Silence policy** |CreateSilencePolicy |CreateSilencePolicy |
||UpdateSilencePolicy |ListSilencePolicies + UpdateSilencePolicy |
||ListSilencePolicies |ListSilencePolicies |
||DeleteSilencePolicies |DeleteSilencePolicies |
||EnableSilencePolicies |EnableSilencePolicies |
||DisableSilencePolicies |DisableSilencePolicies |


<span id="As7niomD"></span>
##
