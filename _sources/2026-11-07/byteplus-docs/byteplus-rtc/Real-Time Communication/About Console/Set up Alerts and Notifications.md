---
title: "Set up Alerts and Notifications"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-135773"
---

Alerts and notifications enable you to keep track of the RTC calls' quality and get informed of users' abnormal events promptly. You can get notified via e\-mail. This assists the operators, maintainers, and related roles in discovering issues and solving problems.

Before you can receive alerts, you must create alert rules. Each rule consists of one or more conditions that, when met, trigger an alert.

You get notified via e\-mail when an alert is triggered. You can also review all alert records on the RTC console.

<span id="create-alert-rules"></span>
## Create alert rules

Start with adding and applying custom rules. You can also enable Dynamic Threshold without applying your own rules or in addition to your rules.

<span id="custom-rules"></span>
### Custom rules

To create a new alert rule, go to RTC console \> Alerts \> Alert Rules, and click on New Rule.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/alert-rules.png) </span>

<span id="edit-a-rule"></span>
#### Edit a rule

Alert types include Quality, Real\-time metrics, and Events. Follow the rules below when you create and edit any rule.


* Keep the rules as simple as you can to avoid obscurity.

* Clear and precise alert severity helps maintainers identify seriousness and carry out related procedures quickly and precisely.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/quality-metrics-conditions.png) </span>

<span id="quality-metrics"></span>
##### Quality Metrics

Quality Metrics include indicators in Quality Metrics and User Feedback. Statistics of the day will not be ready until 10:00 AM tomorrow.


* We recommend you choose the default value for a condition. You can also refer to the average, minimum, and maximum values before deciding the alerting range for an indicator.

* You can add multiple conditions for an alert rule. AND means all these conditions should be met before an alert can be triggered. OR means when one of the conditions is met, it triggers an alert. Ten conditions at most can be added to a Quality Metrics alert rule.


You can specify online users and call duration as advanced filters to focus on the more important calls.


> * Online users include normal users and invisible users but exclude virtual users who join a room for the purpose of cloud media processing.

> * Advanced filters do not take effect when the concerning indicator is user feedback rate. The console ignores the advanced filters while dealing with the user feedback rate.


<span id="real-time-metrics"></span>
##### Real\-time Metrics

Real\-time Metrics include indicators for rooms or users. And if the conditions are met, an alert notification is triggered immediately.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/real-time-metric-conditions.png) </span>

Refer to the following table for the field descriptions.


|Field |Description |
|---|---|
|Rule settings |You can add multiple conditions for an alert rule. AND means all these conditions should be met before an alert can be triggered. OR means when one of the conditions is met, it triggers an alert. Ten conditions at most can be added to a Real\-time Metrics alert rule.<br><br>A cycle lasts 30 sec. To avoid false alarms triggered by an occasional fault, set the trigger condition to fulfill the value range in multiple cycles. As the example in the screen shot above, the alarm will be triggered if the success rate of joining room in 5 s \>= 90% in 3 cycles consecutively. |
|Do not disturb |Repeated alarms will not be triggered during this time period. |
|Validity period |Only between the time period can you get notified per the rules. |
|Scope of rules |The rule takes effect on all rooms or users. You can designate specific rooms or users to monitor. |


<span id="events"></span>
##### Events

Event alerts notified the following issues:


* Connectivity events, such as failure of joining a room, failure of sending the first frame, or failure of decoding the first frame.

* Device errors, such as CPU performance alarm, Weak Wi\-Fi signal.

> You can add multiple conditions for an alert rule. AND means all these conditions should be fulfilled before an alert can be triggered. OR means one of the conditions is fulfilled and can trigger the alert. Three conditions at most can be added to an event alert rule.


You can specify online users and call duration as advanced filters to focus on the more important calls.


> * Online users include normal users and invisible users but exclude virtual users who join a room for the purpose of cloud media processing.

> * Advanced filters do not take effect when the concerning event is No\-sound issue (BETA). The console ignores the advanced filters while dealing with No\-sound issue (BETA).


<span id="manage-rules"></span>
#### Manage rules

Click on Enable to activate the alert rule on RTC Console \> Alerts \> Alert Rules.


