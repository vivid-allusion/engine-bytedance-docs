---
title: "Managing Server-side Monitoring alert templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_Server-side_Monitoring_alert_templates"
---

This topic describes the various operations supported for Server\-side Monitoring alert templates.

<span id="vtrhzatX"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, select **Alert Center \-\> Alert settings** to open the "Alert settings" page.

3. In the alert configuration section on the left, select **Server\-side Monitoring**, and go to the **Alert template** tab.

4. Click the button in the "Actions" column for the target Server\-side Monitoring alert template to perform the corresponding action. The currently supported management operations are as follows:

   
   |Actions |Description |
   |---|---|
   |Edit |Modify the configuration of an existing Server\-side Monitoring alert template. For detailed descriptions of configuration items, see [Creating Server-side Monitoring alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_an_alert_template_for_Server-side_Monitoring). |
   |Copy |Quickly create a new template based on an existing alert template. For more details, see Method 2 in [Creating Server-side Monitoring alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_an_alert_template_for_Server-side_Monitoring). |
   |Delete |Delete Server\-side Monitoring alert templates that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Deleted Server\-side Monitoring alert templates cannot be recovered. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the template cannot be directly deleted. You need to first delete the associated alerting rule group before deleting the template.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the configuration modification of variables and rules will be restricted.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Variables</strong>: You cannot create variables or delete existing variables. You can only edit the query statements, default values, and match expressions of the variables.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Rule</strong>: You cannot delete existing rules. You can only edit the rule name, description, and trigger condition. You can add new rules.</div><br> |
