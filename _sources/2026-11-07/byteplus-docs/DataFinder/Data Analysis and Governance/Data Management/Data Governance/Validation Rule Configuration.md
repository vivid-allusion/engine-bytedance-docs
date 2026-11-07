---
title: "Validation Rule Configuration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Validation_Rule_Configuration"
---

DataFinder presets common data warehousing verification rules for you. When the event warehousing does not meet the verification rules, the corresponding event will be intercepted. At the same time, DataFinder also supports you to customize data verification rules according to business needs. This article introduces the configuration points for creating custom verification rules.

<span id="a1ede72d"></span>
# Precautions


* At present, only SaaS\-cloud\-native environments support custom validation rule configuration capabilities.

* The current function is turned off by default. If you wish to use the ability to customize validation rules, you can contact BytePlus technical support to turn the function on.

* For details on DataFinder's preset validation rules see [Reference: Preset Data Validation Rules](https://docs.byteplus.com/docs/DataFinder/Storage_Details_Original_Data_Quality#_3-%E6%95%B0%E6%8D%AE%E6%A0%A1%E9%AA%8C%E8%A7%84%E5%88%99), Before creating a custom validation rule, you can check whether the preset validation rule meets your business requirements.


<span id="70d2caa4"></span>
# New custom validation rule


1. After logging in and entering the DataFinder console, click **Data Management** \> **Data Governance** \> **Verification Rule Configuration** in the top navigation bar. After entering the verification rule configuration page, click the **New Verification Rule** button in the upper right corner.

2. Configuration basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fc79988741e477f9abd6d109286bbdb~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |rule name |Custom rule name for subsequent identification of custom validation rules. |
   |rule type |Currently supports event quantity, event property validation, user property validation three types of rules.<br><br><br>* Event Volume: A validation rule that verifies the number of reported events over a period of time.<br><br>* Event property verification, user property verification: Verify whether the event/user property meets the verification rules. |
   |Validation Object & Validation Rules |Select the validation object according to the interface prompts and configure the validation rules. The validation rules of the event property need to specify the event before selecting the event property. Details of event and property validation rules can be found in the following [Reference: Validation rule description](https://docs.byteplus.com/docs/DataFinder/Validation_Rule_Configuration#87af5721)sections.<br><br><br>* The verification rule supports adding multiple, and the logical relationship between multiple verification rules is "OR", that is, if one of the verification rules is satisfied, the alarm and data interception can be carried out according to the alarm rule.<br><br>* Support configuring filter conditions for each check rule configured, and the logical relationship between multiple filter conditions is "AND". |
   

3. Alarm settings. You can choose whether to turn on the monitoring alarm of the verification rule as needed. After opening, when the subsequent data is put into storage, if the abnormal data that does not meet the verification rule reaches a certain amount, an alarm message will be triggered according to the alarm rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd67676951041dfa499dc6a709936eb~tplv-goo7wpa0wc-image.image) </span>

   The channels that currently support alarm notifications include mailboxes and enterprise groups. If you want to send alarm messages to the enterprise group, you need to add the webhook information related to the enterprise group on DataFinder. Please refer to the details [Webhook Management](https://docs.byteplus.com/docs/DataFinder/Webhook_Management_).

4. Data interception settings. You can choose whether to intercept abnormal data as needed. After opening, when subsequent data is put into storage, abnormal data that does not meet the verification rules will be intercepted according to the interception rules and will not be put into storage.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Event property/user property rules need to be configured, event volume rules do not need to be configured.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba48a8e755d94223b03822ab6b4c4aa0~tplv-goo7wpa0wc-image.image) </span>


<span id="7ecfa406"></span>
# Enable/close, edit, delete validation rules

After the custom verification rule is created, you can view the list of custom verification rules on the verification rule page, and support operations such as opening and closing the verification rule.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d61039cab7c140cea12cfc1fa010e991~tplv-goo7wpa0wc-image.image) </span>


* After closing the validation rule, the validation rule will no longer take effect in the future. If you no longer wish to perform the relevant warehousing validation, you can turn off the corresponding validation rule.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you configure the alarm notification after the verification rule is triggered, after a verification rule is closed on the verification rule page, after the subsequent verification rule is triggered, the data will not be intercepted and put into storage, and can be put into storage normally; but the alarm message may also be triggered and sent.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you also want to turn off alarm notifications, you need to click the <strong>Edit</strong> button to turn off alarms in the <strong>Monitor alarm</strong> configuration of the validation rule.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8950c9795d8b43609a14491b32dfaa26~tplv-goo7wpa0wc-image.image" width="400px" />   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The verification rule of the event volume type does not support closing the alarm. If you do not want to trigger the verification into the warehouse or receive the alarm notification in the future, you can directly delete the corresponding verification rule.   </div>
   

* Closed validation rules support direct deletion.

* The created verification rule can be edited and modified. Editing and modifying only supports modifying the alarm and interception settings of the verification rule, and the verification rule does not support modification.

* You can also check the number of alarms and abnormal data of the corresponding verification rule on the verification rule list page, and click the corresponding data to view the details.


<span id="87af5721"></span>
# Reference: Validation rule description

<span id="0790d93b"></span>
## Event Volume Validation Rule Description

Event volume verification is used to monitor the amount of reported data for a specific event tracking, and to trigger an alarm when the amount of event reports is greater than or less than a certain number within a specific time range.

For example, an alarm will be raised when the order payment event exceeds 10,000 within 5 minutes.

The time interval for verification can be divided into minutes, hours, and natural days, with a minimum interval of 10 minutes.

<span id="a9b91681"></span>
## Property validation rule description

Event/User Properties The following validation rules can be selected on demand according to the interface prompt.


|**Rule type** |**Rule description** |
|---|---|
|mandatory verification |Indicates that the property is a required field, and that the property is not uploaded (missing key) or null (missing value) is an exception. |
|enumeration validation |You can enter all enumeration values for this property, or an exception if the value reported by the property is not in the enumeration value configured by the rule. Property not uploaded or null is not within the scope of the exception. |
|Regular Match Check |You can enter a regular expression that the property value should match, or an exception if it does not match. Property not uploaded or null is not within the scope of the exception. |
|interval check |A field of a numeric type can define a range of values for the property. If the value reported by the property is not within this range, it is an exception. Property not uploaded or null is not within the scope of the exception. |
|include validation |The property value contains a check for a specific value, or an exception if the reported property value does not contain the specific value set. Property not uploaded or null is not within the scope of the exception. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When configuring validation rules using event property values, the configuration results of property values are case\-sensitive, so:</div>



* <div data-tips="true" data-tips-type="warning">When using <strong>preset event properties</strong>, because the DataFinder automatically processes all preset event property values to lowercase during reporting, you need to configure the event property values to lowercase.</div>


   <div data-tips="true" data-tips-type="warning">For example, when the preset event property is reported as "iOS", it will be processed as "ios" after warehousing, so you need to configure it as "ios" here.   </div>
   

* <div data-tips="true" data-tips-type="warning">When using the <strong>custom event property</strong>, the DataFinder does not process the reported results of the event property, you need to configure it according to the actual reported results.</div>
