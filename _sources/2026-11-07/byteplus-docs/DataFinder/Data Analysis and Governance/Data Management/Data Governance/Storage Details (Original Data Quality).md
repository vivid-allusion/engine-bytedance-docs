---
title: "Storage Details (Original Data Quality)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Storage_Details_Original_Data_Quality"
---

Data warehousing details (raw data quality) A module for understanding the warehousing situation after the data in the project is reported, which can quickly view the number of current project warehousing/abandonment events, count the number of events hitting various error types, and view data detailed logs.

<span id="5498e4c9"></span>
# Configure warehousing abnormality monitoring alarm

DataFinder supports configuring abnormal warehousing monitoring alarms. After the configuration is completed, when subsequent data warehousing is abnormal, an alarm message will be triggered according to the alarm rules.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The monitoring alarm configuration result will affect the alarm message when subsequent data is warehoused. If the monitoring alarm is not configured, although the monitoring alarm will not be triggered, you can still actively view the abnormal data information on the obvious page of warehousing verification.</div>


* <div data-tips="true" data-tips-type="tip">The current data that supports checksum alarms include: events (excluding virtual events), event attributes, and user attribute data.</div>


* <div data-tips="true" data-tips-type="tip">After the monitoring task is created, it will take effect in about 10 minutes.</div>


1. Click the Create Monitoring Alert button in the upper right corner of the page to configure the monitoring alarm parameters in the pop\-up page.

2. Monitor the configuration. According to the interface prompts, configure parameters such as monitoring objects and monitoring rules.

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Monitor name** |Customize the monitoring name for subsequent identification of monitoring rules. |
   |**Monitoring object & monitoring object related parameters** |* Select the monitoring object type as event, event attribute, or user attribute according to the monitoring needs.<br><br>* Different types of monitoring objects need to be selected according to the interface prompts, corresponding to specific events, event attributes, and user attributes. Event properties further select the associated event name. |
   |**Error type** |You can select the validation rules to monitor in the drop\-down list, which contains the DataFinder preset validation rules and custom validation rules currently supported by the validation object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">See below for the full list of validation rules preset by DataFinder <a href="https://docs.byteplus.com/docs/DataFinder/Storage_Details_Original_Data_Quality#_3-%E6%95%B0%E6%8D%AE%E6%A0%A1%E9%AA%8C%E8%A7%84%E5%88%99">Reference: Preset Data Validation Rules</a>; the list of custom validation rules that have been created can be viewed on the validation rule configuration page, see for details <a href="https://docs.byteplus.com/docs/DataFinder/Validation_Rule_Configuration">Validation Rule Configuration</a>.</div><br> |
   |**Monitoring rules** |Currently supports configuration monitoring rules trigger condition is **any condition is met** or **cumulative conditions are met**. For example, when the monitoring object is an event:<br><br><br>* Any condition is met: The monitoring alarm will only be triggered when any one of the warehousing events meets the monitoring rules.<br><br>* Accumulation conditions are met: When the cumulative number of all warehousing events meets the monitoring rules, a monitoring alarm will be triggered.<br><br><br>The current monitoring rule that triggers an alarm is the number of abnormal data that does not meet the validation rule within a period of time.<br><br><br>* You can configure the monitoring time range and data volume limit according to the interface prompts.<br><br>* Support configuring multiple monitoring rules, and the logical relationship between each monitoring rule is "OR". |
   |**Monitoring range**<br><br>(Not supported when the **monitoring object** is a **user property** ) |You can filter through event attributes, and support configuring multiple filter conditions. The logical relationship between filter conditions can be uniformly set to "OR" or "AND".<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When using event property values for monitoring scope filtering, the configuration results of property values are case\-sensitive, so:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When using <strong>preset event properties</strong> , because the DataFinder automatically processes all preset event property values to lowercase during reporting, you need to configure the event property values to lowercase.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">For example, when the preset event property is reported as "iOS", it will be processed as "ios" after warehousing, so you need to configure it as "ios" here.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="warning">When using the <strong>custom event property</strong> , the DataFinder does not process the reported results of the event property, you need to configure it according to the actual reported results.</div><br> |
   

3. Alarm settings. Configure the monitoring period and the sending channel of the alarm message according to the interface prompts.

   If you want the alert message to be sent to the enterprise group, you need to create a webhook message for the corresponding enterprise group on the DataFinder, see details [Webhook Management](https://docs.byteplus.com/docs/DataFinder/Webhook_Management_).


<span id="_2-功能说明"></span>
# View and handle abnormal data

The following is a general guide for viewing, analyzing, and processing abnormal data on the data entry details page.

<span id="_2-1-列表字段说明"></span>
## List of warehousing events

You can view the list of rights events currently in storage and its related abnormal data and other information on the warehousing verification details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d534c8fa7a84ab38b8678e7dab6a3d2~tplv-goo7wpa0wc-image.image) </span>


