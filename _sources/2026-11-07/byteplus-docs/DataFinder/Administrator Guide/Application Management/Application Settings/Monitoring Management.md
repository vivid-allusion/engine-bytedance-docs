---
title: "Monitoring Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Monitoring_Management"
---

In the Dashboard board of the BytePlus Growth Analysis platform, you can create monitoring tasks to achieve dynamic data monitoring, automatically determine whether the indicator fluctuates within the normal range according to the monitoring rules, and trigger alarms (emails, group messages) when there is an abnormality. There is no need for manual daily tracking and judgment, and automated monitoring is realized to help you pay attention to the fluctuations in various data dimensions of key data in real time.

<span id="da054f22"></span>
# Notes: Chart requirements to support monitoring


|**Chart requirements** |**Detailed description** |
|---|---|
|Analysis tool limitations |When using analysis tools for analysis, you can save the analysis chart to the Dashboard, and then use the monitoring task to monitor the data of the corresponding Dashboard. The currently supported analysis tools are as follows:<br><br><br>* Event Analysis<br><br>* Custom Retention<br><br>* Funnel Analysis<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cb2471497a0490b90341ae85ceb3056~tplv-goo7wpa0wc-image.image) </span> |
|Time frame requirements for analyzing data |When monitoring chart data, monitoring of data **based on time dynamic changes** is currently supported, namely:<br><br><br>* **Heaven level**: Under the time unit of heaven level:<br><br>   * When the analysis time of the chart is **today**, the **past 7 days**, the **past 5 days** and other dynamic ranges, the chart can be monitored.<br><br>   * If the analysis time of the chart is fixed **2023.12.01~ 2023.12.07** , the monitoring of the chart is not supported.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In this scenario, the analysis time of the chart is fixed, the chart data is fixed, and there is no need for data monitoring at the business level.      </div><br>      <br><br>* **Hour level** & **5 minute level**: In the time unit of hour and 5 minute level, the time range of the chart needs to include **today** in order to support data monitoring of the chart.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/117326e391b446c7b3e6645ef3fcb2f0~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">At present, only SaaS\-cloud native cloud hosting scenarios support 5\-minute monitoring capabilities, and the function is turned off by default. If you need to use it, you can contact BytePlus technical support staff for evaluation and activation. If you are using another environment, the 5\-minute monitoring capability is not currently supported.   </div><br>    |


<span id="b7417d7a"></span>
# Prerequisite


* The chart to be monitored has been saved as a Dashboard chart.

* Already have monitoring\-related operation permissions, that is, be added as a group member or administrator. For details of the operation permissions of different roles to monitoring, please refer to the following **reference: Monitoring operation permissions details** .


<span id="b9c7eca5"></span>
# Create a monitoring portal


|**Entry 1: Analysis Tools Page** |**Entry 2: Dashboard Page** |
|---|---|
|On the Supported Analysis Tools page, after saving the analysis chart to the Dashboard board, you can click the " **Monitoring Data** " button to add monitoring tasks.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2fa5da6e3b84e7fb419054939cb837b~tplv-goo7wpa0wc-image.image) </span> |On the Dashboard page, for charts that meet the monitoring conditions, click the upper right corner of the chart  **...**  \> **Add monitoring tasks** to enter the chart monitoring task configuration page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f1518b73762475abbf311b9185b6b33~tplv-goo7wpa0wc-image.image) </span> |


<span id="d103fc28"></span>
# **Configure monitoring tasks**

After entering the task configuration page from the monitoring task configuration entrance, you can configure task information such as task name and monitoring rules according to the interface prompts. The core configuration items are described as follows.

<span id="76c993da"></span>
## **Configure monitoring rules**

Configure monitoring rules, that is, configure what indicators need to be monitored for the current chart, and what are the abnormal scenarios of indicators that trigger monitoring alarm messages in the future. The current Finder provides you with **custom rules** and **intelligent monitoring** two monitoring methods.

<span id="_2-3-2-自定义监控"></span>
### **Custom monitoring rules**

Finder allows you to flexibly configure chart monitoring rules according to business needs, including selecting monitoring metrics and setting monitoring exception determination criteria. Detailed configuration parameters are described below.


