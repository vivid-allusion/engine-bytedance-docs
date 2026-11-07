---
title: "Alert management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Alert_management"
---

Server\-side Monitoring provides alerting and monitoring capabilities for resources within AgentKit, such as agent runtimes and tools. You can use preset alert templates provided by the system to create alert tasks quickly or create custom alert tasks. This topic describes how to quickly create alert tasks and monitor the health status of services in real time.

<span id="1L71BLOU"></span>
## Prerequisites


* Server\-side Monitoring has been activated. For detailed steps, see [Activating Server-side Monitoring](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).

* You have prepared notification channels as needed, such as an email address, a Webhook URL, or a publicly accessible alert callback URL.


<span id="dlojddz9"></span>
## Limits

Alert rules in preset alert templates cannot be modified.

<span id="TijydDxH"></span>
## Procedure


<Tabs>
<Tab zoneid="Ea3JTEEL4G" title="Method 1: Apply a preset alert template">
<TabTitle>Method 1: Apply a preset alert template</TabTitle>

1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Alert template**. You will be redirected to the preset alert template page in Server\-side Monitoring. Then, you can view the preset alert templates provided by the system.

4. Click **Application** in the Actions column on the right side of the target template to go to the **Alerting rule** tab on the Template details page. Then, you can view the detailed configuration of the alert rules.

5. Select the **Application scope** tab and click **Add application scope** to configure the alert application scope. You can quickly filter AgentKit\-related services by platform and service name. For configuration details, follow the guide in [applying a preset alert template](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

6. Return to the preset alert template details page, and click **Submit** in the alert change notification. The system will automatically create an alert task based on the configuration and monitor metric status in real time.


</Tab>
<Tab zoneid="lntufzDoa9" title="Method 2: Create a custom alert template">
<TabTitle>Method 2: Create a custom alert template</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select **Alarm Management \> Alarm Template** in the left navigation bar to go to the alert template management page.

3. Click the **Alarm template** tab, and **Create alert template**. Configure the basic information to create an alert template of the AI type.

4. Return to the alert template management page, and click **Edit** in the Actions column to the right of the target alert template.

5. Click the **Alerting rule** tab and the **Add alerting rule** button in sequence. Configure the alert rule name, alert policy, notification policy, and other details as needed. All AI\-related alert metrics are listed in the alert query section. For configuration details, follow the guide for [creating an alert template](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

6. Select the **Application scope** tab and click **Add application scope** to configure a detailed alert application scope. You can quickly filter AgentKit\-related services by platform and service name. For configuration details, follow the guide for [creating an alert template](https://docs.byteplus.com/en/docs/apmplus/Alert_templates).

7. Return to the alert template details page, and click **Submit** in the alert change notification. The system will automatically create an alert task based on the configuration and monitor metric health status in real time.





</Tab>
<Tab zoneid="U6eM21u6Ay" title="Method 3: Create an alert task">
<TabTitle>Method 3: Create an alert task</TabTitle>

1. Log in [to the Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select **Alarm Management \> Alarm Task** in the left navigation bar to go to the alert template management page.

3. Click **Create alerting task** and configure the alert task as needed. You can quickly filter AgentKit\-related services by selecting AI and specifying a platform. The alert query section lists all AI\-related metrics. For configuration details, follow the guide for [creating an alert task](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).





</Tab>
</Tabs>


<span id="W04ENyKW"></span>
## What to do next


* Go to the alert task page and click the target alert task name to view the alert trend, alert history, and other alert details. For more details, see [Alert tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* Go to the alert history page and filter the target alert task. Then, you can view an overview of the alert conditions, alert distribution trend, and other details of the target alert task within the specified time period. For more details, see [Alert history](https://docs.byteplus.com/en/docs/apmplus/Alert_history).
