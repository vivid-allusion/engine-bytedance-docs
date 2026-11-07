---
title: "Alarm Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Alarm_Management"
---

DataFinder provides you with an alarm management page where you can view all current alarm lists and alarm details. This article introduces you to the operational essentials of alarm management.

<span id="af15807c"></span>
# Precautions


* Currently, only SaaS\-cloud native environments are supported.

* The current function is turned off by default. If you want to use the alarm management function, you can contact the BytePlus technical support staff to turn it on.


<span id="f76b95d5"></span>
# Function introduction

After logging in and entering the DataFinder console, click **Data Management** \> **Data Governance** \> **Alarm Management** in the top navigation bar to enter the Alarm Management page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37077067118140aaa58dd6d19b9845cc~tplv-goo7wpa0wc-image.image) </span>

<span id="d9ae4345"></span>
## Alarm record source

The advanced management page will summarize and display all the monitoring and alarm rules you have configured in the data governance major function module, including:


|**Alarm source** |**Comparison description** |
|---|---|
|**Validation Rules Configuration** page Monitor Alerts in Custom Validation Rules. |The monitoring alarm on the verification rule configuration page is a custom verification rule, which will be triggered when the data is warehoused and does not meet the custom verification rule. |
|**Data warehousing details** page to create a monitoring alert. |The monitoring alarms in the data warehousing details page are the monitoring alarms for all recommended rules, that is, the warehousing verification rules preset by the DataFinder are included, and the custom verification rules are also included. When the corresponding alarms are not met, the corresponding alarms will be triggered. |


<span id="e34f04ae"></span>
## Alarm Supported Operations


* You can click the corresponding monitoring name to view the monitoring task details; click the number of alarms and abnormal data to view the alarm and abnormal details.

* For monitoring alarm records created from the **data warehousing details** page, you can turn them on or off in the monitoring alarm page, or click Modify alarm monitoring information.

* For the monitoring alarm of custom verification rules created from the **verification rule configuration** page, the current page does not support operations such as opening and modifying. You need to go to the **verification rule configuration** page to modify.
