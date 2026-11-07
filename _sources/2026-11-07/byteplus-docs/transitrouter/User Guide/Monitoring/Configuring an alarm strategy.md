---
title: "Configuring an alarm strategy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Configuring-an-alert-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

By configuring alarm strategies for your Transit Router (TR), you can promptly detect exceptions in its monitoring metrics, ensuring stable and smooth operation of your services. You can customize alarm strategies for TR instances and bandwidth packages, or use the pre\-configured alarm templates provided by TR.

We recommend using the pre\-configured templates. This not only improves configuration efficiency but also allows you to copy a template and adjust it flexibly according to your needs.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

IAM users may be unable to directly configure alarm strategies. To configure, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instance-faq#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf). Grant CloudMonitor administrative permissions to the IAM user.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the Cloud Monitor console.

2. In the left navigation pane, select **Alarm Center \> Alarm Template**.

3. Select the **Preset alert template** tab.

4. Type the **name** of the preset template in the search box, and select **TransitRouter** from the dropdown to find the target template.

5. You can click the name of the preset template, such as **TransitRouter preset alarm template**, to view detailed rules for triggering alarms and confirm whether this template meets your requirements.

   If the preset alarm template does not meet your needs, you can see [Create an alarm template](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template) to create a suitable alarm template and enable it, or see [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) to modify the preset alarm template to a suitable strategy.

6. Click the switch in the **Enable** column to the right of the template, or click **Enable** on the template details page to enable the alarm template.

7. In the **Configure contact groups** pop\-up window, specify the alarm channel where you expect to receive notifications.

8. Click **Create** to complete configuration.

   You can configure contacts for receiving alarms based on [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-contacts).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you turn on the switch in the Enable column, the system automatically generates and applies the corresponding alarm strategy. After you turn off the switch, the system deletes all alarm strategies generated from the preset alarm template accordingly. For more details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center">Using the Alarm Center</a>.</div>



* <div data-tips="true" data-tips-type="tip">Enable <strong>TransitRouter preset alarm template</strong> with one click: The system automatically generates 3 alarm strategies, each applied to all TR instances, attachments, and inter\-region attachments under this BytePlus account.</div>


* <div data-tips="true" data-tips-type="tip">Enable <strong>TransitRouterBandwidthPackage preset alarm template</strong> with one click: The system automatically generates 1 alarm strategy applied to all TR bandwidth packages under this BytePlus account.</div>



<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[SetStateOfRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds): Enable or disable a TR preset alarm template.
