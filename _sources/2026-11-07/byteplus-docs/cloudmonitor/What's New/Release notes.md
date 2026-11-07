---
title: "Release notes"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Release-notes"
---

This topic describes the release notes of Cloud Monitor feature versions and the corresponding documentation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The <strong>Regions</strong> column lists the regions where the feature change applies at the time of the release. The actual supported regions are subject to those displayed in the console. In this column, <strong>All</strong> refers to all regions where the service is available.</div>



<span id="ahtb55np"></span>
## September 2026


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Export data |Supports exporting metric data as .xlsx files based on a custom time range, statistical method, and aggregation granularity. This facilitates offline analysis, issue review, and data archiving. |All |[Exporting monitoring data](https://docs.byteplus.com/en/docs/cm/Dataexport) |


<span id="gEKpyFig"></span>
## May 2026


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Exporting monitoring data to self\-managed Prometheus |Added support for exporting monitoring data to self\-managed Prometheus via the Remote Write method. |All |[Exporting monitoring data to self-managed Prometheus](https://docs.byteplus.com/en/docs/cloudmonitor/Export_monitoring_data_to_self-managed_Prometheus) |


<span id="yniBYKc8"></span>
## January 2026


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Historical data backfilling |The exporter provided historical data backfilling, which allows you to manually backfill data that is lost due to export interruption. |All |[Historical data backfilling](https://docs.byteplus.com/en/docs/cloudmonitor/Backfill_historical_data_to_Prometheus) |
|LimitQPSGetMetricData adaptive rate limiting |LimitQPSGetMetricData in the exporter supported adaptive rate limiting for metadata requests. |All |[Exporting monitoring data to self-managed Prometheus](https://docs.byteplus.com/en/docs/cloudmonitor/Export_monitoring_data_to_self-managed_Prometheus) |


<span id="0FfJO7Lc"></span>
## November 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Added account name and ID to default notification templates |Added account name and ID to default notification templates for Lark, DingTalk, WeCom, and Slack notification channels. The fields are used to indicate the accurate source of notification messages. |All |[Creating notification templates](https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template) |
|Installed the O11yAgent collection add\-on on Windows ECS instances |Installed the O11yAgent collection add\-on on Windows ECS instances by using the installation scripts or the cloud assistant Agent. |All |[Manually installing the O11yAgent collection add-on](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually) |


<span id="ZLLHarme"></span>
## September 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Alert policy |Supported using the same metric to configure multiple alert trigger conditions during the creation of alert policies. In addition, the alert duration logic is optimized. This allows you to specify that if the alert trigger condition is met in N cycles out of M cycles, an alert will be triggered. |All |[Creating an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) |
|Resource group |When you bind alert templates to object groups, you can bind one alert template to multiple object groups, or bind one object group to multiple alert templates. |All |* [Creating alert templates](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template)<br><br>* [Creating an object group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group)<br><br>* [Applying alert templates to resource groups](https://docs.byteplus.com/en/docs/cloudmonitor/Applying-an-alarm-template-to-a-resource-group) |
|Event center |Pushed cloud product events to Message Queue for Kafka in the China (Shanghai) region. |All |[Creating an event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) |


<span id="wonS0unT"></span>
## August 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Monitoring dashboard |Added data collection interval and aggregation dimensions (including average value, maximum value, and minimum value) to monitoring dashboard charts. |All |[Basic monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Basic-monitoring) |
|Silence policy |Supported associating more instances during the configuration of suppressed resources for a suppression policy. |All |* [Alert suppression](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm_silence)<br><br>* [Event suppression](https://docs.byteplus.com/en/docs/cloudmonitor/Event_silencing) |
|Resource details |Viewed other bound resources and unbound the resources on the resource details page of callback URLs, contact groups, and notification policies. |All |* [Managing callback URLs](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address)<br><br>* [Creating contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact)<br><br>* [Creating notification policies](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy) |
|Alert policy |Viewed the list of effective resource instances in the alert policy details. |All |[Viewing alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy) |
|Resource group |Viewed the list of effective resource instances in the object group details. |All |[Creating an object group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group) |
|O11yAgent monitoring add\-on |Supported configuring an endpoint for the O11yAgent add\-on, which allows the add\-on  to access the add\-on management platform by using PrivateLink. This achieves add\-on status display, upgrade, and other features. |All |[Creating O11yAgent endpoints](https://docs.byteplus.com/en/docs/cloudmonitor/creating_o11yagent_privatelink) |


<span id="DieVIzDL"></span>
## July 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Custom notification template |Added custom notification templates, which allow you to specify the structure and content of alert notifications and event notifications by using Markdown syntax and Go template syntax. |All |[Notification template](https://docs.byteplus.com/en/docs/cloudmonitor/Notification_template) |


<span id="E1e0BqQs"></span>
## April 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Alert callback |Supported encrypting the callback URL by using a Token to ensure the authenticity of the callback URL source and prevent information security risks caused by Webhook address leakage. |All |[Managing callback URLs](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address) |
|Alert callback |Added the Slack alert callback type, which supports receiving alerts and event information through Slack. |All |* [Managing callback URLs](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address)<br><br>* [Receiving alert notifications via Slack](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving_Alarm_Notifications_in_Slack_channels) |


<span id="4e865250"></span>
## February 2025


|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Event suppression |Supported more flexible event suppression based on fields in cloud product events. |All |[Event suppression](https://docs.byteplus.com/en/docs/cloudmonitor/Event_silencing) |
|Alert levels |Supported configuring different thresholds for different levels of alerts based on the same trigger condition during the configuration of alert policies. |All |* [Creating an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy)<br><br>* [Achieving differentiated alert notifications by using the alert grading feature](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm_classification_feature_for_alarm_differentiation_notifications) |
|Notification policy |Supported configuring notification policies, which allow alerts of different levels to use different notification channels. |All |[Creating notification policies](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy) |


<span id="4e865250"></span>
##