* Event Name: Name of the reported event

* SDK type: web, mp (Mini Program), app, empty means reporting data through non\-SDK such as http api. At this time, the "SDK version" is also empty

* SDK version: SDK version number

* Error type: The type of error the event was detected for, including event errors and attribute errors; see section 3. Data Validation Rules for validation rules

* Number of received pieces: The number of data pieces received by the system, and the data legitimacy verification has not been carried out at this time

* Number of discarded items: The number of items that the data did not enter the system due to errors, quantity exceeding limits, etc

* Number of warehouses: The number of data pieces that can be queried when entering the system

* Number of exception attributes: The number of times the exception attribute is included. Attribute exceptions usually only cause the relevant attribute to be discarded, without affecting the event itself


<span id="_2-2-查看异常数据详情"></span>
## View full exception data details

You can click on the event name on the left side of the list to view the error details of the event. The system will automatically display the latest 10 error logs for the current event. You can filter by error type and error code to locate the specific error type.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The details only support viewing the records of the last 7 days.</div>


* <div data-tips="true" data-tips-type="warning">Events/properties that are disabled, as well as event properties whose reporting type is inconsistent with the metadata registry, are simply discarded; if you want to view such data in the data details, you need to set the event public property $data_validation_test reporting value to true.</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b363e84833a367055370af03434cea9.png) </span>

<span id="5646c26c"></span>
## AI Lab: Intelligent Event Anomaly Monitoring

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The intelligent monitoring function of abnormal events has been turned off and will be offline in the near future. Please pay attention.</div>


DataFinder AI Lab is a multi\-dimensional intelligent assistant provided by DataFinder combined with AI large model capabilities, including AI event anomaly detection capabilities. After turning on the event abnormality monitoring switch of the AI Lab, the subsequent AI Lab will automatically scan and monitor the reported events for you, and prompt you for suspected problems identified by the AI, further improving the identification and governance efficiency of reported events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0745c40726249efa99c8a62dfe9a2c2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-下载错误明细"></span>
## Download error details


* Click "Download" on the far right of each event to export a list of error data for that event.

* Click "Download Error Details" in the upper right corner of the list to export the full error data list.


<span id="_3-数据校验规则"></span>
# **Reference: Preset Data Validation Rules**

DataFinder has preset common data warehousing verification rules for you. If the verification rules are not met when the event is warehoused, the entire event will be intercepted. The preset event verification rules and warehousing exceptions include the following situations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current DataFinder also supports you to customize data validation rules according to business needs. Please refer to the alarm prompt configuration for creating custom validation rules and custom validation rules <a href="https://docs.byteplus.com/docs/DataFinder/Validation_Rule_Configuration">Validation Rule Configuration</a>.</div>



