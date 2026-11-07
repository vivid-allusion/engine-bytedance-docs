---
title: "Managing VMP alert rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_VMP_alert_rules"
---

This topic describes the operations that you can perform on VMP alert rules.

<span id="W82MyBRG"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration ** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP ** and click the **Alert Rule ** tab.

4. Click the button in the "Actions" column for the target VMP alert rule to perform the corresponding action. The currently supported management operations are as follows:

   
   |Actions |Description |
   |---|---|
   |Alert history |View the alert records and detailed information triggered by the current alert rule. For more details, see [Viewing VMP alert events](https://docs.byteplus.com/en/docs/Observability_Platform/Alert_event). |
   |Notification history |View the notification message records and detailed information triggered by the current alert rule. For more details, see [Viewing VMP notification history](https://docs.byteplus.com/en/docs/Observability_Platform/Notification_history). |
   |Edit |Modify the configuration of an existing VMP alert rule. For detailed descriptions of parameters, see[ Creating VMP alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules). |
   |Enable/Disable |The switch for detecting monitoring metric data, which can be manually enabled or disabled based on actual scenarios.<br><br><br>* **Enable**: Re\-enable a rule that is in the disabled state. Once enabled, the rule continues monitoring based on the configured conditions.<br><br>* **Disable**: Disable a rule that is in the enabled state. Once disabled, the rule no longer takes effect. |
   |Delete |Delete VMP alert rules that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted VMP alert rules cannot be recovered. Proceed with caution.</div><br> |
