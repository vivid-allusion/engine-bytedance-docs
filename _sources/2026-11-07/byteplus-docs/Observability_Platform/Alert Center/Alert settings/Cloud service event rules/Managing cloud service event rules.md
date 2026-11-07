---
title: "Managing cloud service event rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_cloud_service_event_rules"
---

This topic describes various operations supported by cloud service event rules.

<span id="P1qPjFm7"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the "Alert Configuration" page.

3. In the alert configuration section on the left, select **Cloud Service Event** and click the **Event Rule** tab.

4. Click a button in the "Actions" column that corresponds to the target cloud service event rule to perform the corresponding operation. The currently supported management operations are as follows:

   
   |Actions |Description |
   |---|---|
   |Edit |Modify the configuration of an existing cloud service event rule. For detailed descriptions of parameters, see [Creating cloud service event rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_cloud_service_event_rules). |
   |Enable/Disable |The switch for detecting monitoring metric data, which can be manually enabled or disabled based on actual scenarios.<br><br><br>* **Enable**: You can re\-enable a rule that is in the "Disabled" state. After a rule is re\-enabled, it will continue monitoring and delivering cloud service events based on the configured effective period, delivery channel, and other conditions.<br><br>* **Disable**: You can disable a rule that is in the "Enabled" state. After a rule is disabled, it will no longer take effect and will not deliver cloud service events. |
   |Delete |Delete a cloud service event rule that is no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted cloud service event rules cannot be recovered. Proceed with caution.</div><br> |