|**Error code** |**Error description** |**Validation rule** |**Optimization suggestions** |
|---|---|---|---|
|1010001 |Event name is invalid |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,255}$` |Event names begin with a letter and can include letters, numbers, _. \-, the length must not exceed 255 characters, please modify the name |
|1010002 |Event names conflict with system reserved event name rules |Not a preset event name starting with $and __ |Conflict with the system reserved event name rules, event names must not start with $or __, please start with a letter, can contain letters, numbers, _. \-, the length must not exceed 255 characters, please modify the name |
|1010003 |Event name conflicts with virtual event name |Same name as the created virtual event |The event name must not have the same name as the virtual event. Please modify the name |
|1010004 |number of events exceeded |More than 1000 events in a single application, the event falls metadata status = \-2, the slotting tag is closed, the event is not built, and the attributes are not dropped from the library<br><br>Privatization configurable cap, up to 5000 |The number of events has reached the upper limit, and new events cannot be added. Please go to the meta\-event list page and "disable" useless events. |
|1010006 |The time of the warehousing event exceeds the valid window period |The event occurred within the last 7 days or beyond the next 24 hours |Event tracking occurred earlier than the past 7 days, and event reporting is delayed. It is recommended to check the network link situation on the client side, or improve the reporting frequency (need to modify the SDK configuration) |
|1010007 |Event metadata not accepted or blacklisted |Events not registered/accepted or marked as blacklisted |If you need the event to be warehoused, please change the event status to "enabled" or "hidden". |
|1010008 |Event metadata does not exist |Event metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |


When only an attribute exception is detected, it will not affect the warehousing of the event, but the abnormal attribute will be intercepted and not warehoused. Attribute exceptions include the following:


|**Error code** |**Error description** |**Validation rule** |**Optimization suggestions** |
|---|---|---|---|
|1020001 |Invalid event property name |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter and can include letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name |
|1020002 |Event property names conflict with system reservation rules |Not a preset event name starting with $and __<br><br>Whitelisted ("$inactive", "$inline", "$target_uuid_list", "$source_uuid", "$is_spider", "$source_id", "$is_first_time") |The event property name conflicts with the system reservation rules. The name must not start with $and __. Please modify the name |
|1020003 |The number of attributes per event exceeds the limit |A single event suggests 300 properties, more than 300 but not more than 500, the status is set to 0, which means build is disabled, but can be displayed on the page; more than 500 states are set to \-2, which means hidden and not built |The number of single event attributes has reached the upper limit of 300, and the excess part cannot be warehoused. Please go to the metadata\-event attribute list page and disable the useless event attribute. |
|1020004 |Invalid event attribute data type |Inconsistent with the attribute data type recorded in metadata, and the strong conversion failed |The actual reported data format is inconsistent with the attribute data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type |
|1020005 |Invalid event property value |* SaaS\-Cloud Native: Over 2048 characters |If the attribute value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
|1020006 |Event property not accepted or in blacklist |Event properties Event not registered/not accepted or marked as blacklisted |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
|1020007 |Event attribute metadata does not exist |Event attribute metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
|1030001 |Event public property name is invalid |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter and can include letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name |
|1030002 |Event public property names conflict with system reservation rules |Not a preset event name starting with $and __<br><br>Whitelisted ("$inactive", "$inline", "$target_uuid_list", "$source_uuid", "$is_spider", "$source_id", "$is_first_time") |The event public property name conflicts with the system reservation rules. Property names must not start with $and __. Please modify the name |
|1030003 |The number of common attributes of a single application event exceeds the limit |More than 300 (100 in privatization 4.6 and below) event public properties with status set to \-2 do not participate in the build |The number of event public properties has reached 300, and the excess part cannot be warehoused. Please go to the metadata\-event property list page and disable the useless event public properties. |
|1030004 |Invalid event attribute data type |Inconsistent with the attribute data type recorded in metadata, and the strong conversion failed |The actual reported data format is inconsistent with the attribute data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type |
|1030005 |Invalid event public property value |* SaaS\-Cloud Native: Over 2048 characters |If the attribute value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
|1030006 |Event public property not accepted or blacklisted |Event public property not accepted or blacklisted |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
|1030007 |Event public attribute metadata does not exist |Event public attribute metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
|1040001 |Invalid user property name |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter and can include letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name |
|1040002 |The number of user attributes exceeds the limit |The number of user attributes exceeds the 500 limit |The number of user attributes has reached the upper limit, and new attributes cannot be added. Please go to the user attribute list page and "disable" useless attributes. |
|1040003 |Invalid user attribute type |Inconsistent with the attribute data type recorded in metadata, and the strong conversion failed |The actual reported data format is inconsistent with the attribute data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type |
|1040004 |Invalid user attribute value |* SaaS\-Cloud Native: Over 2048 characters |If the attribute value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
|1040005 |User attributes not accepted or in the blacklist |User attributes not accepted or in the blacklist |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
|1040007 |User attribute metadata does not exist |User attribute metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |


<span id="_4-常见问题"></span>
# Common problem

<span id="_4-1-抛弃条数和异常属性条数的关系是什么？"></span>
## Q1: What is the relationship between the number of discards and the number of exception attributes?

The number of warehoused items = the number of received items \- the number of discarded items. Since the attribute abnormality only affects the attribute warehousing and does not cause the entire data to be discarded, the number of abnormal attribute items is not directly linked to the discarded item. The number of abnormal attribute items is the number of attribute abnormalities detected in all the received items.

<span id="_4-2-抛弃条数是否可以回补？"></span>
## Q2: Can the number of discarded items be compensated?

The number of discarded items cannot be replenished at present, so it is recommended that you pay attention to the governance dashboard, deal with data abnormalities in a timely manner, and avoid data loss.

<span id="_4-3-为什么看不到错误日志详情？"></span>
## Q3: Why can't I see the error log details?

The detailed data only retains the log data of the last 7 days, and the data over 7 days only supports viewing the statistical results, not the logs.
