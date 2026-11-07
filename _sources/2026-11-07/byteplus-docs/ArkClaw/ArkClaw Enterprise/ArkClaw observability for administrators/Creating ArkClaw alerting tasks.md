---
title: "Creating ArkClaw alerting tasks"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_alerting_tasks"
---

APM provides alerting and monitoring capabilities for ArkClaw instances. It not only supports the creation of custom alert tasks but also enables the quick creation of alert tasks using system\-provided preset alert templates. This topic describes how to quickly create alerting tasks and monitor the health status of ArkClaw instances in real time.

<span id="IrP1vpAe"></span>
## Prerequisites


* The APM service has been activated. For more details, see [Activating APM](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).

* A notification receiving method has been prepared based on your business requirements, such as an email address, a Webhook address, or a publicly accessible alert callback address.


<span id="IOFWskt5"></span>
## Limits

You cannot modify alert rules in preset alert templates.

<span id="9Po3DZht"></span>
## Procedure


<Tabs>
<Tab zoneid="jF4Dy39N" title="Method 1: Apply preset alert templates">
<TabTitle>Method 1: Apply preset alert templates</TabTitle>

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click **Claw Management \> Claws**.

3. Click the name of the target ArkClaw instance to go to the instance details page.

4. Click **Alert Template** and click Preset alert template. Then, you can view the alert templates preset by the system for ArkClaw.

5. Click **Application** in the Actions column that corresponds to the target template to go to the **Alert rule** tab of the details page for the preset alert template and view the detailed configurations of the alert rule.

6. Click the **Application scope** tab and then click **Add application scope** to configure the application scope of the alert. You can quickly filter ArkClaw\-related services by platform and service name.  For the detailed descriptions of the configuration, see [Application preset alert templates](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

7. Go back to the details page of the preset alert template, and click **Submit** in the alert modification prompt. The system will automatically create alert tasks based on the configuration and monitor the health status of the metrics in real time.


</Tab>
<Tab zoneid="ZSwq2QDx" title="Method 2: Configure custom alert templates">
<TabTitle>Method 2: Configure custom alert templates</TabTitle>

1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server).

2. In the left navigation pane, click **Alert Management \> Alert Template** to go to the alert template management page.

3. Click the **Alert template** tab and then click **Create alert template**. Configure basic information to create an alert template of the Claw type.

4. Go back to the Alert template page. Click **Edit** in the Actions column that corresponds to the target alert template.

5. Click the **Alert rule** tab and then click **Add alert rule**. Configure the details of the alert rule based on your business requirements, such as the alert rule name, alert policy, and send policy. You can view all AI\-related alert metrics from the Alert query drop\-down list. For the detailed descriptions of the configuration, see [Creating alert templates](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

6. Click the **Application scope** tab and then click **Add application scope** to configure the detailed application scope for the alert. You can quickly filter ArkClaw\-related services by platform and service name.  For the detailed descriptions of the configuration, see [Applying preset alert templates](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

7. Go back to the alert template details page, and click **Submit** in the alert modification prompt. The system will automatically create alert tasks based on the configuration and monitor the health status of the metrics in real time.


</Tab>
<Tab zoneid="DFt4dBtV" title="Method 3: Create alert tasks">
<TabTitle>Method 3: Create alert tasks</TabTitle>

1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server).

2. In the left navigation pane, click **Alert Management \> Alert Task** to go to the alert template management page.

3. Click **Create alert task** and configure the alert task details. You can quickly filter services by Claw tag and platform and view all ArkClaw\-related alert metrics from the Alert query drop\-down list. For the detailed descriptions of the configuration, see [Creating alert tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).


</Tab>
</Tabs>


<span id="6igqLoSF"></span>
## What to do next


* Go to the Alert task page. Click the name of the target alert task to view alert details such as alert trend charts and alert history. For more details, see [Viewing alert details](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* Go to the Alert records page. Filter for the target alert task, and view the details of the target alert task within a specified time period, such as the overview of the alert status and alert distribution trend charts. For more details, see [Alert history](https://docs.byteplus.com/en/docs/apmplus/Alert_history).
