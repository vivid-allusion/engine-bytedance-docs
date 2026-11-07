---
title: "Anti-fraud settings"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/anti_fraud_with_verification_codes"
---

Verification code fraud occurs when attackers repeatedly request OTPs to exploit messaging systems, causing sudden traffic surges and potential financial losses. This document identifies common fraud patterns, explains the need for anti\-fraud protection, and provides configuration recommendations to mitigate risks.

<span id="9c463ae1"></span>
### Characteristics of frauds

The following are some common characteristics of fraudulent activities:


* Sequential Number Spamming: Attackers generate consecutive phone numbers (e.g., +1111111110, +1111111111) to flood messaging systems with bulk requests to inflate traffic volume.

* Sudden Traffic Surges: There are abnormal spikes in message volume from specific regions or operators, often with low conversion rates.

* Timing of Frauds: Frauds often occur at nights and on holidays.

* Targets of Frauds:

   * Small\-scale applications, new APIs, or untested scenarios

   * Small\-scale telecom operators or high\-cost operators in less\-developed countries.


<span id="316c1d21"></span>
### Reasons for anti\-fraud settings

SMS frauds have become one of the core threats to businesses:


* Direct financial loss: Fraudulent activities like OTP flooding and bot\-driven bulk registrations result in a large number of unnecessary SMS fees.

* Damaged user experience: Users may fail to register due to OTP frequency limits (triggered by attacks) or develop negative brand impressions from SMS bombing.


BytePlus Messaging aims to shift enterprises from "reactive response" to "proactive interception" through automated and intelligent defenses.

<span id="57f052ae"></span>
### Configure anti\-fraud settings

To activate anti\-fraud protections, use these key settings in the BytePlus console:


|Enhance End\-User Authentication |* **Collect Client\-Reported Information**: Analyze specific characteristics and perform targeted filtering and interception. For example, check for IP clusters, number segment clusters, concentrated client versions, and IMSI forgery identification;<br><br>* **Add Human\-Interaction Verification Features**: Implement CAPTCHA, slider verification, character verification, line connection verification, and other interactive features;<br><br>* **Set Cooling Time Between Repeated Requests**;<br><br>* **Cooling Time for Promotional Activities**: Some fraudulent activities are related to promotional campaigns. Consider adding a cooling time for new users participating in such activities. |
|---|---|
|Ensure Account Security |* **Set an IP Whitelist**: You can provide your requested IPs to BytePlus for IP whitelisting. Once set, BytePlus will intercept requests from non\-whitelisted IPs;<br><br>* **Regularly Change API Access Keys**: This prevents malicious usage and fraud by unauthorized parties.<br><br>   * For BytePlus SDK users, go to [IAM-Access Key Management](https://console.byteplus.com/iam/identitymanage/user) to set it up as shown below:<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ee710be7bc34afaa324d04bb0dd2948~tplv-goo7wpa0wc-image.image) </span><br><br>   * For BytePlus openAPI users, go to [BytePlus Messaging - Message Group](https://console.byteplus.com/sms/subaccount/list?subAccountId=75036172&projectName=) module as shown below:<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec942ebcfa8c4ea0bfd9302edf0e00d5~tplv-goo7wpa0wc-image.image) </span> |
|Increase rate limit |* **Set Rate Limits for Your Service**: Configure the maximum number of messages a single phone number can receive per minute, hour, or 24 hours. Note that rate limiting does not prevent attacks; it only blocks requests that exceed the rate limit. To set this up, go to [BytePlus Messaging - Settings - Frequency Control](https://bytedance.larkoffice.com/docx/EIoIdbu1IorlVyxZRfMc20J3nng#share-EwA5dCoM4o1n6vxRLW7chzjbnZe):<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b24bff0a4ba4694985c77fbe3ea9c50~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Set Rate Limits for Individual IPs**. |
|Disable messaging for unintended countries/regions |If your business does not involve certain countries/regions, or you do not intend to send messages to specific countries/regions, it is recommended to log in to the Volcengine console and set those countries/regions as restricted. Once set, Volcengine will intercept messages sent to those regions.<br><br>**How to Set This Up:** <br><br>**Sub\-account (Message Group) Level**:<br><br><br>1. Go to the [Message Group List](https://console.byteplus.com/sms/subaccount/list?subAccountId=75036172&projectName=) page in the BytePlus Messaging console and click "Edit";<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9222ca3c87b14271914b82c6d5828203~tplv-goo7wpa0wc-image.image) </span><br><br><br>2. Click **Markets Allowed to Send** to set the allowed countries/regions.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff1189cb9d7848528f7956b5b85e88c4~tplv-goo7wpa0wc-image.image) </span> |
|Set sending limits |If you can estimate the daily messaging volume for your account or a specific country/region, you can set alert thresholds and sending limits. When the alert threshold is reached, a notification will be sent to a designated contact. When the sending limit is reached, messages will be intercepted. However, please carefully set the interception limits to ensure they do not affect your normal business operations.<br><br><br>* **Set Alert or Sending Limits**: This can be configured based on the Volcengine main account, message group, country/region, or Messaging type. To set this up, go to [BytePlus Messaging - Delivery Threshold](https://console.byteplus.com/sms/send-limit/oversea):<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dde7aa1d2dee498aacedbcc9e4034351~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Set Alert Contacts**: Configure this under [BytePlus Messaging - Alert Notification Contact](https://console.byteplus.com/sms/alarm-config).<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1585eb574f31409986c47e1d7e907a56~tplv-goo7wpa0wc-image.image) </span> |
