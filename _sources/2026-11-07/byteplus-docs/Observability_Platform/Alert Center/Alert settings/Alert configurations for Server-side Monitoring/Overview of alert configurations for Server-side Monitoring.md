---
title: "Overview of alert configurations for Server-side Monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_alert_configurations_for_Server-side_Monitoring"
---

Server‑Side Monitoring alert configuration includes four key components: alert object, trigger policy, send policy, and notification policy, along with other settings such as "project". These configurations form a complete Server‑Side Monitoring alert rule, defining the entire logic of "which objects to monitor, which metrics to track, what conditions trigger an alert, who to notify after triggering, and through which channels."

<span id="Et924udB"></span>
## Glossary


* **Alert object**: Specifies the services or instances being monitored in the alert rule, determining the effective scope of the alert. Currently supported alert objects include service, runtime, custom metrics, host, process, container, AI, and Claw.

* **Trigger policy**: Defines the alert triggering conditions. This is the core decision logic of the alert rule, directly affecting the sensitivity and accuracy of alerts. It typically includes monitoring metrics, statistical windows, alert thresholds, consecutive trigger counts, and other parameters.

* **Send policy**: The policy for sending notification messages after an alert is triggered, including rule evaluation frequency, send frequency, alert batch aggregation intervals, and other settings. Properly configuring the send policy helps filter out data spikes, reduces notification noise during frequent alerts, and prevents alert storms.

* **Notification policy**: Specifies the methods, channels, contacts, and alert content display formats for receiving notifications when alerts of different severity levels occur and when alerts are resolved.


<span id="XQJ0hrlH"></span>
## Resource relationships

Alert templates and preset alert templates contain only partial alert configurations. These resources not only consolidate scattered alert settings into reusable standards but also enable quick batch creation of alert rules, reuse of best practices, and improved configuration efficiency. The key alert configuration differences across various resources are as follows:


|Key settings |Alert rules |Preset alert templates |Alert templates |
|---|---|---|---|
|Alert object |✅ |❌ |❌ |
|Trigger policy |✅ |✅ |✅ |
|Send policy |✅ |✅ |✅ |
|Notification policy |✅ |❌ |❌ |


<span id="4PmGEgXo"></span>
## Alert rule creation methods

Server\-Side Monitoring provides multiple alert rule creation methods, allowing you to select the most suitable one based on your actual scenario.


* **Custom creation of alert rules**: If you wish to customize alert rules for specific scenarios or have only a small number of alert rules, we recommend manually creating alert rules directly. This does not compromise usage efficiency and allows for fine\-grained tuning of alert configurations. For procedure and configuration details, see Method 1 in [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).

* **Use preset alert templates**: If you lack established experience in alert configuration and want to set up an alert monitoring system quickly, we recommend directly using the standardized alert templates officially provided for rapid implementation. When using a preset alert template, you only need to provide the application scope and notification policy to complete all settings in the alert rule, allowing you to create alert rules quickly based on the preset alert templates. For procedure and configuration details, see Method 2 in [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).

* **Use custom alert templates**: If you already have established experience in alert configuration and want to reuse configurations within the same region while reducing duplicate creation of alert rules, follow the steps below to create and apply alert template groups, so you can turn that experience into standardized practices.

   1. [Create alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_an_alert_template_for_Server-side_Monitoring): Create alert templates based on accumulated experience, consolidating configurations such as alert type, alert severity, trigger policy, and send policy into templates for rapid reuse.

   2. **Use ** **alert templates**: Fill a custom alert template with the application scope and notification policy, and you will have all configurations in the alert rule complete. For procedure and configuration details, see Method 3 in [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).

* **Import/export alert rules via JSON:**  If suitable alert rules already exist in other projects and you wish to batch copy alert rules across accounts, regions, or projects, we recommend using the import/export feature to export Server\-Side Monitoring alert rules from other projects and then import them into the current project. For procedure and configuration details, see Method 4 in [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).