|**Parameter** |**Configuration instructions** |
|---|---|
|Monitoring method |Select **Custom Rules** .<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95f59f5ea58f4bc68e5b744591985c45~tplv-goo7wpa0wc-image.image) </span> |
|Rule configuration |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0c264d88c2e472e82397277060a745f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Select the indicator to be monitored: You can select the indicator to be monitored from all the indicators on the current chart in the drop\-down box.<br><br>* Configure the abnormal judgment standard of the corresponding indicator: After selecting the monitoring indicator, set the abnormal scene of the corresponding indicator, and then perform abnormal judgment and send an alarm according to the scene configured here. The filter conditions supported by the exception determination for the day\-level chart and the hour/5\-minute chart do not match.<br><br>   * Day\-level charts: support comparing the previous day/fixed value/the same period last week, etc., rising/falling/fluctuating over, a certain value or a certain proportion.<br><br>   * Hourly chart: Support comparison of the same period of the previous day/previous day cumulative/previous hour, etc., rise/fall/fluctuation over, a certain proportion.<br><br>* Currently, it supports adding monitoring rules for multiple monitoring indicators/indicator groups, and supports setting the logical relationship of alarm triggering rules for multiple monitoring indicators to "AND" or "OR".<br><br>   * When you want to monitor the same monitoring indicator/indicator group, and there are multiple monitoring rules for this monitoring indicator/indicator group, it is recommended that you directly add multiple monitoring rules under the same monitoring indicator, and set the logical relationship of multiple monitoring rules to "AND" or "OR".<br><br>   * When you want to monitor different monitoring indicators/indicator groups, it is recommended that you add multiple monitoring indicators and configure the monitoring rules for each monitoring indicator separately (also supports setting multiple rules, and the logical relationship between each rule is "AND" or "OR"), and set multiple monitoring indicators /indicator groups The logical relationship is "AND" or "OR".<br><br><br>Detailed support is subject to the console interface. Please refer to the effective logic of monitoring rules in each typical scenario [Reference: Monitoring rules take effect logic](https://docs.byteplus.com/docs/DataFinder/Monitoring_Management#e275e14d). |


<span id="4390eb45"></span>
### **Intelligent monitoring**

Finder provides you with intelligent monitoring capabilities. The Finder system can automatically determine whether the actual data is abnormal according to historical data laws. If the actual data value is determined to be abnormal, an alarm message will be automatically sent according to the subsequent configuration of the reach rule.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">At present, only the charts of the event analysis tool class support intelligent monitoring.</div>



* Hour level: 95% confidence interval, 7 days backtracking. That is, the historical data referred to is the historical data in the past 7 days, and the data determined to be abnormal is the data whose value is not within the 95% confidence interval of the historical data.

* Day level: 95% confidence interval, 60 days backtracking. That is, the historical data referred to is the historical data within the past 60 days, and the data determined to be abnormal is the data whose value is not within the 95% confidence interval of the historical data.


<span id="e3ebc484"></span>
## Configure monitoring reach


|**Parameter** |**Configuration Notes \- Hour\-by\-Hour Chart** |**Configuration Notes \- Day Chart** |
|---|---|---|
|**Monitoring frequency** |per hour |every day |
|**Monitoring period** |Support for flexible selection of the time frame for which monitoring data is required. The time granularity can be down to the hour granularity.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b05b44e2b19b496380f993bacc628306~tplv-goo7wpa0wc-image.image) </span><br><br>If your time zone has special requirements, you can also configure different time zones. |Support for flexible selection of the time frame for which monitoring data is required. The time granularity can be down to the day granularity.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a98f6018a3404c03a71afe7cdcf2d6d8~tplv-goo7wpa0wc-image.image) </span><br><br>If your time zone has special requirements, you can also configure different time zones. |
|**Advanced Frequency Control/Trigger Time** |For hourly charts, in order to prevent sudden anomalies from causing frequent alarms, you can set a limit on the frequency of sending alarm messages.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fb5f6b7ef4c429e9613c606cfcafa68~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For hourly charts, the chart data generation cycle is short, and monitoring is automatically triggered by the system after the data is produced, eliminating the need for manual configuration.</div><br> |For day\-level charts, you need to configure the time to start monitoring.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to pay attention that the monitoring trigger time needs to be after the monitoring indicator data has been normally produced. For example, your monitoring scenario asks whether Monitor Indicator A is up 20% today compared to yesterday. Today's data for indicator A will be generated at about 3 am today, and your monitoring trigger time needs to be configured after 3 am. If the data for indicator A has not been generated before 3 am, the monitoring task will not take effect normally.</div><br><br><br>Currently supported configuration is **default** or **custom** two ways.<br><br><br>* **Default** : After the data construction is completed, the monitoring is automatically triggered to determine whether the data is abnormal according to the monitoring rules. In this scenario, the monitoring trigger time must be after the data generation time.<br><br>* **Customization** : Flexibly select the time point to trigger the monitoring, and only "complete the data calculation and trigger the alarm condition" within the selected time, and push the alarm. |
|**Notification method** |Currently, both mailbox and enterprise group are supported.<br><br><br>* Mailbox: Support sending alarm messages to fixed mailboxes. You can directly fill in the email address that needs to send the alarm message, or select the user mailbox that has been added as a group user in the drop\-down box. See the instructions for adding group users [User Management](https://docs.byteplus.com/docs/DataFinder/User_Management).<br><br>* Enterprise groups: Support sending alert messages to Lark, WeCom, DingTalk, and Slack enterprise groups through webhooks. You can [Webhook Management](https://docs.byteplus.com/docs/DataFinder/Webhook_Management_)add webhooks to it, and then select the corresponding enterprise group in the drop\-down box. ||
|**Send test** |Click **Send Test** in the lower left corner to send a test email to the notification method configured above. ||


<span id="_2-4-监控管理页面"></span>
# **Monitoring task management**

Entrance location: Application Management \> Monitoring Management, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9513e14c956a4c78acaf13e0e60f71f2~tplv-goo7wpa0wc-image.image) </span>


