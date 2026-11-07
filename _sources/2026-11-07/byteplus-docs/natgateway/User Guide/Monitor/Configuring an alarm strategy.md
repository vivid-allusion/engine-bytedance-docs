---
title: "Configuring an alarm strategy"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Configuring_an_alert_policy"
---

You can configure alarm strategies for Internet/VPC NAT Gateways on the CloudMonitor platform. This helps detect exceptions promptly and ensure stable business operations. You can either configure these strategies or use preset alarm templates. For detailed monitoring metrics of Internet/VPC NAT Gateways, see [Internet NAT Gateway monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_NAT) and [VPC NAT Gateway monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_PrivateNAT)

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created alarm contacts and groups on the CloudMonitor platform. For specific procedure, see [Create a contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

* IAM users may be unable to directly configure alarm strategies. To configure, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf). Grant CloudMonitor administrative permissions to the IAM user.


<span id=".6YWN572u5oyH5qCH5ZGK6K2m"></span>
## Configure metric alarms


1. Log in to [the Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation pane, select **Alarm Center \> Alarm Template**.

3. Select the **Preset alert template** tab.

4. Specify the search condition Name in the search box and input NAT Gateway to find the target template.

5. You can click the name of the Internet NAT Gateway preset alert template or the VPC NAT Gateway preset alert template to view detailed alert\-triggering rules and confirm whether the template meets your alert requirements.

   * **Internet NAT Gateway preset alarm template**

   * **VPC NAT Gateway preset alarm template**

6. Click the switch in the **Enable** column to the right of the template, or click **Enable** on the template details page to enable the alert template.

7. In the **Configure contact groups** pop\-up window, specify your expected channel to receive alarm notifications, and click **Apply** to complete the configuration.

   > You can configure contacts for receiving alarms based on [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-contacts).   
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[SetStateOfRulesByIds](https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds): Enable or disable the Internet NAT Gateway preset alarm template.
