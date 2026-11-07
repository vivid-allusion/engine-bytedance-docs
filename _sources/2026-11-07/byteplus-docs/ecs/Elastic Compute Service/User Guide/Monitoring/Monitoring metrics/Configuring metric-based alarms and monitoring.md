---
title: "Configuring metric-based alarms and monitoring"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics"
---

The system provides pre\-configured alarm templates for CPU and disk resource usage of ECS instances. You can enable them with one click and immediately receive alarm notifications for instance resources.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created an [ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have enabled [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Cloud Monitor console.](https://console.byteplus.com/cloud-monitor) 

2. In the left navigation pane, select "Alarm Center \> Alarm Template".

3. Select the "Preset alarm template" tab.

4. In the search box, specify the search condition as "Name", and input "ECS preset alarm template" to find the target template.

5. You can click the name of the preset template "ECS preset alarm template" to view information such as the resource type (ECS instance), dimension, and trigger condition for alarms. Then, confirm whether this template meets your requirements.

   > If the preset template rules can not meet your requirements, you can also create an alarm template yourself by following the instructions in [Creating an alarm template](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template).   
   

6. Click the "Enable" button to the right of "ECS preset alarm template", or click the "Enable" button on the template details page to enable the target alarm template.

7. In the "Configure contact groups" pop\-up window, specify the channel you need to receive notifications. Then, click the "Confirm" button to complete the configuration.

   > You can configure the recipient of alarms and contact information based on [Alarm contacts](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-contacts).   
   

8. When you click the "Enable" button, alert strategies are automatically generated and enabled for all ECS instance resources under the account. When you disable the function, all alert strategies generated from preset alarm templates are immediately deleted. For more details, refer to [Alarm Center user guide](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center).


<span id=".55u45YWz5pON5L2c"></span>
## Related operation

If the preset alarm templates can not meet your requirements, you can click the "Create alert strategy" button. There, you can create a custom alert strategy. For more information, refer to [Creating an alert strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