* The top can be filtered by my managed, my received, and unlimited relationships.

   * I manage: I create

   * I received: Judging by email

   * Unlimited relationships: including what I create + what I receive (judged by email)

* You can check the monitoring list and edit, view alarm records, close, delete and other operations.


<span id="_2-5-操作权限"></span>
## **Detailed rules for monitoring operation authority**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Attribution</strong> is <strong>unlimited</strong>: Represents monitoring tasks created by others in the group.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Attribution</strong> to <strong>yourself</strong>: Represents a monitoring task created for yourself.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Attribution</strong> is <strong>Receive</strong>: It means that the push mailbox contains the monitoring tasks of your own mailbox, including the monitoring tasks created by yourself and others.</div>




|**Operation** |**Attribution** |**Group Administrator (within the Group)**  |**Administrator (in\-app with permissions)**  |**Member** |
|---|---|---|---|---|
|View the list.<br><br>View alarm logs |unlimited |✓ |✓ |× |
||himself |✓ |✓ |✓ |
||receive |✓ |✓ |✓ |
|Create |unlimited |✓ |✓ |✓ |
|Edit,<br><br>Change state,<br><br>delete |unlimited |✓ |✓ |× |
||himself |✓ |✓ |✓ |
||receive |✓ |✓ |× |


<span id="e275e14d"></span>
# Reference: Monitoring rules take effect logic

<span id="1786fb35"></span>
## Scenario 1: Only one metric needs to be monitored


* Scene description:

   At present, it is only necessary to monitor a specific indicator, and determine whether to trigger a monitoring alarm according to the changing trend of this indicator.

* Monitoring rule configuration suggestions:

   Add a monitoring indicator; one or more monitoring rules can be configured according to the actual situation, and multiple monitoring rules support setting the logical relationship to "AND" or "OR";

* Monitoring rules take effect logic:

   
   |The logical relationship is "AND". |Logical relationship "OR" |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b763820ba3ad49e4802bdaf7a45997d5~tplv-goo7wpa0wc-image.image) </span><br><br>The alarm will only be triggered when the "App Launch (Total Number (PV)) " indicator increases by more than 100 and the increase rate exceeds 10%. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f83b462bda34109985c9a86c2c6f00e~tplv-goo7wpa0wc-image.image) </span><br><br>When the "App Launches (Total Number (PV)) " indicator increases by more than 100% or increases by more than 10%, an alarm will be triggered. |
   


<span id="78fb1ca2"></span>
## Scenario 2: Multiple metrics need to be monitored


* Scene description:

   At present, multiple indicators need to be monitored, and whether to trigger monitoring alarms is determined according to the changing trend of each indicator.

