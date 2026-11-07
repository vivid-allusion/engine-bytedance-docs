---
title: "Configuring an alarm strategy"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Configure-alert-policies"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can configure an alarm strategy for the Bandwidth Package on the Cloud Monitor platform to promptly detect critical events and exceptions, ensuring stable business operation. You can set alarm strategies for Bandwidth Packages or use preset alarm templates provided for Bandwidth Packages.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created alarm contacts and groups on the CloudMonitor platform. For specific procedure, see [Creating an alarm contact and group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

* IAM users may be unable to directly configure alarm strategies. To configure, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf). Grant CloudMonitor administrative permissions to the IAM user.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation pane, select **Alarm Center \> Alarm Template**.

3. Select the **Preset alert template** tab.

4. Type the **name** of search condition in the search box, **Bandwidth Package**, to find the target template.

5. You can click **Bandwidth Package preset alarm template**, the preset template name, to view the trigger condition details and confirm whether this template meets your requirements.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the preset alarm template does not meet your needs, you can see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template">Create an alarm template</a> to create and enable a template that meets your requirements, or see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Create an alarm strategy</a> to modify a preset alarm template into an alarm strategy that meets your requirements.   </div>
   

6. Click the switch in the **Enable** column to the right of the template, or click **Enable** on the template details page to enable the alarm template.

7. In the **Configure contact groups** pop\-up window, specify your expected channel to receive alarm notifications, and click **Apply** to complete the configuration.

   > You can configure contacts for receiving alarms based on [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-contacts).   
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you turn on the switch in the Enable column, the system automatically generates and applies the corresponding alarm strategy to all Bandwidth Package resources under this BytePlus account. After you turn off the switch, the system deletes all alarm strategies generated from the preset alarm template accordingly. For more details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center">Using the Alarm Center</a>.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[SetStateOfRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds): Enable or disable a preset alarm template for Bandwidth Package.
