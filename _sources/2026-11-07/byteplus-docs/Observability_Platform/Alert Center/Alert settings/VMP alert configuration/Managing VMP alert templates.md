---
title: "Managing VMP alert templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_VMP_alert_templates"
---

This topic describes the operations that you can perform on VMP alert templates.

<span id="wrZX0xHk"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click ** Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select ** VMP** and click the ** Alert Template** tab.

4. Click the button in the "Actions" column for the target VMP alert template to perform the corresponding action. The currently supported management operations are as follows:

   
   |Actions |Description |
   |---|---|
   |Apply template |Configure the workspace, notification policy, and aggregation policy, and then apply the alert template. Based on the template, alert rules and one alert rule group are automatically generated to monitor resources. For detailed descriptions, see [Creating VMP alert rule groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rule_groups). |
   |Edit |Modify the configuration of an existing VMP alert template. For detailed descriptions of parameters, see [Creating VMP alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_templates). |
   |Delete |Delete VMP alert templates that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Deleted VMP alert templates cannot be recovered. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the template cannot be directly deleted. You need to first delete the associated alerting rule group before deleting the template.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the configuration modification of variables and rules will be restricted.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Variables</strong>: You cannot create variables or delete existing variables. You can only edit the query statements, default values, and match expressions of the variables.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Rule</strong>: You cannot delete existing rules. You can only edit the rule name, description, and trigger condition. You can add new rules.</div><br> |
