---
title: "Alert"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/FAQs-about-alarm-strategies"
---

<span id=".5ZGK6K2m6IGU57O75Lq65pSv5oyB5ZOq56eN6YCa55-l5pa55byP77yf"></span>
## What alert notification methods are supported?

Alert notifications can be received through phone calls, SMS messages, emails, Feishu, DingTalk, and WeCom. For more details, refer to the following topics:


* [Receiving alert notifications through the Feishu group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Receiving alert notifications through the DingTalk group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Receiving alert notifications through the WeCom group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)


<span id=".5ZGK6K2m6IGU57O757uE5a-557uE5YaF6IGU57O75Lq65Liq5pWw5pyJ6ZmQ5Yi25ZCX77yf"></span>
## What are the limits on the number of contacts in an alert contact group?


* A single contact can be added to up to 10 contact groups.

* The number of contacts in a single contact group is not limited.


<span id=".5pSv5oyB5a-55ZOq5Lqb5LqR5Lqn5ZOB6K6-572u5ZGK6K2m562W55Wl77yf"></span>
## Which cloud products support configuring alert policies?

Currently, many cloud products support alert policies. For specific details, see [Cloud product metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

<span id="646957c2"></span>
## How is an alert recovery notification triggered?


* For an alert, if a resource generates no alert for 5 consecutive minutes, the alert is deemed cleared. In this case, an alert recovery notification is triggered.

* For a NoData alert, if a resource resumes data reporting for 5 consecutive minutes, the alert is deemed recovered, and an alert recovery notification is triggered.


<span id="2bd84a83"></span>
## Can the same alert policy be used in different regions?

If the trigger condition of a pre\-configured alert template meets your expectations, you can enable the pre\-configured alert template with one click to automatically generate the corresponding alert policy. The enabled preset alert template will be applied to all regions and all resources.

<span id="c6fc0384"></span>
## Why does the alert notification indicate two resources are affected, but only one resource is listed in the affected resources list?

When you select **Rule and Resource** for **Notification aggregation policy** for your alert policy, the timelines for sending alert notifications for each resource may not align. As a result, even if two resources are continuously alerting, the system checks the notification cycle for each resource and excludes silenced resources each time it sends an alert.