* Click on View \> Edit to modify the existing rules.

* If an alert rule is no longer needed. You can disable it and then delete it.

* However, modifying and deleting alert rules will not clear the records that are logged.


<span id="beta-dynamic-threshold"></span>
### [BETA] Dynamic Threshold

Dynamic Threshold empowers the Alerts and Notifications so that you can monitor the quality metrics without adding alert rules by yourself. And it is based on the principle of statistics and normal distribution, which can effectively filter the interference data so that only true bad indicators are reported.

The indicators monitored by Dynamic Threshold are subject to change with the update of the statistical algorithms. The calculation scales of the indicators are consistent with those in the quality overview.


1. To enable Dynamic Threshold, go to RTC Console \> Alerts \> Dynamic Threshold and then click on TRY NOW.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/dynamic-threshold.png) </span>


2. Choose an appID or a business ID.

> Click on Add Apps if you intend to enable Dynamic Threshold for multiple apps or business IDs.


3. Set the alert time and click OK to apply the changes.

* Even after you enable Dynamic Threshold, you can modify the settings or delete them.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/modify-alert-rules.png) </span>


* Alarms generated by Dynamic Threshold are logged as Dynamic Threshold type. Check them in the Alert Records.


<span id="how-to-get-notifications"></span>
### How to get notifications

You can get notifications from the followings.


* Email: You will receive alert messages via Email by default. The Email address that is related to your BytePlus account. You can change the email address [here](https://console.byteplus.com/user/security).

* Bot on Lark, WeCom, and DingTalk: You must provide the webhook URL of the Bot and enable the Bot.

* Callback: Provide the URL to receive the callback, such as the webhook URL of your custom Bot.

   Parse the request body as you receive the callback to get the alert message and related information. The following table provides the description on each item in the request body in JSON.



|**Item** |**Description** |
|---|---|
|AppId |Your App ID which you can read from the [RTC Console](https://console.byteplus.com/rtc/listRTC). |
|BusinessId |Business ID you have set for your app. |
|AlertType |Alert type<br><br><br>* Quality: `QualityAlert`<br><br>* Realtime: `RealtimeAlert`<br><br>* Event: `EventAlert` |
|Timestamp |UTC timestamp standing for the time when the alert is generated. In the RFC 3339 format, dates and times are represented in the following format: YYYY\-MM\-DDTHH: MM:SSZ, where T is the separator between the date and time, and Z indicates the time is in Coordinated Universal Time (UTC). |
|AlertName |Name of the alert rule |
|RoomId |Room ID. You can get this item when the alert type is Realtime or Event. |
|UserId |User ID. You can get this item when the alert type is Realtime or Event on user scale. |
|AlertRule |Indicates the alert rule that triggered this alert message. |
|url |The url varies from different alert types.<br><br><br>* For quality metrics: The related metrics on [Quality overview](https://console.byteplus.com/rtc/callQualityRTC/qos)<br><br>* For the User feedback rate: The related metrics on [User feedback](https://console.byteplus.com/rtc/callQualityRTC/feedback)<br><br>* Realtime metrics and Event: The [Diagnostic tool](https://console.byteplus.com/rtc/callQualityRTC/diagnosis). It directs to room details if the alert is on room scale while to user details if it is on user scale. The diagnostic report shows details from the perspective of a subscriber. However, for indicators related to the first frame, the report is from the perspective of a publisher. |


<span id="review-alert-logs"></span>
## Review alert logs

> To prevent false alarms, fluctuations from small sample sizes are considered low\-confidence and are not logged.


To review alert logs, go to RTC Console \> Monitor \> Alerts \> Alert Records.


* Choose an Appid or business ID to filter the records in the logs.

* Click the filter icon and choose a condition to filter.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Console/alerts/alert-records.png) </span>


* Click Details to view the historical data.

* Click View Rules to redirect to the Diagnostic Tool, where you can analyze the issue.


<span id="resolve-alert-records"></span>
### Resolve Alert Records

You can mark an alert record as Resolved when the problem has been solved, or it doesn't need to be focused on. To change the state of a record, select a new state for it in the state list which is located on the right of the table.
