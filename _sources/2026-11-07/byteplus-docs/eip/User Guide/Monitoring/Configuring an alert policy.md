---
title: "Configuring an alert policy"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Configure-alert-policies"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can configure alert policies for an Elastic IP Address (EIP) on the Cloud Monitor console to promptly detect exceptions and ensure stable business operation, or use the preset alert templates provided for the EIP. For more details on EIP monitoring metrics, see [EIP monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_EIP).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* You have created alarm contacts and groups on the Cloud Monitor console. For detailed steps, see [Create a contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

* IAM users may be unable to directly configure alert policies. To grant Cloud Monitor management permissions to the IAM user, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf).


<span id=".6YWN572u5oyH5qCH5ZGK6K2m"></span>
## Configure metric alarms


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation pane, select **Alarm Center \> Alarm Template**.

3. Select the **Preset alert template** tab.

4. Specify the search condition **Name** in the search box and enter **Elastic IP** to find the target template.

5. Click the preset template name (**Elastic IP preset alarm template)**  to view detailed rules for triggering alarms and confirm whether this template meets your alarm requirements.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the preset alarm template does not meet your needs, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template">Create an alarm template</a> to create and enable a suitable alarm template, or see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a> to modify a preset alarm template into an alarm policy that meets your requirements.   </div>
   

6. Click the toggle in the **Enable** column on the right side of the template list, or click **Enable** on the template detail page to enable the alert template.

7. In the **Configure contact group** popup, specify the preferred notification channels for receiving alarm notifications, then click **Apply** to complete the configuration.

   > You can see [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-contacts) to configure the contacts and their contact information for receiving alarms.   
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you turn on the toggle in the <strong>Enable</strong> column, the system automatically generates and applies the corresponding alarm policy to all EIP resources under this BytePlus account. After you turn off the toggle, all alarm policies generated from the preset alarm template are deleted accordingly. For more details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center">Using Alarm Center</a>.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[SetStateOfRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds): Enable or disable an EIP preset alert template.