* Monitoring rule configuration suggestions:

   Add multiple monitoring indicators; configure the monitoring rules of each monitoring indicator according to the actual situation. Multiple monitoring rules support setting the logical relationship to "AND" or "OR"; At the same time, configure the logical relationship of each monitoring indicator to "AND" or "OR".

   A configuration example is as follows.

   
   |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a590a4fe5943e3a162045ff319c090~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Added two monitoring metrics:<br><br>   * The first monitoring metric:<br><br>      * Select "Total Page Views (PV) " as the monitoring metric.<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>   * The second monitoring indicator:<br><br>      * "Total app launches (PV) " is selected as the monitoring metric.<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>* The current logical relationship between the two monitoring metrics is "AND". |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2732e54b90c4dc38ef99a691f9fee08~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Added two monitoring metrics:<br><br>   * The first monitoring metric:<br><br>      * Select "Total Page Views (PV) " as the monitoring metric.<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>   * The second monitoring indicator:<br><br>      * "Total app launches (PV) " is selected as the monitoring metric.<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>* The current logical relationship between the two monitoring indicators is "OR". |
   

* Monitoring rules take effect logic:

   
   |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a590a4fe5943e3a162045ff319c090~tplv-goo7wpa0wc-image.image) </span><br><br><br>* When the first monitoring indicator **and** the second monitoring indicator meet the monitoring alarm triggering conditions (monitoring rules), the alarm will be triggered.<br><br>* The judgment logic for each monitoring indicator to meet the monitoring alarm triggering conditions (monitoring rules) is consistent with the example of "Scenario 1" above. Taking the first monitoring indicator A1 as an example, when the value of "Total Page Views (PV) " rises by more than 100 or the increase rate exceeds 10% from the previous day, the monitoring alarm triggering conditions are met. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2732e54b90c4dc38ef99a691f9fee08~tplv-goo7wpa0wc-image.image) </span><br><br><br>* When the first monitoring indicator **or** the second monitoring indicator meets the monitoring alarm trigger condition (monitoring rule), the alarm will be triggered.<br><br>* The judgment logic for each monitoring indicator to meet the monitoring alarm triggering conditions (monitoring rules) is consistent with the example of "Scenario 1" above. Taking the first monitoring indicator A1 as an example, when the value of "Total Page Views (PV) " rises by more than 100 or the increase rate exceeds 10% from the previous day, the monitoring alarm triggering conditions are met. |
   |Summarize:<br><br><br>* When A1 satisfies and B1 also satisfies the triggering alarm condition, the alarm will be triggered.<br><br>* Whether A1 or B1 satisfies the trigger alarm condition is consistent with the example in "Scenario 1" above. |Summarize:<br><br><br>* When one of the A1 or B1 indicators meets the triggering condition, the alarm is triggered.<br><br>* Whether A1 or B1 satisfies the trigger alarm condition is consistent with the example in "Scenario 1" above. |
   


<span id="3b6bf314"></span>
## Scenario 3: Only one indicator group needs to be monitored, and the indicator monitoring rules within the indicator group are consistent


* Scene description:

   At present, only a specific indicator group needs to be monitored, and there are multiple sub\-items in the indicator group. According to the changing trend of several sub\-items fixed in this indicator group, it is decided whether to trigger a monitoring alarm.

* Monitoring rule configuration suggestions:

   Add a monitoring indicator, the indicator selects the sub\-indicator items that need to be monitored in the indicator group (support multi\-selection); one or more monitoring rules can be configured according to the actual situation, and multiple monitoring rules support setting the logical relationship to "AND" or "OR";

   The configuration example is as follows.

   
   |The logical relationship within a single indicator is "AND". |Logical relationship "OR" within a single indicator |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b763820ba3ad49e4802bdaf7a45997d5~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Two sub\-indicator items in the indicator group are selected within a single monitoring indicator: "Total number of tasks: Moonshot AI", "Total number of tasks: xxxdeepseek".<br><br>* The current monitoring indicator has two monitoring rules, and the logical relationship between the rules is "AND". |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f83b462bda34109985c9a86c2c6f00e~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Two sub\-indicator items in the indicator group are selected within a single monitoring indicator: "Total number of tasks: Moonshot AI", "Total number of tasks: xxxdeepseek".<br><br>* The current monitoring indicator has two monitoring rules, and the logical relationship between the rules is "OR". |
   

* Monitoring rules take effect logic:

   
   |The logical relationship within a single indicator is "AND". |Logical relationship "OR" within a single indicator |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b763820ba3ad49e4802bdaf7a45997d5~tplv-goo7wpa0wc-image.image) </span><br><br>When the value of "Total Quests: Moonshot AI" increases by more than 100 and the increase rate exceeds 10% from the previous day, or the value of "Total Quests: xxxdeepseek" increases by more than 100 and the increase rate exceeds 10% from the previous day, a monitoring alarm will be triggered. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f83b462bda34109985c9a86c2c6f00e~tplv-goo7wpa0wc-image.image) </span><br><br>When the value of "Total Tasks: Moonshot AI" increases by more than 100 or the increase rate exceeds 10% from the previous day, or the value of "Total Tasks: xxxdeepseek" increases by more than 100 or the increase rate exceeds 10% from the previous day, a monitoring alarm will be triggered. |
   |Summary: If multiple indicator items in the indicator group are selected within a single indicator, a monitoring alarm will be triggered if one of the sub\-indicator items meets the indicator group rules. ||
   


<span id="599ab88c"></span>
## Scenario 4: Only one indicator group needs to be monitored, but the indicator monitoring rules within the indicator group are inconsistent


* Scene description:

   At present, only a specific indicator group needs to be monitored, and there are multiple sub\-indicators in the indicator group. It is necessary to decide whether to trigger a monitoring alarm according to the changing trend of several sub\-indicators in this indicator group.

* Monitoring rule configuration suggestions:

   Add multiple monitoring indicators, each monitoring indicator selects the sub\-index items that need to be monitored in the indicator group (support multi\-selection); each monitoring indicator is configured with one or more monitoring rules according to the actual situation, and multiple monitoring rules support setting the logical relationship to "AND" or "OR";

   Configuration example.

   
   |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a590a4fe5943e3a162045ff319c090~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Added two monitoring metrics:<br><br>   * The first monitoring metric:<br><br>      * Two sub\-indicator items in the indicator group were selected: "Total Tasks: Moonshot AI", "Total Tasks: xxxdeepseek".<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>   * The second monitoring indicator:<br><br>      * Two sub\-indicator items in the indicator group were selected: "Success Rate: Moonshot AI", "Success Rate: xxxdeepseek".<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>* The current logical relationship between the two monitoring metrics is "AND". |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2732e54b90c4dc38ef99a691f9fee08~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Added two monitoring metrics:<br><br>   * The first monitoring metric:<br><br>      * Two sub\-indicator items in the indicator group were selected: "Total Tasks: Moonshot AI", "Total Tasks: xxxdeepseek".<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>   * The second monitoring indicator:<br><br>      * Two sub\-indicator items in the indicator group were selected: "Success Rate: Moonshot AI", "Success Rate: xxxdeepseek".<br><br>      * Two monitoring rules are configured, and the logical relationship between the rules is "OR".<br><br>* The current logical relationship between the two monitoring indicators is "OR". |
   

* Monitoring rules take effect logic:

   
   |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |The internal logical relationship of a single indicator is "OR"; the logical relationship of multiple indicators is "AND" |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a590a4fe5943e3a162045ff319c090~tplv-goo7wpa0wc-image.image) </span><br><br><br>* When the first monitoring indicator and the second monitoring indicator meet the monitoring alarm triggering conditions (monitoring rules), the alarm will be triggered.<br><br>* The judgment logic for each monitoring indicator to meet the monitoring alarm triggering conditions (monitoring rules) is consistent with the example in "Scenario 3" above. Taking the first monitoring indicator as an example, when the value of "Total Tasks: Moonshot AI" increases by more than 100 or the increase rate exceeds 10% from the previous day, or the value of "Total Tasks: xxxdeepseek" increases by more than 100 or the increase rate exceeds 10% from the previous day, the monitoring alarm triggering conditions are met. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2732e54b90c4dc38ef99a691f9fee08~tplv-goo7wpa0wc-image.image) </span><br><br><br>* When the first monitoring indicator or the second monitoring indicator meets the monitoring alarm triggering condition (monitoring rule), the alarm will be triggered.<br><br>* The judgment logic for each monitoring indicator to meet the monitoring alarm triggering conditions (monitoring rules) is consistent with the example in "Scenario 3" above. Taking the first monitoring indicator as an example, when the value of "Total Tasks: Moonshot AI" increases by more than 100 or the increase rate exceeds 10% from the previous day, or the value of "Total Tasks: xxxdeepseek" increases by more than 100 or the increase rate exceeds 10% from the previous day, the monitoring alarm triggering conditions are met. |
   |Summary: When adding multiple monitoring indicators, when there are multiple monitoring rules under each monitoring indicator, whether a single indicator meets the logic of triggering monitoring alarm conditions is consistent with the scenario of adding a single indicator . ||
